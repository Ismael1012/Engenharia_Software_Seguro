# Roteiro de apresentação — Etapas 3 e 4

**Duração aproximada:** 3 minutos  
**Tema:** arquitetura segura, código seguro e testes de segurança  
**Materiais na tela:** diagrama da Etapa 3, tabelas RS01–RS03 e DA01–DA03, testes TS01–TS06 e pseudocódigos da Etapa 4.

## 00:00–00:20 — Introdução e ligação com os riscos

**Na tela:** título “Etapas 3 e 4 — Da análise de riscos à implementação segura”.

**Fala:**

“Nas Etapas 3 e 4, transformamos os riscos anteriores em decisões técnicas verificáveis. Primeiro projetamos a arquitetura segura do Entrega Fácil. Depois demonstramos, com testes e pseudocódigo, como duas decisões seriam implementadas, mantendo a ligação entre risco, requisito e prática de código.”

## 00:20–01:15 — Etapa 3: requisitos e vulnerabilidades

**Na tela:** tabela dos requisitos RS01–RS03.

**Fala:**

“Selecionamos três riscos prioritários. Para o R09, de indisponibilidade da API, o requisito RS01 limita requisições por origem e rota, responde com HTTP 429 quando o limite é excedido e gera alertas.

Para o R07, de exposição de dados de entrega, o RS02 permite endereço, telefone e localização apenas a perfis autorizados e vinculados a um pedido ativo. Após a entrega, a localização deixa de ser disponibilizada.

Para o R01, de uso indevido de conta, o RS03 exige MFA administrativo e nova autenticação antes de operações sensíveis, como alterar dados bancários ou confirmar reembolso.

Esses requisitos foram relacionados às vulnerabilidades CWE-770, sobre ausência de limites; CWE-639, sobre falha de autorização; e CWE-287, sobre autenticação inadequada.”

## 01:15–01:55 — Etapa 3: arquitetura e decisões

**Na tela:** diagrama da arquitetura segura; destacar cada componente conforme ele for mencionado.

**Fala:**

“No diagrama, as aplicações se comunicam com um API Gateway e WAF, que limitam requisições antes que o tráfego alcance os serviços internos.

A autenticação centralizada utiliza MFA e sessões revogáveis. Nos serviços de negócio, a autorização é validada no servidor considerando perfil, vínculo com o pedido e estado da operação. Banco de dados e integrações ficam atrás desses controles, enquanto logs centralizados apoiam auditoria.

As decisões DA01, DA02 e DA03 tratam, respectivamente, disponibilidade, proteção dos dados de entrega e uso indevido de contas.”

## 01:55–02:42 — Etapa 4: testes e práticas seguras

**Na tela:** testes TS01–TS06 e, em seguida, os dois pseudocódigos.

**Fala:**

“Na Etapa 4 selecionamos autorização por vínculo com pedido ativo e reautenticação para operações sensíveis. Os testes foram definidos antes do pseudocódigo.

Na primeira prática, o TS01 permite ao entregador consultar seu pedido ativo. O TS02 bloqueia pedidos de outro entregador e o TS03 impede acesso após a entrega. A API nega por padrão e valida perfil, vínculo e status em cada solicitação.

Na segunda prática, o TS04 confirma reembolso somente com MFA recente. O TS05 recusa a operação sem reautenticação e o TS06 bloqueia comprovantes expirados ou reutilizados. A confirmação possui uso único, é vinculada ao reembolso e consumida na mesma transação. Uma chave de idempotência impede processamento duplicado.”

## 02:42–03:00 — Encerramento

**Na tela:** fluxo resumido “Risco → Requisito → Arquitetura → Teste → Pseudocódigo”.

**Fala:**

“Assim, os riscos foram convertidos em requisitos mensuráveis, posicionados na arquitetura e representados por testes e práticas de implementação. Essa rastreabilidade permite verificar se os controles realmente tratam os riscos prioritários do Entrega Fácil.”

## Orientações de apresentação

- Falar em ritmo natural, sem ler nomes completos de URLs ou referências.
- Apontar visualmente o componente mencionado no diagrama.
- Mostrar apenas as linhas relevantes das tabelas, evitando rolagem rápida.
- Destacar que o código é pseudocódigo conceitual, conforme permitido pelo enunciado.
- Ensaiar uma vez com cronômetro; o texto foi dimensionado para aproximadamente três minutos em ritmo de 135 a 145 palavras por minuto.
