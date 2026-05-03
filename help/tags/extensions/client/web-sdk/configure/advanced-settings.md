---
title: Configurações avançadas
description: Defina as configurações avançadas para a extensão de tag do Web SDK.
exl-id: d830a210-77ab-4823-b5fa-c1194a01bea3
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 21%

---

# Configurações avançadas {#advanced}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_advanced"
>title="Configurações avançadas"
>abstract="Configurações avançadas. A Adobe recomenda manter as opções como estão para a maioria das implementações."

Esta seção de configuração permite-lhe alterar as opções avançadas. A Adobe recomenda manter as opções como estão para a maioria das implementações.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensions]** e selecione **[!UICONTROL Configure]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Role até a seção **[!UICONTROL Advanced Settings]**.

![Imagem mostrando as configurações avançadas usando a página de extensão de marca do Web SDK](../assets/advanced-settings.png)

Atualmente, há uma opção disponível.

## [!UICONTROL Edge base path]

Use este campo para alterar o caminho base usado para interagir com a Edge Network. A Adobe pode solicitar que você altere este campo se participar de determinados testes alfa ou beta; caso contrário, a Adobe recomenda deixá-lo com o valor padrão de `ee`.

Este campo é o equivalente da tag [`edgeBasePath`](/help/collection/js/commands/configure/edgebasepath.md) ao configurar a biblioteca JavaScript.
