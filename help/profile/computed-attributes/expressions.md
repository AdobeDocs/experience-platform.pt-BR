---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;solução de problemas;API
title: Expressões PQL de amostra para atributos calculados
topic: guide
type: Documentation
description: Atributos calculados são funções usadas para agregação de dados no nível do evento em atributos no nível do perfil. Essas funções exigem o uso de expressões válidas de Linguagem de Query de Perfil (PQL). Este guia descreve algumas das expressões PQL mais usadas para atributos calculados.
translation-type: tm+mt
source-git-commit: 92533f732cc14b57d2a0a34ce9afe99554f9af04
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 2%

---


# (Alfa) expressões PQL de amostra para atributos calculados

>[!IMPORTANT]
>
>A funcionalidade de atributo calculado está atualmente em alfa e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

No Adobe Experience Platform, os atributos calculados são funções usadas para agregação de dados no nível do evento em atributos no nível do perfil. Essas funções são computadas automaticamente para que possam ser usadas em segmentação, ativação e personalização. Cada atributo calculado é definido com informações básicas, como nome e descrição, classe do schema e caminho para o campo no qual o valor será mantido e uma expressão, cujo valor calculado é o valor que você gostaria de armazenar no atributo calculado.

As expressões usadas nos atributos calculados são criadas usando [!DNL Profile Query Language] (PQL), uma linguagem de query compatível com o Modelo de Dados de Experiência (XDM), projetada para suportar a definição e execução de query para dados de Perfil do Cliente em tempo real.

Os atributos calculados suportam atualmente as seguintes funções: soma, contagem, mín, máx e booleano. Este guia descreve algumas das expressões PQL mais usadas que você pode usar ao definir seus próprios atributos calculados para sua organização. Para obter mais informações sobre o PQL e links para diretrizes de formatação adicionais e exemplos de query suportados, visite [Visão geral do PQL](../../segmentation/pql/overview.md).

## Expressões de transmissão

A tabela a seguir fornece detalhes para expressões de query mais usadas e suportadas no modo de transmissão.

| Descrição | Expressão PQL | Tipo de entrada:<br/>Perfil ou Evento de experiência (EE[]) | Tipo de resultado |
|---|---|---|---|
| Contagem de downloads de imagens nos últimos 7 dias. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes) e eventType=&quot;download&quot; e contentType = &quot;image&quot;].count() | Perfil e EE[] | Número inteiro |
| A soma dos gastos dos clientes com artigos esportivos nos últimos 7 dias. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes) e eventType=&quot;transaction&quot; e categoria = &quot;porting Goods&quot;].sum(commerce.order.priceTotal) | Perfil e EE[] | Número inteiro ou Duplo |
| Gastos médios de clientes com artigos esportivos nos últimos 7 dias.<br/><br/>**Observação:** requer a criação de três atributos calculados. | **ca1:** xEvent[(timestamp occur  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.sum(commerce.order.priceTotal)<br/><br/>**ca2:** xEvent[(timestamp occur  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.count()<br/><br/>**ca3:** ca1 / ca2]] | Perfil e EE[] | Duplo |
| O cliente gastou mais de 100 dólares em artigos esportivos nos últimos 7 dias?<br/><br/>**Observação:** requer a criação de dois atributos calculados. | **ca1:** xEvent[(carimbo de data e hora ocorre  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.sum(commerce.order.priceTotal)<br/><br/>**ca2:** ca1 > 100] | Perfil e EE[] | Booleano |
| O cliente fez uma compra nos últimos 7 dias? | chain(xEvent, timestamp, [A: WHAT(eventType = &quot;transaction&quot;) WHEN(&lt; 7 dias antes agora)]) | Perfil e EE[] | Booleano |
| Os usuários mais baixos gastam com artigos esportivos nos últimos 7 dias. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes) e eventType=&quot;transaction&quot; e categoria = &quot;porting Goods&quot;].min(commerce.order.priceTotal) | Perfil e EE[] | Número inteiro ou Duplo |
| O maior gasto de usuários em artigos esportivos nos últimos 7 dias. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes) e eventType=&quot;transaction&quot; e categoria = &quot;porting Goods&quot;].max(commerce.order.priceTotal) | Perfil e EE[] | Número inteiro ou Duplo |
| Contagem de downloads de cada produto baixado, nos últimos 7 dias, indexados por produto. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.count())) | Perfil e EE[] | Mapear[Cadeia de Caracteres, Número Inteiro] |
| Soma de propriedade numérica sobre downloads de cada produto baixado, nos últimos 7 dias, indexada por produto. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal))) | Perfil e EE[] | Map[String, Integer] ou Map[String, Duplo] |
| Média de propriedade numérica sobre downloads de cada produto baixado, nos últimos 7 dias, indexada por produto.<br/><br/>**Observação:** requer a criação de três atributos calculados. | **ca1:** xEvent[(timestamp occur  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal)))<br/><br/>**ca2:** xEvent[(timestamp occur  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.groupBy(product).map( K, G) => mapEntry(K, G.count()))<br/><br/>**ca3:** ca2 / ca1]] | Perfil e EE[] | Mapear[Cadeia de Caracteres, Duplo] |
| Mínimo de propriedade numérica sobre downloads de cada produto baixado, nos últimos 7 dias, indexado por produto. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.min(commerce.order.priceTotal))) | Perfil e EE[] | Map[String, Integer] ou Map[String, Duplo] |
| Máximo de propriedade numérica sobre downloads de cada produto baixado, nos últimos 7 dias, indexado por produto. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.max(commerce.order.priceTotal))) | Perfil e EE[] | Map[String, Integer] ou Map[String, Duplo] |
| Expressão numérica no perfil, não referenciando eventos. | if(pessoa.gênero = &quot;mulher&quot;, 60, 65) | Perfil | Número inteiro ou Duplo |
| Expressão booleana no perfil, não referenciando eventos. | people.bornYear >= 2000 | Perfil | Booleano |
| Expressão de string no perfil, não evento de referência. | if(homeAddress.countryCode em [&quot;US&quot;,&quot;MX&quot;,&quot;CA&quot;], &quot;NA&quot;, &quot;ROW&quot;) | Perfil | String |

## Expressões em lote

A tabela a seguir fornece detalhes para expressões de query que estão disponíveis somente no modo de lote, o que significa que não estão disponíveis no momento em streaming.

| Descrição | Expressão PQL | Tipo de entrada:<br/>Perfil ou Evento de experiência (EE[]) | Tipo de resultado |
|---|---|---|---|
| Se a soma da expressão numérica sobre downloads de produtos nos últimos 7 dias excede 100, indexada por produto. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal) > 100)) | Perfil e EE[] | Mapear[Cadeia de Caracteres, Booliano] |
| Se a média de expressão numérica sobre downloads de produtos nos últimos 7 dias excede 100, indexada por produto. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.average(commerce.order.priceTotal) > 100)) | Perfil e EE[] | Mapear[Cadeia de Caracteres, Booliano] |
| Acúmulo de várias métricas para cada produto baixado, nos últimos 7 dias, indexadas por produto. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, {&quot;count&quot;: G.count(), &quot;sum&quot;: G.sum(commerce.order.priceTotal)}) | Perfil e EE[] | Map[String, Object] onde Object é um tipo XDM personalizado |