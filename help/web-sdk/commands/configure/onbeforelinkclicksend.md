---
title: onBeforeLinkClickSend
description: Retorno de chamada que é executado antes do envio dos dados de rastreamento do link.
exl-id: 8c73cb25-2648-4cf7-b160-3d06aecde9b4
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---


# `onBeforeLinkClickSend`

>[!IMPORTANT]
>
>Esse retorno de chamada está obsoleto. Em vez disso, use [`filterClickDetails`](clickcollection.md).

O retorno de chamada `onBeforeLinkClickSend` permite registrar uma função JavaScript que pode alterar os dados de rastreamento de link enviados antes que esses dados sejam enviados para o Adobe. Este retorno de chamada permite manipular o objeto `xdm` ou `data`, incluindo a capacidade de adicionar, editar ou remover elementos. Você também pode cancelar condicionalmente o envio de dados, como com o tráfego de bot do lado do cliente detectado. Ele é compatível com o SDK da Web 2.15.0 ou posterior.

Este retorno de chamada só é executado quando [`clickCollectionEnabled`](clickcollectionenabled.md) está habilitado e [`filterClickDetails`](clickcollection.md) não contém uma função registrada. Se `clickCollectionEnabled` estiver desabilitado ou se `filterClickDetails` contiver uma função registrada, esse retorno de chamada não será executado. Se `onBeforeEventSend` e `onBeforeLinkClickSend` contêm funções registradas, `onBeforeLinkClickSend` é executado primeiro.

>[!WARNING]
>
>Esse retorno de chamada permite o uso do código personalizado. Se qualquer código incluído no retorno de chamada acionar uma exceção não capturada, o processamento do evento será interrompido. Os dados não são enviados para o Adobe.

## Configurar no antes do link e clicar em enviar retorno de chamada usando a extensão de tag do SDK da Web {#tag-extension}

Selecione o botão **[!UICONTROL Fornecer antes do link para enviar código de retorno de chamada]** ao [configurar a extensão de marca](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Esse botão abre uma janela modal onde você pode inserir o código desejado.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e clique em **[!UICONTROL Configurar]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Role para baixo até a seção [!UICONTROL Coleção de dados] e marque a caixa de seleção **[!UICONTROL Habilitar coleta de dados de cliques]**.
1. Selecione o botão rotulado **[!UICONTROL Fornecer antes do link e clicar em enviar código de retorno de chamada]**.
1. Esse botão abre uma janela modal com um editor de código. Insira o código desejado e clique em **[!UICONTROL Salvar]** para fechar a janela modal.
1. Clique em **[!UICONTROL Salvar]** nas configurações de extensão e publique suas alterações.

No editor de código, você tem acesso às seguintes variáveis:

* **`content.clickedElement`**: o elemento DOM que foi clicado.
* **`content.xdm`**: a carga XDM para o evento.
* **`content.data`**: a carga do objeto de dados para o evento.
* **`return true`**: Saia imediatamente do retorno de chamada com os valores de variável atuais. O retorno de chamada `onBeforeEventSend` será executado se contiver uma função registrada.
* **`return false`**: Saia imediatamente do retorno de chamada e interrompa o envio de dados para o Adobe. O retorno de chamada `onBeforeEventSend` não é executado.

Qualquer variável definida fora de `content` pode ser usada, mas não está incluída na carga enviada para o Adobe.

```js
// Set an already existing value to something else
content.xdm.web.webPageDetails.URL = "https://example.com/current.html";

// Use nullish coalescing assignments to create objects if they don't yet exist, preventing undefined errors. 
// Can be omitted if you are certain that the object is already defined
content.xdm._experience ??= {};
content.xdm._experience.analytics ??= {};
content.xdm._experience.analytics.customDimensions ??= {};
content.xdm._experience.analytics.customDimensions.eVars ??= {};

// Then set the property to the clicked element
content.xdm._experience.analytics.customDimensions.eVars.eVar1 = content.clickedElement;

// Use optional chaining to check if each object is defined, preventing undefined errors
if(content.xdm.web?.webInteraction?.type === "other") content.xdm.web.webInteraction.type = "download";
```

De modo semelhante a [`onBeforeEventSend`](onbeforeeventsend.md), você pode `return true` para concluir a função imediatamente ou `return false` para suspender o envio de dados para o Adobe. Se você anular o envio de dados em `onBeforeLinkClickSend` quando `onBeforeEventSend` e `onBeforeLinkClickSend` contiverem funções registradas, a função `onBeforeEventSend` não será executada.

## Configurar no antes do link e clicar em enviar retorno de chamada usando a biblioteca JavaScript do SDK da Web {#library}

Registre o retorno de chamada `onBeforeLinkClickSend` ao executar o comando `configure`. Você pode alterar o nome da variável `content` para qualquer valor desejado alterando a variável de parâmetro dentro da função embutida.

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeLinkClickSend: function(content) {
    // Add, modify, or delete values
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
    
    // Return true to complete the function immediately
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to cancel sending data immediately
    if(myBotDetector.isABot()){
      return false;
    }
  }
});
```

Você também pode registrar sua própria função em vez de uma função em linha.

```js
function lastChanceLinkLogic(content) {
  content.xdm.application ??= {};
  content.xdm.application.name = "App name";
}

alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeLinkClickSend: lastChanceLinkLogic
});    
```
