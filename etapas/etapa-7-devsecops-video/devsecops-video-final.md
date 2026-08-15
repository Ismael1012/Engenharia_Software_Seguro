# Etapa 7 — Roteiro consolidado do vídeo final

Este arquivo reúne, sem resumir as falas já elaboradas, os roteiros das Etapas 1 a 7 e a apresentação do pipeline DevSecOps. Os arquivos separados podem ser mantidos como apoio individual para os apresentadores.

**Vídeo publicado:** [Apresentação final do projeto Entrega Fácil](https://www.youtube.com/watch?v=arO6msi1nhE&feature=youtu.be)

## Etapas 1 e 2 — Ismael

### Introdução

“Olá, eu sou o Ismael e juntamente com o Davi, Ezequiel e o Francisco, vamos apresentar o trabalho que foi desenvolvido ao longo dessa disciplina. Então eu vou explicar brevemente sobre as primeiras duas etapas do trabalho, onde o nosso objetivo foi analisar a segurança de um sistema antes de sua implementação, identificando possíveis ameaças, comportamentos maliciosos e impactos.”

### Slide 1 — Sistema escolhido

“Para o nosso trabalho, optamos por escolher um aplicativo de delivery, pois ele envolve diferentes usuários, informações e operações que precisam ser consideradas na construção e, principalmente, na segurança do software.”

### Slide 2 — Características do sistema

“Nesse sistema, temos diferentes níveis de acesso e uma comunicação entre os usuários. Também são trabalhados dados pessoais e de localização, além de informações relacionadas aos pedidos e pagamentos. Por isso, ele apresenta vários pontos que podem ser explorados de maneira indevida e que precisam ser considerados na análise de segurança.”

### Slide 3 — Diagrama de casos de uso

“A partir dessas características, primeiro identificamos o funcionamento normal do sistema por meio do diagrama de casos de uso. Nele, temos quatro atores principais: cliente, restaurante, entregador e administrador, cada um relacionado às funcionalidades que pode executar.”

“Por exemplo, o cliente pode realizar pedidos e acompanhar sua entrega; o restaurante pode gerenciar seus produtos e pedidos; o entregador pode atualizar a entrega; e o administrador possui funções de gerenciamento do sistema.”

“Também mantivemos cada caso de uso representando uma única função, evitando juntar operações diferentes em um mesmo caso.”

### Slide 4 — Diagrama de casos de abuso

“Depois de identificar o funcionamento normal, analisamos como essas mesmas funcionalidades poderiam ser utilizadas de forma maliciosa.”

“Inicialmente, identificamos 18 possíveis casos de abuso. Porém, para manter o diagrama mais objetivo, selecionamos 12 casos mais relevantes, priorizando aqueles que poderiam causar maior impacto à segurança do sistema.”

“Também buscamos manter uma representação dos diferentes tipos de atores mal-intencionados, como atacante externo, cliente, restaurante, entregador e fraudador.”

“Por exemplo, um atacante externo pode tentar invadir uma conta, um cliente mal-intencionado pode manipular o valor de um pedido, e um entregador pode confirmar uma entrega que não foi realizada.”

“Os casos selecionados foram então relacionados às funcionalidades correspondentes e utilizados como base para a análise de ameaças com STRIDE.”

### Slide 5 — Etapa 2: análise e tratamento dos riscos

“Na segunda etapa, transformamos as ameaças e os casos de abuso em riscos avaliáveis. Para cada risco, atribuímos valores de probabilidade e impacto de um a quatro e calculamos a pontuação pela multiplicação desses dois valores. Os resultados foram classificados como baixos, médios, altos ou críticos.”

“Os principais riscos foram a indisponibilidade da API, representada pelo R09; a exposição de endereço, telefone ou localização, no R07; o uso indevido de contas, no R01; e o cadastro falso de restaurantes ou entregadores, no R02. A prioridade considerou não apenas a pontuação, mas também o número de usuários afetados, os possíveis danos financeiros e de privacidade e as dependências entre os controles.”

“Depois, relacionamos os riscos às funções Govern, Identify, Protect, Detect, Respond e Recover do NIST CSF 2.0. Para cada risco definimos uma estratégia de tratamento, controles concretos, responsáveis e evidências de verificação. Também estimamos o risco residual, deixando claro que ele só poderá ser confirmado depois da implementação e dos testes.”

## Etapas 3 e 4 — Davi

“Nas Etapas 3 e 4, transformamos os riscos anteriores em decisões técnicas verificáveis. Primeiro projetamos a arquitetura segura do Entrega Fácil. Depois demonstramos, com testes e pseudocódigo, como duas decisões seriam implementadas, mantendo a ligação entre risco, requisito e prática de código.”

### Etapa 3: requisitos e vulnerabilidades

“Selecionamos três riscos prioritários. Para o R09, de indisponibilidade da API, o requisito RS01 limita requisições por origem e rota, responde com HTTP 429 quando o limite é excedido e gera alertas.

Para o R07, de exposição de dados de entrega, o RS02 permite endereço, telefone e localização apenas a perfis autorizados e vinculados a um pedido ativo. Após a entrega, a localização deixa de ser disponibilizada.

Para o R01, de uso indevido de conta, o RS03 exige MFA administrativo e nova autenticação antes de operações sensíveis, como alterar dados bancários ou confirmar reembolso.

Esses requisitos foram relacionados às vulnerabilidades CWE-770, sobre ausência de limites; CWE-639, sobre falha de autorização; e CWE-287, sobre autenticação inadequada.”

### Etapa 3: arquitetura e decisões

“No diagrama, as aplicações se comunicam com um API Gateway e WAF, que limitam requisições antes que o tráfego alcance os serviços internos.

A autenticação centralizada utiliza MFA e sessões revogáveis. Nos serviços de negócio, a autorização é validada no servidor considerando perfil, vínculo com o pedido e estado da operação. Banco de dados e integrações ficam atrás desses controles, enquanto logs centralizados apoiam auditoria.

As decisões DA01, DA02 e DA03 tratam, respectivamente, disponibilidade, proteção dos dados de entrega e uso indevido de contas.”

### Etapa 4: testes e práticas seguras

“Na Etapa 4 selecionamos autorização por vínculo com pedido ativo e reautenticação para operações sensíveis. Os testes foram definidos antes do pseudocódigo.

Na primeira prática, o TS01 permite ao entregador consultar seu pedido ativo. O TS02 bloqueia pedidos de outro entregador e o TS03 impede acesso após a entrega. A API nega por padrão e valida perfil, vínculo e status em cada solicitação.

Na segunda prática, o TS04 confirma reembolso somente com MFA recente. O TS05 recusa a operação sem reautenticação e o TS06 bloqueia comprovantes expirados ou reutilizados. A confirmação possui uso único, é vinculada ao reembolso e consumida na mesma transação. Uma chave de idempotência impede processamento duplicado.”

### Encerramento das Etapas 3 e 4

“Assim, os riscos foram convertidos em requisitos mensuráveis, posicionados na arquitetura e representados por testes e práticas de implementação. Essa rastreabilidade permite verificar se os controles realmente tratam os riscos prioritários do Entrega Fácil.”

## Etapa 5 — Ezequiel

### Objetivo e ambiente autorizado

“Na Etapa 5 verificamos como uma ferramenta identifica possíveis falhas em uma aplicação web. Utilizamos o OWASP Juice Shop, executado localmente e criado para treinamento. Assim, o teste ocorreu em ambiente controlado e autorizado, sem analisar sistemas de terceiros.”

### Ferramenta e execução

“Utilizamos o OWASP ZAP 2.17.0 para uma varredura automatizada no endereço local da aplicação, com política padrão, spider tradicional e spider moderno. As capturas registram a configuração, a conclusão e os alertas encontrados.”

### Três achados selecionados

“Entre os resultados, selecionamos três achados para análise. O A01 foi uma possível injeção SQL no endpoint de pesquisa. Esse problema pode permitir que uma entrada altere a consulta ao banco. A correção proposta é usar consultas parametrizadas, evitar concatenação de entrada e aplicar privilégio mínimo no banco de dados.

O A02 foi uma configuração CORS permissiva, com origem curinga. A recomendação é usar uma lista explícita de origens confiáveis e testar separadamente os endpoints autenticados.

O A03 foi a ausência do cabeçalho Content Security Policy. Ela não cria uma injeção isoladamente, mas reduz a proteção caso outra falha permita conteúdo malicioso. A proposta é configurar uma política restritiva, primeiro em modo de relatório.”

### Limitações, relação com o projeto e conclusão

“Os alertas do ZAP não comprovam sozinhos que uma vulnerabilidade é explorável. Por isso, consideramos contexto, possíveis falsos positivos e a necessidade de confirmação manual. Embora o teste tenha usado o Juice Shop, os resultados orientam o Entrega Fácil na proteção de consultas, APIs e interfaces. Nenhum achado foi considerado corrigido apenas pela proposta: após implementar os controles, seria necessária uma nova varredura para produzir evidências da correção.”

## Etapa 6 — Luis Francisco

### Conceito e objetivo

“Na Etapa 6 definimos como o Entrega Fácil identificaria comportamentos suspeitos em operação. Prevenir significa aplicar controles como MFA, autorização e limitação de requisições. Detectar significa perceber rapidamente uma tentativa ou atividade anormal, inclusive quando a prevenção não foi suficiente.”

### Eventos e fontes de dados

“O sistema deve registrar autenticações, falhas de MFA, sessões, acessos negados, consultas a dados pessoais, mudanças em pedidos e pagamentos, ações administrativas e eventos da API. Os logs devem conter ator, ação, recurso, origem, horário e resultado, sem expor dados sensíveis.”

### Três regras de detecção

“A primeira regra trata o R01, de uso indevido de conta. Mais de dez logins malsucedidos para a mesma conta ou origem, em dois minutos, geram alerta, limitação progressiva e desafio adicional. Sessões só são revogadas quando outros sinais indicam comprometimento.

A segunda regra observa o R09, de indisponibilidade da API. Mais de cem requisições por segundo pela mesma origem, ou muitas respostas 429, acionam o WAF, limitação mais rigorosa e alerta.

A terceira regra trata o R07, de exposição de dados. Cinco acessos negados a pedidos diferentes, pela mesma conta em dez minutos, podem indicar varredura. O sistema limita consultas, preserva evidências e solicita nova autenticação.”

### Resposta e melhoria contínua

“Depois do alerta, a equipe realiza a triagem para confirmar o incidente ou falso positivo e classificar sua gravidade. Em seguida, contém o evento, preserva registros, investiga a causa, corrige a falha e recupera os serviços. Uma revisão pós-incidente avalia a resposta e ajusta as regras. Assim, o monitoramento complementa a prevenção e melhora continuamente a segurança do Entrega Fácil.”

## Etapa 7 — Pipeline DevSecOps

### Conceito

“Na Etapa 7 reunimos os resultados em um pipeline DevSecOps, integrando segurança a todo o ciclo de desenvolvimento, e não somente à implantação.”

### Fluxo do pipeline

“O fluxo começa com STRIDE e análise de riscos. Os riscos prioritários geram requisitos e decisões de arquitetura. Na implementação, aplicamos código seguro e testes automatizados. Depois, código e dependências passam por análise estática, e a aplicação é verificada com o ZAP. Após a aprovação, ocorre a implantação controlada. Em operação, logs e regras de detecção apoiam resposta e melhoria contínua.”

### Condições de bloqueio

“O pipeline é bloqueado por teste crítico reprovado, segredo exposto, dependência crítica sem tratamento ou falha de acesso administrativo. Cada fase produz evidências, como testes, relatórios e logs. Assim, a implantação depende de critérios verificáveis, enquanto o monitoramento retorna informações ao planejamento e mantém a segurança em evolução.”

## Aprendizados e encerramento — Grupo

“Com este trabalho, aprendemos que a segurança não deve ser pensada apenas depois que o sistema está pronto. Ela começa na identificação das ameaças, continua na análise dos riscos, influencia a arquitetura e o código e precisa ser verificada e monitorada durante toda a operação. Também entendemos a importância de documentar as decisões e manter uma relação clara entre riscos, controles e testes. Como grupo, percebemos que desenvolver software seguro é um processo contínuo e uma responsabilidade compartilhada por todos. Obrigado pela atenção.”
