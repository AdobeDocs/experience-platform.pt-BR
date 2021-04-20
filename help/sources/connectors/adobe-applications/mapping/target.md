---
keywords: Experience Platform, home, tópicos populares, target mapping, Target mapping
solution: Experience Platform
title: Mapeamento de dados de evento do Adobe Target para XDM
topic-legacy: overview
description: Saiba como mapear campos de evento do Adobe Target para um esquema do Experience Data Model (XDM) para uso no Adobe Experience Platform.
exl-id: dab08ab6-6c1c-460a-bb52-8dcdb5709a34
translation-type: tm+mt
source-git-commit: af5564a07577a0123e1a45043d5479f6ad45d73e
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---

# Mapeamento de campos de target

O Adobe Experience Platform permite assimilar dados do Adobe Target por meio do conector de origem do Target. Ao usar o conector, todos os dados dos campos do Target devem ser mapeados para os campos [Experience Data Model (XDM)](../../../../xdm/home.md) associados à classe XDM ExperienceEvent.

A tabela a seguir descreve os campos de um esquema de Evento de experiência (*campo ExperienceEvent XDM*) e os campos Target correspondentes aos quais eles devem ser mapeados (*Campo Solicitação de destino*). Também são fornecidas notas adicionais para alguns mapeamentos.

>[!NOTE]
>
>Role a tela para a esquerda/direita para exibir o conteúdo completo da tabela.

| Campo ExperienceEvent XDM | Campo Solicitação de direcionamento | Notas |
| ------------------------- | -------------------- | ----- |
| **`id`** | Um identificador de solicitação exclusivo |
| **`dataSource`** |  | Configurado para &quot;1&quot; para todos os clientes. |
| `dataSource._id` | Um valor gerado pelo sistema que não pode ser transmitido com a solicitação. | A ID exclusiva dessa fonte de dados. Isso seria fornecido pelo indivíduo ou sistema que criou a fonte de dados. |
| `dataSource.code` | Um valor gerado pelo sistema que não pode ser transmitido com a solicitação. | Um atalho para o @id completo. Pelo menos um do código ou @id pode ser usado. Às vezes, esse código é chamado de código de integração da fonte de dados. |
| `dataSource.tags` | Um valor gerado pelo sistema que não pode ser transmitido com a solicitação. | As tags são usadas para indicar como os aliases representados por uma determinada fonte de dados devem ser interpretados por aplicativos que usam esses aliases.<br><br>Exemplos:<br><ul><li>`isAVID`: Fontes de dados que representam as IDs de visitante do Analytics.</li><li>`isCRSKey`: Fontes de dados que representam aliases que devem ser usados como chaves no CRS.</li></ul>Tags são definidas quando a fonte de dados é criada, mas também são incluídas em mensagens de pipeline ao referenciar uma determinada fonte de dados. |
| **`timestamp`** | Carimbo de data e hora do evento |
| **`channel`** | `context.channel` | Funciona somente com o delivery de exibição. As opções são &quot;web&quot; e &quot;móvel&quot;, com &quot;web&quot; sendo o padrão. |
| **`endUserIds`** |
| `endUserIds.experience.tntId` | `tntId/mboxPC` |
| `endUserIds.experience.mcId` | `marketingCloudVisitorId` |
| **`environment`** |
| `environment.browserDetails.userAgent` | `mboxRequest.userAgent` |
| `environment.browserDetails.viewPortHeight` | `mboxRequest.browserHeight` |
| `environment.browserDetails.viewPortWidth` | `mboxRequest.browserWidth` |
| `environment.operatingSystem` | `deviceAtlas.osName` |
| `environment.operatingSystemVersion` | `deviceAtlas.osVersion` |
| `environment.viewportHeight` | `mboxRequest.screenHeight` |
| `environment.viewportWidth` | `mboxRequest.screenWidth` |
| `environment.colorDepth` | `mboxRequest.colorDepth` |
| `environment.carrier` | Nome da operadora de celular resolvido com base no endereço IP da solicitação. |
| `environment.ipV4` | `mboxRequest.ipAddress` (se no formato V4) |
| `environment.ipV6` | `mboxRequest.ipAddress` (se no formato V6) |
| **`experience`** |
| `experience.target.clientCode` | `mboxRequest.client` |
| `experience.target.mboxName` | `mboxRequest.mboxName` |
| `experience.target.mboxVersion` | `mboxRequest.mboxVersion` |
| `experience.target.sessionId` | `mboxRequest.sessionId` |
| `experience.target.environmentID` | Mapeamento interno do Target para ambientes definidos pelo cliente (como dev, qa ou prod). |
| `experience.target.supplementalDataID` | Identificador usado para unir eventos do Target aos eventos do Analytics |
| `experience.target.pageDetails.pageId` | `mboxRequest.pageId` |
| `experience.target.pageDetails.pageScore` | `mboxRequest.mboxPageValue` |
| `experience.target.activities` | Lista (matriz) de atividades para as quais o visitante se qualificou |
| `experience.target.activities[i].activityID` | A ID de qualquer atividade para a qual o visitante se qualificou |
| `experience.target.activities[i].version` | A versão de qualquer atividade específica para a qual o visitante se qualificou |
| `experience.target.activities[i].activityEvents` | Inclui detalhes de eventos de atividade que o usuário acessou com este evento. |
| **`device`** |
| `device.typeIDService` | `XDMDevice.Device.TypeIDService.typeIDService_deviceatlas` |
| `device.type` | Uma das seguintes propriedades de `deviceAtlas` (ou NULL): <ul><li>`type_mobile`</li><li>`type_tablet`</li><li>`type_desktop`</li><li>`type_ereader`</li><li>`type_television`</li><li>`type_settop`</li><li>`type_mediaplayer`</li></ul> |
| `device.typeID` | (string vazia) |
| `device.manufacturer` | `deviceAtlas.manufacturer` |
| `device.model` | `deviceAtlas.model` |
| `device.modelNumber` | (string vazia) |
| `device.screenHeight` | `deviceAtlas.displayHeight` |
| `device.screenWidth` | `deviceAtlas.displayWidth` |
| `device.colorDepth` | `deviceAtlas.displayColorDepth` |
| **`placeContext`** |
| `placeContext.geo.id` | UUID aleatório (obrigatório) |
| `placeContext.geo.city` | O nome da cidade foi resolvido com base no endereço IP da solicitação. |
| `placeContext.geo.countryCode` | Código do país resolvido com base no endereço IP da solicitação. |
| `placeContext.geo.dmaId` | Código de área de mercado designada resolvido com base no endereço IP da solicitação. |
| `placeContext.geo.postalCode` | Código postal resolvido com base no endereço IP da solicitação. |
| `placeContext.geo.stateProvince` | O estado ou província foi resolvido com base no endereço IP da solicitação. |
| `placeContext.localTime` | `mboxRequest.offsetTime` + `mboxRequest.currentServerTime` |
| **`commerce`** |  | Defina somente se os detalhes do pedido estiverem presentes na solicitação. |
| `commerce.order.priceTotal` | `mboxRequest.orderTotal` |
| `commerce.order.purchaseOrderNumber` | `mboxRequest.orderId` |
| `commerce.order.purchaseID` | `mboxRequest.orderId` |
| **`web`** |
| `web.withWebPageDetails.url` | `mboxURL.context.address.url` |
| `web.webReferrer.url` | `mboxReferrer.context.address.url` |
| **`identityMap`** |
| `identityMap.TNTID` | `tntId.mboxPC` |
| `identityMap.ECID` | `marketingCloudVisitorId` |

{style=&quot;table-layout:auto&quot;}
