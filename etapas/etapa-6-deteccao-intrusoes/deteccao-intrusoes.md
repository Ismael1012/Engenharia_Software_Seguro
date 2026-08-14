# Monitoramento e Detecção de Intrusões

Este documento apresenta o roteiro para o monitoramento contínuo e a detecção de intrusões no sistema **Entrega Fácil**, detalhando conceitos fundamentais, eventos indispensáveis para registro em log, regras de detecção alinhadas aos riscos identificados nas etapas anteriores e os procedimentos recomendados após a emissão de um alerta.

---

## 1. O que é Detecção de Intrusões

A **Detecção de Intrusões** é o conjunto de processos, mecanismos e ferramentas responsáveis por monitorar continuamente os eventos que ocorrem em uma aplicação, rede ou infraestrutura, com o objetivo de identificar comportamentos anômalos, atividades suspeitas ou violações das políticas de segurança do sistema.

Em uma plataforma de delivery como o **Entrega Fácil**, a detecção de intrusões atua como uma camada contínua de vigia operacional. Ela analisa requisições à API, tentativas de autenticação, transações de pedidos/pagamentos e acessos a dados sensíveis (como endereços e localizações de clientes) para sinalizar possíveis ataques em andamento ou abusos de privilégios.

---

## 2. Diferença entre Prevenir e Detectar

Embora atuem de forma complementar dentro de uma estratégia de defesa em profundidade, **prevenção** e **detecção** possuem papéis e dinâmicas distintas na segurança da informação:

*   **Prevenir (Controle Proativo / Antecipado):**
    *   **Conceito:** Implementa salvaguardas e barreiras para **impedir** que um ataque ou abuso ocorra antes que cause qualquer dano ao sistema.
    *   **Exemplos no Entrega Fácil:** Exigir autenticação multifator (MFA) para administradores, aplicar controle de acesso baseado em papéis e atributos (RBAC/ABAC) no servidor, validar e sanitizar rigorosamente parâmetros de entrada, e impor limites de taxa (*rate limiting*) na borda da API.
    *   **Limitação:** Nenhuma medida preventiva é 100% infalível contra falhas humanas, credenciais vazadas fora do sistema, vulnerabilidades desconhecidas (*Zero-Day*) ou erros de configuração.

*   **Detectar (Controle Reativo / Monitoramento):**
    *   **Conceito:** Identifica e sinaliza eventos suspeitos, anomalias ou tentativas de bypass que **estão acontecendo ou que acabaram de ocorrer**.
    *   **Exemplos no Entrega Fácil:** Sinalizar um volume excessivo de tentativas de login malsucedidas em um curto intervalo, identificar um entregador tentando consultar dados de entregas com as quais não possui vínculo ativo, ou alertar sobre um pico abrupto de respostas de erro na API.
    *   **Valor:** Fornece a visibilidade necessária para que a equipe de operação e segurança possa conter o impacto rapidamente, preenchendo a lacuna onde os mecanismos de prevenção falharam ou não atuaram.

---

## 3. Eventos do Sistema que Devem ser Registrados

Para viabilizar a detecção de intrusões e auditorias de segurança no **Entrega Fácil**, o sistema deve registrar eventos em um repositório de logs centralizado, protegido contra alterações (*append-only*). Cada registro deve conter o identificador do ator, a ação realizada, o recurso afetado, o endereço IP de origem, o timestamp sincronizado (UTC) e o resultado da operação.

Os principais eventos do sistema a serem registrados incluem:

1.  **Eventos de Autenticação e Gestão de Sessão:**
    *   Tentativas de login (bem-sucedidas e malsucedidas).
    *   Solicitações, validações e falhas nos desafios de MFA.
    *   Criação, renovação, expiração e revogação de tokens e sessões.
    *   Alterações de senha e solicitações de redefinição de credenciais.

2.  **Eventos de Autorização e Controle de Acesso:**
    *   Tentativas de acesso recusado (respostas HTTP 401 Unauthorized e HTTP 403 Forbidden).
    *   Tentativas de acesso a rotas e painéis administrativos por perfis não privilegiados.
    *   Consultas a dados pessoais de terceiros (endereço, telefone, localização) sem vínculo com pedido ativo.

3.  **Operações Sensíveis e Regras de Negócio:**
    *   Alterações em dados de cadastro críticos (dados bancários, chave Pix, e-mail e telefone).
    *   Criação, atualização de preço/descrição ou remoção de produtos por restaurantes.
    *   Processamento, autorização, contestação e confirmação de reembolsos e repasses.
    *   Transições do status de pedidos (preparo, despacho, entrega concluída e cancelamento).

4.  **Tráfego na Borda e Disponibilidade da API:**
    *   Disparos da limitação de requisições por IP ou token (respostas HTTP 429 Too Many Requests).
    *   Bloqueios efetuados pelo Web Application Firewall (WAF).
    *   Métricas de latência e consumo desproporcional de recursos por rota ou cliente.

5.  **Ações Administrativas e Moderação:**
    *   Bloqueios ou suspensões de contas de clientes, restaurantes ou entregadores (exigindo justificativa).
    *   Aprovação ou rejeição de novos cadastros de entregadores e restaurantes.
    *   Alterações em permissões e papéis de acesso no painel administrativo.

---

## 4. Regras de Detecção

