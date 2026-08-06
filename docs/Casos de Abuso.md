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
