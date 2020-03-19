---
title: Variáveis mapeadas automaticamente no Analytics
seo-title: Variáveis mapeadas automaticamente no Analytics com o SDK da Web da Adobe Experience Platform
description: Saiba quais variáveis são mapeadas automaticamente no Analytics com o Experience Platform Web SDK
seo-description: Saiba quais variáveis são mapeadas automaticamente no Analytics com o Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# Variáveis (Beta) mapeadas automaticamente no Analytics

>[!IMPORTANT]
>
>O SDK da Web da plataforma Adobe Experience está atualmente em beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

Abaixo está uma lista de variáveis que a Adobe Experience Platform Edge Network mapeia automaticamente no Analytics.

| Caminho do campo XDM | Sequência de consulta do Analytics / Cabeçalho HTTP | Descrição |
| ---------- | ------------------------- | -------- |
| `environment.browserDetails.userAgent` | `User-Agent` | Este é um mapeamento de cabeçalho HTTP, HEADER_USER_AGENT. |
| `environment.browserDetails.acceptLanguage` | `Accept-Language` | Este é um mapeamento de cabeçalho HTTP, HEADER_ACCEPT_LANGUAGE. |
| `environment.browserDetails.cookiesEnabled` | `k` | O parâmetro de consulta do AppMeasurement mapeia COOKIES com a conversão BOOLEAN_TO_YN. |
| `environment.browserDetails.javaScriptVersion` | `j` | Mapeamento do parâmetro de consulta do AppMeasurement J_JSCRIPT. |
| `environment.browserDetails.javaEnabled` | `v` | O parâmetro de consulta do AppMeasurement mapeia JAVA_ENABLED com a conversão BOOLEAN_TO_YN. |
| `environment.browserDetails.viewportHeight` | `bh` | Mapeamento do parâmetro de consulta do AppMeasurement BROWSER_HEIGHT. |
| `environment.browserDetails.viewportWidth` | `bw` | Mapeamento do parâmetro de consulta do AppMeasurement BROWSER_WIDTH. |
| `environment.connectionType` | `ct` | Mapeamento do parâmetro de consulta do AppMeasurement CT_CONNECT_TYPE. |
| `device.colorDepth` | `c` | Mapeamento do parâmetro de consulta do AppMeasurement C_COLOR. |
| `placeContext.geo.stateProvince` | `state` | Mapeamento STATE do parâmetro de consulta AppMeasurement. |
| `placeContext.geo.postalCode` | `zip` | Mapeamento ZIP do parâmetro de consulta do AppMeasurement. |
| `placeContext.geo.latitude` | `lat` | Mapeamento LATITUDE do parâmetro de consulta do AppMeasurement. |
| `placeContext.geo.longitude` | `lon` | Mapeamento LONGITUDE do parâmetro de consulta do AppMeasurement. |
| `web.webPageDetails.server` | `sv` | Mapeamento do parâmetro de consulta do AppMeasurement USER_SERVER. |
| `web.webPageDetails.name` | `gn` | Mapeamento do parâmetro de consulta do AppMeasurement PAGENAME. |
| `web.webPageDetails.URL` | `g` | Mapeamento do parâmetro de consulta do AppMeasurement PAGE_URL. |
| `web.webPageDetails.homePage` | `hp` | O parâmetro de consulta AppMeasurement mapeamento HOMEPAGE com conversão BOOLEAN_TO_YN. |
| `web.webReferrer.URL` | `r` | Mapeamento do parâmetro de consulta AppMeasurement REFERRER. |
| `application.id` | `c.a.appid` | Mapeamento de dados de contexto do AppMeasurement `c.a.appid` . |
| `application.launches.value` | `c.a.launches` | Mapeamento de dados de contexto do AppMeasurement `c.a.launches` . |
| `marketing.trackingCode` | `v0` | Mapeamento CAMPAIGN do parâmetro de consulta do AppMeasurement. |
| `commerce.purchaseID` | `pi` | Mapeamento do parâmetro de consulta AppMeasurement PURCHASEID. |
| `commerce.currencyCode` | `cc` | Mapeamento CURRENCY do parâmetro de consulta AppMeasurement. |
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
| `identitymap.ecid.[0].id` | `mid` | Mapeamento MID do parâmetro de consulta do AppMeasurement. |
