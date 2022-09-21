---
keywords: Advertising Cloud; extensão da advertising cloud; destino da advertising cloud
title: Extensão do Adobe Advertising Cloud
description: A extensão Adobe Advertising Cloud é um destino de publicidade no Adobe Experience Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no Adobe Exchange.
exl-id: 3415a85f-5678-4f5b-b7cf-e185a66d084f
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 3%

---

# Extensão do Adobe Advertising Cloud {#adobe-advertising-cloud-extension}

## Visão geral {#overview}

Este é o [!DNL Advertising Cloud] extensão da implementação [!DNL Advertising Cloud] tags de conversão e segmento para a DSP e a Pesquisa (no momento, o DCO não é compatível).

O Adobe Advertising Cloud é uma extensão de publicidade no Adobe Experience Platform.

Esse destino é uma extensão de tag. Para obter mais informações sobre como as extensões de tags funcionam na Platform, consulte o [visão geral das extensões de tag](../launch-extensions/overview.md).

![Extensão do Adobe Advertising Cloud](../../assets/catalog/advertising/adobe-advertising-cloud/catalog.png)

## Pré-requisitos {#prerequisites}

Essa extensão está disponível no catálogo de Destinos para todos os clientes que compraram a Platform.

Para usar essa extensão, você precisa acessar tags no Platform. Tags são oferecidas aos clientes da Adobe Experience Cloud como um recurso incluso com valor agregado. Entre em contato com o administrador da organização para obter acesso aos recursos de Coleta de dados na interface do usuário e solicitar que ele conceda a você o **[!UICONTROL manage_properties]** para poder instalar extensões.

## Instalar extensão {#install-extension}

Para instalar a extensão Adobe Advertising Cloud:

No [Interface da plataforma](https://platform.adobe.com/), vá para **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.

Selecione a extensão do catálogo ou use a barra de pesquisa.

Clique no destino para realçá-lo e selecione **[!UICONTROL Configurar]** no painel direito. Se a variável **[!UICONTROL Configurar]** o controle está esmaecido, você está perdendo a variável **[!UICONTROL manage_properties]** permissão. Consulte [Pré-requisitos](#prerequisites).

Selecione a propriedade da tag na qual deseja instalar a extensão. Você também tem a opção de criar uma nova propriedade. Uma propriedade é uma coleção de regras, elementos de dados, extensões configuradas, ambientes e bibliotecas. Saiba mais sobre as propriedades na [documentação das tags](../../../tags/ui/administration/companies-and-properties.md).

O fluxo de trabalho direciona você para a interface do usuário da coleta de dados para concluir a instalação.

Você também pode instalar a extensão diretamente no [Interface do usuário da coleção de dados](https://experience.adobe.com/#/data-collection/). Consulte o guia sobre [adição de uma nova extensão](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) para obter mais informações.

## Como usar a extensão {#how-to-use}

Depois de instalar a extensão, você pode iniciar a configuração das regras. Na interface do usuário da Coleta de dados, você pode configurar regras para as extensões instaladas para enviar dados do evento para o destino da extensão somente em determinadas situações. Para obter mais informações sobre como configurar regras para suas extensões, consulte a visão geral em [regras](../../../tags/ui/managing-resources/rules.md) na documentação das tags.

## Configurar, atualizar e excluir extensão {#configure-upgrade-delete}

É possível configurar, atualizar e excluir extensões na interface do usuário da Coleta de dados.

>[!TIP]
>
>Se a extensão já estiver instalada em uma de suas propriedades, a interface do usuário ainda será exibida **[!UICONTROL Instalar]** para a extensão do . Inicie o fluxo de trabalho de instalação conforme descrito em [Instalar extensão](#install-extension) para configurar ou excluir sua extensão.

Para atualizar sua extensão, consulte o guia no [processo de atualização de extensão](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) na documentação das tags.
