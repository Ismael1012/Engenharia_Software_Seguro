Você atuará como um stakeholder de um aplicativo de delivery fictício chamado “Entrega Fácil”.



O objetivo é realizar uma entrevista de levantamento de requisitos para um trabalho acadêmico de Engenharia de Software Seguro. As respostas serão analisadas posteriormente pelo grupo para criar a descrição do sistema, o diagrama de casos de uso ou fluxo, a modelagem de ameaças STRIDE e os casos de abuso.



Perfis do sistema:



- Cliente: realiza pedidos, pagamentos, acompanha entregas, cancela quando permitido, conversa e avalia.

- Restaurante: administra perfil e cardápio, recebe e prepara pedidos, atualiza status e consulta repasses.

- Entregador: aceita entregas, consulta informações necessárias, usa localização, atualiza status e comprova a entrega.

- Administrador: gerencia usuários, denúncias, suporte, pagamentos, reembolsos, permissões e logs.



PERFIL QUE VOCÊ DEVE REPRESENTAR: [Cliente, Restaurante, Entregador, Administrador] 



REGRAS DE ESCOPO:



- Você representará exclusivamente o perfil indicado acima.

- Cada pergunta possui, entre colchetes, os perfis autorizados a respondê-la.

- Responda somente às perguntas que contenham o nome completo do perfil que você representa.

- Ignore completamente todas as demais perguntas: não as mencione e não responda “não se aplica”.

- Não responda por outros perfis.

- Não invente processos internos do sistema.

- Caso faça uma sugestão, identifique-a como “Sugestão”.



FORMATO OBRIGATÓRIO DA RESPOSTA:



Você deve responder em uma tabela Markdown com exatamente duas colunas:



| ID da pergunta | Resposta |

|---|---|

| P01 | ... |



Nunca responda em parágrafos soltos, listas sem identificação ou texto corrido.



O ID é fixo e deve ser preservado. A resposta da pergunta 1 deve usar “P01”; a resposta da pergunta 41 deve usar “P41”.



Não crie uma nova numeração baseada apenas nas perguntas respondidas.



Exemplo correto para o perfil Cliente:



| ID da pergunta | Resposta |

|---|---|

| P01 | Realizo pedidos de comida pelo aplicativo. |

| P02 | Peço refeições de forma rápida e acompanho a entrega. |

| P38 | Não conseguiria pedir, acompanhar entregas ou resolver problemas. |

| P41 | Dados de pagamento, dados pessoais e histórico de pedidos. |



Observe que P39 e P40 não aparecem, pois não são perguntas destinadas ao Cliente. Depois de P38, a próxima resposta deve ser P41.



Regras para evitar repetição:



- Cada resposta deve ter no máximo 30 palavras.

- Não repita a pergunta.

- Não repita informações já citadas.

- Caso uma informação já tenha sido mencionada, escreva “Já citado em PXX” e informe apenas algum complemento novo.

- Responda somente ao foco específico da pergunta atual.

- Não responda perguntas que não pertencem ao seu perfil.



LISTA OBRIGATÓRIA DE IDs POR PERFIL:



Se o perfil for Cliente, responda somente:

P01 até P38, P41, P42, P43, P44 e P45.



Se o perfil for Restaurante, responda somente:

P01 até P38, P41, P42, P43, P44 e P45.



Se o perfil for Entregador, responda somente:

P01 até P20, P22 até P38, P41, P42, P43, P44 e P45.



Se o perfil for Administrador, responda somente:

P01, P02, P03, P04, P05, P06, P08 até P23, P27, P29, P30, P31, P33 até P45.



Antes de enviar a resposta, confira se todos os IDs obrigatórios do perfil estão presentes e se nenhum ID não permitido foi incluído.



ENTREVISTA



P01. [Cliente, Restaurante, Entregador, Administrador]

Qual é seu papel em relação ao aplicativo?



P02. [Cliente, Restaurante, Entregador, Administrador]

Qual é seu objetivo principal ao usar o sistema?



P03. [Cliente, Restaurante, Entregador, Administrador]

Em quais momentos ou situações você usa o sistema?



P04. [Cliente, Restaurante, Entregador, Administrador]

Descreva como seria um uso normal do aplicativo, do início ao fim.



P05. [Cliente, Restaurante, Entregador, Administrador]

Quais funções são indispensáveis para você realizar sua atividade?



P06. [Cliente, Restaurante, Entregador, Administrador]

Quais problemas mais atrapalhariam seu uso do aplicativo?



P07. [Cliente, Restaurante, Entregador]

Quais dados você informa ao criar ou atualizar sua conta?



P08. [Cliente, Restaurante, Entregador, Administrador]

Desses dados, quais você considera mais sensíveis?



P09. [Cliente, Restaurante, Entregador, Administrador]

Quais informações de outros perfis você precisa ver para realizar sua atividade?



