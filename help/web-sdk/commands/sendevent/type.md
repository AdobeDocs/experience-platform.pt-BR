---
title: eventType
description: Defina o tipo de evento para uma chamada sendEvent.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# `eventType`

A variável `eventType` permite definir o tipo de evento enviado usando o SDK da Web. Esse campo preenche o `xdm.eventType` campo. É importante quando você deseja diferenciar os tipos de evento que envia para o Adobe.

O Adobe fornece alguns tipos de evento predefinidos que você pode usar. Consulte [Valores disponíveis para `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) no guia do usuário XDM para obter uma lista completa de valores predefinidos. Você também pode usar seus próprios valores, se preferir.

Se você definir ambos `type` aqui e `xdm.eventType` no [`xdm`](xdm.md) objeto, o valor neste campo tem prioridade.

## Configurar tipo de evento usando a extensão de tag do SDK da Web

Defina o **[!UICONTROL Tipo]** campo suspenso nas ações de uma regra de tag.

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Regras]** e selecione a regra desejada.
1. Em [!UICONTROL Ações], selecione uma ação existente ou crie uma ação.
1. Defina o [!UICONTROL Extensão] campo suspenso até **[!UICONTROL Adobe Experience Platform Web SDK]** e defina o [!UICONTROL Tipo de ação] para **[!UICONTROL Enviar evento]**.
1. Use a lista suspensa em **[!UICONTROL Tipo]** ou insira seu próprio valor.
1. Clique em **[!UICONTROL Manter alterações]**, em seguida, execute o fluxo de trabalho de publicação.

## Configure o tipo de evento usando a biblioteca JavaScript do SDK da Web

Defina o `eventType` propriedade de string ao executar o `sendEvent` comando.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```
