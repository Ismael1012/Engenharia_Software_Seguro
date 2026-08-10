## 8. Análise e priorização de riscos

Esta etapa transforma as ameaças STRIDE e os casos de abuso da Etapa 1 em riscos que podem ser comparados, priorizados e tratados. A análise considera o contexto do **Entrega Fácil**, seus clientes, restaurantes, entregadores, administradores, aplicativos, API, banco de dados e serviços externos.

Para cada risco, foram identificados o evento capaz de causar prejuízo, sua origem na Etapa 1, a condição que permite sua ocorrência, a probabilidade, o impacto e a prioridade inicial.

### 8.1 Critérios de probabilidade

| Valor | Classificação | Critério utilizado |
| --- | --- | --- |
| 1 | Baixa | O evento depende de condições incomuns, acesso muito específico ou grande capacidade técnica. |
| 2 | Média-baixa | O evento é possível, mas depende de uma vulnerabilidade ou condição específica do sistema. |
| 3 | Média-alta | O evento é plausível e pode ocorrer em situações comuns de uso ou ataque. |
| 4 | Alta | O evento pode ocorrer com facilidade, frequência ou durante condições previsíveis do sistema. |

Os valores de probabilidade são justificados em cada risco com base nos perfis envolvidos, nas vulnerabilidades descritas na Etapa 1 e nas condições necessárias para exploração.

### 8.2 Critérios de impacto

| Valor | Classificação | Critério utilizado |
| --- | --- | --- |
| 1 | Baixo | Causa pequeno transtorno, prejuízo limitado ou pode ser corrigido rapidamente. |
| 2 | Moderado | Causa interrupção ou inconsistência limitada, com possibilidade de recuperação. |
| 3 | Alto | Causa prejuízo relevante aos usuários, ao negócio, à administração ou à privacidade. |
| 4 | Muito alto | Pode afetar muitos usuários, comprometer operações críticas, expor dados sensíveis ou causar prejuízo financeiro grave. |

Na avaliação foram considerados prejuízos financeiros, exposição de dados e localização, continuidade das entregas e pagamentos, danos à reputação, riscos físicos aos clientes, capacidade de recuperação e quantidade de pessoas afetadas.

### 8.3 Cálculo e classificação

A pontuação de cada risco é calculada pela fórmula:

`Pontuação = Probabilidade × Impacto`

| Pontuação | Nível do risco |
| --- | --- |
| 1 a 3 | Baixo |
| 4 a 7 | Médio |
| 8 a 11 | Alto |
| 12 a 16 | Crítico |

A pontuação permite comparar os riscos, mas não substitui a análise do contexto. Por esse motivo, a ordem de prioridade também considera ativos afetados, gravidade, dependências e possibilidade de recuperação.

### 8.4 Registro de riscos

