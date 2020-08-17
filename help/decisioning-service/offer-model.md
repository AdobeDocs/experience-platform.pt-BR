---
keywords: Experience Platform;home;popular topics;offer management;Offer Management
solution: Experience Platform
title: Modelo de domínio de decisão de oferta
topic: overview
description: A decisão de oferta é um caso de uso do serviço de decisão no qual você formaliza e gerencia centralmente as regras e previsões usadas para envolver clientes com ofertas.
translation-type: tm+mt
source-git-commit: 23516c66a67ae5663dcf90a40ccba98bfd266ab0
workflow-type: tm+mt
source-wordcount: '2640'
ht-degree: 0%

---


# Visão geral do modelo de domínio de decisão de ofertas

A decisão de oferta é um caso de uso no qual você formaliza e gerencia centralmente as regras e previsões usadas para envolver clientes com ofertas. [!DNL Decisioning Service] A decisão de oferta é considerada um tipo de decisão de _**conteúdo**_. Nesse caso de uso, as opções _**de**_ decisão são conhecidas como _**ofertas**_ e são caracterizadas como tal pelo conteúdo anexado a elas. Para obter uma introdução do modelo de objeto usado pelo [!DNL Decisioning Service], consulte o Modelo [de Domínio do Serviço de](experience-model.md)Decisão.

O objetivo é apresentar ao usuário final uma &quot;Melhor Oferta&quot; em qualquer canal com base em critérios de definição de metas, restrições de custo e frequência, bem como interações anteriores entre canais, incluindo Ofertas anteriores propostas.

Como em todos os casos de uso de decisão, as opções de decisão (oferta) são gerenciadas em um repositório compartilhado por qualquer número de aplicativos. As ofertas podem ser criadas por diferentes departamentos de sua organização ou por parceiros, e essas ofertas podem ser adicionadas e removidas diariamente.

As ofertas são visualmente colocadas em experiências maiores pelo aplicativo que está oferecendo a experiência. _**As disposições**_, às vezes chamadas de pontos ou slots, são componentes importantes para a elaboração de uma estratégia. O design de uma estratégia de oferta geralmente start com a definição dessas disposições. Em geral, uma oferta tem várias representações _**de**_ conteúdo para que possa ser integrada corretamente em várias experiências, em que cada uma tem várias restrições dimensionais ou outras e requer formatos de mídia diferentes.

As ofertas estão frequentemente associadas a bens ou serviços físicos e há um cálculo dos custos envolvidos. Uma organização tem de ser capaz de limitar os recursos que são consumidos pelas ofertas e, por conseguinte, tem de ser capaz de _**limitar**_ o número total de vezes que uma oferta pode ser proposta.

O valor previsto de uma oferta aceita para a organização é o critério de otimização e contraria o custo de fazer uma oferta. O custo, a probabilidade de aceitação e o valor previsto são usados para classificar as ofertas. A melhor Oferta é aquela com maior impacto positivo previsto nas metas de suas atividades ofertas.

A decisão de oferta considera as interações que um usuário final teve, _**em vários canais**_ e aplicativos, aproveita os dados de perfis e eventos de um usuário final. Por exemplo, um aplicativo de central de atendimento pode usar a Decisão de Oferta para ativar ou suprimir uma oferta com base em compras feitas e revisões publicadas pelo usuário final; ou um aplicativo de gerenciamento de e-mail pode depender da decisão de Oferta para selecionar a melhor Oferta em um boletim semanal com base no histórico de navegação em um site.

Ofertas têm outras propriedades interessantes. Frequentemente, há um _**agendamento**_ definido ou data e intervalo de tempo quando a oferta é válida e até quando a oferta precisa ser invalidada.

Por último, o recurso de uma oferta agrava-se com a frequência com que é apresentado. Uma Oferta que não é aceite depois de ter sido proposta repetidamente é uma oportunidade perdida porque poderia ter sido apresentada uma oferta diferente. Por essa razão, a _**fadiga**_ dos utilizadores finais deve ser gerida.

## Visão geral da estratégia de decisão da oferta

A abordagem geral é restringir a seleção de Ofertas até que todas as restrições sejam atendidas, depois aplicar o modelo de classificação às opções restantes e, em seguida, otimizar em várias atividades usando Restrições de limite (eliminação da duplicação e prevenção de opções de fallback).

