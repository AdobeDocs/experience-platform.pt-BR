---
title: Grupo de campos de esquema de extensão completa do Adobe Advertising Cloud ExperienceEvent
description: Saiba mais sobre o grupo de campos de esquema Extensão completa do Adobe Advertising Cloud ExperienceEvent.
badgeBeta: label="Beta" type="Informative"
source-git-commit: adfd0220b8bc53c44abc76a711b148a7e03edb7a
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 7%

---

# [!UICONTROL Extensão completa do campo de esquema da Adobe Advertising Cloud ExperienceEvent]

>[!AVAILABILITY]
>
>O grupo de campos [!UICONTROL Extensão completa do Adobe Advertising Cloud ExperienceEvent] está atualmente na versão beta. A documentação e a funcionalidade estão sujeitas a alterações.

A [!UICONTROL Extensão Completa de ExperienceEvent da Adobe Advertising Cloud] é um grupo de campos de esquema padrão para a [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), que captura métricas comuns coletadas pela Adobe Advertising (anteriormente chamadas de &quot;[!DNL Advertising Cloud]&quot;).

Este documento descreve a estrutura e o caso de uso do grupo de campos de extensão [!DNL Advertising Cloud].

>[!NOTE]
>
>Você também pode pesquisar este grupo de campos [na interface do usuário do Experience Platform](../../ui/explore.md) ou exibir o esquema completo no [repositório XDM público](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

## Estrutura do grupo de campos

O grupo de campos fornece um único objeto `_experience` a um esquema, que contém um único objeto `adcloud`.

![Campos de nível superior para o [!DNL Advertising Cloud] grupo de campos](../../images/field-groups/advertising-full-extension/full-schema.png "Campos de nível superior para o [!DNL Advertising Cloud] grupo de campos")

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `adDeliveryDetails` | Objeto | Detalhes de entrega de anúncio. Consulte a [subseção abaixo no `adDeliveryDetails` objeto](#adDeliveryDetails) para obter mais informações sobre o conteúdo desse objeto. |
| `advertisement` | Objeto | Detalhes de publicidade digital. Consulte a [subseção abaixo no objeto de anúncio](#advertisement) para obter mais informações sobre o conteúdo desse objeto. |
| `campaign` | Objeto | Detalhes da hierarquia da campanha. Consulte a [subseção abaixo no objeto da campanha](#campaign-campaign) para obter mais informações sobre o conteúdo desse objeto. |
| `conversionDetails` | Objeto | Detalhes de conversão para um anúncio. Consulte a [subseção abaixo](#conversionDetails) para obter mais informações sobre o conteúdo desse objeto. |
| `eventType` | String | O tipo de evento do Adobe Advertising. |
| `fees` | Objeto | Detalhes da taxa do Advertising. Consulte a [subseção abaixo no objeto de taxas](#fees) para obter mais informações sobre o conteúdo desse objeto. |
| `inventory` | Objeto | Detalhes do inventário. Consulte a [subseção abaixo](#inventory) para obter mais informações sobre o conteúdo desse objeto. |
| `productDetails` | Objeto | Detalhes do anúncio do produto. Consulte a [subseção abaixo no objeto productDetails](#productDetails) para obter mais informações sobre o conteúdo desse objeto. |
| `stitchId` | String | ID dos servidores de publicidade da Adobe Advertising para rastrear conversões de click-throughs em navegadores que bloqueiam cookies de terceiros. |

## `adDeliveryDetails` {#adDeliveryDetails}

O objeto adDeliveryDetails fornece informações sobre onde e como o anúncio foi entregue, incluindo sites de posicionamento e identificadores de local.

![Diagrama de esquema mostrando o objeto `adDeliveryDetails` e seus campos.](../../images/field-groups/advertising-full-extension/adDeliveryDetails.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `placementWebsite` | String | O site onde o anúncio foi exibido. |
| `siteLinkText` | String | O link do site real selecionado no anúncio. |
| `interestLocationID` | String | O local inferido da consulta de pesquisa. Por exemplo, uma consulta para &quot;Hotel em Goa&quot; retorna a ID para Goa, independentemente da localização de navegação real do usuário. |
| `physicalLocationID` | String | O local de navegação do usuário, representado por uma ID de referência da rede de publicidade. Essa ID não é um nome de local legível (como cidade ou país), mas um código atribuído pela rede de anúncios para identificar um público-alvo geográfico. |

## `advertisement` {#advertisement}

O objeto de anúncio descreve detalhes sobre o anúncio digital, como identificadores, tipo, criativo, direcionamento e palavras-chave associadas.

![Diagrama de esquema mostrando o objeto `advertisement` e seus campos.](../../images/field-groups/advertising-full-extension/advertisement.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `adId` | String | O identificador do anúncio associado a este evento. Essa ID não está relacionada ao padrão do setor de Ad-ID. |
| `runtime` | String | O tempo de execução da unidade de anúncio, diferente do tempo de execução do navegador ou do sistema operacional. Os valores possíveis incluem: `unknown` e `HTML5`. |
| `adClass` | String | A classe de anúncio do evento de direção: `display`, `video` ou `social`. |
| `adUnitType` | String | O identificador do código que renderiza o anúncio em um navegador ou dispositivo. Os valores possíveis incluem:<ul><li>`linearVideo`: Vídeo linear</li><li>`interactiveVideo`: Vídeo interativo</li><li>`banner`: Banner,</li><li>`richMediaBanner`: banner de mídia avançada,</li><li>`newsFeedVideo`: Vídeo de feed de notícias,</li><li>`newsFeedDisplay`: Exibição do feed de notícias,</li><li>`HTML5`: HTML5,</li><li>`inPageVideo`: No vídeo da página,</li><li>`inPageDisplay`: Na exibição da página,</li><li>`facebook`: Facebook,</li><li>`twitter`: Twitter,</li><li>`linearTv`: TV Linear,</li><li>`vod`: vídeo sob demanda</li></ul> |
| `promotedAssetId` | String | O identificador do ativo promovido no anúncio associado a este evento. |
| `creativeID` | String | O identificador do anúncio criativo (como um banner, vídeo ou anúncio social) associado a este evento. |
| `keywordID` | String | O identificador da palavra-chave inserida pelo usuário em uma consulta de pesquisa que acionou esse evento. |
| `keyword` | String | A palavra-chave da listagem na qual o cliente deu lance. |
| `isDynamicSearchAd` | Booleano | Indica se o evento vem de um anúncio de pesquisa dinâmica. |
| `audienceID` | String | O identificador do segmento de público alvo direcionado pelo anúncio. |
| `adGroupID` | String | O identificador do grupo de anúncios associado ao anúncio que acionou esse evento. |
| `campaignID` | String | O identificador da campanha associado ao anúncio que acionou esse evento. |
| `networkType` | String | O tipo de rede em que o evento ocorreu. Os valores possíveis incluem: <ul><li>`search`: O anúncio foi exibido na Rede de Pesquisa.</li><li>`content`: O anúncio foi exibido na Rede de Conteúdo.</li></ul> |
| `matchType` | String | O tipo de correspondência da palavra-chave. Os valores possíveis incluem: <ul><li>`exact`: correspondência exata da palavra-chave</li><li>`broad`: Grande correspondência da palavra-chave</li><li>`phrase`: correspondência de frase da palavra-chave</li></ul> |

## `campaign` {#campaign}

O objeto campaign define a hierarquia da campanha de publicidade, incluindo os identificadores de conta, anunciante, posicionamento e pacote, juntamente com os detalhes da moeda.

![Diagrama de esquema mostrando o objeto `campaign` e seus campos.](../../images/field-groups/advertising-full-extension/campaign.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `accountId` | String | O identificador da conta. |
| `dspId` | String | O identificador da Demand Side Platform (DSP) na qual a campanha é definida. Normalmente, esse identificador é a ID da Adobe Advertising Cloud DSP. |
| `campaignId` | String | O identificador da campanha. |
| `placementId` | String | O identificador do posicionamento. |
| `packageId` | String | O identificador do pacote Advertising DSP. |
| `advertiserId` | String | O identificador do anunciante. |
| `experimentId` | String | O identificador do experimento. |
| `sampleGroupId` | String | O identificador do grupo de amostra. |
| `currency` | String | O código de moeda de faturamento ISO 4217 da conta. Usa o padrão de expressão regular ^[A-Z]{3}$ (três letras maiúsculas). Por exemplo: USD, EUR. |

## `conversionDetails` {#conversionDetails}

O objeto conversionDetails captura informações de rastreamento para conversões de anúncios, incluindo códigos de rastreamento, identidades e propriedades de conversão.

![Diagrama de esquema mostrando o objeto `conversionDetails` e seus campos.](../../images/field-groups/advertising-full-extension/conversionDetails.png "campo conversionDetails")

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `trackingCode` | String | O código de rastreamento de conversão do evento. Para obter uma lista de formatos possíveis, consulte [Formatos de ID AMO](https://experienceleague.adobe.com/en/docs/advertising/integrations/customer-journey-analytics/ids#amo-id-formats). |
| `trackingIdentities` | String | A ID EF ou os detalhes de identidade de rastreamento de um evento. Para obter uma lista de formatos possíveis, consulte [Formatos de ID EF](https://experienceleague.adobe.com/en/docs/advertising/integrations/customer-journey-analytics/ids#ef-id-formats). |
| `conversionProperties` | Objeto | Um mapa de propriedades de conversão, representado como uma matriz de cadeias de pares de valores chave (como `subscriptions=253`). |

## `fees` {#fees}

O objeto de taxas captura mídia, dados e outros custos de publicidade, divididos por Advertising DSP, conta e anunciante.

![Diagrama de esquema mostrando o objeto `fees` e seus campos.](../../images/field-groups/advertising-full-extension/fees.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `DSPMediaFees` | Número | As taxas de mídia faturáveis pela Advertising DSP. |
| `DSPDataFees` | Número | As taxas de dados faturáveis pela Advertising DSP. |
| `DSPOtherFees` | Número | Outras taxas faturáveis pela Advertising DSP. |
| `accountMediaFees` | Número | As taxas de mídia da conta, mas não faturáveis pela Advertising DSP. |
| `accountDataFees` | Número | As taxas de dados da conta, mas não faturáveis pela Advertising DSP. |
| `accountOtherFees` | Número | Outras taxas da conta, mas não faturáveis pela Advertising DSP. |
| `advertiserMediaFees` | Número | As taxas do anunciante de mídia cobradas do anunciante da conta. |
| `advertiserDataFees` | Número | Outras taxas de anunciante cobradas ao anunciante a partir da conta. |
| `advertiserOtherFees` | Número | Outras taxas de anunciante cobradas ao anunciante a partir da conta. |
| `billableMediaNetSpend` | Número | O gasto líquido faturável para publicidade em mídia. |
| `totalMediaNetSpend` | Número | O gasto líquido total para publicidade em mídia. |
| `billableDataNetSpend` | Número | O gasto líquido faturável para publicidade de dados. |
| `billableOtherNetSpend` | Número | O gasto líquido faturável para outros tipos de publicidade. |
| `totalBillableNetSpend` | Número | O gasto líquido faturável total. |
| `totalNonBillableNetSpend` | Número | O gasto líquido não faturável total. |
| `totalNetSpend` | Número | O gasto líquido total. |

## `inventory` {#inventory}

O objeto de inventário registra detalhes sobre a oportunidade de inventário de anúncios, incluindo dados de sessão, códigos de parceiros, IDs de site, moeda de custo e regras de segmentação.

![Diagrama de esquema mostrando o objeto `inventory` e seus campos.](../../images/field-groups/advertising-full-extension/inventory.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `sessionId` | String | A ID da sessão associada a um evento de experiência, usada para vincular eventos independentes que ocorreram na mesma sessão. |
| `feedID` | String | Uma ID composta do editor, troca de anúncios e outros recursos. |
| `sspPartnerCode` | String | O parceiro (exchange) pelo qual a Adobe Advertising Cloud recebe a oportunidade de inventário. |
| `siteID` | String | O identificador do site onde a impressão do anúncio foi veiculada. |
| `costCurrency` | String | O código de moeda ISO 4217 usado para pagar um parceiro por uma oportunidade de anúncio. O valor deve seguir o padrão de expressão regular ^[A-Z]{3}$ (três letras maiúsculas). Por exemplo: USD, EUR. |
| `inventorySourceId` | String | A ID da fonte de inventário da Adobe Advertising Cloud na qual esta oportunidade foi entregue. |
| `segment` | Objeto | Detalhes associados às regras de segmentação do usuário. Suas propriedades incluem:<ul><li>`attributablePartnerId` (Cadeia de caracteres): o identificador do provedor de segmento que possui o attributableSegmentId.</li><li>`attributableSegmentId` (Cadeia de caracteres): o segmento creditado pelo direcionamento de usuário na regra de direcionamento do posicionamento. Isso é usado para fins de rastreamento de custos e parceiros pagantes.</li><li>`segments` (Cadeia de caracteres): a interseção dos segmentos de usuário a\) aos quais o usuário pertencia e b\) que o anúncio estava direcionando. Esta não é a lista completa de segmentos aos quais o usuário pertencia no momento do leilão.</li></ul> |
| `optimizationTag` | String | A tag relacionada à otimização. |
| `attributableDeviceGraphId` | String | O identificador do gráfico de dispositivos atribuído a um evento de conversão. |

## `productDetails` {#productDetails}

O objeto `productDetails` contém informações sobre produtos apresentados nos anúncios de compras de [!DNL Adobe Advertising Search, Social, & Commerce], incluindo identificadores de produtos, país, idioma, partição, título e tipo de anúncio.

![Diagrama de esquema mostrando o objeto `productDetails` e seus campos.](../../images/field-groups/advertising-full-extension/productDetails.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `productID` | String | O identificador do produto apresentado no anúncio associado a este evento. |
| `country` | String | O país de venda do produto apresentado no anúncio associado ao evento. |
| `language` | String | O idioma das informações do produto, conforme indicado no feed de dados da Central de comerciantes do cliente. |
| `partitionID` | String | O identificador do grupo de produtos associado ao anúncio neste evento. |
| `title` | String | O título do produto mostrado no anúncio. |
| `adType` | String | O tipo de anúncio do produto usado em [!DNL Google] campanhas de compras. Os valores possíveis incluem:<ul><li>`pla_with_pog`: Quando o evento veio de uma compra através de um anúncio de compras</li><li>`pla`: Quando o evento veio de um anúncio de compras.</li><li>`pla_multichannel`: Quando o evento de um anúncio de compra incluía opções para os canais de compras &quot;online&quot; e &quot;local&quot;.</li><li>`pla_with_promotion`: quando o evento de um anúncio de compras exibia uma promoção de comerciante.</li></ul> |

## Próximas etapas

Este documento abordou a estrutura e o caso de uso para o grupo de campos de extensão [!DNL Advertising Cloud]. Para obter mais detalhes sobre o próprio grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/adcloud/experienceevent-all.schema.json).

Se você estiver usando este grupo de campos para coletar dados do [!DNL Advertising] usando o Adobe Experience Platform Web SDK, consulte o manual em [configurando uma sequência de dados](../../../datastreams/overview.md) para saber como mapear dados para o XDM no lado do servidor.
