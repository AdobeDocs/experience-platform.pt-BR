---
keywords: Experience Platform;perfil;perfil de cliente em tempo real;solução de problemas;API
title: Expressões PQL de amostra para atributos calculados
type: Documentation
description: Os atributos computados são funções usadas para agregar dados no nível do evento em atributos no nível do perfil. Essas funções exigem o uso de expressões PQL (Profile Query Language) válidas. Este guia descreve algumas das expressões PQL mais usadas para atributos calculados.
exl-id: 7c80e2d3-919a-47f9-a59f-833a70f02a8f
hide: true
hidefromtoc: true
source-git-commit: 5ae7ddbcbc1bc4d7e585ca3e3d030630bfb53724
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 2%

---

# (Alfa) Exemplos de expressões PQL para atributos calculados

>[!IMPORTANT]
>
>No momento, a funcionalidade de atributo computada está em alfa e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

No Adobe Experience Platform, os atributos computados são funções usadas para agregar dados no nível do evento em atributos no nível do perfil. Essas funções são computadas automaticamente para que possam ser usadas na segmentação, ativação e personalização. Cada atributo calculado é definido com informações básicas, como um nome e uma descrição, a classe do esquema e o caminho para o campo no qual o valor será mantido e uma expressão, cujo valor calculado é o valor que você gostaria de armazenar no atributo calculado.

As expressões usadas em atributos computados são criadas usando [!DNL Profile Query Language] (PQL), uma linguagem de consulta compatível com o Experience Data Model (XDM) projetada para oferecer suporte à definição e à execução de consultas para dados de Perfil do cliente em tempo real.

Atualmente, os atributos computados são compatíveis com as seguintes funções: sum, count, min, max e booleano. Este guia descreve algumas das expressões PQL mais usadas que você pode usar ao definir seus próprios atributos calculados para sua organização. Para obter mais informações sobre PQL e links para diretrizes adicionais de formatação e exemplos de consultas compatíveis, visite o [Visão geral do PQL](../../segmentation/pql/overview.md).

## Expressões de transmissão

A tabela a seguir fornece detalhes para expressões de consulta usadas com frequência e com suporte no modo de streaming.

| Descrição | Expressão PQL | Tipo de entrada:<br/>Perfil ou evento de experiência (EE)[]) | Tipo de resultado |
|---|---|---|---|
| Contagem de downloads de imagens nos últimos 7 dias. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes) e eventType=&quot;download&quot; e contentType = &quot;image&quot;].count() | Perfil e EE[] | Número inteiro |
| Soma de gastos do cliente em artigos esportivos nos últimos 7 dias. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes de agora) e eventType=&quot;transaction&quot; e category = &quot;sporting goods&quot;].sum(commerce.order.priceTotal) | Perfil e EE[] | Inteiro ou Duplo |
| Média de gastos do cliente em artigos esportivos nos últimos 7 dias.<br/><br/>**Nota:** Requer a criação de três atributos computados. | **ca1:** xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes de agora) e eventType=&quot;transaction&quot; e category = &quot;sporting goods&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2:** xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes de agora) e eventType=&quot;transaction&quot; e category = &quot;sporting goods&quot;].count()<br/><br/>**ca3:** ca1 / ca2 | Perfil e EE[] | Duplo |
| O cliente gastou mais de US$ 100 com artigos esportivos nos últimos sete dias?<br/><br/>**Nota:** Requer a criação de dois atributos computados. | **ca1:** xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes de agora) e eventType=&quot;transaction&quot; e category = &quot;sporting goods&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2:** ca1 > 100 | Perfil e EE[] | Booleano |
| O cliente fez uma compra nos últimos sete dias? | chain(xEvent, carimbo de data e hora, [A: WHAT(eventType = &quot;transaction&quot;) WHEN(&lt; 7 dias antes agora)]) | Perfil e EE[] | Booleano |
| O menor gasto de usuários com artigos esportivos nos últimos sete dias. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes de agora) e eventType=&quot;transaction&quot; e category = &quot;sporting goods&quot;].min(commerce.order.priceTotal) | Perfil e EE[] | Inteiro ou Duplo |
| O maior gasto de usuários com artigos esportivos nos últimos sete dias. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes de agora) e eventType=&quot;transaction&quot; e category = &quot;sporting goods&quot;].max(commerce.order.priceTotal) | Perfil e EE[] | Inteiro ou Duplo |
| Contagem de downloads de cada produto baixado, nos últimos 7 dias, indexados por produto. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes de agora) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.count())) | Perfil e EE[] | Mapa[String, Número inteiro] |
| Soma da propriedade numérica sobre downloads de cada produto baixado, nos últimos 7 dias, indexada por produto. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes de agora) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal))) | Perfil e EE[] | Mapa[String, Número inteiro] ou Mapa[String, Dupla] |
| Média da propriedade numérica sobre downloads de cada produto baixado, nos últimos 7 dias, indexada por produto.<br/><br/>**Nota:** Requer a criação de três atributos computados. | **ca1:** xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes de agora) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal)))<br/><br/>**ca2:** xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes de agora) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.count()))<br/><br/>**ca3:** ca2 / ca1 | Perfil e EE[] | Mapa[String, Dupla] |
| Mínimo de propriedade numérica sobre downloads de cada produto baixado, nos últimos 7 dias, indexado por produto. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes de agora) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.min(commerce.order.priceTotal))) | Perfil e EE[] | Mapa[String, Número inteiro] ou Mapa[String, Dupla] |
| Máximo de propriedade numérica sobre downloads de cada produto baixado, nos últimos 7 dias, indexado por produto. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes de agora) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.max(commerce.order.priceTotal)) | Perfil e EE[] | Mapa[String, Número inteiro] ou Mapa[String, Dupla] |
| Expressão numérica no perfil, não fazendo referência a eventos. | if(person.gender = &quot;feminino&quot;, 60, 65) | Perfil | Inteiro ou Duplo |
| Expressão booleana no perfil, não fazendo referência a eventos. | person.birthYear >= 2000 | Perfil | Booleano |
| Expressão de cadeia de caracteres no perfil, não fazendo referência a eventos. | if(homeAddress.countryCode em [&quot;US&quot;,&quot;MX&quot;,&quot;CA&quot;], &quot;NA&quot;, &quot;ROW&quot;) | Perfil | String |

## Expressões em lote

A tabela a seguir fornece detalhes para expressões de consulta que estão disponíveis apenas no modo de lote, o que significa que elas não estão disponíveis atualmente no streaming.

| Descrição | Expressão PQL | Tipo de entrada:<br/>Perfil ou evento de experiência (EE)[]) | Tipo de resultado |
|---|---|---|---|
| Se a soma da expressão numérica em downloads de produtos nos últimos 7 dias excede ou não 100, indexada por produto. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes de agora) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal) > 100)) | Perfil e EE[] | Mapa[String, Booleano] |
| Se a média de expressão numérica em downloads de produtos nos últimos 7 dias exceder 100, indexada por produto. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes de agora) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.average(commerce.order.priceTotal) > 100)) | Perfil e EE[] | Mapa[String, Booleano] |
| Acúmulo de várias métricas para cada produto baixado, nos últimos sete dias, indexadas por produto. | xEvent[(o carimbo de data e hora ocorre &lt; 7 dias antes de agora) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, {&quot;count&quot;: G.count(), &quot;sum&quot;: G.sum(commerce.order.priceTotal)})) | Perfil e EE[] | Mapa[String, Objeto] onde Objeto é um tipo XDM personalizado |
