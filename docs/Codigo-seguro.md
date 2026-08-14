# Etapa 4 — Código Seguro e Testes de Segurança

Esta etapa demonstra, por meio de pseudocódigo, como duas decisões da [Etapa 3](Arquitetura-segura.md) seriam implementadas. Os testes foram definidos antes da solução e mantêm a rastreabilidade com os riscos R07 e R01.

## Escopo e premissas

Os exemplos representam endpoints conceituais de API: consulta de dados de entrega e confirmação de reembolso. O pseudocódigo não depende de linguagem ou framework, mas assume que a API identifica o usuário autenticado a partir de sessão ou token validado no servidor.

As respostas de erro não devem revelar endereço, telefone, localização, códigos MFA, tokens, detalhes internos de autorização ou a existência de dados de terceiros. Os registros de auditoria devem conter identificador do ator, ação, recurso, horário, origem e resultado, sem armazenar dados sensíveis desnecessários.

## Prática 1 — Autorização por vínculo com pedido ativo

**Risco e requisito relacionados:** R07 — Exposição de endereço, telefone ou localização; RS02 — acesso somente por perfil autorizado e vínculo com pedido ativo.

### Testes definidos antes da implementação

| ID | Cenário | Pré-condições e entrada | Resultado seguro esperado | Evidência esperada |
| --- | --- | --- | --- | --- |
| TS01 | Uso válido | Entregador autenticado está vinculado ao pedido P100, com status `em_entrega`, e consulta os dados de P100. | A API retorna somente endereço, instruções e contato temporário necessários à entrega; não retorna dados de pagamento. | Resposta HTTP 200 e log `consulta_entrega_permitida` com ator, pedido e horário. |
| TS02 | Acesso horizontal não autorizado | Entregador autenticado está vinculado a P100, mas consulta P200, atribuído a outro entregador. | A API responde HTTP 403, não retorna endereço, telefone ou localização de P200. | Log `consulta_entrega_negada` com ator, pedido solicitado e motivo de falta de vínculo. |
| TS03 | Acesso após o prazo necessário | Entregador antes vinculado a P100 consulta sua localização depois que o pedido foi concluído. | A API responde HTTP 403 e não retorna localização nem dados de contato. | Log `consulta_entrega_negada` com motivo de status encerrado. |

### Pseudocódigo da prática

~~~text
função consultarDadosDeEntrega(usuario, pedidoId):
    pedido = pedidos.buscarPorId(pedidoId)
    se pedido não existir:
        retornar resposta 404 genérica

    permitido = (
        usuario.perfil == "cliente" e pedido.clienteId == usuario.id
    ) ou (
        usuario.perfil == "restaurante" e pedido.restauranteId == usuario.id
    ) ou (
        usuario.perfil == "entregador" e pedido.entregadorId == usuario.id
           e pedido.status em ["aceito", "retirado", "em_entrega"]
    )

    se permitido for falso:
        auditoria.registrar(usuario.id, "consulta_entrega_negada", pedidoId)
        retornar resposta 403 genérica

    dados = selecionarSomenteDadosNecessarios(pedido, usuario.perfil)
    auditoria.registrar(usuario.id, "consulta_entrega_permitida", pedidoId)
    retornar resposta 200 com dados
~~~

**Resultado esperado:** a autorização é verificada no servidor, em cada solicitação, combinando perfil, vínculo com o pedido e estado da entrega. A resposta não depende de controles visuais da interface.

### Critérios de aceite

- Todo acesso a dados de entrega é negado por padrão até que perfil, vínculo e estado sejam validados no servidor.
- Um identificador de pedido previsível ou alterado não concede acesso a dados de terceiros.
- A localização e o contato temporário deixam de ser retornados após a conclusão do pedido.
- Logs de permissão e negação permitem investigar a tentativa, sem reproduzir dados pessoais na mensagem de auditoria.

**Referência OWASP:** [Authorization Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html), especialmente menor privilégio, negação por padrão, validação de permissões em todas as requisições e testes de autorização.

## Prática 2 — Reautenticação para operações sensíveis

**Risco e requisito relacionados:** R01 — Uso indevido de conta; RS03 — MFA administrativo e nova autenticação antes de ações sensíveis.

### Testes definidos antes da implementação

