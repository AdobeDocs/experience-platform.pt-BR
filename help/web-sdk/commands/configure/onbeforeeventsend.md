---
title: onBeforeEventSend
description: Saiba como configurar o SDK da Web para registrar uma função do JavaScript que pode alterar os dados enviados antes que esses dados sejam enviados para o Adobe.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# `onBeforeEventSend`

A variável `onBeforeEventSend` O retorno de chamada permite registrar uma função JavaScript que pode alterar os dados enviados antes que esses dados sejam enviados para o Adobe. Esse retorno de chamada permite manipular a variável `xdm` ou `data` incluindo a capacidade de adicionar, editar ou remover elementos. Você também pode cancelar condicionalmente o envio de dados, como com o tráfego de bot do lado do cliente detectado.

>[!WARNING]
>
>Esse retorno de chamada permite o uso do código personalizado. Se qualquer código incluído no retorno de chamada acionar uma exceção não capturada, o processamento do evento será interrompido. Os dados não são enviados para o Adobe.

## Configure em antes do retorno de chamada do envio do evento usando a extensão de tag do SDK da Web {#tag-extension}

Selecione o **[!UICONTROL Fornecer código de retorno de chamada antes do envio do evento]** botão quando [configuração da extensão de tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Esse botão abre uma janela modal onde você pode inserir o código desejado.

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e, em seguida, clique em **[!UICONTROL Configurar]** no [!UICONTROL Adobe Experience Platform Web SDK] cartão.
1. Role para baixo até [!UICONTROL Coleta de dados] e selecione o botão **[!UICONTROL Fornecer código de retorno de chamada antes do envio do evento]**.
1. Esse botão abre uma janela modal com um editor de código. Insira o código desejado e clique em **[!UICONTROL Salvar]** para fechar a janela modal.
1. Clique em **[!UICONTROL Salvar]** em configurações de extensão, publique as alterações.

No editor de código, você tem acesso às seguintes variáveis:

* **`content.xdm`**: A variável [XDM](../sendevent/xdm.md) carga útil do evento.
* **`content.data`**: A variável [dados](../sendevent/data.md) carga útil do objeto para o evento.
* **`return true`**: saia imediatamente do retorno de chamada e envie dados para o Adobe com os valores atuais na `content` objeto.
* **`return false`**: saia imediatamente do retorno de chamada e interrompa o envio de dados para o Adobe.

Quaisquer variáveis definidas fora do `content` podem ser usados, mas não estão incluídos na carga útil enviada para o Adobe.

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
>Evite retornar `false` no primeiro evento em uma página. Retornando `false` no primeiro evento pode afetar negativamente a personalização.

## Configure em antes do evento enviar retorno de chamada usando a biblioteca JavaScript do SDK da Web {#library}

Registre o `onBeforeEventSend` retorno de chamada ao executar o `configure` comando. Você pode alterar a `content` Variable name para qualquer valor desejado alterando a variável de parâmetro dentro da função inline.

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
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
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: lastChanceLogic
});    
```
