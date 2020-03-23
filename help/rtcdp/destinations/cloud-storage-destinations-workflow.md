---
title: Fluxo de trabalho de destinos de armazenamento em nuvem
seo-title: Fluxo de trabalho de destinos de armazenamento em nuvem
description: Instruções para conectar-se aos locais de armazenamento na nuvem
seo-description: Instruções para conectar-se aos locais de armazenamento na nuvem
translation-type: tm+mt
source-git-commit: 9221c11a30bda3a155d73afec16be55ef8f5d133

---


# Fluxo de trabalho para criar destinos de armazenamento em nuvem

## Visão geral

Esta página explica como você pode se conectar a locais de armazenamento em nuvem na Adobe Real-time Customer Data Platform.

1. Em **[!UICONTROL Connections > Destinations]**, selecione seu destino de armazenamento em nuvem preferencial e, em seguida, selecione **[!UICONTROL Connect destination]**.

   ![Conectar-se ao destino de armazenamento na nuvem](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. Na etapa **Autenticação** , se você já tiver configurado uma conexão com o destino de armazenamento na nuvem, selecione **[!UICONTROL Existing Account]** e selecione a conexão existente. Ou você pode optar por configurar uma nova conexão **[!UICONTROL New Account]** para o destino de armazenamento na nuvem. Preencha as credenciais de autenticação da sua conta e selecione **[!UICONTROL Connect to destination]**.

   >[!NOTE]
   >
   >O Adobe Real-time CDP oferece suporte à validação de credenciais no processo de autenticação e exibe uma mensagem de erro se você inserir credenciais incorretas no local de armazenamento na nuvem. Isso garante que você não conclua o fluxo de trabalho com credenciais incorretas.

   ![Conectar-se ao destino do armazenamento na nuvem - etapa de autenticação](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. Na **[!UICONTROL Setup]** etapa, insira um **[!UICONTROL Name]** e um **[!UICONTROL Description]** para o fluxo de ativação.
   1. Para destinos do Amazon S3, insira o **[!UICONTROL Bucket name]** e o **[!UICONTROL Folder path]** no destino de armazenamento em nuvem onde os arquivos serão entregues. Selecione **[!UICONTROL Create Destination]** depois de preencher os campos acima.
   2. Para destinos SFTP, insira a variável **[!UICONTROL Folder path]**
   ![Conectar-se ao destino do armazenamento na nuvem - etapa de autenticação](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

4. Seu destino agora é criado. Você pode selecionar **[!UICONTROL Save & Exit]** se deseja ativar segmentos posteriormente ou selecionar **[!UICONTROL Next]** para continuar o fluxo de trabalho e selecionar segmentos para ativar. Em ambos os casos, consulte a próxima seção, [Ativar segmentos](#activate-segments), para que o restante do fluxo de trabalho exporte dados.

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos em um destino](/help/rtcdp/destinations/activate-destinations.md) para obter informações sobre o fluxo de trabalho de ativação do segmento.