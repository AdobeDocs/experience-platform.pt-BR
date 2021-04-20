---
keywords: Facebook, facebook, rede social, rede social, autenticação social, autenticação de rede social
title: Criar um destino social
type: Tutorial
description: Saiba como se conectar às suas contas de anúncios sociais no Adobe Experience Platform.
exl-id: a0cdf2b7-b1e8-4a8e-9d5b-58a118e7b689
translation-type: tm+mt
source-git-commit: 805cb72e91e6446f74cc3461d39841740eb576c7
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# Criar um destino social {#social-network-destinations-workflow}

## Visão geral {#overview}

Este tutorial usa [!DNL Facebook] como exemplo, mas o fluxo de trabalho do Adobe Experience Platform é o mesmo para todos os destinos sociais.

## Configurar destino social - apresentação de vídeo {#video}

O vídeo abaixo demonstra como configurar um destino social e ativar segmentos no Adobe Experience Platform. As etapas também são apresentadas sequencialmente nas próximas seções.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

## Selecione o destino social {#select-destination}

Em **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, role até a categoria **[!UICONTROL Social]**. Selecione o destino social preferencial e selecione **[!UICONTROL Configure]**.

![Conectar-se ao destino social](../../assets/catalog/social/workflow/catalog.png)

>[!NOTE]
>
>Se uma conexão com esse destino já existir, você poderá ver um botão **[!UICONTROL Activate]** no cartão de destino. Para obter mais informações sobre a diferença entre **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, consulte a seção [Catálogo](../../ui/destinations-workspace.md#catalog) da documentação do espaço de trabalho de destino.

## Etapa da conta {#account}

Na etapa **Account**, se você tiver configurado anteriormente uma conexão com seu destino social, selecione **[!UICONTROL Existing Account]** e selecione sua conexão existente. Ou você pode selecionar **[!UICONTROL New Account]** para configurar uma nova conexão com seu destino social. Selecione **[!UICONTROL Connect to destination]** e isso o levará ao destino social selecionado para fazer logon e conectar o Adobe Experience Cloud à sua conta de publicidade social.

>[!NOTE]
>
>A plataforma oferece suporte à validação de credenciais no processo de autenticação e exibe uma mensagem de erro se você inserir credenciais incorretas na ID da conta social. Isso garante que você não conclua o fluxo de trabalho com credenciais incorretas.

![Conectar-se ao destino social - etapa de autenticação](../../assets/catalog/social/workflow/pre-connect.png)

Depois que suas credenciais forem confirmadas e o Adobe Experience Cloud estiver conectado à rede social, você poderá selecionar **[!UICONTROL Next]** para prosseguir para a etapa **[!UICONTROL Authentication]**.

![Credenciais confirmadas](../../assets/catalog/social/workflow/post-connect.png)

## Etapa de autenticação {#authentication}

Na etapa **[!UICONTROL Authentication]** , insira um [!UICONTROL Name] e um [!UICONTROL Description] para o fluxo de ativação e preencha o [!UICONTROL Account ID] de sua conta de anúncio de rede social.

>[!IMPORTANT]
>
> * Para destinos [!DNL Facebook], **[!UICONTROL Account ID]** é seu [!DNL Facebook Ad Account ID]. Você pode encontrar essa ID no [!DNL Facebook Ads Manager]. Coloque o prefixo `act_` na ID, conforme mostrado na imagem abaixo.
> * Para destinos [!DNL LinkedIn], **[!UICONTROL Account ID]** é seu [!DNL LinkedIn Campaign Manager Account ID]. Você pode encontrar essa ID no [!DNL LinkedIn Campaign Manager].


![Conectar-se ao destino social - etapa de autenticação](../../assets/catalog/social/workflow/authentication.png)

Nesta etapa, você também pode selecionar qualquer **[!UICONTROL Marketing action]** que deve se aplicar a esse destino. As ações de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar ações de marketing definidas pelo Adobe ou criar sua própria ação de marketing. Para obter mais informações sobre ações de marketing, consulte a [Visão geral das políticas de uso de dados](../../../data-governance/policies/overview.md).

Selecione **[!UICONTROL Create Destination]** depois de preencher os campos acima.

Seu destino foi criado. Você pode selecionar **[!UICONTROL Save & Exit]** se desejar ativar segmentos posteriormente ou selecionar **[!UICONTROL Next]** para continuar o fluxo de trabalho e selecionar segmentos para ativar. Em ambos os casos, consulte a próxima seção, [Ativar segmentos para redes sociais](#activate-segments), para o restante do fluxo de trabalho.

## Ativar segmentos para redes sociais {#activate-segments}

Para obter instruções sobre como ativar segmentos em redes sociais, consulte [Ativar dados para destinos](../../ui/activate-destinations.md).
