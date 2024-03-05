---
title: renderDecision
description: Renderize conteúdo personalizado que esteja qualificado para renderização automática.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# `renderDecisions`

A variável `renderDecisions` permite forçar o SDK da Web a renderizar qualquer conteúdo personalizado que esteja qualificado para renderização automática.

## Renderizar conteúdo personalizado usando a extensão de tag do SDK da Web

Selecione o **[!UICONTROL Renderizar decisões de personalização visual]** nas ações de uma regra de tag.

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Regras]** e selecione a regra desejada.
1. Em [!UICONTROL Ações], selecione uma ação existente ou crie uma ação.
1. Defina o [!UICONTROL Extensão] campo suspenso até **[!UICONTROL Adobe Experience Platform Web SDK]** e defina o [!UICONTROL Tipo de ação] para **[!UICONTROL Enviar evento]**.
1. Role para baixo até [!UICONTROL Personalização] e selecione o **[!UICONTROL Renderizar decisões de personalização visual]** caixa de seleção
1. Clique em **[!UICONTROL Manter alterações]**, em seguida, execute o fluxo de trabalho de publicação.

## Renderize conteúdo personalizado usando a biblioteca JavaScript do SDK da Web

Defina o `renderDecisions` booleano ao executar o `sendEvent` comando. Se omitida, esse valor padrão de propriedade será `false`. Defina esta propriedade como `true` se você quiser renderizar automaticamente o conteúdo personalizado.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```