Abaixo estão apresentadas três regras diretas de detecção, correlacionadas aos riscos prioritários analisados nas etapas anteriores do projeto **Entrega Fácil** (R01, R09 e R07):

### Regra 1: Tentativas Excessivas de Autenticação (Ataque de Força Bruta / Credential Stuffing)

| Campo | Descrição |
| :--- | :--- |
| **Risco observado** | **R01 — Uso indevido de conta** (Ataque de força bruta, credential stuffing ou tentativa de invasão de conta de usuário) |
| **Fonte de dados** | Logs do serviço de autenticação (`auth_logs` — eventos de login, IP de origem, ID do usuário e status da resposta) |
| **Condição de alerta** | Ocorrência de **mais de 10 tentativas malsucedidas de login (HTTP 401)** para a mesma conta de usuário ou provenientes do mesmo endereço IP em um intervalo de **2 minutos** |
| **Resposta inicial** | Aplicar limitação progressiva ao IP e desafio adicional à conta, emitir alerta e notificar o titular. Revogar sessões somente se a correlação indicar comprometimento — por exemplo, login bem-sucedido anômalo, troca de credencial ou uso posterior suspeito — evitando que tentativas externas derrubem sessões legítimas. |

---

### Regra 2: Sobrecarga Anômala de Requisições na API (Ataque de Negação de Serviço - DoS)

| Campo | Descrição |
| :--- | :--- |
| **Risco observado** | **R09 — Indisponibilidade da API** (Ataque de sobrecarga volumétrica ou exploração de endpoints públicos sem controle de capacidade) |
| **Fonte de dados** | Logs de tráfego do API Gateway e WAF (`gateway_access_logs` — contagem de chamadas por segundo, IP de origem e taxa de HTTP 429) |
| **Condição de alerta** | Ocorrência de **mais de 100 requisições por segundo** originadas do mesmo IP/token para endpoints da API ou taxa global de respostas **HTTP 429 superior a 5%** do volume total em um intervalo de **5 minutos** |
| **Resposta inicial** | Ativar regra automatizada no WAF para bloqueio/drop do IP ofensivo na borda, aplicar limitação rigorosa de requisições nos endpoints afetados e acionar alerta de alta prioridade para a equipe de Infraestrutura e DevSecOps |

---

### Regra 3: Múltiplos Acessos Negados a Dados de Entrega (Varredura / Exploração de Falha de Autorização)

| Campo | Descrição |
| :--- | :--- |
| **Risco observado** | **R07 — Exposição de endereço, telefone ou localização** (Tentativa de consulta indevida a entregas de terceiros / exploração IDOR) |
| **Fonte de dados** | Logs do serviço de autorização e auditoria da API (`audit_logs` — tentativas de consulta aos endpoints `/pedidos/{id}/entrega` e `/pedidos/{id}/localizacao`) |
| **Condição de alerta** | Ocorrência de **5 ou mais respostas HTTP 403** para **identificadores de pedidos distintos**, vinculadas à mesma conta autenticada, em um intervalo de **10 minutos**; elevar a confiança quando os IDs forem sequenciais, a frequência for automatizada ou a origem for anômala. |
| **Resposta inicial** | Limitar temporariamente as consultas, preservar as evidências e solicitar reautenticação. Revogar a sessão e sinalizar o perfil para investigação urgente somente após correlação confirmar indícios de varredura, reduzindo falsos positivos causados por interface defeituosa ou uso legítimo. |

---

## 5. O que Deve Acontecer Depois de um Alerta

Quando uma das regras de detecção dispara um alerta, o fluxo de **Resposta a Incidentes** deve ser iniciado de forma estruturada:

1.  **Triagem e Validação Inicial (Triage):**
    *   Verificar se o alerta representa uma ameaça real ou um falso positivo (por exemplo, diferenciar um pico legítimo de vendas em horário de pico de um ataque DoS real).
    *   Classificar a gravidade e o impacto potencial do evento (Baixo, Médio, Alto ou Crítico).

2.  **Contenção Imediata (Containment):**
    *   Executar ações rápidas para conter o avanço do ataque e mitigar os danos imediatos.
    *   *Exemplos de ações:* aplicar bloqueio temporário de IP no WAF, revogar tokens de sessão ativos de contas sob suspeita, suspender pontualmente o endpoint afetado ou limitar o acesso da conta investigada.

3.  **Investigação e Análise de Causa Raiz (Investigation & Eradication):**
    *   Analisar os logs centralizados de auditoria para determinar o vetor do ataque, quais dados foram acessados ou modificados e a extensão do comprometimento.
    *   Corrigir a vulnerabilidade de origem (por exemplo, ajustar regras de autorização no backend, atualizar limites de taxa ou corrigir falhas de validação).

4.  **Recuperação e Normalização (Recovery):**
    *   Restabelecer o funcionamento normal dos serviços ou acessos que foram temporariamente restringidos.
    *   Desbloquear usuários legítimos que foram afetados por contramedidas automáticas após validação de identidade e redefinição de credenciais.
    *   Manter monitoramento intensivo sobre os componentes envolvidos nas horas subsequentes.

5.  **Revisão Pós-Incidente e Lições Aprendidas (Post-Incident Review):**
    *   Elaborar um relatório sumário detalhando a cronologia do evento, a eficácia do alerta e o tempo de resposta da equipe.
    *   Ajustar os limiares e parâmetros das regras de detecção para reduzir falsos positivos e aprimorar a capacidade de resposta contínua.
