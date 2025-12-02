---
title: Definições de configuração da coleta de dados
description: Defina as configurações da coleção de dados na extensão de tag do Web SDK.
source-git-commit: 46c8748e9ab972705b8283c174c285e571acb2ed
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---

# Definições de configuração da coleta de dados

Esta seção de configuração permite determinar como os dados são coletados na extensão.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensions]** e selecione **[!UICONTROL Configure]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Role até a seção **[!UICONTROL Data collection]**.

![Imagem mostrando as configurações de coleta de dados da extensão de marca do Web SDK na interface do usuário de Marcas.](../assets/web-sdk-ext-collection.png)

As opções disponíveis são as seguintes:

## [!UICONTROL On before event send callback]

Uma função de retorno de chamada para avaliar e modificar o payload enviado para o Adobe. No editor de código, você tem acesso às seguintes variáveis:

* **`content.xdm`**: a carga XDM para o evento.
* **`content.data`**: a carga do objeto de dados para o evento.
* **`return true`**: saia imediatamente do retorno de chamada e envie dados para a Adobe com os valores atuais no objeto `content`.
* **`return false`**: saia imediatamente do retorno de chamada e interrompa o envio de dados para a Adobe.

Qualquer variável definida fora de `content` pode ser usada, mas não está incluída na carga enviada para o Adobe.

>[!WARNING]
>
>Esse retorno de chamada permite o uso do código personalizado. Se qualquer código incluído no retorno de chamada acionar uma exceção não capturada, o processamento do evento será interrompido. **Os dados não são enviados para o Adobe.**

```js
// Use nullish coalescing assignments to add objects if they don't yet exist
content.xdm.commerce ??= {};
content.xdm.commerce.order ??= {};

// Then add the purchase ID
content.xdm.commerce.order.purchaseID = "12345";

// Use optional chaining to prevent undefined errors when setting tracking code to lower case
if(content.xdm.marketing?.trackingCode) content.xdm.marketing.trackingCode = content.xdm.marketing.trackingCode.toLowerCase();

// Delete operating system version
if(content.xdm.environment) delete content.xdm.environment.operatingSystemVersion;

// Immediately end onBeforeEventSend logic and send the data to Adobe for this event type
if (content.xdm.eventType === "web.webInteraction.linkClicks") {
  return true;
}

// Cancel sending data if it is a known bot
if (myBotDetector.isABot()) {
  return false;
}
```

>[!TIP]
>Evite retornar `false` no primeiro evento da página. Retornar `false` no primeiro evento pode afetar negativamente a personalização.

Este retorno de chamada é a marca equivalente a [`onBeforeEventSend`](/help/collection/js/commands/configure/onbeforeeventsend.md) na biblioteca JavaScript.

## [!UICONTROL Collect internal link clicks]

Uma caixa de seleção que permite a coleta de dados de rastreamento de links internos no site ou na propriedade. Esta caixa de seleção é a marca equivalente a [`clickCollection.internalLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md) na biblioteca do JavaScript. Quando você ativa essa caixa de seleção, as opções de agrupamento de eventos são exibidas:

* **[!UICONTROL No event grouping]**: Os dados de rastreamento de link são enviados ao Adobe em eventos separados. Os cliques em links enviados em eventos separados podem aumentar o uso contratual dos dados enviados para o Adobe Experience Platform.
* **[!UICONTROL Event grouping using session storage]**: armazena dados de rastreamento de link no armazenamento da sessão até o próximo evento &quot;exibição de página&quot;. No próximo evento considerado uma &quot;exibição de página&quot;, os dados de rastreamento do link armazenados são mesclados com a carga do evento &quot;exibição de página&quot;. A Adobe recomenda ativar essa configuração ao rastrear links internos.
* **[!UICONTROL Event grouping using local object]**: armazena dados de rastreamento de link em um objeto local até o próximo evento &quot;exibição de página&quot;. Se um visitante navega para uma nova página do navegador, os dados de rastreamento de link são perdidos. Essa configuração é mais benéfica no contexto de aplicativos de página única.

A biblioteca de tags considera um determinado evento como uma &quot;visualização de página&quot; quando os seguintes elementos são incluídos na carga:

* `xdm.web.webPageDetails.name` contém um valor de cadeia de caracteres
* `xdm.web.webPageDetails.pageViews.value` é maior que `0`

## [!UICONTROL Collect external link clicks]

Uma caixa de seleção que permite a coleta de links externos. Esta caixa de seleção é a marca equivalente a [`clickCollection.externalLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md) na biblioteca do JavaScript.

