---
title: Variáveis mapeadas automaticamente no Analytics
seo-title: Variáveis mapeadas automaticamente no Analytics com o Adobe Experience Platform Web SDK
description: Saiba quais variáveis são mapeadas automaticamente no Analytics com o Experience Platform Web SDK
seo-description: Saiba quais variáveis são mapeadas automaticamente no Analytics com o Experience Platform Web SDK
keywords: adobe analytics;variables;analytics;automatic map;automatically mapped;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 2%

---


# Variáveis mapeadas automaticamente em [!DNL Analytics]

Abaixo está uma lista de variáveis nas quais o Adobe Experience Platform [!DNL Edge Network] mapeia automaticamente [!DNL Analytics].

| Caminho do campo XDM | [!DNL Analytics Query String] / Cabeçalho HTTP | Descrição |
| ---------- | ------------------------- | -------- |
| `commerce.order.purchaseID` | `pi` | Mapeamento PURCHASEID do parâmetro de query do AppMeasurement. |
| `commerce.order.currencyCode` | `cc` | Mapeamento CURRENCY do parâmetro do query AppMeasurement. |
| `commerce.purchases.value` | `events` | Mapeamento do parâmetro de query do AppMeasurement EVENTO_LISTA_FULL com a conversão COMMERCE_PURCHASE, usando delimitador `,`. |
| `commerce.productViews.value` | `events` | Mapeamento do parâmetro de query do AppMeasurement EVENTO_LISTA_FULL com a conversão COMMERCE_PROD_VISUALIZAÇÃO, usando delimitador `,`. |
| `commerce.productListOpens.value` | `events` | Mapeamento do parâmetro de query do AppMeasurement EVENTO_LISTA_FULL com conversão COMMERCE_SC_OPEN, usando delimitador `,`. |
| `commerce.productListViews.value` | `events` | Mapeamento do parâmetro de query do AppMeasurement EVENTO_LISTA_FULL com conversão COMMERCE_SC_VISUALIZAÇÃO, usando delimitador `,`. |
| `commerce.checkouts.value` | `events` | Mapeamento do parâmetro de query do AppMeasurement EVENTO_LISTA_FULL com conversão COMMERCE_SC_CHECKOUT, usando delimitador `,`. |
| `commerce.productListAdds.value` | `events` | Mapeamento do parâmetro de query do AppMeasurement EVENTO_LISTA_FULL com conversão COMMERCE_SC_ADD, usando delimitador `,`. |
| `commerce.productListRemovals.value` | `events` | Mapeamento do parâmetro de query do AppMeasurement EVENTO_LISTA_FULL com conversão COMMERCE_SC_REMOVE, usando delimitador `,`. |
| `commerce.productViews.id` | `events` | `prodView` Serialização de eventos. |
| `commerce.productListOpens.id` | `events` | `scOpen` Serialização de eventos. |
| `commerce.productListViews.id` | `events` | `scView` Serialização de eventos. |
| `commerce.productListAdds.id` | `events` | `scAdd` Serialização de eventos. |
| `commerce.productListRemovals.id` | `events` | `scRemove` Serialização de eventos. |
| `commerce.checkouts.id` | `events` | `scCheckout` Serialização de eventos. |
| `device.screenHeight` | `s` | Mapeamento da resolução de tela do parâmetro do query AppMeasurement. |
| `device.screenWidth` | `s` | Mapeamento da resolução de tela do parâmetro do query AppMeasurement. |
| `productlistitems.[N].lineitemid` | `products` | Parâmetro de query do AppMeasurement Mapeamento de Categoria de produtos. |
| `productlistitems.[N].name` | `products` | Mapeamento do nome dos produtos do parâmetro do query AppMeasurement. |
| `productlistitems.[N].quantity` | `products` | Parâmetro de query do AppMeasurement - Mapeamento de quantidade de produtos. |
| `productlistitems.[N].pricetotal` | `products` | Mapeamento de preços de produtos do parâmetro de query do AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.@id` | `c.a.media.vsid` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.@id` | `c.a.media.asset` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating.[N].iptc4xmpExt:RatingValue` | `c.a.media.rating` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre` | `c.a.media.genre` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator.[N].iptc4xmpExt:Name` | `c.a.media.originator` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.starts.value` | `c.a.media.view` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.progress10.value` | `c.a.media.progress10` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.firstQuartiles.value` | `c.a.media.progress25` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.midpoints.value` | `c.a.media.progress50` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.thirdQuartiles.value` | `c.a.media.progress75` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.progress95.value` | `c.a.media.progress95` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.completes.value` | `c.a.media.complete` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.mediaSegmentView.value` | `c.a.media.segmentView` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.dropBeforeStart.value` | `c.a.media.view`, `c.a.media.timePlayed`, `c.a.media.play` | Dados de contexto do AppMeasurement. |
| `environment.browserDetails.userAgent` | `User-Agent` | Este é um mapeamento de cabeçalho HTTP, HEADER_USER_AGENT. |
| `environment.browserDetails.acceptLanguage` | `Accept-Language` | Este é um mapeamento de cabeçalho HTTP, HEADER_ACCEPT_LANGUAGE. |
| `environment.browserDetails.cookiesEnabled` | `k` | Mapeamento COOKIES do parâmetro de query do AppMeasurement com conversão BOOLEAN_TO_YN. |
| `environment.browserDetails.javaScriptVersion` | `j` | Mapeamento do parâmetro de query do AppMeasurement J_JSCRIPT. |
| `environment.browserDetails.javaEnabled` | `v` | Parâmetro de query do AppMeasurement mapeamento JAVA_ENABLED com conversão BOOLEAN_TO_YN. |
| `environment.browserDetails.viewportHeight` | `bh` | Mapeamento do parâmetro de query do AppMeasurement BROWSER_HEIGHT. |
| `environment.browserDetails.viewportWidth` | `bw` | Mapeamento do parâmetro de query do AppMeasurement BROWSER_WIDTH. |
| `environment.connectionType` | `ct` | Mapeamento do parâmetro de query do AppMeasurement CT_CONNECT_TYPE. |
| `device.colorDepth` | `c` | Mapeamento do parâmetro de query do AppMeasurement C_COLOR. |
| `placeContext.geo.stateProvince` | `state` | Mapeamento STATE do parâmetro do query AppMeasurement. |
| `placeContext.geo.postalCode` | `zip` | Mapeamento ZIP do parâmetro de query do AppMeasurement. |
| `placeContext.geo.latitude` | `lat` | Mapeamento LATITUDE do parâmetro de query do AppMeasurement. |
| `placeContext.geo.longitude` | `lon` | Mapeamento LONGITUDE do parâmetro de query do AppMeasurement. |
| `web.webPageDetails.server` | `sv` | Mapeamento do parâmetro do query AppMeasurement USER_SERVER. |
| `web.webPageDetails.name` | `gn` | Mapeamento do parâmetro de query do AppMeasurement PAGENAME. |
| `web.webPageDetails.URL` | `g` | Mapeamento do parâmetro de query do AppMeasurement PAGE_URL. |
| `web.webPageDetails.homePage` | `hp` | Mapeamento HOMEPAGE do parâmetro de query do AppMeasurement com a conversão BOOLEAN_TO_YN. |
| `web.webReferrer.URL` | `r` | Mapeamento de QUENS INDICOU de parâmetros de query do AppMeasurement. |
| `web.webInteraction.type` | `pe` | Mapeamento do parâmetro de query do AppMeasurement PAGE_EVENTO com conversão CLICK_MAP_TYPE. |
| `web.webInteraction.URL` | `pev1` | Mapeamento do parâmetro de query do AppMeasurement PAGE_EVENTO_VAR1. |
| `web.webInteraction.name` | `pev2` | Mapeamento do parâmetro de query do AppMeasurement PAGE_EVENTO_VAR2. |
| `web.webPageDetails.siteSection` | `ch` | Mapeamento de CANAIS de parâmetro de query do AppMeasurement. |
| `web.webPageDetails.errorPage` | `pageType` | Mapeamento do parâmetro do query do AppMeasurement PAGE_TYPE_FULL com a conversão ERROR_PAGE_TYPE. |
| `application.id` | `c.a.appid` | Mapeamento de dados de contexto do AppMeasurement `c.a.appid` . |
| `application.launches.value` | `c.a.launches` | Mapeamento de dados de contexto do AppMeasurement `c.a.launches` . |
| `marketing.trackingCode` | `v0` | Mapeamento de CAMPANHAS de parâmetros de query do AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier` | `a.media.name` | Mapeamento de dados de contexto do AppMeasurement `a.media.name` . |
| `media.mediaTimed.primaryAssetReference.xmpDM:duration` | `c.a.media.length` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.length` . |
| `media.mediaTimed.primaryAssetViewDetails.broadcastContentType` | `c.a.contentType` | Mapeamento de dados de contexto do AppMeasurement `c.a.contentType` . |
| `media.mediaTimed.primaryAssetViewDetails.playerName` | `c.a.media.playerName` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.playerName` . |
| `media.mediaTimed.primaryAssetViewDetails.broadcastChannel` | `c.a.media.channel` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.channel` . |
| `media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value` | `c.a.media.segment` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.segment` . |
| `media.mediaTimed.primaryAssetReference.dc:title` | `c.a.media.friendlyName` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.friendlyName` . |
| `media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version` | `c.a.media.sdkVersion` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.sdkVersion` . |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name` | `c.a.media.show` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.show` . |
| `media.mediaTimed.primaryAssetViewDetails.streamFormat` | `c.a.media.format` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.format` . |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number` | `c.a.media.season` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.season` . |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number` | `c.a.media.episode` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.episode` . |
| `media.mediaTimed.primaryAssetViewDetails.broadcastNetwork` | `c.a.media.network` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.network` . |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.type` com a conversão VEDIO_SHOW_TYPE. |
| `media.mediaTimed.primaryAssetViewDetails.sourceFeed` | `c.a.media.feed` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.feed` . |
| `media.mediaTimed.timePlayed.value` | `c.a.media.timePlayed` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.timePlayed` . |
| `media.mediaTimed.totalTimePlayed.value` | `c.a.media.totalTimePlayed` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.totalTimePlayed` . |
| `media.mediaTimed.federated.value` | `c.a.media.federated` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.federated` . |
| `media.mediaTimed.pauses.value` | `c.a.media.pauseCount` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.pauseCount` . |
| `media.mediaTimed.pauseTime.value` | `c.a.media.pauseTime` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.pauseTime` . |
| `media.mediaTimed.resumes.value` | `c.a.media.resume` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.resume` . |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.type` com a conversão VIDEO_SHOW_TYPE. |
| `identityMap.ECID.[0].id` | `mid` | Mapeamento MID do parâmetro de query do AppMeasurement. |
