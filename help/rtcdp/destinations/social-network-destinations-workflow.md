---
title: Fluxo de trabalho de destinos de rede social
seo-title: Fluxo de trabalho de destinos de rede social
description: Instruções para conectar-se à sua rede social e contas
seo-description: Instruções para conectar-se à sua rede social e contas
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# (Beta) Fluxo de trabalho de autenticação de destinos de rede social {#social-network-destinations-workflow}


>[!IMPORTANT]
>
>O fluxo de trabalho para criar destinos de rede social no Adobe Real-time CDP está atualmente em beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

## Fluxo de trabalho para criar destinos de armazenamentos na nuvem

Este tutorial usa o Facebook como exemplo, mas o fluxo de trabalho na Plataforma de dados do cliente em tempo real da Adobe será o mesmo para todos os destinos da Rede social, uma vez mais, adicionado ao produto.

1. Em **[!UICONTROL Connections > Destinations]**, role até a **[!UICONTROL Social]** categoria. Selecione o destino de sua rede social preferida e, em seguida, selecione **[!UICONTROL Connect destination]**.

   ![Conectar-se ao destino da rede social](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. Na etapa **Autenticação** , se você já tiver configurado uma conexão com o destino da rede social, selecione **[!UICONTROL Existing Account]** e selecione a conexão existente. Ou você pode optar por configurar **[!UICONTROL New Account]** uma nova conexão com o destino da sua rede social. Selecione **[!UICONTROL Connect to destination]** e isso levará você ao destino da rede social selecionada para fazer logon e conectar a Adobe Experience Cloud à sua conta de anúncio de rede social.

   >[!NOTE]
   >
   >O Adobe Real-time CDP oferece suporte à validação de credenciais no processo de autenticação e exibe uma mensagem de erro se você inserir credenciais incorretas na ID da conta da rede social. Isso garante que você não conclua o fluxo de trabalho com credenciais incorretas.

   ![Conectar ao destino da rede social - etapa de autenticação](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. Depois que suas credenciais forem confirmadas e a Adobe Experience Cloud estiver conectada à sua rede social, você poderá optar por **[!UICONTROL Next]** prosseguir para a **[!UICONTROL Setup]** etapa.

   ![Credenciais confirmadas](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. Na **[!UICONTROL Setup]** etapa, insira um **[!UICONTROL Name]** e um **[!UICONTROL Description]** para o fluxo de ativação e preencha a conta **[!UICONTROL Account ID]** de anúncio da rede social. Selecione **[!UICONTROL Create Destination]** depois de preencher os campos acima.

   >[!IMPORTANT]
   >
   >Para destinos do Facebook. **[!UICONTROL Account ID]** é sua ID de conta de anúncio do Facebook. Você pode encontrar essa ID no Gerenciador de publicidades do Facebook. Prefixe a ID como `act_` mostrado abaixo:

   ![Conectar ao destino da rede social - etapa de configuração](/help/rtcdp/destinations/assets/social-network-step.png)

5. Seu destino agora é criado. Você pode selecionar **[!UICONTROL Save & Exit]** se deseja ativar segmentos posteriormente ou selecionar **[!UICONTROL Next]** para continuar o fluxo de trabalho e selecionar segmentos para ativar. Em ambos os casos, consulte a próxima seção, [Ativar segmentos em redes](#activate-segments)sociais, para o restante do fluxo de trabalho.

## Ativar segmentos em redes sociais {#activate-segments}

Para obter instruções sobre como ativar segmentos em redes sociais, consulte [Ativar dados para destinos](/help/rtcdp/destinations/activate-destinations.md).