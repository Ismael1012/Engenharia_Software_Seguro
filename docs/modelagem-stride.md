# 5. Modelagem de ameaças com STRIDE

A tabela a seguir aplica o método STRIDE aos componentes e ativos do Entrega Fácil. As ameaças foram definidas a partir das operações descritas pelos stakeholders e dos fluxos de autenticação, pedido, entrega, pagamento e administração.

| ID | Categoria STRIDE | Componente ou ativo | Ameaça identificada | Possível impacto |
| --- | --- | --- | --- | --- |
| T01 | Spoofing | Conta e credenciais | Atacante usa credenciais obtidas por phishing, vazamento ou força bruta para se passar por um usuário legítimo. | Acesso a dados privados, pedidos indevidos e fraude financeira. |
| T02 | Spoofing | Cadastro de restaurante ou entregador | Fraudador cria conta com identidade ou documentos falsos e passa a receber pedidos ou dados de clientes. | Golpes, retirada indevida de pedidos e exposição de dados pessoais. |
| T03 | Tampering | Pedido, cardápio e pagamento | Cliente ou restaurante manipula valores, quantidades, preços ou descontos antes da validação no servidor. | Cobranças incorretas, prejuízo financeiro e inconsistência de pedidos. |
| T04 | Tampering | Dados de conta e dados bancários | Usuário com acesso indevido altera endereço, contato, dados bancários ou configurações de outra conta. | Desvio de repasses, perda de acesso e fraude contra o titular. |
| T05 | Repudiation | Confirmação de retirada, entrega e reembolso | Cliente, entregador ou restaurante nega posteriormente uma entrega, retirada ou solicitação de reembolso realizada. | Disputas financeiras e impossibilidade de responsabilizar o agente. |
| T06 | Repudiation | Logs e registros de auditoria | Ações administrativas críticas são executadas sem registro confiável de autor, horário e justificativa. | Investigação comprometida, decisões contestáveis e impunidade por abuso. |
| T07 | Information Disclosure | Endereço, telefone e localização | Falha de autorização expõe dados de contato ou localização a perfis sem pedido ativo relacionado. | Perseguição, golpes, risco físico e violação de privacidade. |
| T08 | Information Disclosure | Banco de dados, chat e documentos | Dados pessoais, documentos, conversas ou informações financeiras ficam acessíveis por falha de acesso ou vazamento. | Fraude de identidade, sanções e perda de confiança. |
| T09 | Denial of Service | API e infraestrutura | Atacante sobrecarrega endpoints públicos com requisições para impedir o uso normal do aplicativo. | Pedidos, pagamentos e entregas indisponíveis; perda de vendas. |
| T10 | Denial of Service | Controle de contas | Administrador mal-intencionado bloqueia contas legítimas sem justificativa ou revisão. | Usuários impedidos de pedir, vender, entregar ou acessar ganhos. |
| T11 | Elevation of Privilege | API e controle de autorização | Falha na validação de função permite que usuário comum execute operações de administrador ou de outro perfil. | Acesso a dados sensíveis, alterações indevidas e fraude. |
| T12 | Elevation of Privilege | Painel administrativo | Permissões excessivas ou ausência de separação de funções permitem acesso administrativo além do necessário. | Abuso de privilégios, reembolsos indevidos e manipulação de evidências. |

## Relação com os casos de abuso

| Caso de abuso | Ameaças STRIDE relacionadas |
| --- | --- |
| CA01 — Invadir conta de usuário | T01, T04 |
| CA02 — Alterar dados de outra conta | T04, T12 |
| CA03 — Alterar produto ou preço indevidamente | T03 |
| CA04 — Informar status falso do pedido | T03, T05 |
| CA05 — Confirmar entrega não realizada | T05 |
| CA06 — Manipular valor do pedido | T03 |
| CA07 — Publicar avaliação falsa | T03 |
| CA08 — Bloquear usuário sem justificativa | T10, T12 |
| CA09 — Indisponibilizar o aplicativo | T09 |
| CA10 — Acessar dados pessoais de clientes | T07, T08, T11 |
| CA11 — Criar conta falsa de restaurante ou entregador | T02, T11 |
| CA12 — Solicitar reembolso fraudulento | T05 |
