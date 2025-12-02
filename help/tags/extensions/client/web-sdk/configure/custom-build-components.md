---
title: Componentes de build personalizados
description: Crie uma build personalizada do Web SDK que desative os recursos para diminuir o tamanho da build.
source-git-commit: d6aea91d6989775ff5b6038b216ed2518f4a7d98
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# Componentes de build personalizados

A biblioteca do Web SDK inclui vários módulos para vários recursos, como personalização, identidade, rastreamento de links e muito mais. Dependendo dos casos de uso, talvez você só precise de recursos específicos em vez da biblioteca inteira. A desativação dos componentes de build permite usar apenas os módulos necessários, reduzindo o tamanho da biblioteca e melhorando o desempenho.

Quando você desativa um componente, não pode mais editar as configurações desse componente. Se você usar várias instâncias do Web SDK, os componentes de build selecionados serão aplicados a todas as instâncias.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensions]** e selecione **[!UICONTROL Configure]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Expanda a opção **[!UICONTROL Custom build components]** na parte superior.

>[!WARNING]
>
>A modificação incorreta dessas configurações pode causar resultados indesejados, incluindo perda de dados. Teste sua implementação minuciosamente em um ambiente de desenvolvimento antes de publicar essas alterações na produção.

O Adobe oferece a capacidade de desativar os seguintes componentes de build do Web SDK:

| Componente de build | Descrição | Recursos dependentes |
| --- | --- | --- |
| **[!UICONTROL Activity collector]** | Permite a coleta automática de links e o rastreamento Activity Map. | |
| **[!UICONTROL Advertising]** | Permite a integração do Adobe Advertising com o Customer Journey Analytics. | |
| **[!UICONTROL Audiences]** | Oferece suporte à integração com o Adobe Audience Manager, como sincronizações de ID. | |
| **[!UICONTROL Consent]** | Permite usar os recursos de consentimento. | [[!UICONTROL Set consent]](../actions/set-consent.md) ação |
| **[!UICONTROL Event merge]** | Obsoleto. | [[!UICONTROL Event merge ID]](../data-element-types.md) elemento de dados (desaprovado) <br>[[!UICONTROL Reset event merge ID]](../actions/reset-event-merge-id.md) ação (desaprovado) |
| **[!UICONTROL Media Analytics bridge]** | Oferece suporte à integração com o Media Analytics herdado. | [[!UICONTROL Get media analytics tracker]](../actions/get-media-analytics-tracker.md) ação |
| **[!UICONTROL Personalization]** | Oferece suporte a integrações com a Adobe Target e a Adobe Journey Optimizer. | [[!UICONTROL Apply propositions]](../actions/apply-propositions.md) ação |
| **[!UICONTROL Push notifications]** | Habilita notificações por push da Web para o Adobe Journey Optimizer. | [[!UICONTROL Send push subscription]](../actions/send-push-subscription.md) ação |
| **[!UICONTROL Rules engine]** | Ativa a decisão do dispositivo com o Adobe Journey Optimizer. | [[!UICONTROL Evaluate rulsets]](../actions/evaluate-rulesets.md) ação<br> [[!UICONTROL Subscribe ruleset items]](../event-types.md#subscribe-ruleset-items) evento |
| **[!UICONTROL Streaming media]** | Oferece suporte à integração com a coleção de mídia de transmissão. | [[!UICONTROL Send media event]](../actions/send-media-event.md) ação |
