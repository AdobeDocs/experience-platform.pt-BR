---
solution: Experience Platform
title: Mapeamento de dados de eventos do Adobe Target para o XDM
description: Saiba como mapear campos de evento do Adobe Target para um esquema do Experience Data Model (XDM) para usar no Adobe Experience Platform.
exl-id: dab08ab6-6c1c-460a-bb52-8dcdb5709a34
source-git-commit: 81412493b096264ce7a89e3ca2348edb2dcd1798
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# Mapeamentos de campo de target mapping

A tabela a seguir descreve os campos de um esquema de Evento de experiência do Experience Data Model (XDM) e os campos correspondentes do Adobe Target para os quais eles devem ser mapeados. Observações adicionais para alguns mapeamentos também são fornecidas.

>[!NOTE]
>
>Role a tela para a esquerda/direita para visualizar o conteúdo completo da tabela.

| Campo XDM ExperienceEvent | Campo de solicitação do Target | Notas |
| ------------------------- | -------------------- | ----- |
| **`id`** | Um identificador de solicitação exclusivo |
| **`dataSource`** | | Configurado como &quot;1&quot; para todos os clientes. |
| `dataSource._id` | Um valor gerado pelo sistema que não pode ser transmitido com a solicitação. | O identificador exclusivo desta fonte de dados. Isso seria fornecido pelo indivíduo ou sistema que criou a fonte de dados. |
| `dataSource.code` | Um valor gerado pelo sistema que não pode ser transmitido com a solicitação. | Um atalho para o @id completo. Pelo menos um dos códigos ou @id pode ser usado. Às vezes, esse código é chamado de código de integração da fonte de dados. |
| `dataSource.tags` | Um valor gerado pelo sistema que não pode ser transmitido com a solicitação. | As tags são usadas para indicar como os aliases representados por uma determinada fonte de dados devem ser interpretados pelos aplicativos que usam esses aliases.<br><br>Exemplos:<br><ul><li>`isAVID`: fontes de dados que representam IDs de visitante do Analytics.</li><li>`isCRSKey`: fontes de dados que representam aliases que devem ser usados como chaves no CRS.</li></ul>As tags são definidas quando a fonte de dados é criada, mas também são incluídas nas mensagens do pipeline ao fazer referência a uma determinada fonte de dados. |
| **`timestamp`** | Carimbo de data e hora do evento |
| **`channel`** | `context.channel` | Funciona somente com a entrega de visualização. As opções são &quot;web&quot; e &quot;mobile&quot;, e &quot;web&quot; é o padrão. |
| **`endUserIds`** |
| `endUserIds.experience.tntId` | `tntId/mboxPC` |
| `endUserIds.experience.mcId` | `marketingCloudVisitorId` | A ID de Experience Cloud (ECID) também é conhecida como MCID e continua a ser usada em namespaces. |
| **`environment`** |
| `environment.browserDetails.userAgent` | `mboxRequest.userAgent` |
| `environment.browserDetails.viewPortHeight` | `mboxRequest.browserHeight` |
| `environment.browserDetails.viewPortWidth` | `mboxRequest.browserWidth` |
| `environment.operatingSystem` | `deviceAtlas.osName` |
| `environment.operatingSystemVersion` | `deviceAtlas.osVersion` |
| `environment.viewportHeight` | `mboxRequest.screenHeight` |
| `environment.viewportWidth` | `mboxRequest.screenWidth` |
| `environment.colorDepth` | `mboxRequest.colorDepth` |
| `environment.carrier` | O nome da operadora de celular foi resolvido com base no endereço IP da solicitação. |
| `environment.ipV4` | `mboxRequest.ipAddress` (se estiver no formato V4) |
| `environment.ipV6` | `mboxRequest.ipAddress` (se no formato V6) |
| **`experience`** |
| `experience.target.clientCode` | `mboxRequest.client` |
| `experience.target.mboxName` | `mboxRequest.mboxName` |
| `experience.target.mboxVersion` | `mboxRequest.mboxVersion` |
| `experience.target.sessionId` | `mboxRequest.sessionId` |
| `experience.target.environmentID` | Mapeamento interno do Target para ambientes definidos pelo cliente (como desenvolvimento, controle de qualidade ou produção). |
| `experience.target.supplementalDataID` | Identificador usado para compilar eventos do Target com eventos do Analytics |
| `experience.target.pageDetails.pageId` | `mboxRequest.pageId` |
| `experience.target.pageDetails.pageScore` | `mboxRequest.mboxPageValue` |
| `experience.target.activities` | Lista (matriz) de atividades para as quais o visitante se qualificou |
| `experience.target.activities[i].activityID` | A ID de qualquer atividade para a qual o visitante se qualificou |
| `experience.target.activities[i].version` | A versão de qualquer atividade para a qual o visitante se qualificou |
| `experience.target.activities[i].activityEvents` | Inclui os detalhes dos eventos de atividade que o usuário acessou com este evento. |
| **`device`** |
| `device.typeIDService` | `XDMDevice.Device.TypeIDService.typeIDService_deviceatlas` |
| `device.type` | Uma das seguintes propriedades de `deviceAtlas` (ou NULL): <ul><li>`type_mobile`</li><li>`type_tablet`</li><li>`type_desktop`</li><li>`type_ereader`</li><li>`type_television`</li><li>`type_settop`</li><li>`type_mediaplayer`</li></ul> |
| `device.typeID` | (cadeia de caracteres vazia) |
| `device.manufacturer` | `deviceAtlas.manufacturer` |
| `device.model` | `deviceAtlas.model` |
| `device.modelNumber` | (cadeia de caracteres vazia) |
| `device.screenHeight` | `deviceAtlas.displayHeight` |
| `device.screenWidth` | `deviceAtlas.displayWidth` |
| `device.colorDepth` | `deviceAtlas.displayColorDepth` |
| **`placeContext`** |
| `placeContext.geo.id` | UUID aleatório (obrigatório) |
| `placeContext.geo.city` | O nome da cidade foi resolvido com base no endereço IP da solicitação. |
| `placeContext.geo.countryCode` | Código do país resolvido com base no endereço IP da solicitação. |
| `placeContext.geo.dmaId` | Código de área de mercado designada resolvido com base no endereço IP da solicitação. |
| `placeContext.geo.postalCode` | Código postal resolvido com base no endereço IP da solicitação. |
| `placeContext.geo.stateProvince` | Estado resolvido com base no endereço IP da solicitação. |
| `placeContext.localTime` | `mboxRequest.offsetTime` + `mboxRequest.currentServerTime` |
| **`commerce`** | | Definir somente se os detalhes do pedido estiverem presentes na solicitação. |
| `commerce.order.priceTotal` | `mboxRequest.orderTotal` |
| `commerce.order.purchaseOrderNumber` | `mboxRequest.orderId` |
| `commerce.order.purchaseID` | `mboxRequest.orderId` |
| **`web`** |
| `web.withWebPageDetails.url` | `mboxURL.context.address.url` |
| `web.webReferrer.url` | `mboxReferrer.context.address.url` |
| **`identityMap`** |
| `identityMap.TNTID` | `tntId.mboxPC` |
| `identityMap.ECID` | `marketingCloudVisitorId` |

{style="table-layout:auto"}
