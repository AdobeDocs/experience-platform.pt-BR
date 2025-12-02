---
title: documentUnloading
description: Use a API sendBeacon do JavaScript para enviar dados ao Adobe.
exl-id: 7683c0c4-ae2e-46ec-8471-628a10e17afc
source-git-commit: a229cec4a53ab85d13590205a008612719019ebd
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# `documentUnloading`

A propriedade `documentUnloading` permite usar o método [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) do JavaScript para enviar dados para o Adobe. Se uma solicitação típica demorar muito, o navegador poderá cancelar a solicitação. Você pode instruir o Web SDK a usar `sendBeacon` para que a solicitação seja executada em segundo plano depois que você sair da página. Habilite essa propriedade para ajudar a impedir que solicitações de dados sejam canceladas pelo navegador durante o descarregamento.

Vários navegadores impõem um limite de 64 KB à quantidade de dados que podem ser enviados com `sendBeacon` de uma vez. Se o navegador rejeitar o evento porque a carga é muito grande, o Web SDK voltará a usar seu método de transporte normal. Mesmo que um determinado navegador permita cargas maiores, os servidores de coleta de dados da Adobe reduzem as cargas para 64 KB.

Defina o booleano `documentUnloading` ao executar o comando `sendEvent`. Seu valor padrão é `false`. Defina essa propriedade como `true` se desejar usar o método `sendBeacon` para enviar dados ao Adobe.

>[!IMPORTANT]
>
>Propriedade `documentUnloading` incompatível com propriedade [`renderDecisions`](renderdecisions.md). Evite definir ambas as propriedades como `true` simultaneamente.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```

## Descarregamento de documento usando a extensão de tag do Web SDK

A caixa de seleção **[!UICONTROL Document will unload]** está disponível ao configurar uma ação [**[!UICONTROL Send event]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields) ao usar a extensão de tag do Web SDK.
