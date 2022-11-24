---
Keywords: ECID;ecid
title: Extensão do Experience Cloud ID Service
description: A extensão do Serviço de ID do Experience Cloud é um destino de personalização no Adobe Experience Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no Adobe Exchange.
exl-id: 4cc49c14-66ec-43e0-a106-70d9c3646d87
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 4%

---

# [!DNL Experience Cloud] Extensão do serviço de ID {#adobe-ecid-extension}

## Visão geral {#overview}

Essa extensão implementa o [!DNL Experience Cloud] Serviço de ID, que identifica visitantes em todos os [!DNL Experience Cloud] soluções.

[!DNL Experience Cloud] O Serviço de ID é uma extensão de personalização no Adobe Experience Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte o [Página de extensão do serviço de ID do Experience Cloud](../../../tags/extensions/client/id-service/overview.md) na documentação das tags.

Esse destino é uma extensão de tag. Para obter mais informações sobre como as extensões de tags funcionam na Platform, consulte o [visão geral das extensões de tag](../launch-extensions/overview.md).

![Extensão Adobe ECID](../../assets/catalog/personalization/adobe-ecid/catalog.png)

## Pré-requisitos {#prerequisites}

Essa extensão está disponível no catálogo de Destinos para todos os clientes que compraram a Platform.

Para usar essa extensão, você precisa acessar tags no Platform. Tags são oferecidas aos clientes da Adobe Experience Cloud como um recurso incluso com valor agregado. Entre em contato com o administrador da organização para obter acesso à interface do usuário da coleta de dados e solicitar que ela conceda a você a **[!UICONTROL manage_properties]** para poder instalar extensões.

## Instalar extensão {#install-extension}

Para instalar o [!DNL Experience Cloud] Extensão do serviço de ID:

No [Interface da plataforma](https://platform.adobe.com/), vá para **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.

Selecione a extensão do catálogo ou use a barra de pesquisa.

Clique no destino para realçá-lo e selecione **[!UICONTROL Configurar]** no painel direito. Se a variável **[!UICONTROL Configurar]** o controle está esmaecido, você está perdendo a variável **[!UICONTROL manage_properties]** permissão. Consulte [Pré-requisitos](#prerequisites).

Selecione a propriedade da tag na qual deseja instalar a extensão. Você também tem a opção de criar uma nova propriedade. Uma propriedade é uma coleção de regras, elementos de dados, extensões configuradas, ambientes e bibliotecas. Saiba mais sobre as propriedades na [documentação das tags](../../../tags/ui/administration/companies-and-properties.md).

O fluxo de trabalho direciona você para a interface do usuário da coleta de dados para concluir a instalação.

Para obter informações sobre as opções de configuração de extensão e o suporte de instalação, consulte o [Página de extensão do serviço de ID do Experience Cloud](../../../tags/extensions/client/id-service/overview.md) na documentação das tags.

Você também pode instalar a extensão diretamente no [Interface do usuário da coleção de dados](https://experience.adobe.com/#/data-collection/). Consulte o guia sobre [adição de uma nova extensão](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) para obter mais informações.

## Como usar a extensão {#how-to-use}

Depois de instalar a extensão, você pode iniciar a configuração das regras. Na interface do usuário da Coleta de dados, você pode configurar regras para as extensões instaladas para enviar dados do evento para o destino da extensão somente em determinadas situações. Para obter mais informações sobre como configurar regras para suas extensões, consulte a visão geral em [regras](../../../tags/ui/managing-resources/rules.md) na documentação das tags.

## Configurar, atualizar e excluir extensão {#configure-upgrade-delete}

É possível configurar, atualizar e excluir extensões na interface do usuário da Coleta de dados.

>[!TIP]
>
>Se a extensão já estiver instalada em uma de suas propriedades, a interface do usuário ainda será exibida **[!UICONTROL Instalar]** para a extensão do . Inicie o fluxo de trabalho de instalação conforme descrito em [Instalar extensão](#install-extension) para configurar ou excluir sua extensão.

Para atualizar sua extensão, consulte o guia no [processo de atualização de extensão](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) na documentação das tags.
