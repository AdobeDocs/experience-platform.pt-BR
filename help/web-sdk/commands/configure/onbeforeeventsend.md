---
title: onBeforeEventSend
description: Saiba como configurar o SDK da Web para registrar uma função do JavaScript que pode alterar os dados enviados antes que esses dados sejam enviados para o Adobe.
exl-id: 945f4fa1-380c-46aa-a92a-bbcfd6644751
source-git-commit: d3be2a9e75514023a7732a1c3460f8695ef02e68
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# `onBeforeEventSend`

O retorno de chamada `onBeforeEventSend` permite registrar uma função JavaScript que pode alterar os dados enviados antes que esses dados sejam enviados ao Adobe. Este retorno de chamada permite manipular o objeto `xdm` ou `data`, incluindo a capacidade de adicionar, editar ou remover elementos. Você também pode cancelar condicionalmente o envio de dados, como com o tráfego de bot do lado do cliente detectado.

>[!WARNING]
>
>Esse retorno de chamada permite o uso do código personalizado. Se qualquer código incluído no retorno de chamada acionar uma exceção não capturada, o processamento do evento será interrompido. Os dados não são enviados para o Adobe.

## Configure em antes do retorno de chamada do envio do evento usando a extensão de tag do SDK da Web {#tag-extension}

Selecione o botão **[!UICONTROL Fornecer antes do envio do evento do código de retorno de chamada]** ao [configurar a extensão de marca](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Esse botão abre uma janela modal onde você pode inserir o código desejado.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e clique em **[!UICONTROL Configurar]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Role para baixo até a seção [!UICONTROL Coleção de dados] e selecione o botão **[!UICONTROL Fornecer antes do código de retorno de chamada de envio do evento]**.
1. Esse botão abre uma janela modal com um editor de código. Insira o código desejado e clique em **[!UICONTROL Salvar]** para fechar a janela modal.
1. Clique em **[!UICONTROL Salvar]** nas configurações de extensão e publique suas alterações.

No editor de código, você tem acesso às seguintes variáveis:

* **`content.xdm`**: a carga [XDM](../sendevent/xdm.md) para o evento.
* **`content.data`**: a carga do objeto [data](../sendevent/data.md) para o evento.
* **`return true`**: Saia imediatamente do retorno de chamada e envie dados para o Adobe com os valores atuais no objeto `content`.
* **`return false`**: Saia imediatamente do retorno de chamada e interrompa o envio de dados para o Adobe.

Qualquer variável definida fora de `content` pode ser usada, mas não está incluída na carga enviada para o Adobe.

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

## Configure em antes do evento enviar retorno de chamada usando a biblioteca JavaScript do SDK da Web {#library}

Registre o retorno de chamada `onBeforeEventSend` ao executar o comando `configure`. Você pode alterar o nome da variável `content` para qualquer valor desejado alterando a variável de parâmetro dentro da função embutida.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: function(content) {
    // Use nullish coalescing assignments to add a new value
    content.xdm._experience ??= {};
    content.xdm._experience.analytics ??= {};
    content.xdm._experience.analytics.customDimensions ??= {};
    content.xdm._experience.analytics.customDimensions.eVars ??= {};
    content.xdm._experience.analytics.customDimensions.eVars.eVar1 = "Analytics custom value";
    
    // Use optional chaining to change an existing value
    if(content.xdm.web?.webPageDetails) content.xdm.web.webPageDetails.URL = content.xdm.web.webPageDetails.URL.toLowerCase();
    
    // Remove an existing value
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
    
    // Return true to immediately send data
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to immediately cancel sending data
    if(myBotDetector.isABot()){
      return false;
    }
    
    // Assign the value in the 'cid' query string to the tracking code XDM element
    content.xdm.marketing ??= {};
    content.xdm.marketing.trackingCode = new URLSearchParams(window.location.search).get('cid');
  }
});
```

Você também pode registrar sua própria função em vez de uma função em linha.

```js
function lastChanceLogic(content) {
  content.xdm.application ??= {};
  content.xdm.application.name = "App name";
}

alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: lastChanceLogic
});    
```
