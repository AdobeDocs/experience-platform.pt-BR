---
title: eventType
description: Defina o tipo de evento para uma chamada sendEvent.
exl-id: 9d0fae3b-827a-4084-b460-b755e478e06a
source-git-commit: f988d7665a40b589ca281d439b6fca508f23cd03
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# `eventType`

A propriedade `eventType` permite definir o tipo de evento enviado usando o Web SDK. Este campo preenche o campo `xdm.eventType`. Ela é importante quando você deseja diferenciar os tipos de evento enviados para o Adobe.

O Adobe fornece alguns tipos de evento predefinidos que você pode usar. Consulte [Valores disponíveis para `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) no guia do usuário XDM para obter uma lista completa de valores predefinidos. Você também pode usar seus próprios valores, se preferir.

Se você definir `type` aqui e `xdm.eventType` no objeto [`xdm`](xdm.md), o valor neste campo terá prioridade.

Defina a propriedade de cadeia de caracteres `eventType` ao executar o comando `sendEvent`.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```

## Tipo de evento usando a extensão de tag do Web SDK

O equivalente da extensão de marca Web SDK dessa propriedade é o menu suspenso [**[!UICONTROL Type]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields) ao configurar uma ação &#39;[!UICONTROL Send event]&#39;.