| ID | Cenário | Pré-condições e entrada | Resultado seguro esperado | Evidência esperada |
| --- | --- | --- | --- | --- |
| TS04 | Uso válido | Administrador autenticado possui MFA recém-validado, vinculado à ação e ao reembolso R500 pendente. | O reembolso é processado uma única vez, a confirmação é consumida e a ação é auditada. | Resposta HTTP 200 e log `reembolso_confirmado` com administrador, recurso e horário. |
| TS05 | Sessão sem nova autenticação | Administrador possui sessão válida, mas não apresenta MFA recente ao confirmar R500. | A API responde HTTP 401 ou 403, não altera o reembolso e não revela dados financeiros adicionais. | Log `reembolso_negado_sem_reautenticacao`. |
| TS06 | Confirmação expirada ou reutilizada | Administrador apresenta comprovante MFA vencido ou já utilizado para confirmar R500 ou outro reembolso. | A API recusa a operação, invalida o comprovante e solicita novo desafio. | Log `reembolso_negado_mfa_invalido` sem registrar o código MFA. |

### Pseudocódigo da prática

~~~text
função confirmarReembolso(usuario, reembolsoId, comprovanteMfa):
    se usuario.perfil não for "administrador":
        auditoria.registrar(usuario.id, "reembolso_negado_por_perfil", reembolsoId)
        retornar resposta 403 genérica

    valido = autenticacao.validarConfirmacaoRecente(
        usuarioId = usuario.id,
        comprovante = comprovanteMfa,
        acao = "confirmar_reembolso",
        recursoId = reembolsoId,
        validadeMaxima = 5 minutos
    )

    se valido for falso:
        auditoria.registrar(usuario.id, "reembolso_negado_sem_reautenticacao", reembolsoId)
        controleTentativas.registrarFalha(usuario.id, "confirmar_reembolso")
        retornar resposta 401 genérica

    reembolso = reembolsos.buscarPendente(reembolsoId)
    se reembolso não existir:
        retornar resposta 404

    transacao.executarAtomica:
        se reembolso.jaConfirmado ou comprovanteMfa.jaConsumido:
            abortar transacao e retornar resposta 409 genérica
        autenticacao.consumirConfirmacao(comprovanteMfa)
        reembolso.confirmarComChaveIdempotente(reembolsoId)
        auditoria.registrar(usuario.id, "reembolso_confirmado", reembolsoId)
    retornar resposta 200
~~~

**Resultado esperado:** uma sessão isolada não autoriza operações críticas. A confirmação MFA é recente, vinculada à ação e ao recurso, possui uso único e deixa evidência de auditoria.

### Critérios de aceite

- Reembolso não pode ser confirmado por perfil diferente de administrador autorizado.
- A confirmação MFA possui validade máxima de cinco minutos, uso único e vínculo com a ação e o identificador do reembolso.
- Uma tentativa sem confirmação, expirada ou reutilizada não altera o estado financeiro.
- O consumo da confirmação MFA e a mudança do reembolso ocorrem atomicamente; uma chave idempotente impede processamento duplicado em requisições concorrentes.
- Respostas e logs não expõem código MFA, token de sessão, valores financeiros completos ou detalhes internos do controle.

**Referência OWASP:** [Authentication Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html), que orienta autenticação multifator, controles contra abuso de login e reautenticação para operações sensíveis.

## Síntese de rastreabilidade

| Risco | Requisito | Decisão de arquitetura | Prática | Testes |
| --- | --- | --- | --- | --- |
| R07 | RS02 | DA02 — autorização por função, vínculo e estado | Autorização por vínculo com pedido ativo | TS01, TS02 e TS03 |
| R01 | RS03 | DA03 — MFA e reautenticação | Reautenticação para operações sensíveis | TS04, TS05 e TS06 |

## Matriz de cobertura de segurança

| Elemento verificado | Risco | Requisito | Decisão de arquitetura | Testes que fornecem evidência |
| --- | --- | --- | --- | --- |
| Autorização por função, vínculo e estado de pedido | R07 | RS02 | DA02 | TS01, TS02 e TS03 |
| Minimização e expiração de localização | R07 | RS02 | DA02 | TS01 e TS03 |
| MFA recente, de uso único e vinculado à ação | R01 | RS03 | DA03 | TS04, TS05 e TS06 |
| Auditoria de permissões e operações sensíveis | R07 e R01 | RS02 e RS03 | DA02 e DA03 | TS01–TS06 |

Os exemplos são pseudocódigo deliberadamente independente de linguagem ou framework. Uma implementação futura deverá transformar os testes em testes unitários e de integração automatizados.
