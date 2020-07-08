---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Serviço de tomada de decisão
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1592'
ht-degree: 0%

---


# Visão geral do serviço de decisão

[!DNL Decisioning Service] fornece a capacidade de criar experiências personalizadas, otimizadas e orquestradas em aplicativos executados no Adobe Experience Platform. Usando [!DNL Decisioning Service], você pode determinar a melhor *opção* a partir de um conjunto de opções disponíveis. Essas opções, também chamadas de alternativas, podem ser ofertas, recomendações de produtos, componentes de conteúdo para uma experiência da Web, scripts de conversação e ações a serem realizadas. Atualmente, o caso de uso e o domínio da decisão *de* Oferta são suportados, onde as opções de decisão são modeladas especificamente como ofertas, com suporte para mais casos de uso a serem disponibilizados.

Com [!DNL Decisioning Service]isso, os clientes podem reutilizar a lógica comercial, bem como compartilhar um catálogo de opções entre canais e aplicativos. Em vez de gerenciar opções de decisão - e estratégias para selecioná-las - profundamente em um aplicativo, elas podem ser aproveitadas independentemente de quando, como e em que canal o usuário final de um cliente interage com um negócio ou organização.

As estratégias de decisão podem ter em conta as muitas interações que um cliente teve em vários canais e aplicativos. Por exemplo, a atividade do aplicativo da central de atendimento pode ativar ou suprimir uma mensagem de marketing por algum tempo após uma reclamação, e essa mensagem pode se basear em compras feitas e revisões postadas pelo cliente.

[!DNL Decisioning Service] facilita a personalização da experiência evoluída.

| Antes da decisão de experiência | Após a decisão da experiência |
| --- | --- |
| Personalize e otimize as experiências de seus usuários em um único canal ou em um pequeno conjunto de pontos de contato de experiência. | As experiências são respostas orquestradas em interações. |
| As otimizações estão focadas em uma fase única e tipicamente curta da jornada do usuário final | As decisões são baseadas em todo o histórico de interação que abrange desde comportamentos detectados no passado até o contexto mais recente da situação. |
| As opções e as estratégias para selecionar quais apresentar durante a experiência de um cliente são normalmente codificadas profundamente dentro de um aplicativo. | As estratégias para selecionar a melhor opção são definidas fora dos aplicativos específicos do canal e tornam-se reutilizáveis. |
| As experiências do cliente são personalizadas e otimizadas de acordo com uma meta simplista, por exemplo, aumentar o número de finalizações bem-sucedidas em uma página da Web ou a aceitação de uma oferta apresentada em uma interação com um representante. | As experiências do cliente são otimizadas com base em uma compreensão holística das necessidades atuais do cliente e se adaptam a todas as experiências que o usuário teve, boas ou ruins. Por exemplo, uma campanha de marketing pode não ser apropriada para um cliente que tenha apresentado recentemente uma reclamação sobre um produto ou serviço. |

[!DNL Decisioning Service] move seus recursos de personalização da experiência da definição de metas em um único canal para determinar o estágio geral do ciclo de vida do envolvimento de seus clientes com sua marca independentemente dos canais. Um estágio de ciclo de vida é muito mais complexo do que uma associação de segmento, e é quase sempre baseado em fluxos complexos de eventos, regras de negócios e atributos previstos.

Outros termos utilizados por produtos e serviços destinados a servir casos de uso semelhantes:

- Gerenciamento de interação em tempo real (RTIM)
- Gestão de viagens
- Marketing e personalização de canais Omni
- Decisão em tempo real

## Como [!DNL Decisioning Service] funciona?

As experiências podem ser personalizadas usando-se [!DNL Decisioning Service] em tempo real, à medida que seu cliente se envolve com sua marca por meio de um canal de entrada, como seu site ou aplicativo móvel. A decisão também pode ser usada para personalizar mensagens por canal externo, como uma notificação por email ou push.

