---
title: onBeforeLinkClickSend
description: Retorno de chamada que é executado antes do envio dos dados de rastreamento do link.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---

# `onBeforeLinkClickSend`

A variável `onBeforeLinkClickSend` O retorno de chamada permite registrar uma função JavaScript que pode alterar os dados de rastreamento de link enviados antes que esses dados sejam enviados para o Adobe. Esse retorno de chamada permite manipular a variável `xdm` ou `data` incluindo a capacidade de adicionar, editar ou remover elementos. Você também pode cancelar condicionalmente o envio de dados, como com o tráfego de bot do lado do cliente detectado. Ele é compatível com o SDK da Web 2.15.0 ou posterior.

Esse retorno de chamada só é executado quando [`clickCollectionEnabled`](clickcollectionenabled.md) está ativado. Se `clickCollectionEnabled` estiver desativado, esse retorno de chamada não será executado. Se ambos `onBeforeEventSend` e `onBeforeLinkClickSend` contêm funções registradas, a variável `onBeforeLinkClickSend` A função é executada primeiro. Quando a variável `onBeforeLinkClickSend` termina, a variável `onBeforeEventSend` A função é executada.

>[!WARNING]
>
>Esse retorno de chamada permite o uso do código personalizado. Se qualquer código incluído no retorno de chamada acionar uma exceção não capturada, o processamento do evento será interrompido. Os dados não são enviados para o Adobe.

## Ativado antes do link, clique em enviar retorno de chamada usando a extensão de tag do SDK da Web

Selecione o **[!UICONTROL Fornecer código de retorno de chamada antes do envio do evento de clique do link]** botão quando [configuração da extensão de tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Esse botão abre uma janela modal onde você pode inserir o código desejado.

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e, em seguida, clique em **[!UICONTROL Configurar]** no [!UICONTROL Adobe Experience Platform Web SDK] cartão.
1. Role para baixo até [!UICONTROL Coleta de dados] e marque a caixa de seleção **[!UICONTROL Ativar a coleta de dados de cliques]**.
1. Selecione o botão rotulado **[!UICONTROL Fornecer código de retorno de chamada antes do envio do evento de clique do link]**.
1. Esse botão abre uma janela modal com um editor de código. Insira o código desejado e clique em **[!UICONTROL Salvar]** para fechar a janela modal.
1. Clique em **[!UICONTROL Salvar]** em configurações de extensão, publique as alterações.

No editor de código, é possível adicionar, editar ou remover elementos no `content` objeto. Este objeto contém o conteúdo enviado para o Adobe. Não é necessário definir a variável `content` objeto ou envolva qualquer código dentro de uma função. Quaisquer variáveis definidas fora do `content` podem ser usados, mas não estão incluídos na carga útil enviada para o Adobe.

>[!TIP]
>
>Os objetos `content.xdm`, `content.data`, e `content.clickedElement` são sempre definidas neste contexto, portanto, não é necessário verificar se elas existem. Algumas variáveis nesses objetos dependem da implementação e da camada de dados. A Adobe recomenda verificar valores indefinidos nesses objetos para evitar erros de JavaScript.

Por exemplo, digamos que você deseje executar as seguintes ações:

* Modificar o URL da página atual
* Capturar o elemento clicado em um eVar do Adobe Analytics
* Altere o tipo de link de &quot;outro&quot; para &quot;download&quot;

O código equivalente na janela modal seria o seguinte:

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

Semelhante a [`onBeforeEventSend`](onbeforeeventsend.md), você pode `return true` para completar imediatamente a função, ou `return false` para cancelar imediatamente o envio de dados. Se você cancelar o envio de dados no `onBeforeLinkClickSend` quando ambos `onBeforeEventSend` e `onBeforeLinkClickSend` contêm funções registradas, a variável `onBeforeEventSend` A função não é executada.

## Ativado antes do link, clique em enviar retorno de chamada usando a biblioteca JavaScript do SDK da Web

Registre o `onBeforeLinkClickSend` retorno de chamada ao executar o `configure` comando. Você pode alterar a `content` Variable name para qualquer valor desejado alterando a variável de parâmetro dentro da função inline.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeLinkClickSend": function(content) {
    // Add, modify, or delete values
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
    
    // Return true to immediately complete the function
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to immediately cancel sending data
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
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeLinkClickSend": lastChanceLinkLogic
});    
```
