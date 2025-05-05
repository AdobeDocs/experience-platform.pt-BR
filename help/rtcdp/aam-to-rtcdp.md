---
title: Evolução do Audience Manager para a Real-Time CDP
description: Entenda as considerações antes de planejar a migração do Audience Manager para o Adobe Real-Time CDP.
exl-id: 83ab9a5d-9abc-4072-b449-e2a9ecd48639
source-git-commit: 2704184446f7945c744e7e2d2a8c3cda3fc12527
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 86%

---

# Evolução do Audience Manager para a Real-Time CDP

Conforme sua organização evolui para usar a Adobe Real-Time CDP, analise estas considerações para preparar seus dados e entender as principais diferenças entre as duas tecnologias. Este artigo destina-se a um público-alvo profissional.

![Diagrama de evolução do Audience Manager para a Real-Time CDP](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## 1. Considere a arquitetura de dados do Audience Manager

Ao planejar a evolução do Audience Manager para a Real-Time CDP, é importante analisar seus [segmentos do Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html?lang=pt-BR) e determinar quais são os [sinais](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html?lang=pt-BR), [traços](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html?lang=pt-BR) e [regras](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html?lang=pt-BR#segment-builder-section) que compõem esses segmentos.

Além disso, pense nas fontes de dados que você usa atualmente no Audience Manager.

A Adobe recomenda categorizar os segmentos da seguinte maneira:

* Segmentos que podem ser enviados para o Experience Platform por meio do [[!UICONTROL Conector de Source do Audience Manager]](/help/sources/connectors/adobe-applications/audience-manager.md), pois não têm dependências de dados, destino ou desafios de ativação e suas regras de segmentação podem ser criadas por meio do [construtor de segmentos](/help/segmentation/ui/segment-builder.md) da Real-Time CDP mais tarde.
* Segmentos que contêm regras potencialmente compatíveis, mas que podem conter dados que não estarão disponíveis na Real-Time CDP.
* Segmentos que não podem ser criados no Real-Time CDP e não têm funcionalidade.

>[!TIP]
>
>A Adobe Real-Time CDP oferece [três tipos de avaliação de segmento](/help/segmentation/home.md#evaluate-segments): [!UICONTROL lote], [!UICONTROL transmissão] e [!UICONTROL borda]. Clientes que usam segmentos em tempo real no Audience Manager podem ser restringidos pela limitação atual de 500 segmentos de transmissão na Real-Time CDP. Leia mais sobre [medidas de proteção de segmentação](/help/profile/guardrails.md).

## 2. Quais segmentos são essenciais para se enviar por meio do [!UICONTROL Conector de origem do Audience Manager]?

Com base em seus critérios de avaliação, segmentos que não possuam dependências de dados, destino ou contestações de ativação e cujas regras de segmentação possam ser criadas posteriormente por meio da coleção de dados da Real-Time CDP (como o [SDK da Web da Adobe Experience Platform](/help/web-sdk/faq.md)) devem ser enviados por meio do Conector de origem do Audience Manager.

## 3. Você usará o destino [!UICONTROL Públicos-alvo da Experience Cloud] para trazer dados de volta ao Audience Manager?

Segmentos que contêm regras potencialmente compatíveis com a Real-Time CDP, mas que possuem dependências de ativação no Audience Manager, podem ser enviados para o Audience Manager por meio do cartão de destino [Públicos-alvo da Experience Cloud](/help/destinations/catalog/adobe/experience-cloud-audiences.md).

## 4. Dentre os destinos que você utiliza no Audience Manager hoje, quais podem ser movidos para a Real-Time CDP?

A Adobe recomenda que os segmentos ativados no Audience Manager para [destinos com base em pessoas](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=pt-BR) sejam enviados para a Real-Time CDP por meio do [!UICONTROL Conector de origem do Audience Manager], a fim de serem ativados na Real-Time CDP.

Todos os destinos com base em pessoas disponíveis no Audience Manager (como [Facebook](/help/destinations/catalog/social/facebook.md), [[!UICONTROL Google Customer Match]](/help/destinations/catalog/advertising/google-customer-match.md) e [LinkedIn](/help/destinations/catalog/social/linkedin.md)) também estão disponíveis na Real-Time CDP.

Dados primários adicionais e outros parceiros de estratégia de mídia estão disponíveis, como [Pinterest](/help/destinations/catalog/advertising/pinterest.md), [Snapchat](/help/destinations/catalog/advertising/snap-inc.md), [TikTok](/help/destinations/catalog/social/tiktok.md), [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md) e [[!UICONTROL The Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md).

Atualmente, a Real-Time CDP permite mais de 60 destinos nativos no [catálogo](/help/destinations/catalog/overview.md), mais de 20 dos quais são destinos de publicidade ou de redes sociais que oferecem suporte à correspondência de públicos-alvo primários.

## Próximas etapas

Agora que leu esta página, você já possui algumas informações a considerar ao iniciar sua evolução do Audience Manager para a Real-Time CDP.
