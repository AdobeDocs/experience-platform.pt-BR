---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API
title: Expressões PQL de amostra para atributos calculados
topic-legacy: guide
type: Documentation
description: Atributos calculados são funções usadas para agregar dados no nível do evento em atributos no nível do perfil. Essas funções exigem o uso de expressões PQL (Profile Query Language) válidas. Este guia descreve algumas das expressões PQL mais usadas para atributos calculados.
exl-id: 7c80e2d3-919a-47f9-a59f-833a70f02a8f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 2%

---

# Expressões PQL de amostra (Alfa) para atributos calculados

>[!IMPORTANT]
>
>A funcionalidade de atributo calculado está atualmente em alfa e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

No Adobe Experience Platform, os atributos calculados são funções usadas para agregar dados a nível de evento em atributos a nível de perfil. Essas funções são calculadas automaticamente para que possam ser usadas na segmentação, ativação e personalização. Cada atributo calculado é definido com informações básicas, como nome e descrição, classe de esquema e caminho para o campo no qual o valor será mantido e uma expressão, cujo valor calculado é o valor que você gostaria de armazenar no atributo calculado.

As expressões usadas em atributos calculados são criadas usando [!DNL Profile Query Language] (PQL), uma linguagem de consulta compatível com o Experience Data Model (XDM), projetada para oferecer suporte à definição e execução de consultas de dados de Perfil do cliente em tempo real.

Os atributos calculados atualmente suportam as seguintes funções: soma, contagem, mín, máx e booleano. Este guia descreve algumas das expressões PQL mais usadas que podem ser usadas ao definir seus próprios atributos calculados para a organização. Para obter mais informações sobre PQL e links para diretrizes de formatação adicionais e exemplos de consultas compatíveis, visite a [Visão geral de PQL](../../segmentation/pql/overview.md).

## Expressões de transmissão

A tabela a seguir fornece detalhes para as expressões de consulta usadas com frequência compatíveis com o modo de transmissão.

| Descrição | Expressão PQL | Tipo de entrada:<br/>Perfil ou Evento de experiência (EE[]) | Tipo de resultado |
|---|---|---|---|
| Contagem de downloads de imagens nos últimos 7 dias. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes) e eventType=&quot;download&quot; e contentType = &quot;image&quot;].count() | Perfil e EE[] | Número inteiro |
| Soma dos gastos dos clientes com artigos esportivos nos últimos 7 dias. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes agora) e eventType=&quot;transaction&quot; e category = &quot;porting Goods&quot;].sum(commerce.order.priceTotal) | Perfil e EE[] | Número inteiro ou duplo |
| Custo médio do cliente em artigos esportivos nos últimos 7 dias.<br/><br/>**Observação:** requer a criação de três atributos calculados. | **ca1:** xEvent[ (timestamp occur  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.sum(commerce.order.priceTotal)<br/><br/>**ca2:** xEvent[ (timestamp occur  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.count()<br/><br/>**ca3:** ca1 / ca2]] | Perfil e EE[] | Duplo |
| O cliente gastou mais de US$ 100 em artigos esportivos nos últimos 7 dias?<br/><br/>**Observação:** requer a criação de dois atributos calculados. | **ca1:** xEvent[ (carimbo de data e hora ocorre  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.sum(commerce.order.priceTotal)<br/><br/>**ca2:** ca1 > 100] | Perfil e EE[] | Booleano |
| O cliente fez uma compra nos últimos 7 dias? | chain(xEvent, timestamp, [A: WHAT(eventType = &quot;transaction&quot;) WHEN(&lt; 7 dias antes agora)]) | Perfil e EE[] | Booleano |
| Os usuários mais baixos gastam em artigos esportivos nos últimos 7 dias. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes) e eventType=&quot;transaction&quot; e category = &quot;esportista Goods&quot;].min(commerce.order.priceTotal) | Perfil e EE[] | Número inteiro ou duplo |
| O maior gasto de usuários em artigos esportivos nos últimos 7 dias. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes agora) e eventType=&quot;transaction&quot; e category = &quot;porting Goods&quot;].max(commerce.order.priceTotal) | Perfil e EE[] | Número inteiro ou duplo |
| Contagem de downloads de cada produto baixado, nos últimos 7 dias, indexados por produto. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.count())) | Perfil e EE[] | Mapear[Cadeia de caracteres, Número inteiro] |
| Soma da propriedade numérica sobre downloads de cada produto baixado, nos últimos 7 dias, indexada por produto. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal))) | Perfil e EE[] | Mapear[String, Integer] ou Map[String, Double] |
| Média de propriedade numérica sobre downloads de cada produto baixado, nos últimos 7 dias, indexada por produto.<br/><br/>**Observação:** requer a criação de três atributos calculados. | **ca1:** xEvent[ (timestamp occur  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal)))<br/><br/>**ca2:** xEvent[ (timestamp occur  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.groupBy(product).map((K, G) => mapEntry(K, G.count())))<br/><br/>**ca3:** ca2 / ca1]] | Perfil e EE[] | Mapear[Cadeia de caracteres, Duplo] |
| Mínimo de propriedade numérica sobre downloads de cada produto baixado, nos últimos 7 dias, indexado por produto. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.min(commerce.order.priceTotal))) | Perfil e EE[] | Mapear[String, Integer] ou Map[String, Double] |
| Máximo de propriedade numérica sobre downloads de cada produto baixado, nos últimos 7 dias, indexado por produto. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.max(commerce.order.priceTotal))) | Perfil e EE[] | Mapear[String, Integer] ou Map[String, Double] |
| Expressão numérica no perfil, sem fazer referência aos eventos. | if(person.gender = &quot;women&quot;, 60, 65) | Perfil | Número inteiro ou duplo |
| Expressão booleana no perfil, não fazendo referência a eventos. | person.birthYear >= 2000 | Perfil | Booleano |
| Expressão de string no perfil, não referenciando eventos. | if(homeAddress.countryCode em [&quot;US&quot;,&quot;MX&quot;,&quot;CA&quot;], &quot;NA&quot;, &quot;ROW&quot;) | Perfil | String |

## Expressões em lote

A tabela a seguir fornece detalhes para as expressões de consulta que estão disponíveis apenas no modo de lote, o que significa que elas não estão disponíveis no momento no streaming.

| Descrição | Expressão PQL | Tipo de entrada:<br/>Perfil ou Evento de experiência (EE[]) | Tipo de resultado |
|---|---|---|---|
| Se a soma da expressão numérica sobre downloads de produtos nos últimos 7 dias excede 100, indexada por produto. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal) > 100)) | Perfil e EE[] | Mapear[Cadeia de caracteres, Booleano] |
| Se a média de expressão numérica sobre downloads de produtos nos últimos 7 dias excede 100, indexada por produto. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.average(commerce.order.priceTotal) > 100)) | Perfil e EE[] | Mapear[Cadeia de caracteres, Booleano] |
| Acúmulo de várias métricas para cada produto baixado, nos últimos 7 dias, indexadas por produto. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, {&quot;count&quot;: G.count(), &quot;sum&quot;: G.sum(commerce.order.priceTotal)}) | Perfil e EE[] | Mapear[String, Object] onde Object é um tipo XDM personalizado |
