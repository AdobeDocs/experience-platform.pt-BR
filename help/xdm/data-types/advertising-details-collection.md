---
title: Tipo de dados da coleção de detalhes de publicidade
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência (XDM) da Coleção de detalhes de publicidade.
source-git-commit: fe239bee3c853d43c04200092f59537dfeb00c87
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 11%

---

# [!UICONTROL Detalhes de publicidade] Tipo de dados de coleção

[!UICONTROL Detalhes de publicidade] A coleção é um tipo de dados padrão do Experience Data Model (XDM) que captura os principais atributos relacionados aos anúncios. Inclui informações como ID do anúncio, IDs do anunciante e da campanha, duração, posição em uma sequência, detalhes sobre o reprodutor que renderiza o anúncio e assim por diante. Você pode usar esse tipo de dados para rastrear e analisar vários aspectos do desempenho e engajamento do anúncio, e fornecer insights sobre como os públicos-alvo interagem e respondem a diferentes anúncios. Essas informações fornecidas são usadas para rastrear os dados de transmissão.

+++Selecione para exibir um diagrama do tipo de dados Advertising Details Collection.
![Um diagrama do tipo de dados Advertising Details Collection.](../images/data-types/advertising-details-collection.png)
+++

>[!NOTE]
>
>Cada nome de exibição contém um link para informações adicionais sobre os parâmetros de áudio e vídeo. As páginas vinculadas contêm detalhes sobre os dados de anúncios de vídeo coletados pelo Adobe, valores de implementação, parâmetros de rede, relatórios e considerações importantes.

| Nome de exibição | Propriedade | Tipo de dados | Obrigatório | Descrição |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|-----------|----------------------------------------------------------------------------------------------------------------------------------|
| [[!UICONTROL Anunciante de publicidade]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#advertiser) | `advertiser` | string | Não | A empresa ou marca cujo produto é apresentado no anúncio. |
| [[!UICONTROL Campanha publicitária]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#campaign-id) | `campaignID` | string | Não | A ID da campanha publicitária. |
| [[!UICONTROL ID de criação do anúncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-id) | `creativeID` | string | Não | A ID do criativo do anúncio. |
| [[!UICONTROL URL de criação do anúncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-url) | `creativeURL` | string | Não | O URL da campanha criativa. |
| [[!UICONTROL Posição do pod de anúncio (início do anúncio)]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-start) | `podPosition` | inteiro | Sim | O índice do anúncio dentro do início do anúncio principal, por exemplo, o primeiro anúncio tem índice 0 e o segundo anúncio tem índice 1. |
| [[!UICONTROL Duração Ou Duração Do Anúncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-length) | `length` | inteiro | Sim | A duração do anúncio de vídeo em segundos. |
| [[!UICONTROL Nome do anúncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-name) | `friendlyName` | string | Sim | O nome legível do anúncio. Nos relatórios, o “Ad Name” é a classificação e o “Ad Name (variable)” é a eVar. |
| [[!UICONTROL ID de posicionamento do anúncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#placement-id) | `placementID` | string | Não | A ID de posicionamento do anúncio. |
| [[!UICONTROL Nome do reprodutor do anúncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-player-name) | `playerName` | string | Sim | O nome do reprodutor responsável pela renderização do anúncio. |
| [[!UICONTROL ID do site de anúncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#site-id) | `siteID` | string | Não | A ID do site do anúncio. |
