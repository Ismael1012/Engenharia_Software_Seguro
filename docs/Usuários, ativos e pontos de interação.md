## 3. Usuários, ativos e pontos de interação

O sistema envolve os seguintes usuários e perfis de acesso:

- **Cliente:** solicitações de pedidos, pagamentos, acompanhamento de entregas, mensagens e avaliações.
- **Restaurante:** gestão de cardápio, recebimento e preparo de pedidos, atualizações de status, repasses e comunicação.
- **Entregador:** aceitação de entregas, localização temporária, rotas, confirmação de entrega e ganhos.
- **Administrador:** controle de contas, permissões, denúncias, suporte, reembolsos e logs de auditoria.

### 3.1 Ativos importantes

Os principais ativos identificados são:

- **Dados pessoais e sensíveis:** identidade, contato, endereço de entrega, localização temporária, documentos, telefone e e-mail.
- **Credenciais:** senhas, autenticação multifator e tokens de sessão para todos os perfis.
- **Pagamentos:** informações de pagamento, transações, reembolsos, repasses e comprovantes financeiros.
- **Avaliações:** notas e comentários de clientes sobre restaurantes e entregadores.
- **Mensagens:** chats vinculados a pedidos, comunicações de suporte e registros de conversas.
- **Localização:** rotas de entrega, posição do entregador em tempo real e informações de endereço.
- **Documentos:** dados bancários, documentos pessoais, comprovantes e informações de identificação de entregadores e restaurantes.
- **Banco de dados:** armazenamento de usuários, pedidos, pagamentos, avaliações, mensagens, denúncias e logs.
- **Servidores:** infraestrutura de aplicação e banco de dados que processa e entrega o serviço.
- **APIs:** interfaces entre aplicativos móveis, backend, serviços de pagamento e sistemas externos.
- **Aplicativos móveis:** apps dos clientes, restaurantes e entregadores que acessam o sistema.
- **Serviços externos:** gateways de pagamento, geolocalização, notificações, autenticação e serviços de mensageria.

### 3.2 Pontos de interação e componentes

| Elemento | Função |
| --- | --- |
| Aplicativo móvel | Interface utilizada por clientes, restaurantes e entregadores |
| Serviço de autenticação | Valida a identidade e as credenciais dos usuários |
| APIs | Processam pedidos, pagamentos, atualização de status e comunicações |
| Banco de dados | Armazena usuários, pedidos, pagamentos, avaliações, mensagens, denúncias e logs |
| Servidores | Hospedam a aplicação, o banco de dados e os serviços de back-end |
| Serviço de pagamentos | Processa transações, reembolsos e confirmações financeiras |
| Serviço de geolocalização | Fornece localização e rotas para entregas |
| Serviço de notificações | Envia atualizações de pedidos e mensagens aos usuários |

### 3.3 Ativos críticos

Os ativos considerados mais importantes são:

- Contas de usuário e credenciais, pois permitem acesso indevido ao sistema e controle de ações sensíveis.
- Dados de pagamento e transações, por causa do risco financeiro e de fraude em caso de acesso ou alteração.
- Dados pessoais e localização, já que podem causar exposição de privacidade e riscos físicos.
- Integração com APIs e serviços externos, pois interrupções ou manipulações podem quebrar pagamentos, notificações e entregas.
- Banco de dados e servidores, porque indisponibilidade ou destruição afeta a operação completa do serviço.
- Permissões administrativas e logs de auditoria, pois alteração indevida compromete investigação e controle de incidentes.

Esses elementos devem ser tratados como ativos críticos, pois seu comprometimento pode resultar em prejuízos financeiros, danos à privacidade, perda de confiança ou interrupção do serviço.