## [!UICONTROL Collect download link clicks]

Uma caixa de seleção que permite a coleção de links de download. Esta caixa de seleção é a marca equivalente a [`clickCollection.downloadLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md) na biblioteca do JavaScript.

## [!UICONTROL Download link qualifier]

Uma expressão regular que qualifica um URL de link como um link de download. Esta cadeia de caracteres é a marca equivalente a [`downloadLinkQualifier`](/help/collection/js/commands/configure/downloadlinkqualifier.md) na biblioteca JavaScript.

## [!UICONTROL Filter click properties]

Uma função de retorno de chamada para avaliar e modificar propriedades relacionadas a cliques antes da coleção. Esta função é executada antes de [!UICONTROL On before event send callback] e é a marca equivalente a [`clickCollection.filterClickDetails`](/help/collection/js/commands/configure/clickcollection.md) na biblioteca JavaScript. No editor de código, você tem acesso às seguintes variáveis:

* **`content.clickedElement`**: o elemento DOM que foi clicado.
* **`content.pageName`**: O nome da página quando o clique ocorreu.
* **`content.linkName`**: o nome do link clicado.
* **`content.linkRegion`**: A região do link clicado.
* **`content.linkType`**: O tipo de link (saída, download ou outro).
* **`content.linkURL`**: a URL de destino do link clicado.
* **`return true`**: Saia imediatamente do retorno de chamada com os valores de variável atuais.
* **`return false`**: Saia imediatamente do retorno de chamada e cancele a coleta de dados.
* Qualquer variável definida fora de `content` pode ser usada, mas não está incluída na carga enviada para o Adobe.

>[!TIP]
>
>O campo **[!UICONTROL On before link click send]** é um retorno de chamada obsoleto que só é visível para propriedades que já o têm configurado. É a marca equivalente a [`onBeforeLinkClickSend`](/help/collection/js/commands/configure/onbeforelinkclicksend.md) na biblioteca JavaScript. Use o retorno de chamada **[!UICONTROL Filter click properties]** para filtrar ou ajustar os dados de cliques, ou use **[!UICONTROL On before event send callback]** para filtrar ou ajustar a carga geral enviada para o Adobe. Se o retorno de chamada **[!UICONTROL Filter click properties]** e o retorno de chamada **[!UICONTROL On before link click send]** estiverem definidos, somente o retorno de chamada **[!UICONTROL Filter click properties]** será executado.

## Configurações de contexto

Colete automaticamente as informações do visitante, que preenchem campos XDM específicos para você. Escolha **[!UICONTROL All default context information]** ou **[!UICONTROL Specific context information]**. É a marca equivalente a [`context`](/help/collection/js/commands/configure/context.md) na biblioteca JavaScript.

* **[!UICONTROL Web]**: Coleta informações sobre a página atual.
* **[!UICONTROL Device]**: Coleta informações sobre o dispositivo do usuário.
* **[!UICONTROL Environment]**: coleta informações sobre o navegador do usuário.
* **[!UICONTROL Place context]**: Coleta informações sobre a localização do usuário.
* **[!UICONTROL High entropy user-agent hints]**: coleta informações mais detalhadas sobre o dispositivo do usuário.
