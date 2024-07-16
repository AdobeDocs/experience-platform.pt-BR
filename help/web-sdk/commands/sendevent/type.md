---
title: eventType
description: Defina o tipo de evento para uma chamada sendEvent.
exl-id: 9d0fae3b-827a-4084-b460-b755e478e06a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# `eventType`

A propriedade `eventType` permite definir o tipo de evento enviado usando o SDK da Web. Este campo preenche o campo `xdm.eventType`. É importante quando você deseja diferenciar os tipos de evento que envia para o Adobe.

O Adobe fornece alguns tipos de evento predefinidos que você pode usar. Consulte [Valores disponíveis para `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) no guia do usuário XDM para obter uma lista completa de valores predefinidos. Você também pode usar seus próprios valores, se preferir.

Se você definir `type` aqui e `xdm.eventType` no objeto [`xdm`](xdm.md), o valor neste campo terá prioridade.

## Configurar tipo de evento usando a extensão de tag do SDK da Web

Definir o campo suspenso **[!UICONTROL Tipo]** dentro das ações de uma regra de marca.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Regras]** e selecione a regra desejada.
1. Em [!UICONTROL Ações], selecione uma ação existente ou crie uma ação.
1. Defina o campo suspenso [!UICONTROL Extensão] como **[!UICONTROL Adobe Experience Platform Web SDK]** e defina o [!UICONTROL Tipo de Ação] como **[!UICONTROL Enviar evento]**.
1. Use a lista suspensa no campo **[!UICONTROL Tipo]** ou insira seu próprio valor.
1. Clique em **[!UICONTROL Manter alterações]** e execute o fluxo de trabalho de publicação.

## Configurar tipo de evento usando a biblioteca JavaScript do SDK da Web

Defina a propriedade de cadeia de caracteres `eventType` ao executar o comando `sendEvent`.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```