| Componente de estratégia | Realizado como |
| --- | --- |
| Atividades de decisão | Atividades ofertas |
| Opções de decisão | Oferta com representações de conteúdo |
| Opções de fallback | Oferta de fallback com representações de conteúdo |
| Conjunto finito de opções de decisão | inventário de ofertas (também conhecido por biblioteca de ofertas) |
| Categorias tópicas | Filtro de oferta com base em tags e identificadores de oferta |
| Resultados da decisão | Proposta de uma oferta por atividade, para várias atividades de uma só vez |
| Resultados da decisão | Evento de experiência esperado com referência à oferta, por exemplo `eventType='opened'` |
| Algoritmo de decisão | Lógica de serviço interno, parametrizada |
| Limitações | Restrições de posicionamento, restrições de calendário, restrições globais e de limite por usuário, restrições de deduplicação |
| Regras de decisão | Regras de elegibilidade |
| Modelo para utilitário *esperado* | Classificação de oferta ou prioridade |

O número total de ofertas no inventário de opções é geralmente bastante grande (da ordem de 10.000) e cada atividade de oferta pode estar focada em ofertas que se encaixam em uma categoria diferente (tópico). A estratégia de decisão de oferta permite anexar um filtro de oferta a uma atividade de oferta. As restrições adicionais serão avaliadas no momento em que a decisão for solicitada.
As seções a seguir explicam detalhadamente os componentes do domínio de decisão de Oferta.

## Ofertas gerais

