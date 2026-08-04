# Modelagem de ameaças — Entrega Fácil

## 1. Identificação do sistema

| Item | Definição |
| --- | --- |
| Nome do sistema | Entrega Fácil |
| Integrantes | Ismael Hister Oliveira, Luis Francisco Brum Gomes, Ezequiel dos Santos Pereira e Davi Tito Tafernaberry |
| Repositório | [github.com/Ismael1012/Engenharia_Software_Seguro](https://github.com/Ismael1012/Engenharia_Software_Seguro) |

O Entrega Fácil foi escolhido por reunir diferentes perfis com permissões distintas, troca contínua de informações e operações sensíveis. Pedidos, pagamentos, localização, comunicações e decisões administrativas permitem analisar ameaças de segurança realistas com o método STRIDE.

## 2. Descrição do sistema

O Entrega Fácil é um aplicativo de delivery que conecta clientes, restaurantes e entregadores para solicitar, preparar, transportar e acompanhar pedidos. O sistema busca tornar a compra e a entrega de refeições e outros produtos mais práticas, permitindo acompanhamento do pedido e suporte quando houver problemas.

Os principais perfis são:

- **Cliente:** cria conta, consulta restaurantes e cardápios, realiza pagamentos, acompanha pedidos, conversa pelo aplicativo, solicita suporte e avalia a experiência.
- **Restaurante:** administra o perfil e o cardápio, recebe e prepara pedidos, atualiza o status, comunica indisponibilidades e consulta vendas e repasses.
- **Entregador:** mantém-se disponível, aceita entregas, consulta os dados necessários para retirada e entrega, atualiza o percurso, confirma a conclusão e consulta ganhos.
- **Administrador:** gerencia contas e permissões, trata denúncias e atendimentos, acompanha pagamentos e reembolsos, aplica medidas autorizadas e consulta registros de auditoria.

As funcionalidades centrais incluem cadastro e autenticação, gerenciamento de perfis e endereços, busca e cardápio, criação de pedidos, pagamento, atualização de status, despacho e confirmação de entregas, comunicação vinculada ao pedido, avaliações, denúncias, suporte, cancelamentos, reembolsos e repasses.

Para realizar essas operações, o sistema armazena ou transmite dados de identificação e contato, credenciais, endereços de entrega, localização temporária, itens e valores dos pedidos, dados de pagamento e transações, informações de restaurantes e entregadores, mensagens, avaliações, denúncias e logs de ações administrativas.

Os recursos que exigem maior proteção são as contas e credenciais, os dados pessoais e de localização, os dados e transações de pagamento, a integridade dos pedidos e seus status, as permissões administrativas e os registros de auditoria. O comprometimento desses recursos pode causar fraude financeira, exposição de privacidade, entregas indevidas, prejuízo operacional e perda de confiança no serviço.

## Levantamento inicial com stakeholders

O levantamento de requisitos está organizado em [docs/levantamento-stakeholders](levantamento-stakeholders):

- [Prompt da entrevista](levantamento-stakeholders/prompt-entrevista.md)
- [Cliente](levantamento-stakeholders/cliente.md)
- [Restaurante](levantamento-stakeholders/restaurante.md)
- [Entregador](levantamento-stakeholders/entregador.md)
- [Administrador](levantamento-stakeholders/administrador.md)

As entrevistas dos perfis Cliente, Restaurante, Entregador e Administrador foram concluídas. Elas serão utilizadas para completar a descrição do sistema, os ativos, o fluxo e a análise STRIDE.
