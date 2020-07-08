---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: campo Target mapping
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---


# Campos de Target mapping

O Adobe Experience Platform permite que você ingira dados do Adobe Target através do conector de fonte do Público alvo. Ao usar o conector, todos os dados dos campos do Público alvo devem ser mapeados para os campos do Modelo de dados de [experiência (XDM)](../../../../xdm/home.md) associados à classe XDM ExperienceEvent.

A tabela a seguir descreve os campos de um schema do Evento de experiência (campo *XDM ExperienceEvent) e os campos correspondentes do Público alvo para os quais eles devem ser mapeados (campo* Solicitação de ** Público alvo). Também são fornecidas notas adicionais para alguns mapeamentos.

>[!NOTE]
>
>Role para a esquerda/direita para visualização do conteúdo completo da tabela.

| Campo XDM ExperienceEvent | campo Solicitação de Público alvo | Notas |
| ------------------------- | -------------------- | ----- |
| **`id`** | Um identificador de solicitação exclusivo |
| **`dataSource`** |  | Configurado para &quot;1&quot; para todos os clientes. |
| `dataSource._id` | Um valor gerado pelo sistema que não pode ser passado com a solicitação. | A ID exclusiva dessa fonte de dados. Isso seria fornecido pelo indivíduo ou sistema que criou a fonte de dados. |
| `dataSource.code` | Um valor gerado pelo sistema que não pode ser passado com a solicitação. | Um atalho para o @id completo. Pelo menos um código ou @id pode ser usado. Às vezes, esse código é chamado de código de integração da fonte de dados. |
| `dataSource.tags` | Um valor gerado pelo sistema que não pode ser passado com a solicitação. | As tags são usadas para indicar como os aliases representados por uma determinada fonte de dados devem ser interpretados por aplicativos que usam esses aliases.<br><br>Exemplos:<br><ul><li>`isAVID`: Fontes de dados que representam IDs de visitante da Analytics.</li><li>`isCRSKey`: Fontes de dados que representam aliases que devem ser usadas como chaves no CRS.</li></ul>As tags são definidas quando a fonte de dados é criada, mas também são incluídas em mensagens de pipeline ao referenciar uma determinada fonte de dados. |
| **`timestamp`** | carimbo de data e hora do Evento |
| **`channel`** | `context.channel` | Só funciona com delivery de visualização. As opções são &quot;web&quot; e &quot;móvel&quot;, sendo &quot;web&quot; o padrão. |
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
| `environment.carrier` | O nome da operadora de celular foi resolvido com base no endereço IP da solicitação. |
| `environment.ipV4` | `mboxRequest.ipAddress` (se no formato V4) |
| `environment.ipV6` | `mboxRequest.ipAddress` (se no formato V6) |
| **`experience`** |
| `experience.target.clientCode` | `mboxRequest.client` |
| `experience.target.mboxName` | `mboxRequest.mboxName` |
| `experience.target.mboxVersion` | `mboxRequest.mboxVersion` |
| `experience.target.sessionId` | `mboxRequest.sessionId` |
| `experience.target.environmentID` | Mapeamento interno do Público alvo para ambientes definidos pelo cliente (como dev, qa ou prod). |
| `experience.target.supplementalDataID` | Identificador usado para unir eventos de Público alvo a eventos Analytics |
| `experience.target.pageDetails.pageId` | `mboxRequest.pageId` |
| `experience.target.pageDetails.pageScore` | `mboxRequest.mboxPageValue` |
| `experience.target.activities` | Lista (matriz) de atividades para as quais o visitante se qualificou |
| `experience.target.activities[i].activityID` | A ID de qualquer atividade para a qual o visitante se qualificou |
| `experience.target.activities[i].version` | A versão de qualquer atividade para a qual o visitante se qualificou |
| `experience.target.activities[i].activityEvents` | Inclui os detalhes dos eventos de atividade que o usuário acessou com este evento. |
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
| `placeContext.geo.countryCode` | O código do país foi resolvido com base no endereço IP da solicitação. |
| `placeContext.geo.dmaId` | O código da Área de Mercado Designada foi resolvido com base no endereço IP da solicitação. |
| `placeContext.geo.postalCode` | Código postal resolvido com base no endereço IP da solicitação. |
| `placeContext.geo.stateProvince` | Estado ou província resolvido com base no endereço IP da solicitação. |
| `placeContext.localTime` | `mboxRequest.offsetTime` + `mboxRequest.currentServerTime` |
| **`commerce`** |  | Definir somente se os detalhes do pedido estiverem presentes na solicitação. |
| `commerce.order.priceTotal` | `mboxRequest.orderTotal` |
| `commerce.order.purchaseOrderNumber` | `mboxRequest.orderId` |
| `commerce.order.purchaseID` | `mboxRequest.orderId` |
| **`web`** |
| `web.withWebPageDetails.url` | `mboxURL.context.address.url` |
| `web.webReferrer.url` | `mboxReferrer.context.address.url` |
| **`identityMap`** |
| `identityMap.TNTID` | `tntId.mboxPC` |
| `identityMap.ECID` | `marketingCloudVisitorId` |
