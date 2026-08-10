## 9. Tratamento dos riscos com o NIST CSF 2.0

O tratamento proposto usa o NIST Cybersecurity Framework 2.0 para organizar resultados de segurança esperados. As funções não são controles: por exemplo, **Protect** é uma função, proteger o acesso às contas é um resultado esperado e MFA é um controle concreto que pode contribuir para esse resultado.

| Função | Finalidade no Entrega Fácil |
| --- | --- |
| Govern | Definir políticas, responsáveis, prioridades, critérios de aceitação de risco e revisão de acessos. |
| Identify | Conhecer ativos, dados, perfis, dependências externas, vulnerabilidades e riscos da plataforma. |
| Protect | Aplicar salvaguardas para contas, autorização, dados, transações e disponibilidade. |
| Detect | Identificar acessos anormais, alterações suspeitas, indisponibilidade e tentativas de abuso. |
| Respond | Conter incidentes, investigar, comunicar os envolvidos e tratar a causa. |
| Recover | Restaurar dados, acessos e disponibilidade e reduzir os impactos do incidente. |

### 9.1 Estratégias de tratamento

| Estratégia | Descrição |
| --- | --- |
| Evitar | Eliminar a atividade ou condição que gera o risco. |
| Reduzir | Implementar medidas que diminuam probabilidade ou impacto. |
| Compartilhar | Atribuir parte da operação ou das consequências a um terceiro especializado. |
| Aceitar | Manter conscientemente o risco, com justificativa, responsável e acompanhamento. |

### 9.2 Estratégia escolhida para cada risco

| Risco | Nível inicial | Estratégia principal | Justificativa |
| --- | --- | --- | --- |
| R01 | Crítico | Reduzir | O acesso por conta é indispensável, mas MFA, limitação de tentativas e reautenticação reduzem sua exploração. |
| R02 | Crítico | Reduzir | O cadastro de parceiros é necessário, porém a validação de identidade e aprovação controlada reduzem a fraude. |
| R03 | Alto | Reduzir | Pedidos e avaliações precisam continuar disponíveis, com validações e regras aplicadas no servidor. |
| R04 | Alto | Reduzir | Dados de conta são necessários, mas devem ser alterados somente pelo titular autorizado e com confirmação adicional. |
| R05 | Alto | Reduzir | Entregas e reembolsos são funções necessárias; provas e registros reduzem a contestação fraudulenta. |
| R06 | Médio | Reduzir | Logs confiáveis não eliminam a contestação, mas permitem investigar e responsabilizar ações. |
| R07 | Crítico | Reduzir | O endereço é necessário apenas durante a entrega e pode ter acesso limitado ao pedido ativo. |
| R08 | Alto | Reduzir | Dados e documentos devem permanecer no sistema, com acesso mínimo e proteção do armazenamento. |
| R09 | Crítico | Reduzir e compartilhar | Limites, monitoramento e contingência são internos; CDN, WAF e mitigação de DDoS podem ser contratados de provedor especializado. |
| R10 | Médio | Reduzir | O bloqueio é necessário para moderação, mas deve exigir justificativa, registro e revisão. |
| R11 | Alto | Reduzir | A autorização no servidor e a negação por padrão reduzem o acesso entre perfis. |
| R12 | Alto | Reduzir | Menor privilégio, separação de funções e revisão de permissões reduzem abuso administrativo. |

Nesta etapa não há aceitação deliberada de um risco inicial. Caso algum risco residual venha a ser aceito, a aprovação caberá ao responsável de segurança e à gestão do produto, somente após testes e evidências; a decisão deverá indicar nível residual, prazo de revisão e gatilhos de reavaliação, como incidente, mudança de arquitetura ou falha de controle.

### 9.3 Mapeamento dos riscos para as funções do NIST CSF 2.0

| Risco | Govern | Identify | Protect | Detect | Respond | Recover |
| --- | :---: | :---: | :---: | :---: | :---: | :---: |
| R01 — Uso indevido de conta | X |  | X | X | X | X |
| R02 — Cadastro falso | X | X | X | X | X |  |
| R03 — Manipulação de pedido | X |  | X | X | X | X |
| R04 — Alteração de dados de conta | X |  | X | X | X | X |
| R05 — Contestação fraudulenta | X |  | X | X | X | X |
| R06 — Falha de rastreabilidade | X |  | X | X | X |  |
| R07 — Exposição de localização | X |  | X | X | X |  |
| R08 — Vazamento amplo de dados | X | X | X | X | X | X |
| R09 — Indisponibilidade da API | X | X | X | X | X | X |
| R10 — Bloqueio indevido | X |  | X | X | X | X |
| R11 — Obtenção de privilégios | X | X | X | X | X | X |
| R12 — Privilégios administrativos excessivos | X | X | X | X | X |  |

As marcações refletem a necessidade de cada função no tratamento. Por exemplo, R07 exige impedir acesso indevido, detectar consultas anormais e responder ao vazamento, mas não possui uma ação de recuperação capaz de desfazer a exposição já ocorrida.

