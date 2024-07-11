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
>Esse retorno de chamada está obsoleto. Uso [`filterClickDetails`](clickcollection.md) em vez disso.

A variável `onBeforeLinkClickSend` O retorno de chamada permite registrar uma função do JavaScript que pode alterar os dados de rastreamento de link enviados antes que esses dados sejam enviados para o Adobe. Esse retorno de chamada permite manipular a variável `xdm` ou `data` incluindo a capacidade de adicionar, editar ou remover elementos. Você também pode cancelar condicionalmente o envio de dados, como com o tráfego de bot do lado do cliente detectado. Ele é compatível com o SDK da Web 2.15.0 ou posterior.

Esse retorno de chamada só é executado quando [`clickCollectionEnabled`](clickcollectionenabled.md) está ativado e [`filterClickDetails`](clickcollection.md) não contém uma função registrada. Se `clickCollectionEnabled` está desativado ou se `filterClickDetails` contém uma função registrada, portanto, esse retorno de chamada não é executado. Se `onBeforeEventSend` e `onBeforeLinkClickSend` ambos contêm funções registradas, `onBeforeLinkClickSend` é executado primeiro.

>[!WARNING]
>
>Esse retorno de chamada permite o uso do código personalizado. Se qualquer código incluído no retorno de chamada acionar uma exceção não capturada, o processamento do evento será interrompido. Os dados não são enviados para o Adobe.

## Configurar no antes do link e clicar em enviar retorno de chamada usando a extensão de tag do SDK da Web {#tag-extension}

Selecione o **[!UICONTROL Fornecer código de retorno de chamada antes do envio do evento de clique do link]** botão quando [configuração da extensão de tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Esse botão abre uma janela modal onde você pode inserir o código desejado.

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e, em seguida, clique em **[!UICONTROL Configurar]** no [!UICONTROL Adobe Experience Platform Web SDK] cartão.
1. Role para baixo até [!UICONTROL Coleta de dados] e marque a caixa de seleção **[!UICONTROL Ativar a coleta de dados de cliques]**.
1. Selecione o botão rotulado **[!UICONTROL Fornecer código de retorno de chamada antes do envio do evento de clique do link]**.
1. Esse botão abre uma janela modal com um editor de código. Insira o código desejado e clique em **[!UICONTROL Salvar]** para fechar a janela modal.
1. Clique em **[!UICONTROL Salvar]** em configurações de extensão, publique as alterações.

No editor de código, você tem acesso às seguintes variáveis:

* **`content.clickedElement`**: o elemento DOM que foi clicado.
* **`content.xdm`**: a carga XDM do evento.
* **`content.data`**: a carga do objeto de dados para o evento.
* **`return true`**: sai imediatamente do retorno de chamada com os valores de variável atuais. A variável `onBeforeEventSend` O retorno de chamada será executado se contiver uma função registrada.
* **`return false`**: saia imediatamente do retorno de chamada e interrompa o envio de dados para o Adobe. A variável `onBeforeEventSend` O retorno de chamada não é executado.

Quaisquer variáveis definidas fora do `content` podem ser usados, mas não estão incluídos na carga útil enviada para o Adobe.

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

Semelhante a [`onBeforeEventSend`](onbeforeeventsend.md), você pode `return true` para completar a função imediatamente, ou `return false` para interromper o envio de dados para o Adobe. Se você suspender o envio de dados no `onBeforeLinkClickSend` quando ambos `onBeforeEventSend` e `onBeforeLinkClickSend` contêm funções registradas, a variável `onBeforeEventSend` A função não é executada.

## Configurar no antes do link e clicar em enviar retorno de chamada usando a biblioteca JavaScript do SDK da Web {#library}

Registre o `onBeforeLinkClickSend` retorno de chamada ao executar o `configure` comando. Você pode alterar a `content` Variable name para qualquer valor desejado alterando a variável de parâmetro dentro da função inline.

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