| ID | Origem STRIDE e casos de abuso | Evento de risco | Vulnerabilidade ou condição | Probabilidade | Impacto | Pontuação | Nível |
| --- | --- | --- | --- | ---: | ---: | ---: | --- |
| R01 | T01 — Spoofing; CA01 | Um atacante usa credenciais comprometidas para acessar uma conta e realizar pedidos, alterações ou consultas em nome da vítima. | Ausência de MFA, proteção insuficiente contra força bruta e sessão sem revalidação em operações sensíveis. | 3 | 4 | 12 | Crítico |
| R02 | T02 — Spoofing; CA11 | Um fraudador é aprovado como restaurante ou entregador com identidade ou documentos falsos. | Cadastro com verificação documental insuficiente e concessão automática de permissões do perfil. | 3 | 4 | 12 | Crítico |
| R03 | T03 — Tampering; CA03, CA04, CA06 e CA07 | Um usuário manipula preço, quantidade, desconto, status de pedido ou avaliação por meio de alterações indevidas nas requisições ou regras de negócio. | Cálculos e transições confiados ao cliente, validação insuficiente no servidor e ausência de histórico verificável. | 3 | 3 | 9 | Alto |
| R04 | T04 — Tampering; CA01 e CA02 | Um agente com acesso indevido altera endereço, contato, dados bancários ou configurações de outra conta. | Falha de autorização por proprietário do recurso e ausência de nova autenticação para alterações sensíveis. | 2 | 4 | 8 | Alto |
| R05 | T05 — Repudiation; CA04, CA05 e CA12 | Cliente ou entregador contesta fraudulentamente um pedido, uma entrega ou um reembolso. | Prova de entrega insuficiente, regras de reembolso sem evidências e registros de operação incompletos. | 3 | 3 | 9 | Alto |
| R06 | T06 — Repudiation; CA02 e CA08 | Uma ação administrativa crítica não pode ser atribuída ao autor ou é contestada por falta de registros confiáveis. | Logs incompletos, alteráveis ou sem usuário, horário, origem e justificativa. | 2 | 3 | 6 | Médio |
| R07 | T07 — Information Disclosure; CA10 | Endereço, telefone ou localização de um cliente é consultado por um perfil sem pedido ativo relacionado. | Autorização insuficiente por vínculo com o pedido e dados de localização exibidos além do período necessário. | 3 | 4 | 12 | Crítico |
| R08 | T08 — Information Disclosure; CA10 | Dados pessoais, documentos, conversas ou informações financeiras são expostos por consulta indevida ou vazamento de armazenamento. | Controle de acesso inadequado à API, banco de dados ou armazenamento de documentos e permissões excessivas. | 2 | 4 | 8 | Alto |
| R09 | T09 — Denial of Service; CA09 | Endpoints públicos da API são sobrecarregados e impedem pedidos, pagamentos e acompanhamento de entregas. | Ausência de limitação de requisições, proteção de borda e capacidade suficiente para picos de acesso. | 4 | 4 | 16 | Crítico |
| R10 | T10 — Denial of Service; CA08 | Um administrador bloqueia indevidamente uma conta legítima e impede sua operação no aplicativo. | Permissão de bloqueio sem justificativa, revisão ou mecanismo de reversão. | 2 | 3 | 6 | Médio |
| R11 | T11 — Elevation of Privilege; CA10 e CA11 | Um usuário comum acessa funções ou dados de outro perfil, inclusive administrativos. | Verificação de função ausente ou inconsistente no servidor e endpoints sem negação por padrão. | 2 | 4 | 8 | Alto |
| R12 | T12 — Elevation of Privilege; CA02 e CA08 | Um administrador usa permissões excessivas para executar reembolsos, alterações de contas ou ações sobre logs fora de sua necessidade. | Ausência de menor privilégio, separação de funções e revisão periódica de acessos. | 2 | 4 | 8 | Alto |

### 8.5 Justificativas das avaliações

#### R01 — Uso indevido de conta

A probabilidade é média-alta (3), pois phishing, reutilização de senhas e tentativas automatizadas são cenários plausíveis para uma plataforma com vários perfis. O impacto é muito alto (4): o atacante pode expor dados pessoais, criar pedidos fraudulentos, alterar dados de conta e causar prejuízos a clientes, restaurantes e entregadores. A pontuação crítica representa a combinação entre fraude, privacidade e perda de confiança.

#### R02 — Cadastro falso de restaurante ou entregador

A probabilidade é média-alta (3) porque o abuso pode ocorrer sempre que a verificação de identidade e documentos for fraca ou automatizada sem revisão. O impacto é muito alto (4), pois a conta fraudulenta pode receber pedidos, dados de endereço e pagamentos, afetando diretamente clientes e a reputação da plataforma. Por envolver identidade falsa e acesso operacional real, o risco é crítico.

#### R03 — Manipulação de pedidos, preços, status ou avaliações

A probabilidade é média-alta (3), uma vez que clientes e restaurantes interagem frequentemente com essas funções e podem manipular requisições caso o servidor confie no aplicativo. O impacto é alto (3): há perdas financeiras, conflitos sobre pedidos e dano à reputação de restaurantes. O nível alto é adequado porque o prejuízo é relevante, embora normalmente possa ser investigado e corrigido com registros íntegros.

#### R04 — Alteração indevida de dados de conta

A probabilidade é média-baixa (2), pois depende de invasão de conta ou falha específica de autorização por proprietário do dado. O impacto é muito alto (4), especialmente quando o alvo são endereço, contato ou dados bancários, que podem permitir fraude, desvio de repasses e risco à segurança do titular. Portanto, o risco é alto e requer proteção antes das alterações sensíveis.

#### R05 — Contestação fraudulenta de entrega ou reembolso

A probabilidade é média-alta (3) porque disputas de entrega e pedidos de reembolso fazem parte da rotina do serviço e podem ser abusados sem prova adequada. O impacto é alto (3), causando perdas para restaurantes, entregadores ou plataforma e aumentando custos de suporte. A pontuação alta reflete a frequência possível e a dificuldade de decidir disputas sem evidências confiáveis.

#### R06 — Falha de rastreabilidade administrativa

A probabilidade é média-baixa (2), pois depende de registros incompletos, mal protegidos ou de uma operação administrativa crítica sem auditoria. O impacto é alto (3), porque a plataforma não conseguirá responsabilizar o agente, responder a denúncias ou restaurar a confiança após um abuso. O risco é médio, mas apoia a investigação de vários outros riscos.

