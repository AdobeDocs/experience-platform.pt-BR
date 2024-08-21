---
title: Tipo de dados da coleção de detalhes do Advertising
description: Saiba mais sobre o tipo de dados Advertising Details Collection Experience Data Model (XDM).
exl-id: 3f6bf1f9-c728-46af-804a-cb41eb29951b
source-git-commit: 9350cfc299c20bd63a2a559c177b3af02739e5b9
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 14%

---

# [!UICONTROL Detalhes do Advertising] Tipo de dados da coleção

A Coleção [!UICONTROL Detalhes do Advertising] é um tipo de dados padrão do Experience Data Model (XDM) que captura os principais atributos relacionados aos anúncios. Inclui informações como ID do anúncio, IDs do anunciante e da campanha, duração, posição em uma sequência, detalhes sobre o reprodutor que renderiza o anúncio e assim por diante. Você pode usar esse tipo de dados para rastrear e analisar vários aspectos do desempenho e engajamento do anúncio, e fornecer insights sobre como os públicos-alvo interagem e respondem a diferentes anúncios. Essas informações fornecidas são usadas para rastrear os dados de transmissão.

+++Selecione para exibir um diagrama do tipo de dados Coleção de detalhes do Advertising.
![Um diagrama do tipo de dados da Coleção de Detalhes do Advertising.](../images/data-types/advertising-details-collection.png)
+++

>[!NOTE]
>
>Cada nome de exibição contém um link para informações adicionais sobre os parâmetros de áudio e vídeo. As páginas vinculadas contêm detalhes sobre os dados de anúncios de vídeo coletados pelo Adobe, valores de implementação, parâmetros de rede, relatórios e considerações importantes.

| Nome de exibição | Propriedade | Tipo de dados | Obrigatório | Descrição |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|-----------|----------|-----------------------------------------------------------------------------------------------------------------------|
| [[!UICONTROL Anunciante de anúncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#advertiser) | `advertiser` | sequência de caracteres | Não | A empresa ou marca cujo produto é apresentado no anúncio. |
| [[!UICONTROL Campanha publicitária]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#campaign-id) | `campaignID` | sequência de caracteres | Não | A ID da campanha publicitária. |
| [[!UICONTROL Ad Creative ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-id) | `creativeID` | sequência de caracteres | Não | A ID do criativo do anúncio. |
| [[!UICONTROL URL de criação do anúncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-url) | `creativeURL` | sequência de caracteres | Não | A URL do criativo do anúncio. |
| [[!UICONTROL Posição Do Anúncio No Pod (Início Do Anúncio)]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-start) | `podPosition` | inteiro | Sim | O índice do anúncio dentro do início do anúncio principal, por exemplo, o primeiro anúncio tem índice 0 e o segundo anúncio tem índice 1. |
| [[!UICONTROL Duração Ou Comprimento Do Anúncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-length) | `length` | inteiro | Sim | A duração do anúncio de vídeo em segundos. |
| [[!UICONTROL Nome do anúncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-name) | `friendlyName` | sequência de caracteres | Sim | O nome legível do anúncio. Nos relatórios, o &quot;Ad Name&quot; é a classificação e o &quot;Ad Name (variable)&quot; é o eVar. |
| [[!UICONTROL ID de posicionamento do anúncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#placement-id) | `placementID` | sequência de caracteres | Não | A ID de posicionamento do anúncio. |
| [[!UICONTROL Nome do player do anúncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-player-name) | `playerName` | sequência de caracteres | Sim | O nome do player responsável por renderizar o anúncio. |
| [[!UICONTROL ID do Site de Anúncios]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#site-id) | `siteID` | sequência de caracteres | Não | A ID do site do anúncio. |

{style="table-layout:auto"}
