### 5. Modelagem de ameaças com STRIDE

| ID | Categoria STRIDE | Componente ou ativo | Ameaça identificada | Possível impacto |
| --- | --- | --- | --- | --- |
| T01 | Spoofing | Conta do usuário | Invadir conta de usuário | Roubo de dados, pedidos indevidos |
| T02 | Elevation of Privilege | Painel administrativo | Alterar dados de outra conta | Fraude, inconsistência de dados |
| T03 | Tampering | Produtos e cardápio | Alterar produto ou preço indevidamente | Manipulação de preços, fraude financeira e reclamações |
| T04 | Repudiation | Status de entregas | Confirmar entrega não realizada | Prejuízo financeiro |
| T05 | Information Disclosure | Sistema de avaliações | Publicar avaliação falsa | Manipulação de reputação, impacto financeiro | 
| T06 | Denial of Service | Controle de acesso | Bloquar usuário sem justificativa | Exclusão indevida, perda de clientes |

### 5.1 Interpretação da análise

Através da análise dos diagramas é evidente que diferentes partes do sistema precisam de mecanismos específicos de proteção. Cada categoria aponta para um tipo de vulnerabilidade e, consequentemente, para controles distintos. 
As contas dos usuários estão diretamente ligadas a identidade digital; produtos e pedidos dependem da integridade dos dados; logs e registros são fundamentais para responsabilizar autores das operações; sistema de avaliações exige confidencialidade e veracidade; portal e controle de acesso devem permanecer disponíveis e acessíveis apenas a usuários autorizados; funções administrativas devem ser acessíveis somente por usuários autorizado.


## 6. Casos de abuso
### CA01 — Invadir conta de usuário  
**Ator:** atacante externo.

**Objetivo:** acessar indevidamente a conta de um cliente ou restaurante para realizar operações fraudulentas.

**Condições necessárias:**

- o atacante obtém credenciais por phishing ou força bruta.
- o sistema não possui autenticação multifator.
- as sessões não expiram adequadamente.

**Fluxo de abuso:**

1. O atacante coleta credenciais da vítima.
2. O atacante autentica-se no aplicativo como se fosse o usuário legítimo.
3. O atacante acessa dados pessoais e históricos de pedidos.
4. O atacante realiza pedidos ou altera informações da conta.
5. O usuário percebe posteriormente movimentações indevidas.

**Impacto esperado:** roubo de dados, prejuízo financeiro e perda de confiança no sistema.

**Categorias STRIDE relacionadas:** Spoofing, Tampering e Repudiation.

---

### CA02 — Alterar dados de outra conta  
**Ator:** administrador mal-intencionado.

**Objetivo:** modificar informações de clientes ou restaurantes sem autorização.

**Condições necessárias:**

- o administrador possui acesso privilegiado.
- não há trilhas de auditoria eficazes.
- o sistema não valida permissões em operações críticas.

**Fluxo de abuso:**

1. O administrador acessa o painel de controle.
2. O administrador altera dados de contas de terceiros.
3. O sistema registra a alteração sem verificar justificativa.
4. O cliente ou restaurante é prejudicado.

**Impacto esperado:** fraude, perda de integridade dos dados e quebra de confiança.

**Categorias STRIDE relacionadas:** Elevation of Privilege e Tampering.

---

### CA03 — Alterar produto ou preço indevidamente  
**Ator:** restaurante mal-intencionado.

**Objetivo:** manipular preços ou descrições de produtos para obter vantagem indevida.

**Condições necessárias:**

- o sistema não valida alterações com histórico.
- não há controle de versão dos produtos.
- falta de monitoramento de mudanças suspeitas.

**Fluxo de abuso:**

1. O restaurante acessa a função de atualização de produto.
2. O restaurante altera preços ou descrições sem justificativa.
3. O sistema publica as alterações imediatamente.
4. Clientes são induzidos a erro ou pagam valores abusivos.

**Impacto esperado:** fraude financeira, perda de credibilidade e reclamações de clientes.