As decisões podem ser tomadas de muitas maneiras. Uma abordagem é eliminar as opções sucessivamente até que apenas uma seja deixada ou as opções tenham sido removidas e haja algum subconjunto restante ou um vencedor seja escolhido aleatoriamente do conjunto reduzido. Uma variante dessa abordagem para escolher a opção vencedora de acordo com uma fórmula calculada. A classificação de opções qualificadas é realizada usando uma função. Para a decisão de oferta, essa função poderia calcular o custo, o valor da oferta para a empresa e usar uma probabilidade predeterminada de que a oferta seja aceita pelo usuário final. A pontuação resultante pode ser usada para ordenar as ofertas.

Alternativamente, ou adicionalmente, uma estratégia poderia basear-se nos resultados obtidos a partir de interações anteriores com clientes semelhantes que foram propostas opções semelhantes. Nessa estratégia, a função que calculou os valores de prioridade é aprendida. O valor ótimo dos resultados está ligado aos objetivos da atividade e o indicador de desempenho da previsão é a frequência com que os resultados foram alcançados após a proposta da opção.

### Estratégia de decisão

As estratégias de decisão são configuradas por objetos chamados _atividade_. Cada estratégia de decisão é essencialmente um algoritmo ou uma função que utiliza N opções {o1, o2, ...oN} como entrada e produz uma lista ordenada de opções (o1, o2,...oK), em que a primeira opção na lista é considerada a melhor de acordo com um critério de otimização, a segunda opção na lista resultante é então considerada a segunda melhor opção e assim por diante.

A qualquer momento durante a jornada de um cliente, a melhor opção para uma determinada atividade é reavaliada com base no conjunto mais atual de variáveis de contexto, regras e restrições. As variáveis de contexto incluem os registros armazenados em [!DNL Real Time Customer Profile]. Uma entidade de registro central é o perfil de um cliente, mas outras entidades, como os dados operacionais de negócios, estão igualmente disponíveis para a atividade.

O algoritmo ou função que produz a lista das opções de K superior varia com o caso de uso. Os componentes internos desse algoritmo são diferentes para casos de uso diferentes. Os componentes são definidos em um repositório no momento do projeto e &quot;compilados&quot; em instruções para a estratégia de decisão específica do caso de uso.

![otimização de decisão](./images/decisioning-optimization.png)

## Trabalhar com [!DNL Decisioning Service]

A [!DNL Decisioning Service], como outros [!DNL Platform] serviços, adota uma filosofia da API em primeiro lugar. Isso significa que a API é a interface principal na qual todas as funções, incluindo funções administrativas, são disponibilizadas por meio de APIs. Isso também significa que outros [!DNL Platform] serviços, soluções da Adobe e integrações de terceiros usam as mesmas APIs.

Você pode usar [!DNL Decisioning Service] em um modo de interação de solicitação-resposta síncrono facilitado por uma API REST HTTP simples. A chamada da API retorna a melhor opção atual para um único perfil. A seleção da &quot;opção melhor no momento&quot; será alterada com base nas regras e restrições aplicadas a todas as opções que estão sendo consideradas por uma determinada atividade. A REST API permite obter a próxima melhor opção para várias atividades ao mesmo tempo. Isso permite a arbitragem de opções entre canais. Quando respostas para várias atividades são obtidas juntas, regras adicionais podem ser aplicadas.

![API de decisão](./images/decisioning-API.png)

### Integração com outros [!DNL Platform] workflows

O uso de [!DNL Decisioning Service] é opcional e requer apenas algumas etapas além das etapas típicas necessárias para criar [!DNL Profile] entidades e gerenciá-las.

>[!NOTE]
>
>Para tirar o máximo proveito do [!DNL Real-time Customer Profile], o [!DNL Decisioning Service] é integrado diretamente à loja de perfis. As chamadas da API precisam indicar apenas uma das identidades de um determinado perfil.

A sequência típica de start de etapas com a criação de perfis:

