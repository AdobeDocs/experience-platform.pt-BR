---
title: Extensão Medallia
seo-title: Extensão Medallia
description: A extensão Medallia é uma voz do destino do cliente na Plataforma de dados do cliente em tempo real da Adobe. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no Adobe Exchange.
seo-description: A extensão Medallia é uma voz do destino do cliente na Adobe Real-time Customer Data Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no Adobe Exchange.
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# Extensão Medallia {#medallia-extension}

## Visão geral {#overview}

Implante Medallia de forma rápida e contínua em suas propriedades da Web. A extensão também permite que você detecte eventos de pesquisa, capture o feedback dos clientes em tempo real por meio de elementos de dados, use-o em regras para personalizar a experiência do cliente e compartilhar dados com o Adobe Analytics.

Medallia é uma voz da extensão do cliente na Adobe Real-time Customer Data Platform. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103279.medallia-for-adobe-launch.html).

Este destino é uma extensão do Experience Platform Launch. Para obter mais informações sobre como as extensões do Launch funcionam na Adobe Real-time CDP, consulte Visão geral [das extensões do Launch da plataforma](/help/rtcdp/destinations/experience-platform-launch-extensions.md)Experience.

![Extensão Medallia](assets/medallia-extension.png)

## Pré-requisitos {#prerequisites}

Essa extensão está disponível no catálogo Destinos para todos os clientes que compraram a CDP em tempo real da Adobe.

Para usar essa extensão, você precisa acessar o Experience Platform Launch. O Experience Platform Launch é oferecido aos clientes da Adobe Experience Cloud como um recurso incluído, que agrega valor. Entre em contato com o administrador da organização para obter acesso ao Launch e solicitar que ele conceda a você a **[!UICONTROL manage_properties]** permissão para que você possa instalar extensões.

## Instalar extensão {#install-extension}

Para instalar a extensão Medallia:

1. Na interface [CDP em tempo real da](http://platform.adobe.com/)Adobe, vá para **[!UICONTROL Destinations > Catalog]**.
2. Selecione a extensão do catálogo ou use a barra de pesquisa.
3. Clique no destino para realçá-lo e selecione **[!UICONTROL Install Extension]** no painel direito. Se o **[!UICONTROL Install Extension]** controle estiver acinzentado, você não terá a **[!UICONTROL manage_properties]** permissão. Consulte [Pré-requisitos](#prerequisites).
4. Na **[!UICONTROL Select available Launch property]** janela, selecione a propriedade Launch na qual deseja instalar a extensão. Você também tem a opção de criar uma nova propriedade no Launch. Uma propriedade é uma coleção de regras, elementos de dados, extensões configuradas, ambientes e bibliotecas. Saiba mais sobre as propriedades na seção [da página](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Propriedades da documentação do Launch.
5. O fluxo de trabalho leva você ao Launch para concluir a instalação.

Para obter informações sobre as opções de configuração de extensão e suporte de instalação, consulte a página [Medallia no Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103279.medallia-for-adobe-launch.html).

Você também pode instalar a extensão diretamente na interface [do](https://launch.adobe.com/)Experience Platform Launch. Consulte [Adicionar uma nova extensão](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) na documentação do Launch.

## Como usar a extensão {#how-to-use}

Depois de instalar a extensão, você pode start configurando regras para ela diretamente no Launch.

Em Iniciar, você pode configurar regras para suas extensões instaladas para enviar dados de evento para o destino da extensão somente em determinadas situações. Para obter mais informações sobre como configurar regras para suas extensões, consulte a documentação [](https://docs.adobe.com/help/pt-BR/launch/using/reference/manage-resources/rules.html)Regras.

## Configurar, atualizar e excluir extensão {#configure-upgrade-delete}

Você pode configurar, atualizar e excluir extensões na interface do Launch.

>[!TIP]
>
>Se a extensão já estiver instalada em uma de suas propriedades, a interface do usuário CDP em tempo real da Adobe ainda será exibida **[!UICONTROL Install]** para a extensão. Exclua o fluxo de trabalho de instalação conforme descrito em [Instalar extensão](#install-extension) para acessar Iniciar e configurar ou excluir sua extensão.

Para atualizar sua extensão, consulte Atualização [da](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) extensão na documentação do Launch.