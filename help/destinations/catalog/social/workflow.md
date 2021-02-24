---
keywords: Facebook;facebook;rede social;rede social;autenticação de rede social;autenticação de rede social
title: Criar um destino de rede social
type: Tutorial
description: Saiba como se conectar à sua rede social e às suas contas de anúncio no Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 19e38faa84d365682e97c2ec1c6352d127c0ac29
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---


# Criar um destino de rede social {#social-network-destinations-workflow}

Este tutorial usa [!DNL Facebook] como exemplo, mas o fluxo de trabalho do Adobe Experience Platform é o mesmo para todos os destinos de rede social.

Em **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**, vá até a categoria **[!UICONTROL Social]**. Selecione o destino de sua rede social preferida e selecione **[!UICONTROL Configurar]**.

![Conectar-se ao destino da rede social](../../assets/catalog/social/workflow/catalog.png)

>[!NOTE]
>
>Se já existir uma conexão com esse destino, você poderá ver um botão **[!UICONTROL Ativar]** no cartão de destino. Para obter mais informações sobre a diferença entre **[!UICONTROL Ativate]** e **[!UICONTROL Configure]**, consulte a seção [Catalog](../../ui/destinations-workspace.md#catalog) da documentação da área de trabalho de destino.

Na etapa **Authentication**, se você tiver configurado anteriormente uma conexão com o destino da rede social, selecione **[!UICONTROL Conta existente]** e selecione a conexão existente. Ou você pode selecionar **[!UICONTROL Nova conta]** para configurar uma nova conexão com o destino da sua rede social. Selecione **[!UICONTROL Ligar ao destino]** e isto leva-o ao destino selecionado da rede social para iniciar sessão e ligar o Adobe Experience Cloud à sua conta de Anúncio de rede social.

>[!NOTE]
>
>A plataforma suporta a validação de credenciais no processo de autenticação e exibe uma mensagem de erro se você inserir credenciais incorretas na ID da conta da rede social. Isso garante que você não conclua o fluxo de trabalho com credenciais incorretas.

![Conectar ao destino da rede social - etapa de autenticação](../../assets/catalog/social/workflow/pre-connect.png)

Depois que suas credenciais forem confirmadas e o Adobe Experience Cloud estiver conectado à sua rede social, você poderá selecionar **[!UICONTROL Próximo]** para prosseguir para a etapa **[!UICONTROL Configuração]**.

![Credenciais confirmadas](../../assets/catalog/social/workflow/post-connect.png)

Na etapa **[!UICONTROL Setup]**, digite um [!UICONTROL Nome] e um [!UICONTROL Descrição] para o fluxo de ativação e preencha a [!UICONTROL ID da conta] da sua conta de anúncio de rede social.

>[!IMPORTANT]
>
> Para destinos [!DNL Facebook], **[!UICONTROL ID da conta]** é seu [!DNL Facebook Ad Account ID]. Você pode encontrar essa ID no [!DNL Facebook Ads Manager]. Prefixe a ID com `act_` como mostrado abaixo:

![Conectar ao destino da rede social - etapa de configuração](../../assets/catalog/social/workflow/setup.png)

>[!IMPORTANT]
>
> Para destinos [!DNL LinkedIn], **[!UICONTROL ID da conta]** é seu [!DNL LinkedIn Campaign Manager Account ID]. Você pode encontrar essa ID no [!DNL LinkedIn Campaign Manager].

Também nesta etapa, você pode selecionar qualquer **[!UICONTROL ação de marketing]** que deve se aplicar a este destino. As ações de marketing indicam a intenção para a qual os dados serão exportados para o destino. É possível selecionar ações de marketing definidas pelo Adobe ou criar sua própria ação de marketing. Para obter mais informações sobre ações de marketing, consulte [Visão geral das políticas de uso de dados](../../../data-governance/policies/overview.md).

Selecione **[!UICONTROL Criar destino]** depois de preencher os campos acima.

Seu destino agora é criado. Você pode selecionar **[!UICONTROL Salvar e Sair]** se quiser ativar segmentos posteriormente ou selecionar **[!UICONTROL Próximo]** para continuar o fluxo de trabalho e selecionar segmentos para ativação. Em ambos os casos, consulte a próxima seção, [Ativar segmentos para redes sociais](#activate-segments), para o restante do fluxo de trabalho.

## Ativar segmentos em redes sociais {#activate-segments}

Para obter instruções sobre como ativar segmentos em redes sociais, consulte [Ativar dados para destinos](../../ui/activate-destinations.md).