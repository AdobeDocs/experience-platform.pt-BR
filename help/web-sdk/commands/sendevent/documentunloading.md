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

A propriedade `documentUnloading` permite usar o método [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) da JavaScript para enviar dados para o Adobe. Se uma solicitação típica demorar muito, o navegador poderá cancelar a solicitação. Você pode instruir o SDK da Web a usar `sendBeacon` para que a solicitação seja executada em segundo plano depois que você sair da página. Habilite essa propriedade para ajudar a impedir que solicitações de dados sejam canceladas pelo navegador durante o descarregamento.

Vários navegadores impõem um limite de 64 KB à quantidade de dados que podem ser enviados com `sendBeacon` de uma vez. Se o navegador rejeitar o evento porque a carga é muito grande, o SDK da Web voltará a usar seu método de transporte normal.

## Configurar o descarregamento de documentos usando a extensão de tag do SDK da Web

Habilitar o **[!UICONTROL Documento descarregará a caixa de seleção]** nas ações de uma regra de marca.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Regras]** e selecione a regra desejada.
1. Em [!UICONTROL Ações], selecione uma ação existente ou crie uma ação.
1. Defina o campo suspenso [!UICONTROL Extensão] como **[!UICONTROL Adobe Experience Platform Web SDK]** e defina o [!UICONTROL Tipo de Ação] como **[!UICONTROL Enviar evento]**.
1. Habilitar o **[!UICONTROL Documento descarregará a caixa de seleção]** na seção [!UICONTROL Dados].
1. Clique em **[!UICONTROL Manter alterações]** e execute o fluxo de trabalho de publicação.

## Configurar o descarregamento de documentos usando a biblioteca JavaScript do SDK da Web

Defina o booleano `documentUnloading` ao executar o comando `sendEvent`. Seu valor padrão é `false`. Defina essa propriedade como `true` se desejar usar o método `sendBeacon` para enviar dados ao Adobe.

>[!IMPORTANT]
>
>Propriedade `documentUnloading` incompatível com propriedade [`renderDecisions`](renderdecisions.md). Você não deve definir ambas as propriedades como `true` simultaneamente.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```