**Categorias STRIDE relacionadas:** Tampering e Repudiation.

---

### CA04 — Informar status falso do pedido  
**Ator:** cliente mal-intencionado.

**Objetivo:** enganar o sistema ou restaurante sobre o andamento do pedido.

**Condições necessárias:**

- o sistema permite atualização de status sem validação.
- não há confirmação cruzada entre cliente e restaurante.

**Fluxo de abuso:**

1. O cliente acessa sua conta.
2. O cliente altera o status do pedido para “não entregue”.
3. O sistema registra a alteração sem verificação.
4. O restaurante sofre prejuízo financeiro.

**Impacto esperado:** contestação de pagamentos, prejuízo ao restaurante e aumento de fraudes.

**Categorias STRIDE relacionadas:** Tampering e Repudiation.

---

### CA05 — Confirmar entrega não realizada  
**Ator:** entregador mal-intencionado.

**Objetivo:** registrar entregas falsas para receber pagamento sem cumprir o serviço.

**Condições necessárias:**

- o sistema não exige prova de entrega (assinatura ou foto).

- o entregador possui acesso direto à função de atualização.

**Fluxo de abuso:**

1. O entregador acessa o aplicativo.
2. O entregador marca o pedido como entregue sem realizar a entrega.
3. O sistema registra a entrega como concluída.
4. O cliente não recebe o pedido.

**Impacto esperado:** prejuízo financeiro, insatisfação do cliente e perda de credibilidade.

**Categorias STRIDE relacionadas:** Tampering e Repudiation.

---

### CA06 — Manipular valor do pedido  
**Ator:** cliente mal-intencionado.

**Objetivo:** reduzir ou aumentar indevidamente o valor de um pedido.

**Condições necessárias:**

- o sistema não valida cálculos de preço no servidor.
- o cliente consegue manipular requisições no front-end.

**Fluxo de abuso:**

1. O cliente inicia um pedido.
2. O cliente intercepta a requisição e altera o valor.
3. O sistema processa o pagamento com o valor manipulado.
4. O restaurante recebe menos do que deveria.

**Impacto esperado:** fraude financeira, prejuízo ao restaurante e inconsistência nos registros.

**Categorias STRIDE relacionadas:** Tampering.

---

### CA07 — Publicar avaliação falsa  
**Ator:** cliente mal-intencionado.

**Objetivo:** prejudicar ou favorecer restaurantes com avaliações falsas.

**Condições necessárias:**

- o sistema não valida se o cliente realmente realizou o pedido.

- não há mecanismos de detecção de padrões suspeitos.

**Fluxo de abuso:**

1. O cliente acessa a função de avaliação.
2. O cliente publica uma avaliação sem ter feito o pedido.
3. O sistema registra a avaliação como legítima.
4. A reputação do restaurante é manipulada.

**Impacto esperado:** perda de credibilidade, manipulação de reputação e impacto financeiro.

**Categorias STRIDE relacionadas:** Information Disclosure e Tampering.

---

### CA08 — Bloquear usuário sem justificativa  
**Ator:** administrador mal-intencionado.

**Objetivo:** excluir ou bloquear usuários sem motivo legítimo.

**Condições necessárias:**

- o administrador possui acesso irrestrito às funções de bloqueio.
- não há auditoria ou justificativa obrigatória para bloqueios.

**Fluxo de abuso:**

1. O administrador acessa o painel de controle.
2. O administrador bloqueia um usuário sem motivo.
3. O sistema registra o bloqueio como válido.
4. O usuário perde acesso ao aplicativo.

**Impacto esperado:** exclusão indevida, perda de clientes e quebra de confiança.

**Categorias STRIDE relacionadas:** Denial of Service e Elevation of Privilege.

---

### CA09 — Indisponibilizar o aplicativo  
**Ator:** atacante externo.

**Objetivo:** impedir que clientes, restaurantes, entregadores e administradores utilizem o aplicativo normalmente.

**Condições necessárias:**

