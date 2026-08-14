# Etapa 5 — Verificação de Vulnerabilidades

## 1. Contexto, autorização e ambiente

- **Sistema testado:** [OWASP Juice Shop](https://github.com/juice-shop/juice-shop), aplicação deliberadamente vulnerável para treinamento.
- **Endereço do ambiente local:** `http://localhost:3000/#/`.
- **Ferramenta:** OWASP ZAP 2.17.0.
- **Configuração:** modo padrão, política padrão, spider tradicional e spider moderno, seguidos de varredura automatizada.
- **Escopo ético:** somente a instância local, executada pelo grupo; nenhum sistema de terceiros foi testado.

Evidências da sessão:

- [Aplicação executada localmente](sistema-explorado.png);
- [configuração e conclusão da varredura](configuracoes-usadas.png);
- [lista principal de alertas](alertas-gerados.png);
- [execução auxiliar que identificou SQL Injection](teste-auxiliar.png).

A execução principal encontrou oito tipos de alerta. Uma execução auxiliar, mantida no mesmo ambiente autorizado, ampliou a navegação e produziu também o alerta de SQL Injection. Para atender ao escopo mínimo com maior profundidade, foram selecionados três achados representativos.

## 2. Achados selecionados

| ID | Alerta e evidência | Possível impacto | Relação com CWE/OWASP | Correção proposta |
| --- | --- | --- | --- | --- |
| A01 | **SQL Injection** no endpoint de pesquisa `/rest/products/search?q=`. O alerta aparece na [execução auxiliar](teste-auxiliar.png). | Uma entrada incorporada diretamente à consulta pode alterar sua estrutura, permitindo leitura ou modificação de registros conforme as permissões da conta do banco. | [CWE-89](https://cwe.mitre.org/data/definitions/89.html) e OWASP Top 10 — Injection. | Usar consultas parametrizadas em todas as consultas; evitar concatenação de entrada; executar a aplicação com usuário de banco de privilégio mínimo; validar com teste automatizado contendo metacaracteres de SQL. |
| A02 | **CORS configurado com origem curinga**, indicado como “Configuração Incorreta Entre Domínios” na [lista principal](alertas-gerados.png), com resposta contendo `Access-Control-Allow-Origin: *`. | Permite que qualquer origem leia respostas públicas habilitadas para CORS. A exposição de dados autenticados depende também do uso de credenciais, cookies e outros cabeçalhos; por isso o impacto deve ser confirmado por endpoint. | [CWE-942](https://cwe.mitre.org/data/definitions/942.html) — Permissive Cross-domain Policy. | Substituir `*` por allowlist de origens necessárias; não refletir `Origin` sem validação; permitir credenciais somente quando indispensável; testar origens autorizada, não autorizada e `null`. |
| A03 | **Content-Security-Policy ausente**, registrado na [lista principal](alertas-gerados.png). | A ausência de CSP não cria XSS isoladamente, mas remove uma camada de contenção caso outra falha permita injetar HTML ou JavaScript. | [CWE-693](https://cwe.mitre.org/data/definitions/693.html) — Protection Mechanism Failure; OWASP Content Security Policy Cheat Sheet. | Implantar inicialmente `Content-Security-Policy-Report-Only`, ajustar fontes necessárias e depois aplicar política como `default-src 'self'; object-src 'none'; base-uri 'self'; frame-ancestors 'self'`, usando nonces ou hashes quando necessários. |

## 3. Verificação das correções

| Achado | Evidência esperada após correção |
| --- | --- |
| A01 | Testes com entrada maliciosa não alteram a consulta; revisão confirma parametrização; nova varredura não reproduz o alerta. |
| A02 | Origem autorizada recebe o cabeçalho esperado; origem não autorizada não consegue ler a resposta; endpoints autenticados são testados separadamente. |
| A03 | O cabeçalho CSP aparece nas respostas, violações são acompanhadas no modo de relatório e a aplicação continua funcional após ativação da política. |

## 4. Relação com o projeto Entrega Fácil

Embora o teste tenha sido executado no Juice Shop, os resultados orientam o Entrega Fácil: A01 reforça validação e acesso seguro a dados; A02 protege APIs consumidas pelos aplicativos; e A03 reduz o impacto de eventual injeção de conteúdo na interface. Esses controles complementam os riscos R03, R07 e R08 e devem entrar nas verificações dinâmicas do pipeline da Etapa 7.

## 5. Limitações e possíveis falsos positivos

O ZAP observa respostas e comportamentos acessíveis durante a navegação realizada; ele não comprova sozinho que uma vulnerabilidade é explorável nem cobre todos os fluxos autenticados, regras de negócio ou estados da aplicação. Alertas de cabeçalhos indicam ausência de defesa em profundidade, mas sua severidade depende do conteúdo e do endpoint. O alerta de CORS exige validação manual por origem e por uso de credenciais. A SQL Injection deve ser confirmada de forma controlada por detalhes do alerta, revisão de código ou teste seguro, sem extração ou alteração indevida de dados.

Os demais alertas da sessão foram preservados nas capturas, mas não foram aprofundados por serem duplicados, informativos ou de menor prioridade para o limite desta entrega. Nenhum achado foi considerado corrigido: as correções são propostas e só poderão ser confirmadas após implementação e nova verificação.
