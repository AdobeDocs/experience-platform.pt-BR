---
title: Fluxo de trabalho de destinos de rede social
seo-title: Fluxo de trabalho de destinos de rede social
description: Instruções para conectar-se à sua rede social e contas
seo-description: Instruções para conectar-se à sua rede social e contas
translation-type: tm+mt
source-git-commit: ab53e2efffed536e8028beabd64aee843d1eeee8
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---


# Fluxo de trabalho de autenticação de destinos de rede social {#social-network-destinations-workflow}

## Fluxo de trabalho para criar destinos de rede social

Este tutorial usa o Facebook como exemplo, mas o fluxo de trabalho na Plataforma de dados do cliente em tempo real da Adobe será o mesmo para todos os destinos de rede social, uma vez mais, adicionado ao produto.

1. Em **[!UICONTROL Destinos > Catálogo]**, role até a categoria **[!UICONTROL Social]** . Selecione o destino de sua rede social preferida e, em seguida, selecione o destino **[!UICONTROL do]** Connect.

   ![Conectar-se ao destino da rede social](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. Na etapa **Autenticação** , se você já tiver configurado uma conexão com o destino da rede social, selecione Conta **** existente e selecione a conexão existente. Ou você pode selecionar **[!UICONTROL Nova conta]** para configurar uma nova conexão com o destino da sua rede social. Selecione **[!UICONTROL Conectar-se ao destino]** e isso o levará ao destino da rede social selecionada para fazer logon e conectar a Adobe Experience Cloud à sua conta de anúncio de rede social.

   >[!NOTE]
   >
   >O Adobe Real-time CDP oferece suporte à validação de credenciais no processo de autenticação e exibe uma mensagem de erro se você inserir credenciais incorretas na ID da conta da rede social. Isso garante que você não conclua o fluxo de trabalho com credenciais incorretas.

   ![Conectar ao destino da rede social - etapa de autenticação](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. Depois que suas credenciais forem confirmadas e a Adobe Experience Cloud estiver conectada à sua rede social, você poderá selecionar **[!UICONTROL Avançar]** para prosseguir para a etapa **[!UICONTROL de instalação]** .

   ![Credenciais confirmadas](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. Na etapa **[!UICONTROL Configuração]** , digite um **[!UICONTROL Nome]** e uma **[!UICONTROL Descrição]** para o fluxo de ativação e preencha a ID **[!UICONTROL de]** conta da sua conta de anúncio de rede social. Selecione todos os casos de uso de marketing que devem ser aplicados a esse destino. Selecione **[!UICONTROL Criar destino]** depois de preencher os campos acima.

   >[!IMPORTANT]
   >
   > Para destinos do Facebook. **[!UICONTROL A ID]** da conta é a ID da conta do anúncio do Facebook. Você pode encontrar essa ID no Gerenciador de publicidades do Facebook. Prefixe a ID como `act_` mostrado abaixo:

   ![Conectar ao destino da rede social - etapa de configuração](/help/rtcdp/destinations/assets/social-network-setup-step.png)

5. Seu destino agora é criado. Você pode selecionar **[!UICONTROL Salvar e sair]** se quiser ativar segmentos posteriormente ou selecionar **[!UICONTROL Próximo]** para continuar o fluxo de trabalho e selecionar segmentos para ativar. Em ambos os casos, consulte a próxima seção, [Ativar segmentos em redes](#activate-segments)sociais, para o restante do fluxo de trabalho.

## Ativar segmentos em redes sociais {#activate-segments}

Para obter instruções sobre como ativar segmentos em redes sociais, consulte [Ativar dados para destinos](/help/rtcdp/destinations/activate-destinations.md).


<!--

// update IMPORTANT note in step 4 after marketing use cases are released for RTCDP

    >[!IMPORTANT]
    >
    > * The *Single Identity Personalization* marketing use case is selected by default for social network destinations and cannot be removed. 
    > * For Facebook destinations. **[!UICONTROL Account ID]** is your Facebook Ad Account ID. You can find this ID in the Facebook Ads Manager. Prefix the ID with `act_` as shown below: 

    ![Connect to social network destination - setup step](/help/rtcdp/destinations/assets/social-networks-setup-step.png)