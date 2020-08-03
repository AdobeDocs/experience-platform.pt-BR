---
title: Fluxo de trabalho de destinos de rede social
seo-title: Fluxo de trabalho de destinos de rede social
description: Instruções para conectar-se à sua rede social e contas
seo-description: Instruções para conectar-se à sua rede social e contas
translation-type: tm+mt
source-git-commit: be4cf64c89a189a09a4a7774c8fadc76c6ee8458
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 0%

---


# Fluxo de trabalho de autenticação de destinos de rede social {#social-network-destinations-workflow}

## Fluxo de trabalho para criar destinos de rede social

Este tutorial usa [!DNL Facebook] como exemplo, mas o fluxo de trabalho no Adobe Real-time Customer Data Platform será o mesmo para todos os destinos da rede social, uma vez mais adicionado ao produto.

1. Em **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**, role até a categoria **[!UICONTROL Social]** . Selecione o destino de sua rede social preferida e, em seguida, selecione o destino **[!UICONTROL do]** Connect.

   ![Connect to social network destination](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. Na etapa **Autenticação** , se você já tiver configurado uma conexão com o destino da rede social, selecione Conta **** existente e selecione a conexão existente. Ou você pode selecionar **[!UICONTROL Nova conta]** para configurar uma nova conexão com o destino da sua rede social. Selecione **[!UICONTROL Conectar ao destino]** e isso o levará ao destino da rede social selecionada para fazer logon e conectar o Adobe Experience Cloud à sua conta de anúncio de rede social.

   >[!NOTE]
   >
   >A CDP em tempo real do Adobe oferece suporte à validação de credenciais no processo de autenticação e exibe uma mensagem de erro se você inserir credenciais incorretas na ID da conta da rede social. Isso garante que você não conclua o fluxo de trabalho com credenciais incorretas.

   ![Conectar ao destino da rede social - etapa de autenticação](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. Depois que suas credenciais forem confirmadas e o Adobe Experience Cloud estiver conectado à sua rede social, você poderá selecionar **[!UICONTROL Avançar]** para prosseguir para a etapa **[!UICONTROL de instalação]** .

   ![Credenciais confirmadas](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. Na etapa **[!UICONTROL Configuração]** , digite um **[!UICONTROL Nome]** e uma **[!UICONTROL Descrição]** para o fluxo de ativação e preencha a ID **[!UICONTROL de]** conta da sua conta de anúncio de rede social. <br> Também nesta etapa, você pode selecionar qualquer caso **[!UICONTROL de uso de]** Marketing que deve ser aplicado a este destino. Os casos de uso de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar de casos de uso de marketing definidos pelo Adobe ou criar seu próprio caso de uso de marketing. Para obter mais informações sobre casos de uso de marketing, consulte a página [Data Governance em CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) em tempo real. Para obter informações sobre casos individuais de uso de marketing definidos pelo Adobe, consulte a visão geral [das políticas de uso de](/help/data-governance/policies/overview.md#core-actions)dados. <br> Selecione **[!UICONTROL Criar destino]** depois de preencher os campos acima.

   >[!IMPORTANT]
   >
   > * The *Single Identity Personalization* marketing use case is selected by default for social network destinations and cannot be removed.
   > * For [!DNL Facebook] destinations. **[!UICONTROL A ID]** da conta é sua [!DNL Facebook Ad Account ID]. Você pode encontrar essa ID no [!DNL Facebook Ads Manager]. Prefixe a ID como `act_` mostrado abaixo:


   ![Conectar ao destino da rede social - etapa de configuração](/help/rtcdp/destinations/assets/social-networks-setup-step.png)

5. Seu destino agora é criado. Você pode selecionar **[!UICONTROL Salvar e sair]** se quiser ativar segmentos posteriormente ou selecionar **[!UICONTROL Próximo]** para continuar o fluxo de trabalho e selecionar segmentos para ativar. Em ambos os casos, consulte a próxima seção, [Ativar segmentos em redes](#activate-segments)sociais, para o restante do fluxo de trabalho.

## Activate segments to social networks {#activate-segments}

Para obter instruções sobre como ativar segmentos em redes sociais, consulte [Ativar dados para destinos](/help/rtcdp/destinations/activate-destinations.md).