Ofertas gerais, também chamadas de ofertas personalizadas, são as opções no centro das atividades de decisão da oferta. Eles têm atributos como nome e status. O atributo status indica se a entidade está pronta para ser incluída na lista de ofertas ativas aprovadas. Ofertas gerais terão várias restrições adicionadas a elas. Mais informações sobre isso na seção ‎ Restrições [abaixo](#offer-constraints).

## Conteúdo no Oferta

### Ofertas

As disposições definem as restrições de conteúdo e são usadas com uma atividade para especificar o local no qual a próxima melhor experiência será disponibilizada. Isso reduz ainda mais o número de opções que podem ser consideradas e é outra restrição imposta pela atividade. Isso é chamado de restrição de posicionamento. Somente as opções que tiverem conteúdo que atenda a uma restrição de disposição, como oferta, serão consideradas. Este aspecto é avaliado nas fases iniciais da estratégia de decisão. Quando os objetos de opção mudam, as restrições de posicionamento de cada atividade são reavaliadas e a opção pode ser considerada ou sair dela para uma ou mais atividades.

Não é da responsabilidade do [!DNL Decisioning Service] para formalizar os complexos detalhes das dependências de conteúdo. Em vez disso, cada cliente identificará a lista de disposições em todos os canais e fornecerá a essas disposições identificadores e nomes exclusivos. Ao fazer referência a uma disposição específica, o designer afirma que o conteúdo fornecido se encaixará na disposição.

Quando o conteúdo é desenvolvido, o profissional de marketing de oferta e o designer de conteúdo simplesmente (tem que) concordar em um &quot;contrato implícito&quot; que se apoia no nome &quot;Imagem principal do Home page&quot; ou &quot;Script de abertura de chamada de serviço&quot;. A primeira pode ser acordada como uma imagem de largura de 600px e altura de 350px e a segunda pode restringir o conteúdo ao texto em duas variantes de linguagem que não sejam mais de 50 palavras em três ou quatro frases com uma estrutura semântica. Disposição para não armazenar todo o significado do contrato oculto.

### representações da oferta

Para garantir que uma oferta possa ser apresentada corretamente nos diferentes parâmetros das disposições em seus canais, devem ser criadas diferentes representações dessa oferta. O conteúdo que é anexado ao oferta é agrupado por disposições. Cada oferta pode ter uma ou mais representações pelas quais cada uma dessas representações faz referência a uma das disposições definidas. Cada representação em uma oferta deve usar um posicionamento diferente. Quanto mais representações uma oferta tiver mais oportunidade de usar a oferta em diferentes contextos de posicionamento.

Uma disposição restringe o tipo de itens de conteúdo que podem ser adicionados à representação.

## Ofertas de fallback

Ofertas de fallback são opções de decisão que não têm restrições adicionais, exceto as regras de disposições. As ofertas de fallback têm representações de conteúdo que estão ligadas a disposições, como qualquer outra oferta.

As ofertas de fallback são especificadas no atividade para indicar uma experiência de conteúdo viável para uso quando restrições combinadas desqualificarem todas as opções reduzidas. Como não depende do contexto de tempo de execução ou do perfil, a restrição de posicionamento pode ser verificada antecipadamente quando a atividade é montada. Usando ofertas de fallback, há sempre uma resposta para a pergunta: Qual é atualmente a melhor oferta?

## Restrições de oferta

### Restrições do calendário

No domínio de decisão de oferta, as ofertas têm um período de validade. Isso significa que a oferta não pode ser proposta antes de a data e a hora do start terem expirado e que não pode ser proposta mais depois de a data e a hora do  terem expirado. A entidade oferta tem uma estrutura simples que define essas restrições de calendário.

Periodicamente, as Ofertas expiradas serão removidas da lista de opções consideradas. Mas o filtro de calendário é aplicado no momento em que a decisão é solicitada para que as restrições sejam aplicadas com precisão.

### Limitação de restrições

As ofertas podem ter uma restrição de limite opcional. Ele consiste em dois valores:

- O valor de limite global restringe a frequência com que uma oferta pode ser proposta em todo o conjunto de perfis (audiência direcionada).

- A tampa por perfil e determina a frequência com que essa Oferta pode ser proposta para o mesmo perfil.

### Restrições de duplicação

Quando uma decisão é solicitada, o cliente pode solicitar propostas para várias atividades de uma só vez. Esse é um cenário típico na decisão de conteúdo. Cada atividade contribui com uma ou mais opções de conteúdo para a experiência geral. Devido ao aspecto da composição, as decisões precisam ser arbitradas em todas as atividades para evitar a duplicação - a menos que as atividades escolham um subconjunto desvinculado do inventário geral de opções. Uma opção de alta classificação provavelmente vai ficar alta em todas as atividades e seria uma experiência ruim se todas as atividades propusessem a mesma opção. Por outro lado, se um sistema delivery quiser saber qual é a melhor conversão entre todos os canais e se não houver nenhuma restrição de limite, pode ser interessante propor a mesma opção entre diferentes atividades.

No momento, as restrições de duplicação não são gravadas no repositório de objetos de negócios. Em vez disso, a eliminação da duplicação é a estratégia padrão em tempo de execução. Um parâmetro de solicitação pode substituir o comportamento padrão para suprimir a etapa de eliminação da duplicação.

### [!DNL Profile] restrições - Regras de elegibilidade

Até à data, as restrições discutidas têm sido aplicáveis independentemente de quem é feita a seleção da oferta. A decisão de experiência também oferece suporte a um caso de uso em que a personalização de proposições se baseia em eventos de registro e de série de tempo de um cliente. As regras são avaliadas por perfil, para decidir se uma oferta se qualifica ou deve ser suprimida para esse usuário. Para fazer isso, uma regra de elegibilidade pode ser associada a cada oferta. Além dos eventos de perfil e experiência de um usuário final, a regra de elegibilidade levará em conta os dados de contexto em tempo real. Esses dados são fornecidos pelo serviço de delivery e podem assumir a forma de dados não relacionados a um perfil, como níveis de inventário, condições meteorológicas, horários de voo.

É importante distinguir entre regras de definição de metas e segmentação e entre regras de elegibilidade e regras de prioridade para a tomada de decisões. Para direcionar um conjunto de perfis é a saída (seleção de audiência) para qualificação, um conjunto de opções (ofertas permitidas) é a saída da avaliação.

## Coleções de ofertas

O inventário é o conjunto geral de opções consideradas para decisão. O inventário pode ser dividido em categorias ou coleções. Uma coleção de opções é representada por uma tag comum que essas opções têm. Os filtros são usados para testar se as ofertas se encaixam em determinada categoria ou, mais especificamente, compartilham a mesma tag ou tags.

### Tags

As tags fornecem uma maneira de expressar que um grupo de opções pertence a uma categoria.

Uma opção pode ter mais de uma tag e, portanto, estar em várias categorias ao mesmo tempo. As categorias também podem se sobrepor ou conter outra. Quando uma categoria &quot;S&quot; é definida por ofertas que têm a tag &quot;A&quot; e a categoria &quot;R&quot; é definida por opções com ambas as tags &quot;A&quot; e &quot;B&quot;, então &quot;S&quot; será um superconjunto de &quot;R&quot;.

### Filtros

Os filtros são usados para definir os critérios para um conjunto de opções que pertence a uma categoria. Os filtros podem ser considerados query contra o inventário de ofertas gerais. Há duas maneiras básicas de formar um filtro: declarando que uma oferta tem uma ou mais tags e selecionando explicitamente o conjunto de ofertas. O método anterior pode ser configurado para indicar que uma oferta nessa coleção deve ter todas as tags especificadas ou que uma opção se qualifica quando tem pelo menos uma das tags especificadas.

Quando as opções são explicitamente colocadas em uma coleção, seu conjunto de tags é ignorado para essa coleção.

## Atividades ofertas

O Atividade configura e controla o processo de decisão. Atualmente, a estratégia de decisão é principalmente pré-determinada, mas as iterações futuras do modelo de domínio de decisão de Oferta permitirão a seleção de modelos, regras adicionais e restrições.

Uma experiência pode ser montada usando várias atividades simultaneamente. Atualmente, até 30 atividades podem ser endereçadas em uma única solicitação de decisão. Se mais de 30 atividades ou slots em uma experiência precisarem ser preenchidos com conteúdo, várias solicitações poderão ser feitas para o mesmo perfil. No entanto, quando as atividades forem incluídas na mesma solicitação de decisão, a eliminação da duplicação de apresentações da oferta será realizada entre essas atividades.

Se as atividades forem definidas de uma forma que elas selecionem de conjuntos separados de ofertas, então não faz muita diferença se as atividades são combinadas na mesma solicitação ou divididas em solicitações separadas. Mas as restrições de tempo de rede e de resposta podem exigir a combinação de atividades na mesma solicitação. Como solicitações diferentes podem ser roteadas para nós de serviço diferentes, os mesmos dados de perfil podem precisar ser buscados em nós diferentes. Isso reduz a largura de banda efetiva de E/S disponível para outras solicitações.

As atividades são usadas para inserir conteúdo em uma experiência. Para facilitar (não garantir) que os itens de conteúdo &quot;se encaixem&quot; corretamente, uma atividade faz referência a uma única disposição. Observe que uma disposição nem sempre é um lugar/slot concreto, mas mais como uma abstração desses lugares/slots. Por exemplo, em uma página da Web com uma grade de blocos, cada bloco poderia ser regido pelo mesmo posicionamento, supondo que todos tenham formato e tamanho semelhantes e possam ter conteúdo semelhante. No entanto, um bloco individual normalmente seria fornecido por sua própria atividade.

A figura a seguir ilustra como as entidades comerciais estão relacionadas entre si:

![](./images/figure-10.png)

Quando os clientes criam e vinculam o gráfico de objetos para decisões, normalmente haverá três fluxos de trabalho diferentes. Esses são os seguintes:

- Configurar as entidades de suporte, como tags e disposições. Essas entidades são usadas para estruturar, filtrar e agrupar outras entidades. Eles também são usados para oferecer alguma coordenação entre o segundo e o terceiro fluxo de trabalho. Este fluxo de trabalho constitui algum trabalho inicial, mas a qualquer momento é possível refinar a configuração. Embora as tags sejam relativamente simples, as disposições exigem um pouco mais de planejamento. No mínimo, uma empresa precisa fazer um inventário de todos os locais onde uma decisão é apresentada.

- Criação de ofertas com as várias representações e regras de negócios (restrições). Este fluxo de trabalho central fornece as opções entre as quais precisamos selecionar as melhores. As tags do primeiro fluxo de trabalho são usadas para categorizar ofertas e as disposições são usadas para indicar quais opções podem ser apresentadas e onde.

   - Esse fluxo de trabalho também define restrições absolutas para as ofertas. Elas são absolutas porque sempre serão aplicadas e não estão afetando apenas a classificação entre um conjunto de ofertas. Por exemplo, quando uma restrição de calendário é definida, é imposto que a oferta nunca será selecionada antes da data/hora do start definida e nunca depois da data/hora de término. As restrições que serão definidas neste fluxo de trabalho são as restrições [do](#calendar-constraints)calendário, as restrições [de](#capping-constraints) limite e as restrições [de](#profile-constraints---eligibility-rules)qualificação. Um subfluxo de trabalho aqui é a definição de regras adicionais que determinam quem está qualificado para receber uma determinada oferta.

      - Ao mesmo tempo, as restrições são criadas para uma oferta, suas representações são selecionadas. Esse fluxo de trabalho presume que o conteúdo já foi criado em algum lugar e é simplesmente carregado e escolhido no repositório de conteúdo. Aqui é onde as disposições do primeiro fluxo de trabalho entram em vigor. Uma oferta pode selecionar disposições e associar o conteúdo a essa [disposição](#offer-placements).

      - Criar ofertas de fallback adequadas é a última etapa neste fluxo de trabalho. Uma oferta de fallback é muito parecida com uma oferta geral sem restrições.

- O último fluxo de trabalho está preocupado com a criação de atividades. No entanto, essa etapa não ocorre necessariamente em sequência após o fluxo de trabalho para criar ofertas. Ambos os processos estão em andamento e em paralelo. As atividades são usadas para restringir o escopo das opções por tópico e por local onde as decisões são apresentadas. Uma atividade faz referência a uma [coleção](#offer-collections) e a uma disposição. Também deve especificar uma oferta [de](#fallback-offers) fallback que é usada nos casos em que uma oferta qualificada não pode ser determinada.

