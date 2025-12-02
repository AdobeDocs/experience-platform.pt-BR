---
title: sendEvent
description: Envie dados para o Adobe Experience Platform Edge Network.
exl-id: 83de368d-78d4-4e28-aadd-afaea1ca091d
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# `sendEvent`

O comando `sendEvent` é a principal maneira de enviar dados para a Adobe. Seu objeto de resposta é a maneira principal de recuperar conteúdo personalizado, identidades e destinos de público-alvo. Use o objeto [`xdm`](xdm.md) para enviar dados que mapeiam para o esquema do Adobe Experience Platform. Use o objeto [`data`](data.md) para enviar dados não XDM. A carga útil ao enviar dados para o Adobe tem um limite máximo de 64 KB.

Execute o comando `sendEvent` ao chamar a instância configurada do Web SDK. Chame o comando [`configure`](../configure/overview.md) antes de chamar o comando `sendEvent`.

```js
alloy("sendEvent", {
  data: dataObject,
  documentUnloading: false,
  edgeConfigOverrides: { datastreamId: "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  personalization: { decisionScopes: ["hero-banner"]},
  renderDecisions: true,
  type: "commerce.purchases",
  xdm: adobeDataLayer.getState(reference)
});
```

## Objeto de resposta

Se você decidir [manipular respostas](../command-responses.md) com este comando, as seguintes propriedades estarão disponíveis no objeto de resposta:

* **`propositions`**: Uma matriz de propostas retornadas pela Edge Network. As propostas que são renderizadas automaticamente incluem o sinalizador `renderAttempted` definido como `true`.
* **`inferences`**: uma matriz de objetos de inferência, que contém informações de aprendizado de máquina sobre este usuário.
* **`destinations`**: Uma matriz de objetos de destino retornada pela Edge Network.

## Enviar evento usando a extensão de tag do Web SDK

O equivalente da extensão de tag do Web SDK desse comando é a ação [**[!UICONTROL Send event]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields).
