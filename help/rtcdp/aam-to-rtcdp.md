---
title: Evolução do Audience Manager para a Real-Time CDP
description: Entenda as considerações antes de planejar a migração do Audience Manager para o Adobe Real-Time CDP.
exl-id: 83ab9a5d-9abc-4072-b449-e2a9ecd48639
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 67%

---

# Evolução do Audience Manager para a Real-Time CDP

Conforme sua organização evolui para usar a Adobe Real-Time CDP, analise estas considerações para preparar seus dados e entender as principais diferenças entre as duas tecnologias. Este artigo destina-se a um público-alvo profissional.

![Diagrama de evolução do Audience Manager para a Real-Time CDP](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## &#x200B;1. Considere a arquitetura de dados do Audience Manager

Ao planejar a evolução do Audience Manager para a Real-Time CDP, é importante analisar seus [segmentos do Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html) e determinar quais são os [sinais](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html), [traços](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html) e [regras](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html#segment-builder-section) que compõem esses segmentos.

Além disso, pense nas fontes de dados que você usa atualmente no Audience Manager.

A Adobe recomenda categorizar os segmentos da seguinte maneira:

* Segmentos que podem ser enviados para a Experience Platform por meio do [[!UICONTROL Audience Manager Source Connector]](/help/sources/connectors/adobe-applications/audience-manager.md), pois não têm dependências de dados, destino ou desafios de ativação, e suas regras de segmentação podem ser criadas por meio do [construtor de segmentos](/help/segmentation/ui/segment-builder.md) do Real-Time CDP posteriormente.
* Segmentos que contêm regras potencialmente compatíveis, mas que podem conter dados que não estarão disponíveis na Real-Time CDP.
* Segmentos que não podem ser criados no Real-Time CDP e não têm funcionalidade.

>[!TIP]
>
>A Adobe Real-Time CDP oferece [três tipos de avaliação de segmento](/help/segmentation/home.md#evaluate-segments): [!UICONTROL Batch], [!UICONTROL Streaming] e [!UICONTROL Edge]. Clientes que usam segmentos em tempo real no Audience Manager podem ser restringidos pela limitação atual de 500 segmentos de transmissão na Real-Time CDP. Leia mais sobre [medidas de proteção de segmentação](/help/profile/guardrails.md).

## &#x200B;2. Quais segmentos são críticos para enviar via [!UICONTROL Audience Manager Source Connector]?

Com base em seus critérios de avaliação, segmentos que não possuam dependências de dados, destino ou contestações de ativação e cujas regras de segmentação possam ser criadas posteriormente por meio da coleção de dados da Real-Time CDP (como o [SDK da Web da Adobe Experience Platform](/help/collection/js/faq.md)) devem ser enviados por meio do Conector de origem do Audience Manager.

## &#x200B;3. Você usará o destino [!UICONTROL Experience Cloud Audiences] para trazer os dados de volta para a Audience Manager?

Segmentos que contêm regras potencialmente compatíveis com a Real-Time CDP, mas que possuem dependências de ativação no Audience Manager, podem ser enviados para o Audience Manager por meio do cartão de destino [Públicos-alvo da Experience Cloud](/help/destinations/catalog/adobe/experience-cloud-audiences.md).

## &#x200B;4. Dentre os destinos que você utiliza no Audience Manager hoje, quais podem ser movidos para a Real-Time CDP?

A Adobe recomenda que os segmentos ativados no Audience Manager para [destinos com base em pessoas](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=pt-BR) sejam enviados para a Real-Time CDP por meio do [!UICONTROL Audience Manager Source Connector] para ativação via Real-Time CDP.

Todos os destinos com base em pessoas disponíveis no Audience Manager - [Facebook](/help/destinations/catalog/social/facebook.md), [[!UICONTROL Google Customer Match]](/help/destinations/catalog/advertising/google-customer-match.md), [LinkedIn](/help/destinations/catalog/social/linkedin.md) - também estão disponíveis no Real-Time CDP.

Outros parceiros de estratégia de mídia e dados primários como o [Pinterest](/help/destinations/catalog/advertising/pinterest.md), [Snapchat](/help/destinations/catalog/advertising/snap-inc.md), [TikTok](/help/destinations/catalog/social/tiktok.md), [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md) e [[!UICONTROL The Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md) estão disponíveis.

Atualmente, a Real-Time CDP permite mais de 60 destinos nativos no [catálogo](/help/destinations/catalog/overview.md), mais de 20 dos quais são destinos de publicidade ou de redes sociais que oferecem suporte à correspondência de públicos-alvo primários.

## Próximas etapas

Agora que leu esta página, você já possui algumas informações a considerar ao iniciar sua evolução do Audience Manager para a Real-Time CDP.
