---
title: Variáveis do Adobe Analytics mapeadas automaticamente no SDK da Web da Adobe Experience Platform
description: Saiba quais variáveis são mapeadas automaticamente no Adobe Analytics com o SDK da Web do Experience Platform
seo-description: Learn which variables are automatically mapped in Adobe Analytics with the Adobe Experience Platform Web SDK
keywords: adobe analytics; variáveis; analytics; mapa automático; mapeado automaticamente;
exl-id: 856fada7-b62c-4fd2-9372-a19ae1cdec33
source-git-commit: dcbe4c1b5a085878562990ed2db8e5cb27b93e28
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 5%

---

# Variáveis mapeadas automaticamente em [!DNL Analytics]

Abaixo está uma lista de variáveis que a Adobe Experience Platform Edge Network mapeia automaticamente para o Adobe Analytics. Informações detalhadas sobre os parâmetros de consulta de coleta de dados do Adobe Analytics podem ser encontradas no [Guia de implementação do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/validate/query-parameters.html).

>[!NOTE]
>As informações nesta página também se aplicam ao SDK do Adobe Mobile.

| Caminho do campo XDM | [!DNL Analytics Query String] / Cabeçalho HTTP | Descrição |
| ---------- | ------------------------- | ----------------------------------------- |
| application.id | c.a.appid | Dados de contexto do AppMeasurement `c.a.appid` mapeamento. |
| application.launches.value | c.a.launches | Dados de contexto do AppMeasurement `c.a.launches` mapeamento. |
| commerce.checkouts.id | eventos | `scCheckout` serialização de eventos. Se esse campo for excluído (ou seja, para eventos não serializados), o sistema gera e atribui seu próprio valor de ID à entidade. |
| commerce.checkouts.value | eventos | Mapeamento EVENT_LIST_FULL do parâmetro de consulta do AppMeasurement com conversão COMMERCE_SC_CHECKOUT, usando delimitador `,`. |
| commerce.order.currencyCode | cc | Mapeamento de MOEDA do parâmetro de consulta AppMeasurement. |
| commerce.order.purchaseID | pi | Mapeamento PURCHASEID do parâmetro de consulta AppMeasurement. |
| commerce.productListAdds.id | eventos | `scAdd` serialização de eventos. Se esse campo for excluído (ou seja, para eventos não serializados), o sistema gera e atribui seu próprio valor de ID à entidade. |
| commerce.productListAdds.value | eventos | Mapeamento EVENT_LIST_FULL do parâmetro de consulta do AppMeasurement com conversão COMMERCE_SC_ADD, usando delimitador `,`. |
| commerce.productListOpens.id | eventos | `scOpen` serialização de eventos. Se esse campo for excluído (ou seja, para eventos não serializados), o sistema gera e atribui seu próprio valor de ID à entidade. |
| commerce.productListOpens.value | eventos | Mapeamento EVENT_LIST_FULL do parâmetro de consulta do AppMeasurement com conversão COMMERCE_SC_OPEN, usando delimitador `,`. |
| commerce.productListRemovals.id | eventos | `scRemove` serialização de eventos. Se esse campo for excluído (ou seja, para eventos não serializados), o sistema gera e atribui seu próprio valor de ID à entidade. |
| commerce.productListRemovals.value | eventos | Mapeamento EVENT_LIST_FULL do parâmetro de consulta do AppMeasurement com conversão COMMERCE_SC_REMOVE, usando delimitador `,`. |
| commerce.productListViews.id | eventos | `scView` serialização de eventos. Se esse campo for excluído (ou seja, para eventos não serializados), o sistema gera e atribui seu próprio valor de ID à entidade. |
| commerce.productListViews.value | eventos | Mapeamento EVENT_LIST_FULL do parâmetro de consulta do AppMeasurement com conversão COMMERCE_SC_VIEW, usando delimitador `,`. |
| commerce.productViews.id | eventos | `prodView` serialização de eventos. Se esse campo for excluído (ou seja, para eventos não serializados), o sistema gera e atribui seu próprio valor de ID à entidade. |
| commerce.productViews.value | eventos | Mapeamento EVENT_LIST_FULL do parâmetro de consulta do AppMeasurement com conversão COMMERCE_PROD_VIEW, usando delimitador `,`. |
| commerce.purchases.value | eventos | Mapeamento EVENT_LIST_FULL do parâmetro de consulta do AppMeasurement com conversão COMMERCE_PURCHASE, usando delimitador `,`. |
| device.colorDepth | c | Mapeamento C_COLOR do parâmetro de consulta do AppMeasurement. |
| device.screenHeight | s | Mapeamento da resolução de tela do parâmetro de consulta do AppMeasurement. |
| device.screenWidth | s | Mapeamento da resolução de tela do parâmetro de consulta do AppMeasurement. |
| environment.browserDetails.acceptLanguage | Accept-Language | Este é um mapeamento HTTP Header, HEADER_ACCEPT_LANGUAGE. |
| environment.browserDetails.cookiesEnabled | k | Mapeamento COOKIES do parâmetro de consulta do AppMeasurement com conversão BOOLEAN_TO_YN. |
| environment.browserDetails.javaEnabled | v | Parâmetro de consulta do AppMeasurement mapeamento JAVA_ENABLED com conversão BOOLEAN_TO_YN. |
| environment.browserDetails.javaScriptVersion | j | Mapeamento J_JSCRIPT do parâmetro de consulta do AppMeasurement. |
| environment.browserDetails.userAgent | User-Agent | Este é um mapeamento de cabeçalho HTTP, HEADER_USER_AGENT. |
| environment.browserDetails.viewportHeight | bh | Mapeamento BROWSER_HEIGHT do parâmetro de consulta do AppMeasurement. |
| environment.browserDetails.viewportWidth | bw | Mapeamento BROWSER_WIDTH do parâmetro de consulta do AppMeasurement. |
| environment.connectionType | ct | Mapeamento CT_CONNECT_TYPE do parâmetro de consulta do AppMeasurement. |
| environment.ipV4 | X-Forwarded-For | Este é um HTTP Header mapping, X-FORWARDED-FOR. |
| identityMap.ECID[0].id | mid | Mapeamento de MID do parâmetro de consulta do AppMeasurement. |
| marketing.trackingCode | v0 | Mapeamento CAMPAIGN do parâmetro de consulta do AppMeasurement. |
| media.mediaTimed.completes.value | c.a.media.complete | Dados de contexto do AppMeasurement. |
| media.mediaTimed.dropBeforeStart.value | c.a.media.view, c.a.media.timePlayed, c.a.media.play | Dados de contexto do AppMeasurement. |
| media.mediaTimed.federated.value | c.a.media.federated | Dados de contexto do AppMeasurement `c.a.media.federated` mapeamento. |
| media.mediaTimed.firstQuartiles.value | c.a.media.progress25 | Dados de contexto do AppMeasurement. |
| media.mediaTimed.mediaSegmentView.value | c.a.media.segmentView | Dados de contexto do AppMeasurement. |
| media.mediaTimed.midpoints.value | c.a.media.progress50 | Dados de contexto do AppMeasurement. |
| media.mediaTimed.pauseTime.value | c.a.media.pauseTime | Dados de contexto do AppMeasurement `c.a.media.pauseTime` mapeamento. |
| media.mediaTimed.pauses.value | c.a.media.pauseCount | Dados de contexto do AppMeasurement `c.a.media.pauseCount` mapeamento. |
| media.mediaTimed.primaryAssetReference.@id | c.a.media.asset | Dados de contexto do AppMeasurement. |
| media.mediaTimed.primaryAssetReference.dc:title | c.a.media.friendlyName | Dados de contexto do AppMeasurement `c.a.media.friendlyName` mapeamento. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator[N].iptc4xmpExt:Name | c.a.media.originator | Dados de contexto do AppMeasurement. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number | c.a.media.episode | Dados de contexto do AppMeasurement `c.a.media.episode` mapeamento. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre | c.a.media.genre | Dados de contexto do AppMeasurement. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating[N].iptc4xmpExt:RatingValue | c.a.media.rating | Dados de contexto do AppMeasurement. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number | c.a.media.season | Dados de contexto do AppMeasurement `c.a.media.season` mapeamento. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier | a.media.name | Dados de contexto do AppMeasurement `a.media.name` mapeamento. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name | c.a.media.show | Dados de contexto do AppMeasurement `c.a.media.show` mapeamento. |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | Dados de contexto do AppMeasurement `c.a.media.type` mapeamento com conversão VEDIO_SHOW_TYPE. |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | Dados de contexto do AppMeasurement `c.a.media.type` mapeamento com conversão VIDEO_SHOW_TYPE. |
| media.mediaTimed.primaryAssetReference.xmpDM:duration | c.a.media.length | Dados de contexto do AppMeasurement `c.a.media.length` mapeamento. |
| media.mediaTimed.primaryAssetViewDetails.@id | c.a.media.vsid | Dados de contexto do AppMeasurement. |
| media.mediaTimed.primaryAssetViewDetails.broadcastChannel | c.a.media.channel | Dados de contexto do AppMeasurement `c.a.media.channel` mapeamento. |
| media.mediaTimed.primaryAssetViewDetails.broadcastContentType | c.a.contentType | Dados de contexto do AppMeasurement `c.a.contentType` mapeamento. |
| media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | c.a.media.network | Dados de contexto do AppMeasurement `c.a.media.network` mapeamento. |
| media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value | c.a.media.segment | Dados de contexto do AppMeasurement `c.a.media.segment` mapeamento. |
| media.mediaTimed.primaryAssetViewDetails.playerName | c.a.media.playerName | Dados de contexto do AppMeasurement `c.a.media.playerName` mapeamento. |
| media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version | c.a.media.sdkVersion | Dados de contexto do AppMeasurement `c.a.media.sdkVersion` mapeamento. |
| media.mediaTimed.primaryAssetViewDetails.sourceFeed | c.a.media.feed | Dados de contexto do AppMeasurement `c.a.media.feed` mapeamento. |
| media.mediaTimed.primaryAssetViewDetails.streamFormat | c.a.media.format | Dados de contexto do AppMeasurement `c.a.media.format` mapeamento. |
| media.mediaTimed.progress10.value | c.a.media.progress10 | Dados de contexto do AppMeasurement. |
| media.mediaTimed.progress95.value | c.a.media.progress95 | Dados de contexto do AppMeasurement. |
| media.mediaTimed.resumes.value | c.a.media.resume | Dados de contexto do AppMeasurement `c.a.media.resume` mapeamento. |
| media.mediaTimed.starts.value | c.a.media.view | Dados de contexto do AppMeasurement. |
| media.mediaTimed.thirdQuartiles.value | c.a.media.progress75 | Dados de contexto do AppMeasurement. |
| media.mediaTimed.timePlayed.value | c.a.media.timePlayed | Dados de contexto do AppMeasurement `c.a.media.timePlayed` mapeamento. |
| media.mediaTimed.totalTimePlayed.value | c.a.media.totalTimePlayed | Dados de contexto do AppMeasurement `c.a.media.totalTimePlayed` mapeamento. |
| placeContext.geo.latitude | lat | Mapeamento LATITUDE do parâmetro de consulta do AppMeasurement. |
| placeContext.geo.longitude | lon | Mapeamento LONGITUDE do parâmetro de consulta do AppMeasurement. |
| placeContext.geo.postalCode | CEP | Mapeamento ZIP do parâmetro de consulta do AppMeasurement. |
| placeContext.geo.stateProvince | estado | Mapeamento de STATE do parâmetro de consulta AppMeasurement. |
| productListItems[N].lineItemId | produtos | Parâmetro de consulta AppMeasurement Mapeamento de categoria de produtos. |
| productlistitems[N].name | produtos | Parâmetro de consulta do AppMeasurement Mapeamento do nome dos produtos. |
| productlistitems[N].priceTotal | produtos | Parâmetro de consulta AppMeasurement Mapeamento de preço de produtos. |
| productlistitems[N].quantity | produtos | Parâmetro de consulta AppMeasurement - Mapeamento de quantidade de produtos. |
| web.webInteraction.URL | pev1 | Mapeamento do parâmetro de consulta do AppMeasurement PAGE_EVENT_VAR1. |
| web.webInteraction.name | pev2 | Mapeamento do parâmetro de consulta do AppMeasurement PAGE_EVENT_VAR2. |
| web.webInteraction.type | pe | `web.webInteraction.type=other` para `pe=lnk_o`; `web.webInteraction.type=download` para `pe=lnk_d`; `web.webInteraction.type=exit` para `pe=lnk_e` |
| web.webPageDetails.URL | g | Mapeamento PAGE_URL do parâmetro de consulta do AppMeasurement. |
| web.webPageDetails.errorPage | pageType | Parâmetro de consulta do AppMeasurement mapeamento PAGE_TYPE_FULL com conversão ERROR_PAGE_TYPE. |
| web.webPageDetails.homePage | hp | Mapeamento HOMEPAGE do parâmetro de consulta do AppMeasurement com conversão BOOLEAN_TO_YN. |
| web.webPageDetails.name | gn | Mapeamento PAGENAME do parâmetro de consulta do AppMeasurement. |
| web.webPageDetails.server | sv | Mapeamento USER_SERVER do parâmetro de consulta do AppMeasurement. |
| web.webPageDetails.siteSection | ch | Mapeamento de CANAL do parâmetro de consulta do AppMeasurement. |
| web.webReferrer.URL | r | Mapeamento do referenciador do parâmetro de consulta do AppMeasurement. |

{style=&quot;table-layout:auto&quot;}
