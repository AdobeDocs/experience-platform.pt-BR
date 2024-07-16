---
title: renderDecision
description: Renderize conteúdo personalizado que esteja qualificado para renderização automática.
exl-id: 6f7a3531-c2b6-4e90-a7ad-9f0fe4dc39e9
source-git-commit: f12d222e81a39a26bd71ab4bede05aa992889605
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# `renderDecisions`

A propriedade `renderDecisions` permite forçar o SDK da Web a renderizar qualquer conteúdo personalizado que esteja qualificado para renderização automática.

## Renderizar conteúdo personalizado usando a extensão de tag do SDK da Web

Marque a caixa de seleção **[!UICONTROL Renderizar decisões de personalização visual]** nas ações de uma regra de marca.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Regras]** e selecione a regra desejada.
1. Em [!UICONTROL Ações], selecione uma ação existente ou crie uma ação.
1. Defina o campo suspenso [!UICONTROL Extensão] como **[!UICONTROL Adobe Experience Platform Web SDK]** e defina o [!UICONTROL Tipo de Ação] como **[!UICONTROL Enviar evento]**.
1. Role para baixo até a seção [!UICONTROL Personalization] e marque a caixa de seleção **[!UICONTROL Renderizar decisões de personalização visual]**.
1. Clique em **[!UICONTROL Manter alterações]** e execute o fluxo de trabalho de publicação.

## Renderizar conteúdo personalizado usando a biblioteca JavaScript do SDK da Web

Defina o booleano `renderDecisions` ao executar o comando `sendEvent`. Se omitida, essa propriedade assumirá `false` como padrão. Defina essa propriedade como `true` se desejar renderizar automaticamente o conteúdo personalizado.

>[!IMPORTANT]
>
>Propriedade `renderDecisions` incompatível com propriedade [`documentUnloading`](documentunloading.md). Você não deve definir ambas as propriedades como `true` simultaneamente.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```
