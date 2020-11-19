---
keywords: beemray,beemray extension
title: Extensão de Beemray
seo-title: Extensão de Beemray
description: A extensão Beemray é um destino de personalização na Plataforma de dados do cliente em tempo real. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no Adobe Exchange.
seo-description: A extensão Beemray é um destino de personalização na Plataforma de dados do cliente em tempo real. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no Adobe Exchange.
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 4%

---


# [!DNL Beemray] extensão {#beemray-extension}

## Visão geral {#overview}

[!DNL Beemray] ajuda a acelerar seu produto com contexto situacional. Permitindo que você obtenha insights, crie novas experiências, impulsione interações e envolva-se em momentos que realmente importam. A Beemray automatiza a inteligência contextual usando o aprendizado de máquina. A Beemray se conecta com a Adobe Experience Cloud e com o resto de seus parceiros técnicos. Tudo acontece em tempo real. Esta extensão instala o [!DNL Beemray] SDK no site.

Beemray é uma extensão de personalização na Plataforma de dados do cliente em tempo real. Para obter mais informações sobre a funcionalidade de extensão, consulte a página de extensão no [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101063.beemray-human-context.html).

Este destino é uma [!DNL Adobe Experience Platform Launch] extensão. Para obter mais informações sobre como [!DNL Platform Launch] as extensões funcionam no CDP em tempo real do Adobe, consulte Visão geral [das extensões do](/help/rtcdp/destinations/experience-platform-launch-extensions.md)Experience Platform Launch.

![Extensão de Beemray](assets/beemray-extension.png)

## Pré-requisitos {#prerequisites}

Esta extensão está disponível no [!DNL Destinations] catálogo para todos os clientes que compraram o Adobe Real-time CDP.

Para usar essa extensão, você precisa ter acesso a [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] é oferecido aos clientes da Adobe Experience Cloud como um recurso incluído, de valor agregado. Entre em contato com o administrador da organização para obter acesso [!DNL Platform Launch] e solicitar que ele conceda a permissão **[!UICONTROL manage_properties]** para que você possa instalar extensões.

## Instalar extensão {#install-extension}

Para instalar a [!DNL Beemray] extensão:

1. Na interface [CDP em tempo real do](http://platform.adobe.com/)Adobe, vá para **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**.
2. Selecione a extensão do catálogo ou use a barra de pesquisa.
3. Clique no destino para realçá-lo e selecione **[!UICONTROL Configurar]** no painel direito. Se o controle **[!UICONTROL Configurar]** estiver acinzentado, você não terá a permissão **[!UICONTROL manage_properties]** . Consulte [Pré-requisitos](#prerequisites).
4. Na janela **[!UICONTROL Selecionar propriedade]** de lançamento de plataforma disponível, selecione a [!DNL Platform Launch] propriedade na qual deseja instalar a extensão. Você também tem a opção de criar uma nova propriedade em [!DNL Platform Launch]. Uma propriedade é uma coleção de regras, elementos de dados, extensões configuradas, ambientes e bibliotecas. Saiba mais sobre as propriedades na seção [da página](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Propriedades da [!DNL Launch] documentação.
5. O fluxo de trabalho leva você [!DNL Platform Launch] a concluir a instalação.

Para obter informações sobre as opções de configuração de extensão e suporte de instalação, consulte a página [Beemray no Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101063.beemray-human-context.html).

Você também pode instalar a extensão diretamente na interface [do](https://launch.adobe.com/)Adobe Experience Platform Launch. Consulte [Adicionar uma nova extensão](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) na [!DNL Platform Launch] documentação.

## Como usar a extensão {#how-to-use}

Depois de instalar a extensão, você pode fazer um start ao configurar as regras para ela diretamente no [!DNL Platform Launch].

Em [!DNL Platform Launch], você pode configurar regras para suas extensões instaladas para enviar dados de evento para o destino da extensão somente em determinadas situações. Para obter mais informações sobre como configurar regras para suas extensões, consulte a documentação [](https://docs.adobe.com/help/pt-BR/launch/using/reference/manage-resources/rules.html)Regras.

## Configurar, atualizar e excluir extensão {#configure-upgrade-delete}

Você pode configurar, atualizar e excluir extensões na [!DNL Platform Launch] interface.

>[!TIP]
>
>Se a extensão já estiver instalada em uma de suas propriedades, a interface do usuário CDP em tempo real do Adobe ainda exibirá **[!UICONTROL Instalar]** para a extensão. Exclua o fluxo de trabalho de instalação conforme descrito em [Instalar extensão](#install-extension) para acessar [!DNL Platform Launch] e configurar ou excluir sua extensão.

Para atualizar sua extensão, consulte Atualização [da](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) extensão na [!DNL Platform Launch] documentação.



