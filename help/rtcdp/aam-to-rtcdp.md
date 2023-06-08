---
title: Evolução do Audience Manager para o Real-Time CDP
description: Entenda as considerações antes de planejar a migração do Audience Manager para o Real-Time CDP.
source-git-commit: 147e95cce203933d591fc807d9d20bcbc06e68e3
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---


# Evolução do Audience Manager para o Real-Time CDP

À medida que sua organização evolui para usar o Adobe Real-Time CDP, leve em conta essas considerações para preparar seus dados e conhecer as diferenças críticas entre as duas tecnologias. Este artigo destina-se a um público-alvo de profissionais.

![Audience Manager para o diagrama de evolução do Real-Time CDP](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## 1. Considere a arquitetura de dados no Audience Manager

Ao considerar a evolução do Audience Manager para o Real-Time CDP, agora é um momento crítico para analisar seu [segmentos Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html?lang=en) e determinar o que [sinais](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html?lang=en), [características](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html?lang=en), e [regras](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html?lang=en#segment-builder-section) são os que compõem esses segmentos.

Além disso, pense nas fontes de dados que você usa atualmente no Audience Manager.

A Adobe recomenda que você categorize seus segmentos da seguinte maneira:

* Segmentos que podem ser enviados para o Experience Platform por meio de [[!UICONTROL Conector de origem do Audience Manager]](/help/sources/connectors/adobe-applications/audience-manager.md), já que não têm dependências de dados, destino ou desafios de ativação, e suas regras de segmentação podem ser criadas por meio da Real-time CDP [construtor de segmentos](/help/segmentation/ui/segment-builder.md) posteriormente.
* Segmentos que têm regras que podem ser compatíveis, mas podem ter dados que não estarão disponíveis no Real-Time CDP.
* Segmentos que não podem ser criados na Real-time CDP e não têm funcionalidade.

>[!TIP]
>
>Ofertas do Adobe Real-Time CDP [três tipos de avaliação de segmento](/help/segmentation/home.md#evaluate-segments): [!UICONTROL Lote], [!UICONTROL Streaming], e [!UICONTROL Edge]. Os clientes que usam segmentos em tempo real no Audience Manager podem ser restritos pela limitação atual de 500 segmentos de transmissão no Real-Time CDP. Leia mais sobre [medidas de proteção de segmentação](/help/profile/guardrails.md).

## 2. Quais segmentos são essenciais para enviar por meio do [!UICONTROL Conector de origem do Audience Manager]?

Com base em seus critérios de avaliação, segmentos que não têm dependências de dados, nenhum desafio de destino ou ativação e suas regras de segmentação podem ser criadas por meio da coleta de dados do Real-Time CDP, como [Adobe Experience Platform Web SDK](/help/edge/web-sdk-faq.md) posteriormente deve ser enviado por meio do Conector de origem do Audience Manager.

## 3. Você usará o [!UICONTROL Públicos do Experience Cloud] destino para trazer os dados de volta para o Audience Manager?

Segmentos que têm regras que podem ser compatíveis com o Real-Time CDP, mas têm dependências de ativação para o Audience Manager, podem ser enviados para o Audience Manager por meio de [Públicos do Experience Cloud](/help/destinations/catalog/adobe/experience-cloud-audiences.md) cartão de destino.

## 4. Quais destinos você tem em vigor no Audience Manager hoje para começar a migrar para o Real-Time CDP?

A Adobe recomenda que os segmentos sejam ativados em Audience Manager para [destinos com base em pessoas](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=en) seja enviado para o Real-Time CDP por meio da [!UICONTROL Conector de origem do Audience Manager], para então ativar por meio do Real-Time CDP.

Todos os destinos com base em pessoas disponíveis no Audience Manager - [Facebook](/help/destinations/catalog/social/facebook.md), [[!UICONTROL Correspondência de cliente do Google]](/help/destinations/catalog/advertising/google-customer-match.md), [LinkedIn](/help/destinations/catalog/social/linkedin.md) - também estão disponíveis no Real-Time CDP.

Outros parceiros primários de estratégia de mídia e dados, como [Pinterest](/help/destinations/catalog/advertising/pinterest.md), [Snapchat](/help/destinations/catalog/advertising/snap-inc.md), [TikTok](/help/destinations/catalog/social/tiktok.md), [Anúncios do Amazon](/help/destinations/catalog/advertising/amazon-ads.md), e [[!UICONTROL A Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md) estão disponíveis.

Atualmente, o Real-Time CDP oferece suporte a mais de 60 destinos nativos no [catálogo](/help/destinations/catalog/overview.md), mais de 20 dos quais são destinos de anúncios ou sociais que oferecem suporte à correspondência de públicos-alvo primários.

## Próximas etapas

Depois de ler esta página, agora você tem um primeiro conjunto de considerações a serem levadas em conta ao iniciar sua evolução do Audience Manager para o Real-Time CDP.
