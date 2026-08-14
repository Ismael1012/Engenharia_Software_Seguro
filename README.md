# Entrega Fácil — Engenharia de Software Seguro

Projeto acadêmico da disciplina de Engenharia de Software Seguro. O repositório documenta a análise de segurança de uma plataforma conceitual de delivery, desde a modelagem de ameaças até as etapas futuras de arquitetura, implementação, verificação e operação segura.

> O escopo atual é documental: o objetivo é analisar riscos e propor controles para o sistema, não implementar uma plataforma de delivery completa.

## Sistema analisado

O **Entrega Fácil** conecta clientes, restaurantes e entregadores para realizar pedidos, pagamentos, acompanhamento de entregas, mensagens, avaliações e atendimento. Um perfil administrativo gerencia contas, permissões, denúncias, reembolsos e registros de auditoria.

| Perfil | Responsabilidades principais |
| --- | --- |
| Cliente | Criar pedidos, realizar pagamentos, acompanhar entregas, comunicar-se e avaliar. |
| Restaurante | Gerenciar cardápio, receber e preparar pedidos, atualizar status e acompanhar repasses. |
| Entregador | Aceitar entregas, consultar rota e localização temporária, confirmar entregas e acompanhar ganhos. |
| Administrador | Gerenciar contas e permissões, tratar denúncias, suporte e reembolsos, além de consultar logs. |

Os ativos mais críticos são contas e credenciais, dados pessoais e localização, pagamentos e repasses, pedidos e seus status, permissões administrativas, logs de auditoria, APIs, banco de dados e integrações externas.

## Integrantes

| Integrante | Matrícula |
| --- | --- |
| Ismael Hister Oliveira | 2410102162 |
| Luis Francisco Brum Gomes | 2310100558 |
| Ezequiel dos Santos Pereira | 2510200470 |
| Davi Tito Tafernaberry | 2410101763 |

Repositório do grupo: [github.com/Ismael1012/Engenharia_Software_Seguro](https://github.com/Ismael1012/Engenharia_Software_Seguro)

## Entregáveis

### Etapa 1 — Casos de abuso e modelagem de ameaças com STRIDE

| Artefato | Conteúdo |
| --- | --- |
| [Visão do sistema](docs/modelagem-de-ameacas.md) | Identificação, descrição, ativos, componentes e fluxo principal. |
| [Usuários, ativos e pontos de interação](docs/Usuários%2C%20ativos%20e%20pontos%20de%20interação.md) | Perfis, dados protegidos, componentes e ativos críticos. |
| [Modelagem STRIDE](docs/modelagem-stride.md) | Ameaças T01–T12 e relação com os casos de abuso. |
| [Casos de abuso](docs/Casos%20de%20Abuso.md) | Cenários CA01–CA12, condições, fluxo, impacto e relação com STRIDE. |
| [Levantamento com stakeholders](docs/levantamento-stakeholders/) | Roteiro e entrevistas por perfil. |

**Diagramas versionados:**

- [Diagrama de casos de uso — PNG](diagramas/diagrama-caso-de-uso.png) e [fonte Draw.io](diagramas/diagrama-caso-de-uso.drawio)
- [Diagrama de casos de abuso — PNG](diagramas/Casos%20de%20Abuso.png) e [fonte Draw.io](diagramas/Casos%20de%20Abuso.drawio)

### Etapa 2 — Análise, priorização e tratamento de riscos com NIST CSF 2.0

| Artefato | Conteúdo |
| --- | --- |
| [Análise e priorização de riscos](docs/Análise%20e%20priorização%20de%20riscos.md) | Critérios, registro R01–R12, justificativas e ordem de prioridade. |
| [Tratamento de riscos](docs/Tratamento%20de%20riscos.md) | Estratégias, NIST CSF 2.0, controles, responsáveis, evidências, implementação e risco residual. |

### Etapa 3 — Projeto de uma arquitetura segura

[Acessar requisitos, vulnerabilidades catalogadas, diagrama e decisões de arquitetura](docs/Arquitetura-segura.md).

### Etapa 4 — Código seguro e testes de segurança

[Acessar as duas práticas, os testes definidos antes da solução e o pseudocódigo](docs/Codigo-seguro.md).

### Etapa 5 — Verificação de vulnerabilidades

[Acessar o relatório da verificação autorizada no OWASP Juice Shop](evidencias/etapa-5/relatorio-da-verificacao.md).

### Etapa 6 — Monitoramento e detecção de intrusões

[Acessar o roteiro de eventos, regras de detecção e resposta a alertas](roteiros/etapa-6-Monitoramento%20e%20Detecção%20de%20Intrusões.md).

### Etapa 7 — DevSecOps e vídeo final

[Acessar o pipeline, os critérios de bloqueio e o roteiro do vídeo final](roteiros/etapa-7-devsecops-e-video-final.md).

> **Vídeo final:** inserir aqui o endereço compartilhado do vídeo após a publicação, verificando o acesso pelo professor.

## Organização do repositório

```text
.
├── README.md
├── docs/                         # Documentos das etapas 1 a 4 e entrevistas
│   └── levantamento-stakeholders/
├── diagramas/                    # Imagens e arquivos-fonte Draw.io/Mermaid
│   └── etapa-3/
├── evidencias/
│   └── etapa-5/                  # Relatório e capturas da verificação
└── roteiros/                     # Etapas 6 e 7

```
