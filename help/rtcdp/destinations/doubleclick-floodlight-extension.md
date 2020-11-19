---
keywords: DoubleClick Floodlight;doubleclick floodlight extension;doubleclick;floodlight
title: Extensão do DoubleClick Floodlight (Beta)
seo-title: Extensão do DoubleClick Floodlight (Beta)
description: A extensão DoubleClick Floodlight (Beta) é um destino de publicidade na Plataforma de dados do cliente em tempo real. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no Adobe Exchange.
seo-description: A extensão DoubleClick Floodlight (Beta) é um destino de publicidade na Plataforma de dados do cliente em tempo real. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no Adobe Exchange.
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 4%

---


# [!DNL DoubleClick Floodlight] Extensão (Beta)

## Visão geral {#overview}

Essa extensão permite a implantação rápida e fácil de [!DNL DoubleClick Floodlight] tags usando o formato tradicional de Floodlight (não a tag global do site). Observação: Esta extensão está em beta.

[!DNL DoubleClick Floodlight] (Beta) é uma extensão de publicidade na Plataforma de dados do cliente em tempo real. Para obter mais informações sobre a funcionalidade de extensão, consulte a documentação de [!DNL Google] suporte do [DoubleClick Floodlight](https://support.google.com/dcm/answer/2823388?hl=en).

Este destino é uma extensão Adobe Experience Platform Launch. Para obter mais informações sobre como as extensões de lançamento de plataforma funcionam no Adobe Real-time CDP, consulte Visão geral [das extensões do](/help/rtcdp/destinations/experience-platform-launch-extensions.md)Adobe Experience Platform Launch.

![Extensão do DoubleClick Floodlight](assets/doubleclick-floodlight-extension.png)

## Pré-requisitos {#prerequisites}

Esta extensão está disponível no [!DNL Destinations] catálogo para todos os clientes que compraram o Adobe Real-time CDP.

Para usar essa extensão, você precisa acessar o Adobe Experience Platform Launch. O Launch de plataforma é oferecido aos clientes da Adobe Experience Cloud como um recurso incluído, de valor agregado. Entre em contato com o administrador da organização para obter acesso ao Platform Launch e peça que ele conceda a você a permissão **[!UICONTROL manage_properties]** para que você possa instalar extensões.

## Instalar extensão {#install-extension}

Para instalar a extensão DoubleClick Floodlight (Beta):

1. Na interface [CDP em tempo real do](http://platform.adobe.com/)Adobe, vá para **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.
2. Selecione a extensão do catálogo ou use a barra de pesquisa.
3. Clique no destino para realçá-lo e selecione **[!UICONTROL Configurar]** no painel direito. Se o controle **[!UICONTROL Configurar]** estiver acinzentado, você não terá a permissão **[!UICONTROL manage_properties]** . Consulte [Pré-requisitos](#prerequisites).
4. Na janela de propriedades **** Selecionar lançamento de plataforma disponível, selecione a propriedade Inicialização de plataforma na qual deseja instalar a extensão. Você também tem a opção de criar uma nova propriedade no Launch da plataforma. Uma propriedade é uma coleção de regras, elementos de dados, extensões configuradas, ambientes e bibliotecas. Saiba mais sobre as propriedades na seção [da página](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Propriedades da documentação do Launch da plataforma.
5. O fluxo de trabalho leva você ao Platform Launch para concluir a instalação.

Você também pode instalar a extensão diretamente na interface [do](https://launch.adobe.com/)Adobe Experience Platform Launch. Consulte [Adicionar uma nova extensão](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) na documentação de lançamento da plataforma.


## Como usar a extensão {#how-to-use}

Depois de instalar a extensão, é possível configurar o start das regras para ela diretamente no Platform Launch.

No Platform Launch, você pode configurar regras para suas extensões instaladas para enviar dados de evento para o destino da extensão somente em determinadas situações. Para obter mais informações sobre como configurar regras para suas extensões, consulte a documentação [](https://docs.adobe.com/help/pt-BR/launch/using/reference/manage-resources/rules.html)Regras.

## Configurar, atualizar e excluir extensão {#configure-upgrade-delete}

Você pode configurar, atualizar e excluir extensões na interface do Platform Launch.

>[!TIP]
>
>Se a extensão já estiver instalada em uma de suas propriedades, a interface do usuário CDP em tempo real do Adobe ainda exibirá **[!UICONTROL Instalar]** para a extensão. Exclua o fluxo de trabalho de instalação conforme descrito em [Instalar extensão](#install-extension) para acessar o Launch da plataforma e configurar ou excluir sua extensão.

Para atualizar sua extensão, consulte Atualização [da](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) extensão na documentação do Launch da plataforma.






