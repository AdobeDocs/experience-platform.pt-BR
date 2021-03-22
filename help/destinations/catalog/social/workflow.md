---
keywords: Facebook, facebook, rede social, rede social, autenticação de rede social, autenticação de rede social
title: Criar um destino de rede social
type: Tutorial
description: Saiba como se conectar à sua rede social e às suas contas no Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---


# Criar um destino de rede social {#social-network-destinations-workflow}

## Visão geral {#overview}

Este tutorial usa [!DNL Facebook] como exemplo, mas o fluxo de trabalho do Adobe Experience Platform é o mesmo para todos os destinos de rede social.

Em **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, role até a categoria **[!UICONTROL Social]**. Selecione o destino preferido da rede social e selecione **[!UICONTROL Configure]**.

![Conectar-se ao destino da rede social](../../assets/catalog/social/workflow/catalog.png)

>[!NOTE]
>
>Se uma conexão com esse destino já existir, você poderá ver um botão **[!UICONTROL Activate]** no cartão de destino. Para obter mais informações sobre a diferença entre **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, consulte a seção [Catálogo](../../ui/destinations-workspace.md#catalog) da documentação do espaço de trabalho de destino.

## Etapa de autenticação {#authentication}

Na etapa **Authentication**, se você já tiver configurado uma conexão com o destino da rede social, selecione **[!UICONTROL Existing Account]** e selecione a conexão existente. Ou você pode selecionar **[!UICONTROL New Account]** para configurar uma nova conexão com o destino da sua rede social. Selecione **[!UICONTROL Connect to destination]** e isso o levará ao destino de rede social selecionado para fazer logon e conectar o Adobe Experience Cloud à sua conta de anúncio de rede social.

>[!NOTE]
>
>A plataforma oferece suporte à validação de credenciais no processo de autenticação e exibe uma mensagem de erro se você inserir credenciais incorretas na ID da conta da rede social. Isso garante que você não conclua o fluxo de trabalho com credenciais incorretas.

![Conectar-se ao destino da rede social - etapa de autenticação](../../assets/catalog/social/workflow/pre-connect.png)

Depois que suas credenciais forem confirmadas e o Adobe Experience Cloud estiver conectado à rede social, você poderá selecionar **[!UICONTROL Next]** para prosseguir para a etapa **[!UICONTROL Setup]**.

![Credenciais confirmadas](../../assets/catalog/social/workflow/post-connect.png)

## Etapa de configuração {#setup}

Na etapa **[!UICONTROL Setup]** , insira um [!UICONTROL Name] e um [!UICONTROL Description] para o fluxo de ativação e preencha o [!UICONTROL Account ID] de sua conta de anúncio de rede social.

>[!IMPORTANT]
>
> Para destinos [!DNL Facebook], **[!UICONTROL Account ID]** é seu [!DNL Facebook Ad Account ID]. Você pode encontrar essa ID no [!DNL Facebook Ads Manager]. Coloque o prefixo `act_` na ID, conforme mostrado abaixo:

![Conectar-se ao destino da rede social - etapa de configuração](../../assets/catalog/social/workflow/setup.png)

>[!IMPORTANT]
>
> Para destinos [!DNL LinkedIn], **[!UICONTROL Account ID]** é seu [!DNL LinkedIn Campaign Manager Account ID]. Você pode encontrar essa ID no [!DNL LinkedIn Campaign Manager].

Além disso, nesta etapa, você pode selecionar qualquer **[!UICONTROL Marketing action]** que deve se aplicar a esse destino. As ações de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar ações de marketing definidas pelo Adobe ou criar sua própria ação de marketing. Para obter mais informações sobre ações de marketing, consulte a [Visão geral das políticas de uso de dados](../../../data-governance/policies/overview.md).

Selecione **[!UICONTROL Create Destination]** depois de preencher os campos acima.

Seu destino foi criado. Você pode selecionar **[!UICONTROL Save & Exit]** se desejar ativar segmentos posteriormente ou selecionar **[!UICONTROL Next]** para continuar o fluxo de trabalho e selecionar segmentos para ativar. Em ambos os casos, consulte a próxima seção, [Ativar segmentos para redes sociais](#activate-segments), para o restante do fluxo de trabalho.

## Ativar segmentos para redes sociais {#activate-segments}

Para obter instruções sobre como ativar segmentos em redes sociais, consulte [Ativar dados para destinos](../../ui/activate-destinations.md).