### 9.4 Plano de tratamento

| Risco | Estratégia | Controles propostos | Funções relacionadas | Responsáveis | Evidências e verificação |
| --- | --- | --- | --- | --- | --- |
| R01 | Reduzir | MFA por aplicativo autenticador; limitação de tentativas por conta e IP; reautenticação antes de trocar dados bancários ou confirmar reembolso; expiração e revogação de sessão; alerta de novo dispositivo. | Protect, Detect, Respond, Recover | Desenvolvimento e infraestrutura | Testes de MFA e bloqueio de tentativas; logs de login; simulação de sessão comprometida; verificação de alerta e revogação. |
| R02 | Reduzir | Validação de CPF/CNPJ e documentos; aprovação manual para perfis de parceiro; conta sem acesso a pedidos até aprovação; registro da decisão e origem da validação. | Govern, Identify, Protect, Detect, Respond | Operação de parceiros, desenvolvimento e prevenção a fraude | Teste de cadastro com documento inválido; amostra de aprovações revisada; logs de decisão; simulação de revogação de parceiro fraudulento. |
| R03 | Reduzir | Recalcular preços, descontos e frete no servidor; validar transições permitidas de status; manter histórico de preço e status; permitir avaliação somente após pedido concluído. | Protect, Detect, Respond, Recover | Desenvolvimento, produto e operação de pagamentos | Teste de requisição com valor e status manipulados; revisão do histórico; alerta para alterações incomuns; teste de restauração de estado. |
| R04 | Reduzir | Verificar no servidor o proprietário do recurso; exigir MFA ou senha atual para dados bancários; aplicar janela de confirmação e aviso ao titular após alteração sensível. | Protect, Detect, Respond, Recover | Desenvolvimento e suporte | Testes de acesso a recurso de terceiro; teste de alteração sem nova autenticação; logs e notificações; simulação de reversão pelo suporte. |
| R05 | Reduzir | Exigir código de entrega e, quando adequado, foto ou confirmação do cliente; registrar linha do tempo imutável do pedido; exigir evidências para reembolso e revisão em casos de alto valor. | Protect, Detect, Respond, Recover | Desenvolvimento, suporte, operação de entregas e financeiro | Teste de entrega sem código; consulta da trilha do pedido; amostra de reembolsos revisada; simulação de contestação e decisão documentada. |
| R06 | Reduzir | Enviar logs administrativos a serviço centralizado e somente de acréscimo; registrar autor, horário sincronizado, IP, ação, alvo e justificativa; restringir leitura e alteração de logs. | Govern, Protect, Detect, Respond | Infraestrutura, segurança e gestão administrativa | Teste de tentativa de alteração de log; consulta de rastreabilidade; verificação de retenção e sincronização de horário; revisão periódica de eventos críticos. |
| R07 | Reduzir | Aplicar autorização por vínculo com pedido ativo; mostrar endereço e contato apenas a envolvidos na entrega; ocultar ou remover localização após conclusão; registrar acessos fora do fluxo esperado. | Protect, Detect, Respond | Desenvolvimento, segurança e responsável por privacidade | Teste de perfil sem pedido relacionado; teste pós-entrega; análise de logs de consulta; simulação de incidente de privacidade. |
| R08 | Reduzir | Proteger endpoints e documentos com autorização no servidor; separar permissões de banco e armazenamento; criptografar dados em repouso com chaves gerenciadas; revisar permissões e acessos em lote. | Identify, Protect, Detect, Respond, Recover | Desenvolvimento, infraestrutura, segurança e responsável por privacidade | Testes de acesso cruzado e a documento privado; revisão de permissões; alerta de exportação incomum; teste de recuperação de backup sem ampliar acessos. |
| R09 | Reduzir e compartilhar | Limitar requisições por endpoint; usar WAF e mitigação de DDoS do provedor; cache para conteúdo público; monitorar latência, erro e capacidade; executar plano de contingência e comunicação. | Govern, Identify, Protect, Detect, Respond, Recover | Infraestrutura, desenvolvimento, provedor de nuvem e gestão de produto | Teste de carga autorizado; relatório do WAF; alertas de disponibilidade; simulação do plano de contingência e registro de comunicação. |
| R10 | Reduzir | Exigir justificativa obrigatória; separar solicitação e aprovação de bloqueio para casos não emergenciais; notificar o usuário; permitir revisão e reversão com trilha de auditoria. | Govern, Protect, Detect, Respond, Recover | Administração, suporte e desenvolvimento | Teste de bloqueio sem justificativa; auditoria de bloqueios; simulação de recurso e reversão; verificação de notificação ao usuário. |
| R11 | Reduzir | Aplicar RBAC/ABAC no servidor em todos os endpoints protegidos; negar acesso por padrão; testar autorização por objeto e função; revisar rotas administrativas antes de publicação. | Govern, Identify, Protect, Detect, Respond, Recover | Desenvolvimento e segurança | Testes automatizados de perfis e acesso a dados de terceiros; teste de endpoint administrativo com cliente comum; revisão de código e logs de negações. |
| R12 | Reduzir | Definir catálogo de papéis; separar permissões de reembolso, bloqueio, contas e logs; exigir MFA administrativo; revisar acessos trimestralmente e remover permissões sem necessidade. | Govern, Identify, Protect, Detect, Respond | Gestão, segurança, administradores e desenvolvimento | Matriz de permissões aprovada; testes de separação de funções; relatório trimestral de revisão; logs de operações administrativas. |