- Autentique para [!DNL Experience Platform].
- Defina um schema com base na classe do perfil e, opcionalmente, defina um schema com base na classe do evento da experiência.
- Configure um conjunto de dados para fazer upload de dados de registro e de séries de tempo [!DNL Customer Profile].
- Adicione dados por meio do conjunto de dados configurado na etapa anterior ou dados de instância de fluxo por meio do Pipeline.
- Transmita eventos de experiência no para enriquecer o perfil com dados comportamentais. [!DNL Platform]

Além disso, para usar [!DNL Decisioning Service], execute as seguintes etapas:

- Defina os componentes de decisão usando as APIs do repositório. São as entidades de lógica empresarial que compõem a estratégia de decisão. Os componentes de decisão serão automaticamente compilados em um formato usado pelo [!DNL Decision Service Runtime]. As APIs do repositório são ilustradas no lado esquerdo no diagrama abaixo.
- Chame a API de tempo de execução para obter a melhor opção de acordo com a lógica comercial definida na etapa anterior. As [!DNL Decision Service Runtime] APIs estão ilustradas no lado direito no diagrama abaixo.

![decisioning-API1](./images/decisioning-API1.png)

A ativação das entidades de lógica comercial acontece automática e continuamente. Assim que uma nova opção for salva no repositório e for marcada como &quot;aprovada&quot;, ela será candidata para inclusão no conjunto de opções disponíveis. Assim que uma regra de decisão for atualizada, o conjunto de regras será remontado e preparado para execução em tempo de execução. Nesta etapa de ativação automática, todas as restrições definidas pela lógica de negócios que não dependem do contexto de tempo de execução serão avaliadas. Os resultados desta etapa de ativação são enviados para um cache onde estão disponíveis para o [!DNL Decisioning Service] tempo de execução. Isso é ilustrado no diagrama a seguir.

![decisioning-API2](./images/decisioning-API2.png)

Depois que os conjuntos de opções, os conjuntos de regras e as restrições são ativados e são encaminhados para [!DNL Decisioning Service] nós, uma API simples é usada para postar uma solicitação de decisão. Normalmente, a API é chamada por um serviço de delivery que utiliza a opção proposta (por exemplo, a próxima melhor ação ou a próxima melhor oferta) e monta a experiência ou executa a ação. Se a proposta for uma oferta, o conteúdo que representa essa oferta será procurado e inserido em uma experiência fornecida ao usuário final. Isso é ilustrado no diagrama a seguir.

![decisioning-API3](./images/decisioning-API3.png)

[!DNL Delivery Service] reúne dados para a solicitação de decisão. Determina a ID da entidade do perfil para a qual a melhor opção é decidida. Ele também reúne todos os dados de contexto que não são armazenados, mas são potencialmente usados pela lógica de decisão. [!DNL Customer Profile]

A lógica de decisão é organizada por atividades, cada uma delas especifica um filtro para o subconjunto de opções que devem ser consideradas para essa atividade, juntamente com uma única opção de fallback.

Cada decisão é tomada primeiro aplicando restrições para reduzir o número de opções e, em seguida, classificando as opções restantes. Embora boa parte da lógica seja avaliada no interior [!DNL Decisioning Service], vários serviços de adjunção são usados para auxiliar nesses dois aspectos. Por exemplo, um serviço de limite gerencia os limites superiores para a frequência com que uma opção pode ser usada em qualquer decisão, e outro serviço pode hospedar um modelo de aprendizado de máquina usado para calcular pontuações para um perfil e uma opção.

Para saber mais sobre como usar as APIs do repositório, consulte o tutorial sobre como [gerenciar entidades e regras de decisão usando APIs](./tutorials/entities.md)

Para saber mais sobre como usar o [!DNL Decisioning Service] tempo de execução, consulte o tutorial [Trabalhar com o tempo de execução do serviço de decisão usando APIs](./tutorials/runtime.md)