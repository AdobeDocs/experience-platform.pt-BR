---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, campos, esquemas, esquemas, esquemas, detalhes da página da Web, tipo de dados, tipo de dados, tipo de dados, página da Web
solution: Experience Platform
title: Tipo de dados do canal de experiência
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados do Experience Channel Experience Data Model (XDM).
source-git-commit: b9168052174c250810e59e403cb77419d510df3b
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 4%

---

# [!UICONTROL Tipo ] de dados do canal de experiência

[!UICONTROL Os ] canais de experiência são um tipo de dados padrão do Experience Data Model (XDM) que descreve um canal de experiência. Um canal de experiência representa um método ou caminho para como as experiências digitais são consumidas.

Há vários canais de experiência, cada um com restrições diferentes sobre como o conteúdo é entregue, como a interação do cliente pode ser observada e como os dados são coletados. Em um canal, as experiências podem ser entregues a locais específicos. Os locais e os tipos de locais que existem em um canal diferem de canal para canal.

![](../images/data-types/experience-channel.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_id` | String | Uma ID que identifica exclusivamente o canal. Cada canal de experiência específico define uma constante `@id`. |
| `_type` | String | Fornece um rótulo de classificação aproximado para canais com propriedades semelhantes. |
| `contentTypes` | Matriz de cadeias de caracteres | Os tipos de conteúdo que esse canal pode fornecer. |
| `locationTypes` | Matriz de cadeias de caracteres | Os tipos de locais (locais virtuais) em que esse canal consiste e onde pode fornecer conteúdo. |
| `mediaAction` | String | Descreve uma ação de mídia de evento de experiência, se aplicável. |
| `mediaType` | String | Descreve se o tipo de mídia é pago, de propriedade ou ganho. |
| `metricTypes` | Matriz de cadeias de caracteres | As métricas que podem ser coletadas neste canal. |
| `mode` | String | Como as experiências são entregues neste canal. |
| `typeAtSource` | String | Um nome personalizado para o canal. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.schema.json)
