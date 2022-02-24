---
keywords: Experience Platform, home, tópicos populares, fontes, conectores, conectores de origem, campanha, serviços gerenciados da campanha
title: Criar uma conexão de origem do Adobe Campaign Managed Services usando a interface do usuário da plataforma
description: Saiba como conectar o Adobe Experience Platform ao Adobe Campaign Managed Services usando a interface do usuário da plataforma.
hide: true
hidefromtoc: true
source-git-commit: 57a34b10e40dee80638392477d49c21e107c491f
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 1%

---


# Criar uma conexão de origem do Adobe Campaign Managed Services usando a interface do usuário da plataforma

Este tutorial fornece etapas para criar um conector de origem para trazer seus dados do Adobe Campaign Managed Services para o Adobe Experience Platform.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../../../home.md): A Platform permite que os dados sejam assimilados de várias fontes, além de fornecer a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): A Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Conectar o Adobe Campaign Managed Services à plataforma

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Também é possível usar a barra de pesquisa para restringir as fontes exibidas.

Em **[!UICONTROL Aplicativos Adobe]** categoria , selecione **[!UICONTROL Adobe Campaign Managed Services]** e depois selecione **[!UICONTROL Adicionar dados]**.

### Selecionar dados {#select-data}

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_instance"
>title="Instância ACC"
>abstract="O nome do ambiente Adobe Campaign Classic que você deseja usar."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_mapping"
>title="Target mapping"
>abstract="Os target mappings são objetos técnicos usados pelo Campaign para entregar mensagens e contêm todas as configurações técnicas necessárias para enviar deliveries (endereços, números de telefone, indicadores de aceitação, identificadores adicionais...)."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_schema"
>title="Nome do esquema"
>abstract="O nome da entidade definida no banco de dados do Adobe Campaign."
>text="Learn more in documentation"

O [!UICONTROL Selecionar dados] será exibida, fornecendo uma interface para configurar os valores para o [!UICONTROL Instância do Adobe Campaign], [!UICONTROL Target mapping]e [!UICONTROL Nome do esquema].
