---
keywords: extensão do Audience Manager DIL;audience manager de destino;extensão dil
title: Extensão do Audience Manager DIL
description: A extensão do Audience Manager DIL é um destino da Plataforma de gerenciamento de dados (DMP) no Adobe Experience Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no Adobe Exchange.
exl-id: 7e1099de-0650-4ee2-b746-721afe194097
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 3%

---

# Extensão do Audience Manager DIL {#aam-dil-extension}

## Visão geral {#overview}

Esta é a extensão do Adobe Audience Manager Data Integration Library (implementação do lado do cliente). Observação: essa extensão não deve ser usada para o encaminhamento pelo lado do servidor (SSF) de dados do Adobe Analytics. Para SSF, use a extensão do Adobe Analytics. Importante: a partir da versão 8.0, o DIL tem uma dependência forte no [!DNL Experience Cloud] ID Service, versão 3.3 ou superior. Implemente o Serviço de ID do [!DNL Experience Cloud] e o DIL para obter recursos completos de integração de dados do [!DNL Audience Manager].

[!DNL Audience Manager] O DIL é uma extensão da Plataforma de Gerenciamento de Dados (DMP) no Adobe Experience Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a [página de extensão do Audience Manager](../../../tags/extensions/client/audience-manager/overview.md) na documentação de tags.

Esse destino é uma extensão de tag. Para obter mais informações sobre como as extensões funcionam na Experience Platform, consulte a [visão geral das extensões de tag](../launch-extensions/overview.md).

![Extensão do Audience Manager DIL](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Pré-requisitos {#prerequisites}

Esta extensão está disponível no catálogo [!DNL Destinations] para todos os clientes que compraram o Experience Platform.

Para usar essa extensão, você precisa acessar as tags na Adobe Experience Platform. As tags são oferecidas aos clientes do Adobe Experience Cloud como um recurso incluso de valor agregado. Entre em contato com o administrador da organização para obter acesso às tags e solicite a concessão da permissão **[!UICONTROL manage_properties]** para que você possa instalar extensões.

## Instalar extensão {#install-extension}

Para instalar a extensão do DIL [!DNL Audience Manager]:

Na [interface do Experience Platform](https://platform.adobe.com/), vá para **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.

Selecione a extensão no catálogo ou use a barra de pesquisa.

Clique no destino para realçá-lo e selecione **[!UICONTROL Configurar]** no painel direito. Se o controle **[!UICONTROL Configurar]** estiver esmaecido, você não terá a permissão **[!UICONTROL manage_properties]**. Consulte [Pré-requisitos](#prerequisites).

Selecione a propriedade na qual deseja instalar a extensão. Você também tem a opção de criar uma nova propriedade. Uma propriedade é uma coleção de regras, elementos de dados, extensões configuradas, ambientes e bibliotecas. Saiba mais sobre as propriedades na [documentação de tags](../../../tags/ui/administration/companies-and-properties.md#properties-page).

O fluxo de trabalho o orienta pelas etapas necessárias para concluir a instalação.

Para obter informações sobre as opções de configuração de extensão, consulte a [página de extensão do Audience Manager](../../../tags/extensions/client/audience-manager/overview.md) na documentação das tags.

Você também pode instalar a extensão diretamente na [Interface da Coleção de Dados](https://experience.adobe.com/#/data-collection/). Consulte o guia em [adicionando uma nova extensão](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) para obter mais informações.

## Como usar a extensão {#how-to-use}

Depois de instalar a extensão, você pode começar a configurar regras. Na interface da Coleção de dados, é possível configurar regras para as extensões instaladas para enviar dados do evento para o destino da extensão somente em determinadas situações. Para obter mais informações sobre como configurar regras para suas extensões, consulte a visão geral sobre [regras](../../../tags/ui/managing-resources/rules.md) na documentação de tags.

## Configurar, atualizar e excluir extensão {#configure-upgrade-delete}

É possível configurar, atualizar e excluir extensões na interface da coleção de dados.

>[!TIP]
>
>Se a extensão já estiver instalada em uma de suas propriedades, a interface ainda exibirá **[!UICONTROL Instalar]** para a extensão. Inicie o fluxo de trabalho de instalação conforme descrito em [Instalar extensão](#install-extension) para configurar ou excluir sua extensão.

Para atualizar sua extensão, consulte o manual no [processo de atualização da extensão](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) na documentação das tags.
