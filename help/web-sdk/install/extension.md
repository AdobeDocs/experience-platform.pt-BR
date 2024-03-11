---
title: Instale o SDK da Web usando a extensão de tag
description: Faça referência à biblioteca do SDK da Web usando a Coleção de dados da Adobe Experience Cloud.
exl-id: ba8348c9-f642-4230-9f7f-4496d4154d83
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Instale o SDK da Web usando a extensão de tag

O Adobe oferece uma extensão de tag dedicada para implementar e configurar o SDK da Web. Este método de implementação é o método principal recomendado pelo Adobe para implantar e manter o código de coleta de dados.

Depois de conhecer o [pré-requisitos](overview.md), você pode implantar a extensão de tag do SDK da Web usando as seguintes etapas:

## Instalar a extensão em uma tag

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada ou crie uma.
1. Navegue até **[!UICONTROL Extensões]**, em seguida, selecione a **[!UICONTROL Catálogo]** guia.
1. Localize e instale o **[!UICONTROL Adobe Experience Platform Web SDK]** extensão.
1. Selecione a sandbox e o fluxo de dados apropriados para cada ambiente e clique em **[!UICONTROL Salvar]**.

Consulte a documentação sobre como [configurar a extensão de tag do SDK da Web](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) para obter mais informações.

## Publicar o código da tag no desenvolvimento

A extensão SDK da Web agora está instalada para essa tag. Agora você pode publicar o código da tag para uso em um ambiente de desenvolvimento.

1. Navegue até **[!UICONTROL Fluxo de publicação]** e selecione **[!UICONTROL Adicionar biblioteca]**.
1. Dê a essa biblioteca o nome que desejar, como &quot;Adicionar biblioteca SDK da Web&quot;. Defina o [!UICONTROL Ambiente] para &quot;Desenvolvimento&quot;.
1. Selecionar **[!UICONTROL Adicionar todos os recursos alterados]** e, em seguida, clique em **[!UICONTROL Salvar e criar no desenvolvimento]**.

## Instalar o código do carregador no site

Agora que o código da tag foi publicado, você pode adicionar o código do carregador de tag ao seu site.

1. Navegue até **[!UICONTROL Ambientes]**, em seguida, clique no ícone de Caixa ao lado de &quot;Desenvolvimento&quot; para abrir uma janela modal que contém instruções de instalação desse ambiente.
1. Copie o código incorporado e cole-o no `<head>` do seu site.

## Preencha sua implementação e publique na produção

Consulte a [Visão geral da extensão SDK da Web](../../tags/extensions/client/web-sdk/overview.md) para obter mais informações sobre a própria extensão e [Visão geral das tags](../../tags/home.md) para obter mais informações sobre como navegar na interface de tags.