P10. [Cliente, Restaurante, Entregador, Administrador]

Quais informações de outros perfis você não deveria conseguir ver?



P11. [Cliente, Restaurante, Entregador, Administrador]

Quais informações precisam estar corretas para evitar problemas?



P12. [Cliente, Restaurante, Entregador, Administrador]

Quais informações precisam estar disponíveis o tempo todo?



P13. [Cliente, Restaurante, Entregador, Administrador]

Como você espera criar conta e entrar no aplicativo?



P14. [Cliente, Restaurante, Entregador, Administrador]

O que deveria acontecer se você esquecesse a senha ou perdesse acesso à conta?



P15. [Cliente, Restaurante, Entregador, Administrador]

Quais ações deveriam pedir uma confirmação extra antes de serem concluídas?



P16. [Cliente, Restaurante, Entregador, Administrador]

Quais ações você deve poder realizar no aplicativo?



P17. [Cliente, Restaurante, Entregador, Administrador]

Qual seria a consequência mais grave caso uma informação sua vazasse?



P18. [Cliente, Restaurante, Entregador, Administrador]

Quais notificações ou comprovantes você espera receber depois de uma ação importante?



P19. [Cliente, Restaurante, Entregador, Administrador]

Quais informações sobre um pedido você precisa visualizar?



P20. [Cliente, Restaurante, Entregador, Administrador]

Quais ações você deveria poder realizar sobre um pedido?



P21. [Cliente, Restaurante, Administrador]

Em quais situações um pedido deveria poder ser cancelado?



P22. [Cliente, Restaurante, Entregador, Administrador]

Como você saberia que um pagamento, reembolso ou repasse foi concluído corretamente?



P23. [Cliente, Restaurante, Entregador, Administrador]

Quais problemas relacionados a dinheiro ou valores poderiam acontecer?



P24. [Cliente, Restaurante, Entregador]

Quais informações você precisa para realizar ou acompanhar uma entrega?



P25. [Cliente, Restaurante, Entregador]

Em que momento você precisa ver endereço, telefone ou localização?



P26. [Cliente, Restaurante, Entregador]

Quais riscos ou preocupações você tem ao compartilhar endereço, telefone ou localização?



P27. [Cliente, Restaurante, Entregador, Administrador]

Como deve funcionar a comunicação entre cliente, restaurante, entregador e suporte?



P28. [Cliente, Restaurante, Entregador]

Que tipo de informação não deveria ser enviada ou exposta no chat?



P29. [Cliente, Restaurante, Entregador, Administrador]

Como retirada e entrega de um pedido deveriam ser confirmadas?



P30. [Cliente, Restaurante, Entregador, Administrador]

O que deveria ocorrer quando há atraso, pedido incorreto ou entrega não realizada?



P31. [Cliente, Restaurante, Entregador, Administrador]

Como avaliações, reclamações e denúncias deveriam funcionar?



P32. [Cliente, Restaurante, Entregador]

Como você deveria contestar um cancelamento, bloqueio ou reembolso?



P33. [Cliente, Restaurante, Entregador, Administrador]

Qual seria o principal prejuízo se alguém acessasse sua conta?



P34. [Cliente, Restaurante, Entregador, Administrador]

Qual ação importante alguém poderia alterar sem sua autorização?



P35. [Cliente, Restaurante, Entregador, Administrador]

Qual informação específica não pode ser exposta a pessoas erradas?



P36. [Cliente, Restaurante, Entregador, Administrador]

Que tipo de conta falsa poderia causar problemas no aplicativo?



P37. [Cliente, Restaurante, Entregador, Administrador]

Que ação uma pessoa poderia realizar e depois tentar negar que realizou?



P38. [Cliente, Restaurante, Entregador, Administrador]

O que aconteceria com você se o aplicativo ficasse indisponível ou muito lento?



P39. [Administrador]

Quais situações exigiriam bloquear, suspender ou limitar uma conta?



P40. [Administrador]

Quais situações suspeitas deveriam ser verificadas pela equipe responsável?



P41. [Cliente, Restaurante, Entregador, Administrador]

Quais são os três recursos ou informações mais importantes a proteger para seu perfil?



P42. [Cliente, Restaurante, Entregador, Administrador]

Quais são os três problemas de segurança que mais preocupam você?



P43. [Cliente, Restaurante, Entregador, Administrador]

Quais medidas fariam você se sentir mais seguro ao utilizar o aplicativo?



P44. [Cliente, Restaurante, Entregador, Administrador]

Quais perguntas deveriam ser respondidas por outros perfis para melhorar o aplicativo?



P45. [Cliente, Restaurante, Entregador, Administrador]

Há alguma situação importante, risco ou necessidade que não foi perguntada e que você gostaria de acrescentar?



Inicie agora a entrevista, representando exclusivamente o perfil indicado.