- o sistema não possui mecanismos adequados de limitação de requisições;
- a infraestrutura não consegue absorver grande volume de acessos;
- não existem proteções contra ataques de negação de serviço.

**Fluxo de abuso:**

1. O atacante identifica endpoints públicos do aplicativo.
2. O atacante envia grande quantidade de requisições simultâneas.
3. Os servidores passam a consumir excessivamente seus recursos.
4. O sistema apresenta lentidão, falhas ou indisponibilidade.
5. Usuários legítimos deixam de conseguir acessar ou realizar pedidos.

**Impacto esperado:** indisponibilidade do serviço, perda de vendas, atrasos em pedidos e danos à reputação da plataforma.

**Categorias STRIDE relacionadas:** Denial of Service.

---

### CA10 — Acessar dados pessoais de clientes  
**Ator:** atacante externo, entregador mal-intencionado, restaurante mal-intencionado ou administrador mal-intencionado.

**Objetivo:** obter indevidamente informações pessoais de clientes, como nome, telefone, endereço, localização ou histórico de pedidos.

**Condições necessárias:**

- o sistema possui falhas de autorização;
- os dados são disponibilizados para usuários sem necessidade operacional;
- não existem controles adequados sobre o acesso às informações pessoais.

**Fluxo de abuso:**

1. O agente mal-intencionado acessa uma funcionalidade contendo dados de clientes.
2. O sistema não verifica corretamente se o usuário possui permissão.
3. O agente consulta informações de clientes com os quais não possui relação.
4. Os dados são copiados, armazenados ou compartilhados indevidamente.
5. As informações podem ser utilizadas para fraude, perseguição ou outros crimes.

**Impacto esperado:** violação de privacidade, exposição de endereços, risco à segurança física dos clientes e sanções legais para a plataforma.

**Categorias STRIDE relacionadas:** Information Disclosure e Elevation of Privilege.

---

### CA11 — Criar conta falsa de restaurante ou entregador  
**Ator:** fraudador.

**Objetivo:** passar-se por um restaurante ou entregador legítimo para obter dinheiro, pedidos ou informações pessoais de clientes.

**Condições necessárias:**

- o sistema não verifica adequadamente documentos e identidade;
- o cadastro de restaurantes ou entregadores é aprovado automaticamente;
- os dados fornecidos não são comparados com fontes confiáveis.

**Fluxo de abuso:**

1. O usuário mal-intencionado inicia o cadastro como restaurante ou entregador.
2. O atacante fornece informações falsas ou documentos adulterados.
3. O sistema aceita o cadastro sem validação suficiente.
4. A conta recebe permissões destinadas ao perfil informado.
5. O atacante acessa pedidos, pagamentos ou dados pessoais de clientes.

**Impacto esperado:** fraude financeira, exposição de dados pessoais, roubo de pedidos e perda de confiança na plataforma.

**Categorias STRIDE relacionadas:** Spoofing, Tampering e Elevation of Privilege.

---

### CA12 — Solicitar reembolso fraudulento  
**Ator:** cliente mal-intencionado.

**Objetivo:** obter a devolução do valor de um pedido que foi entregue corretamente.

**Condições necessárias:**

- o sistema permite solicitações de reembolso sem provas suficientes;
- não existe confirmação confiável da entrega;
- os registros do pedido são incompletos ou facilmente contestáveis.

**Fluxo de abuso:**

1. O cliente realiza um pedido normalmente.
2. O pedido é preparado e entregue corretamente.
3. O cliente informa falsamente que o pedido não foi entregue ou chegou incorreto.
4. O cliente solicita o reembolso pelo suporte.
5. O sistema aprova a devolução sem verificar adequadamente os registros.
6. O cliente permanece com o pedido e recebe o valor de volta.

**Impacto esperado:** prejuízo financeiro para o restaurante ou plataforma, aumento de fraudes e conflitos com entregadores.

**Categorias STRIDE relacionadas:** Repudiation e Tampering.

