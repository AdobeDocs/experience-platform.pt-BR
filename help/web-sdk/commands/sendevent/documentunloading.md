---
title: documentUnloading
description: Use a API sendBeacon do JavaScript para enviar dados ao Adobe.
exl-id: 7683c0c4-ae2e-46ec-8471-628a10e17afc
source-git-commit: f12d222e81a39a26bd71ab4bede05aa992889605
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# `documentUnloading`

A variável `documentUnloading` permite usar a propriedade do JavaScript [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) método para enviar dados para o Adobe. Se uma solicitação típica demorar muito, o navegador poderá cancelar a solicitação. Você pode instruir o SDK da Web a usar o `sendBeacon` para que a solicitação seja executada em segundo plano depois que você sair da página. Habilite essa propriedade para ajudar a impedir que solicitações de dados sejam canceladas pelo navegador durante o descarregamento.

Vários navegadores impõem um limite de 64 KB à quantidade de dados que podem ser enviados com `sendBeacon` de uma só vez. Se o navegador rejeitar o evento porque a carga é muito grande, o SDK da Web voltará a usar seu método de transporte normal.

## Configurar o descarregamento de documentos usando a extensão de tag do SDK da Web

Ativar o **[!UICONTROL O documento será descarregado]** nas ações de uma regra de tag.

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Regras]** e selecione a regra desejada.
1. Em [!UICONTROL Ações], selecione uma ação existente ou crie uma ação.
1. Defina o [!UICONTROL Extensão] campo suspenso até **[!UICONTROL Adobe Experience Platform Web SDK]** e defina o [!UICONTROL Tipo de ação] para **[!UICONTROL Enviar evento]**.
1. Ativar o **[!UICONTROL O documento será descarregado]** caixa de seleção na caixa [!UICONTROL Dados] seção.
1. Clique em **[!UICONTROL Manter alterações]**, em seguida, execute o fluxo de trabalho de publicação.

## Configure o descarregamento de documentos usando a biblioteca JavaScript do SDK da Web

Defina o `documentUnloading` booleano ao executar o `sendEvent` comando. Seu valor padrão é `false`. Defina esta propriedade como `true` se quiser usar o `sendBeacon` método para enviar dados para o Adobe.

>[!IMPORTANT]
>
>A variável `documentUnloading` propriedade é incompatível com o [`renderDecisions`](renderdecisions.md) propriedade. Você não deve definir as duas propriedades como `true` simultaneamente.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```
