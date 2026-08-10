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

[Acessar documento da Etapa 2](docs/Análise%20e%20priorização%20de%20riscos.md)

O documento contém critérios de probabilidade e impacto, registro de riscos R01–R12, justificativas, priorização, estratégias de tratamento, mapeamento para as funções Govern, Identify, Protect, Detect, Respond e Recover, controles propostos, responsáveis, evidências, ordem de implementação e risco residual estimado.

### Próximas etapas

| Etapa | Entregável previsto |
| --- | --- |
| 3 — Arquitetura segura | 3 requisitos de segurança, 3 mapeamentos para CWE/OWASP, diagrama de arquitetura e 3 decisões justificadas. |
| 4 — Código seguro | 2 práticas de código seguro, cada uma com testes definidos antes da solução, implementação ou pseudocódigo e referência OWASP. |
| 5 — Verificação | Uma sessão autorizada de verificação, evidências e análise de até 3 achados com correções propostas. |
| 6 — Detecção de intrusões | Roteiro com eventos registrados, 3 regras de detecção e respostas iniciais. |
| 7 — DevSecOps e vídeo final | Pipeline proposto, critérios de bloqueio, roteiro e vídeo de apresentação. |

## Organização do repositório

```text
.
├── README.md
├── docs/                     # Documentos das etapas e entrevistas
│   └── levantamento-stakeholders/
└── diagramas/                # Imagens e arquivos-fonte Draw.io
```

## Critérios de colaboração

Cada integrante deve realizar commits próprios, com alterações relevantes e mensagens descritivas. Novos documentos, diagramas, fontes dos diagramas e evidências devem permanecer versionados neste repositório. As decisões das próximas etapas devem manter rastreabilidade com a cadeia **ameaça → risco → controle → requisito → teste**.
