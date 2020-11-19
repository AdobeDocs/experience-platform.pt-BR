---
title: Variáveis mapeadas automaticamente no Adobe Analytics
seo-title: Variáveis mapeadas automaticamente no Adobe Analytics com o Adobe Experience Platform Web SDK
description: Saiba quais variáveis são mapeadas automaticamente no Adobe Analytics com o Experience Platform Web SDK
seo-description: Saiba quais variáveis são mapeadas automaticamente no Adobe Analytics com o Experience Platform Web SDK
keywords: adobe analytics;variables;analytics;automatic map;automatically mapped;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---


# Variáveis mapeadas automaticamente em [!DNL Analytics]

Abaixo está uma lista de variáveis que o Adobe Experience Platform Edge Network mapeia automaticamente para [!DNL Analytics].

| Caminho do campo XDM | [!DNL Analytics Query String] / Cabeçalho HTTP | Descrição |
| ---------- | ------------------------- | ----------------------------------------- |
| `application.id` | `c.a.appid` | Mapeamento de dados de contexto do AppMeasurement `c.a.appid` . |
| `application.launches.value` | `c.a.launches` | Mapeamento de dados de contexto do AppMeasurement `c.a.launches` . |
| `commerce.checkouts.id` | `events` | `scCheckout` serialização de eventos. Se esse campo for excluído (isto é, para eventos não serializados), o sistema gera e atribui seu próprio valor de ID à entidade. |
| `commerce.checkouts.value` | `events` | Mapeamento do parâmetro de query do AppMeasurement EVENTO_LISTA_FULL com conversão COMMERCE_SC_CHECKOUT, usando delimitador `,`. |
| `commerce.order.currencyCode` | `cc` | Mapeamento CURRENCY do parâmetro do query AppMeasurement. |
| `commerce.order.purchaseID` | `pi` | Mapeamento PURCHASEID do parâmetro de query do AppMeasurement. |
| `commerce.productListAdds.id` | `events` | `scAdd` serialização de eventos. Se esse campo for excluído (isto é, para eventos não serializados), o sistema gera e atribui seu próprio valor de ID à entidade. |
| `commerce.productListAdds.value` | `events` | Mapeamento do parâmetro de query do AppMeasurement EVENTO_LISTA_FULL com conversão COMMERCE_SC_ADD, usando delimitador `,`. |
| `commerce.productListOpens.id` | `events` | `scOpen` serialização de eventos. Se esse campo for excluído (isto é, para eventos não serializados), o sistema gera e atribui seu próprio valor de ID à entidade. |
| `commerce.productListOpens.value` | `events` | Mapeamento do parâmetro de query do AppMeasurement EVENTO_LISTA_FULL com conversão COMMERCE_SC_OPEN, usando delimitador `,`. |
| `commerce.productListRemovals.id` | `events` | `scRemove` serialização de eventos. Se esse campo for excluído (isto é, para eventos não serializados), o sistema gera e atribui seu próprio valor de ID à entidade. |
| `commerce.productListRemovals.value` | `events` | Mapeamento do parâmetro de query do AppMeasurement EVENTO_LISTA_FULL com conversão COMMERCE_SC_REMOVE, usando delimitador `,`. |
| `commerce.productListViews.id` | `events` | `scView` serialização de eventos. Se esse campo for excluído (isto é, para eventos não serializados), o sistema gera e atribui seu próprio valor de ID à entidade. |
| `commerce.productListViews.value` | `events` | Mapeamento do parâmetro de query do AppMeasurement EVENTO_LISTA_FULL com conversão COMMERCE_SC_VISUALIZAÇÃO, usando delimitador `,`. |
| `commerce.productViews.id` | `events` | `prodView` serialização de eventos. Se esse campo for excluído (isto é, para eventos não serializados), o sistema gera e atribui seu próprio valor de ID à entidade. |
| `commerce.productViews.value` | `events` | Mapeamento do parâmetro de query do AppMeasurement EVENTO_LISTA_FULL com a conversão COMMERCE_PROD_VISUALIZAÇÃO, usando delimitador `,`. |
| `commerce.purchases.value` | `events` | Mapeamento do parâmetro de query do AppMeasurement EVENTO_LISTA_FULL com a conversão COMMERCE_PURCHASE, usando delimitador `,`. |
| `device.colorDepth` | `c` | Mapeamento do parâmetro de query do AppMeasurement C_COLOR. |
| `device.screenHeight` | `s` | Mapeamento da resolução de tela do parâmetro do query AppMeasurement. |
| `device.screenWidth` | `s` | Mapeamento da resolução de tela do parâmetro do query AppMeasurement. |
| `environment.browserDetails.acceptLanguage` | `Accept-Language` | Este é um mapeamento de cabeçalho HTTP, HEADER_ACCEPT_LANGUAGE. |
| `environment.browserDetails.cookiesEnabled` | `k` | Mapeamento COOKIES do parâmetro de query do AppMeasurement com conversão BOOLEAN_TO_YN. |
| `environment.browserDetails.javaEnabled` | `v` | Parâmetro de query do AppMeasurement mapeamento JAVA_ENABLED com conversão BOOLEAN_TO_YN. |
| `environment.browserDetails.javaScriptVersion` | `j` | Mapeamento do parâmetro de query do AppMeasurement J_JSCRIPT. |
| `environment.browserDetails.userAgent` | `User-Agent` | Este é um mapeamento de cabeçalho HTTP, HEADER_USER_AGENT. |
| `environment.browserDetails.viewportHeight` | `bh` | Mapeamento do parâmetro de query do AppMeasurement BROWSER_HEIGHT. |
| `environment.browserDetails.viewportWidth` | `bw` | Mapeamento do parâmetro de query do AppMeasurement BROWSER_WIDTH. |
| `environment.connectionType` | `ct` | Mapeamento do parâmetro de query do AppMeasurement CT_CONNECT_TYPE. |
| `environment.ipV4` | `X-Forwarded-For` | Este é um mapeamento de Cabeçalho HTTP, X-FORWARDED-FOR. |
| `identityMap.ECID.[0].id` | `mid` | Mapeamento MID do parâmetro de query do AppMeasurement. |
| `marketing.trackingCode` | `v0` | Mapeamento de CAMPANHAS de parâmetros de query do AppMeasurement. |
| `media.mediaTimed.completes.value` | `c.a.media.complete` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.dropBeforeStart.value` | `c.a.media.view`, `c.a.media.timePlayed`, `c.a.media.play` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.federated.value` | `c.a.media.federated` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.federated` . |
| `media.mediaTimed.firstQuartiles.value` | `c.a.media.progress25` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.mediaSegmentView.value` | `c.a.media.segmentView` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.midpoints.value` | `c.a.media.progress50` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.pauseTime.value` | `c.a.media.pauseTime` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.pauseTime` . |
| `media.mediaTimed.pauses.value` | `c.a.media.pauseCount` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.pauseCount` . |
| `media.mediaTimed.primaryAssetReference.@id` | `c.a.media.asset` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.dc:title` | `c.a.media.friendlyName` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.friendlyName` . |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator.[N].iptc4xmpExt:Name` | `c.a.media.originator` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number` | `c.a.media.episode` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.episode` . |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre` | `c.a.media.genre` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating.[N].iptc4xmpExt:RatingValue` | `c.a.media.rating` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number` | `c.a.media.season` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.season` . |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier` | `a.media.name` | Mapeamento de dados de contexto do AppMeasurement `a.media.name` . |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name` | `c.a.media.show` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.show` . |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.type` com a conversão VEDIO_SHOW_TYPE. |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.type` com a conversão VIDEO_SHOW_TYPE. |
| `media.mediaTimed.primaryAssetReference.xmpDM:duration` | `c.a.media.length` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.length` . |
| `media.mediaTimed.primaryAssetViewDetails.@id` | `c.a.media.vsid` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastChannel` | `c.a.media.channel` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.channel` . |
| `media.mediaTimed.primaryAssetViewDetails.broadcastContentType` | `c.a.contentType` | Mapeamento de dados de contexto do AppMeasurement `c.a.contentType` . |
| `media.mediaTimed.primaryAssetViewDetails.broadcastNetwork` | `c.a.media.network` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.network` . |
| `media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value` | `c.a.media.segment` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.segment` . |
| `media.mediaTimed.primaryAssetViewDetails.playerName` | `c.a.media.playerName` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.playerName` . |
| `media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version` | `c.a.media.sdkVersion` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.sdkVersion` . |
| `media.mediaTimed.primaryAssetViewDetails.sourceFeed` | `c.a.media.feed` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.feed` . |
| `media.mediaTimed.primaryAssetViewDetails.streamFormat` | `c.a.media.format` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.format` . |
| `media.mediaTimed.progress10.value` | `c.a.media.progress10` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.progress95.value` | `c.a.media.progress95` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.resumes.value` | `c.a.media.resume` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.resume` . |
| `media.mediaTimed.starts.value` | `c.a.media.view` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.thirdQuartiles.value` | `c.a.media.progress75` | Dados de contexto do AppMeasurement. |
| `media.mediaTimed.timePlayed.value` | `c.a.media.timePlayed` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.timePlayed` . |
| `media.mediaTimed.totalTimePlayed.value` | `c.a.media.totalTimePlayed` | Mapeamento de dados de contexto do AppMeasurement `c.a.media.totalTimePlayed` . |
| `placeContext.geo.latitude` | `lat` | Mapeamento LATITUDE do parâmetro de query do AppMeasurement. |
| `placeContext.geo.longitude` | `lon` | Mapeamento LONGITUDE do parâmetro de query do AppMeasurement. |
| `placeContext.geo.postalCode` | `zip` | Mapeamento ZIP do parâmetro de query do AppMeasurement. |
| `placeContext.geo.stateProvince` | `state` | Mapeamento STATE do parâmetro do query AppMeasurement. |
| `productlistitems.[N]._[NAME_SPACE].*` | `products` | Parâmetro de query do AppMeasurement Produtos Eventos de merchandise / mapeamento de Evars. |
| `productlistitems.[N].name` | `products` | Mapeamento do nome dos produtos do parâmetro do query AppMeasurement. |
| `productlistitems.[N].priceTotal` | `products` | Mapeamento de preços de produtos do parâmetro de query do AppMeasurement. |
| `productlistitems.[N].quantity` | `products` | Parâmetro de query do AppMeasurement - Mapeamento de quantidade de produtos. |
| `web.webInteraction.URL` | `pev1` | Mapeamento do parâmetro de query do AppMeasurement PAGE_EVENTO_VAR1. |
| `web.webInteraction.name` | `pev2` | Mapeamento do parâmetro de query do AppMeasurement PAGE_EVENTO_VAR2. |
| `web.webInteraction.type` | `pe` | `web.webInteraction.type=other` para `pe=lnk_o`; `web.webInteraction.type=download` para `pe=lnk_d`; `web.webInteraction.type=exit` to `pe=lnk_e` |
| `web.webPageDetails.URL` | `g` | Mapeamento do parâmetro de query do AppMeasurement PAGE_URL. |
| `web.webPageDetails.errorPage` | `pageType` | Mapeamento do parâmetro do query do AppMeasurement PAGE_TYPE_FULL com a conversão ERROR_PAGE_TYPE. |
| `web.webPageDetails.homePage` | `hp` | Mapeamento HOMEPAGE do parâmetro de query do AppMeasurement com a conversão BOOLEAN_TO_YN. |
| `web.webPageDetails.name` | `gn` | Mapeamento do parâmetro de query do AppMeasurement PAGENAME. |
| `web.webPageDetails.server` | `sv` | Mapeamento do parâmetro do query AppMeasurement USER_SERVER. |
| `web.webPageDetails.siteSection` | `ch` | Mapeamento de CANAIS de parâmetro de query do AppMeasurement. |
| `web.webReferrer.URL` | `r` | Mapeamento de QUENS INDICOU de parâmetros de query do AppMeasurement. |
