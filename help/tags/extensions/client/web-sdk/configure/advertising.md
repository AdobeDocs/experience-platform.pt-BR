---
title: Definições de configuração do Adobe Advertising
description: Ativar ou desativar a funcionalidade da plataforma do lado da demanda.
source-git-commit: 526cb473a6288f367db9cb00c0277cce7543cd57
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Definições de configuração do Adobe Advertising

>[!AVAILABILITY]
>
>O Adobe Advertising para o Web SDK está atualmente em **beta**. A funcionalidade e a documentação estão sujeitas a alterações.

A seção **[!UICONTROL Adobe Advertising]** permite habilitar ou desabilitar a funcionalidade da Plataforma de Demanda (DSP), se usada na implementação. Você só precisará definir esse campo se sua implementação usar uma DSP.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensions]** e selecione **[!UICONTROL Configure]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Role até a seção **[!UICONTROL Adobe Advertising]**.

Atualmente, há uma opção disponível.

## [!UICONTROL Adobe Advertising DSP]

Um menu suspenso que ativa ou desativa a funcionalidade DSP para o Adobe Advertising.

* **[!UICONTROL Enabled]**: Habilita o rastreamento de view-through.
* **[!UICONTROL Disabled]**: Desabilita o rastreamento de view-through.

Quando ativadas, as seguintes configurações estão disponíveis:

* **[!UICONTROL Advertisers]**: os anunciantes para os quais habilitar o rastreamento de view-through.
* **[!UICONTROL ID5 partner ID]**: Opcional. ID do parceiro ID5 da sua organização. Essa configuração permite que o Web SDK colete IDs universais ID5.
* **[!UICONTROL RampID JavaScript path]**: Opcional. O caminho para o código JavaScript [!DNL LiveRamp RampID] da sua organização (`ats.js`).  Esta configuração permite que o Web SDK colete [!DNL RampID] IDs universais.
