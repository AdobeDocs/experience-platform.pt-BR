---
title: Configurações avançadas
description: Defina as configurações avançadas para a extensão de tag do Web SDK.
source-git-commit: d6aea91d6989775ff5b6038b216ed2518f4a7d98
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# Configurações avançadas

Esta seção de configuração permite-lhe alterar as opções avançadas. A Adobe recomenda deixar essas opções como estão para a maioria das implementações.

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