### 9.5 Ordem inicial de implementação

1. **Definir responsáveis, ativos críticos e matriz de papéis**, pois a governança e a definição de acesso são pré-requisitos para os demais controles.
2. **Validar autorização no servidor e limitar dados ao vínculo com o pedido**, reduzindo R04, R07, R08, R11 e R12 de forma conjunta.
3. **Proteger contas e cadastros de parceiros**, com MFA, limitação de tentativas e aprovação de identidade, para tratar R01 e R02.
4. **Proteger disponibilidade da API**, implantando limitação de requisições, WAF, monitoramento e contingência para R09, o risco de maior pontuação.
5. **Validar regras de pedido, entrega, preço e reembolso**, reduzindo R03 e R05 e preservando evidências da operação.
6. **Centralizar logs, alertas, resposta e recuperação**, apoiando R06 e R10 e permitindo verificar a eficácia dos controles anteriores.
7. **Revisar riscos, permissões e resultados de testes periodicamente**, pois mudanças de funcionalidade, parceiros ou incidentes podem alterar as avaliações.

Essa ordem prioriza riscos críticos, mas também antecipa controles de autorização e auditoria que reduzem vários riscos e são dependências para os controles seguintes.

### 9.6 Estimativa do risco residual

Os níveis abaixo são estimativas esperadas após implementação, testes e obtenção das evidências previstas. Não representam risco já reduzido.

| Risco | Nível inicial | Nível residual esperado | Condição para aceitar o residual |
| --- | --- | --- | --- |
| R01 | Crítico | Médio | MFA, limitação de tentativas, alertas e revogação de sessão aprovados em testes. |
| R02 | Crítico | Médio | Verificação documental, aprovação de parceiros e revogação testadas em fluxos simulados. |
| R03 | Alto | Médio | Cálculos e transições validados no servidor, histórico íntegro e testes de manipulação aprovados. |
| R04 | Alto | Baixo | Autorização por proprietário, nova autenticação e processo de reversão funcionando. |
| R05 | Alto | Médio | Provas de entrega, registros e regra de revisão de reembolso validados. |
| R06 | Médio | Baixo | Logs completos, protegidos e consultáveis em uma investigação simulada. |
| R07 | Crítico | Médio | Acesso limitado ao pedido ativo, dados removidos no momento correto e testes de acesso indevido aprovados. |
| R08 | Alto | Médio | Permissões revisadas, acessos cruzados bloqueados, monitoramento ativo e recuperação testada. |
| R09 | Crítico | Médio | Teste de carga, WAF, alertas e plano de contingência executados com sucesso. |
| R10 | Médio | Baixo | Justificativa, revisão, notificação e reversão de bloqueio verificadas. |
| R11 | Alto | Baixo | Todos os endpoints protegidos com negação por padrão e testes de função e objeto aprovados. |
| R12 | Alto | Baixo | Matriz de papéis, MFA administrativo e revisão de permissões aprovadas pela gestão. |

### 9.7 Conclusão do tratamento

Os riscos mais importantes são a indisponibilidade da API (R09), a exposição de endereço e localização (R07), o uso indevido de contas (R01) e o cadastro falso de parceiros (R02). Eles receberam prioridade por afetarem muitos usuários, comprometerem operações essenciais do delivery ou poderem causar fraude, violação de privacidade e risco físico.

A estratégia predominante é **reduzir** os riscos, pois pedidos, pagamentos, cadastros e entregas são atividades essenciais e não podem ser simplesmente eliminados. O NIST CSF 2.0 organiza essa redução principalmente nas funções Govern, Protect, Detect e Respond; Identify, Recover e o uso de provedores especializados também são essenciais para dados, disponibilidade e continuidade.

Os controles essenciais são autorização no servidor por perfil e vínculo com o pedido, MFA, validação de identidade de parceiros, validações de regras de negócio no servidor, provas de entrega, logs administrativos protegidos, limitação de requisições e monitoramento de disponibilidade. A principal limitação desta avaliação é que ela se baseia em uma arquitetura conceitual, sem métricas reais de tráfego, incidentes ou testes de segurança. Nas próximas etapas, os controles prioritários deverão gerar requisitos de segurança, decisões de arquitetura, exemplos de implementação e testes verificáveis.
