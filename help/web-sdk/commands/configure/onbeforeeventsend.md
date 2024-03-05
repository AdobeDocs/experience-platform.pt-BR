---
title: onBeforeEventSend
description: Retorno de chamada que é executado antes do envio dos dados.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# `onBeforeEventSend`

A variável `onBeforeEventSend` O retorno de chamada permite registrar uma função JavaScript que pode alterar os dados enviados antes que esses dados sejam enviados para o Adobe. Esse retorno de chamada permite manipular a variável `xdm` ou `data` incluindo a capacidade de adicionar, editar ou remover elementos. Você também pode cancelar condicionalmente o envio de dados, como com o tráfego de bot do lado do cliente detectado.

>[!WARNING]
>
>Esse retorno de chamada permite o uso do código personalizado. Se qualquer código incluído no retorno de chamada acionar uma exceção não capturada, o processamento do evento será interrompido. Os dados não são enviados para o Adobe.

## Ativado antes do envio do evento usando a extensão de tag do SDK da Web

Selecione o **[!UICONTROL Fornecer código de retorno de chamada antes do envio do evento]** botão quando [configuração da extensão de tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Esse botão abre uma janela modal onde você pode inserir o código desejado.

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e, em seguida, clique em **[!UICONTROL Configurar]** no [!UICONTROL Adobe Experience Platform Web SDK] cartão.
1. Role para baixo até [!UICONTROL Coleta de dados] e selecione o botão **[!UICONTROL Fornecer código de retorno de chamada antes do envio do evento]**.
1. Esse botão abre uma janela modal com um editor de código. Insira o código desejado e clique em **[!UICONTROL Salvar]** para fechar a janela modal.
1. Clique em **[!UICONTROL Salvar]** em configurações de extensão, publique as alterações.

No editor de código, é possível adicionar, editar ou remover elementos no `content` objeto. Este objeto contém o conteúdo enviado para o Adobe. Não é necessário definir a variável `content` objeto ou envolva qualquer código dentro de uma função. Quaisquer variáveis definidas fora do `content` podem ser usados, mas não estão incluídos na carga útil enviada para o Adobe.

>[!TIP]
>
>Os objetos `content.xdm` e `content.data` são sempre definidas neste contexto, portanto, não é necessário verificar se elas existem. Algumas variáveis nesses objetos dependem da implementação e da camada de dados. A Adobe recomenda verificar valores indefinidos nesses objetos para evitar erros de JavaScript.

Por exemplo, se você deseja:

* Adicionar o elemento XDM `xdm.commerce.order.purchaseID`
* Forçar todos os caracteres em `xdm.marketing.trackingCode` para minúsculas
* Excluir `xdm.environment.operatingSystemVersion`
* Se um tipo de evento for um clique em links, enviar dados imediatamente, independentemente do código abaixo dele
* Cancelamento do envio de dados para o Adobe se um bot for detectado

O código equivalente na janela modal seria o seguinte:

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

>[!NOTE]
>
>Evite retornar `false` no primeiro evento em uma página. Retornando `false` no primeiro evento pode afetar negativamente a personalização.

## Ativado antes do evento enviar retorno de chamada usando a biblioteca JavaScript do SDK da Web

Registre o `onBeforeEventSend` retorno de chamada ao executar o `configure` comando. Você pode alterar a `content` Variable name para qualquer valor desejado alterando a variável de parâmetro dentro da função inline.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(content) {
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
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": lastChanceLogic
});    
```
