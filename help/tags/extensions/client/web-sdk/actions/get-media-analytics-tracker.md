---
title: Obter o rastreador do Media Analytics
description: Exporta a API de mídia herdada para um objeto de janela.
source-git-commit: c55e425f146e4afdb2314b432c9dc48391e02e63
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 0%

---

# Obter o Media Analytics Tracker

A ação **[!UICONTROL Get Media Analytics tracker]** é usada para obter a API do Media Analytics herdada. Ao configurar a ação e um nome de objeto é fornecido, a API herdada do Media Analytics é exportada para esse objeto de janela. Essa ação é útil para migrar do Media Analytics herdado para o Media Analytics de streaming.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Rules]** e selecione a regra desejada.
1. Em [!UICONTROL Actions], selecione uma ação existente ou crie uma ação.
1. Defina o campo suspenso [!UICONTROL Extension] como **[!UICONTROL Adobe Experience Platform Web SDK]** e defina [!UICONTROL Action type] como **[!UICONTROL Get Media Analytics tracker]**.

![Imagem da interface do usuário do Experience Platform mostrando o tipo de ação Obter Media Analytics Tracker.](../assets/get-media-analytics-tracker.png)

Essa ação contém um único campo que pode ser configurado:

* **[!UICONTROL Export the Media Legacy API to this window object]**: seleciona o objeto desejado para o qual exportar a API Media Legacy. Se nenhum for fornecido, a ação exportará a API para `window.Media`.