#### R07 — Exposição de endereço, telefone ou localização

A probabilidade é média-alta (3), pois falhas de autorização em APIs podem ser exploradas por usuários autenticados e os dados são consultados durante fluxos comuns de entrega. O impacto é muito alto (4): além da violação de privacidade, a exposição pode resultar em golpes, perseguição e risco físico ao cliente. Por isso, este é um risco crítico.

#### R08 — Vazamento amplo de dados e documentos

A probabilidade é média-baixa (2), pois pressupõe uma falha específica na API, no banco de dados ou no armazenamento de documentos. O impacto é muito alto (4), já que documentos, conversas, dados financeiros e informações pessoais de muitos usuários podem ser expostos, com consequências legais e reputacionais. O risco é alto mesmo com probabilidade menor.

#### R09 — Indisponibilidade da API

A probabilidade é alta (4): picos de demanda são previsíveis em horários de refeição e endpoints públicos também podem sofrer sobrecarga intencional. O impacto é muito alto (4), pois clientes deixam de pedir, restaurantes deixam de vender, entregadores perdem trabalho e pagamentos ou entregas em andamento ficam sem atualização. A pontuação 16 faz deste o risco prioritário.

#### R10 — Bloqueio indevido de conta

A probabilidade é média-baixa (2) porque exige abuso de uma conta administrativa ou um processo de bloqueio mal projetado. O impacto é alto (3), pois pode interromper a renda do entregador, as vendas do restaurante ou o acesso do cliente. É um risco médio, mas exige trilha de auditoria e reversão rápida.

#### R11 — Obtenção indevida de privilégios

A probabilidade é média-baixa (2), pois requer uma falha de autorização em endpoint protegido. O impacto é muito alto (4), já que uma única falha pode permitir acesso a dados de terceiros, gestão de contas e operações administrativas. A classificação alta também se justifica por ser uma condição que pode viabilizar R04, R07, R08 e R12.

#### R12 — Uso abusivo de privilégios administrativos

A probabilidade é média-baixa (2) porque depende de permissões excessivas ou de uma conta administrativa comprometida. O impacto é muito alto (4), pois reembolsos, bloqueios, alterações cadastrais e evidências de auditoria podem ser manipulados. O risco é alto por concentrar grande poder operacional em um único perfil.

### 8.6 Priorização

A ordem inicial de prioridade é:

1. **R09 — Indisponibilidade da API:** possui a maior pontuação e paralisa simultaneamente as operações de todos os perfis.
2. **R07 — Exposição de endereço, telefone ou localização:** é crítico e pode causar dano físico, além de prejuízos à privacidade.
3. **R01 — Uso indevido de conta:** combina fraude financeira, alteração de dados e acesso a informações privadas.
4. **R02 — Cadastro falso de restaurante ou entregador:** permite que um fraudador entre no fluxo operacional e tenha contato com pedidos e dados de clientes.
5. **R11 — Obtenção indevida de privilégios:** embora tenha pontuação menor, sua correção reduz simultaneamente R04, R07, R08 e R12; por isso é uma dependência técnica prioritária.
6. **R03 — Manipulação de pedidos, preços, status ou avaliações:** afeta diretamente cobranças, entregas e confiança nos restaurantes.
7. **R05 — Contestação fraudulenta de entrega ou reembolso:** gera perdas recorrentes e exige evidências confiáveis para sua resolução.
8. **R08 — Vazamento amplo de dados e documentos:** pode atingir muitos usuários e gerar consequências legais, embora dependa de condição mais específica.
9. **R04 — Alteração indevida de dados de conta:** apresenta alto impacto financeiro e de privacidade, principalmente em dados bancários.
10. **R12 — Uso abusivo de privilégios administrativos:** deve ser reduzido após a definição central de autorização e separação de funções.
11. **R06 — Falha de rastreabilidade administrativa:** é essencial para investigar incidentes e sustenta os controles dos riscos anteriores.
12. **R10 — Bloqueio indevido de conta:** exige tratamento, mas seu impacto tende a ser mais localizado e reversível que os demais.

### 8.7 Conclusão da análise

A análise mostra que as ameaças não possuem a mesma prioridade. Os riscos críticos exigem atenção inicial, mas a correção de autorização no servidor (R11) também foi antecipada porque reduz vários riscos de privacidade e de abuso de privilégios. As classificações representam uma avaliação inicial e deverão ser revistas quando houver dados reais de tráfego, incidentes, arquitetura e testes.
