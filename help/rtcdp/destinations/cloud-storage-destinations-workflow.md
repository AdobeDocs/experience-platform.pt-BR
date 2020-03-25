---
title: Fluxo de trabalho de destinos de armazenamentos na nuvem
seo-title: Fluxo de trabalho de destinos de armazenamentos na nuvem
description: Instruções para conectar-se aos locais dos armazenamentos na nuvem
seo-description: Instruções para conectar-se aos locais dos armazenamentos na nuvem
translation-type: tm+mt
source-git-commit: 60b10aa823af55d6f38651308dc93eeb57a7fee6

---


# Fluxo de trabalho para criar destinos de armazenamentos na nuvem

## Visão geral

Esta página explica como você pode se conectar aos locais do armazenamento em nuvem na Plataforma de dados do cliente em tempo real da Adobe.

1. Em **[!UICONTROL Connections > Destinations]**, selecione o destino preferencial do armazenamento na nuvem e, em seguida, selecione **[!UICONTROL Connect destination]**.

   ![Conectar-se ao destino do armazenamento na nuvem](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

1. Na etapa **Autenticação** , se você tiver configurado anteriormente uma conexão com o destino do armazenamento na nuvem, selecione **[!UICONTROL Existing Account]** e selecione a conexão existente. Ou você pode optar por configurar **[!UICONTROL New Account]** uma nova conexão com o destino do armazenamento na nuvem. Preencha as credenciais de autenticação da sua conta e selecione **[!UICONTROL Connect to destination]**. Consulte destino [do](/help/rtcdp/destinations/amazon-s3-destination.md) Amazon S3 e destino [](/help/rtcdp/destinations/sftp-destination.md) SFTP para obter detalhes sobre as credenciais inseridas na etapa **Autenticação** .

   >[!NOTE]
   >
   >O Adobe Real-time CDP oferece suporte à validação de credenciais no processo de autenticação e exibe uma mensagem de erro se você inserir credenciais incorretas no local do armazenamento na nuvem. Isso garante que você não conclua o fluxo de trabalho com credenciais incorretas.

   ![Conectar ao destino do armazenamento na nuvem - etapa de autenticação](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

1. Na **[!UICONTROL Setup]** etapa, insira um **[!UICONTROL Name]** e um **[!UICONTROL Description]** para o fluxo de ativação. <br>
Para destinos do Amazon S3, insira o **[!UICONTROL Bucket name]** e o **[!UICONTROL Folder path]** no destino do armazenamento da nuvem onde os arquivos serão entregues. Selecione **[!UICONTROL Create Destination]** depois de preencher os campos acima.

   ![Conectar-se ao destino do armazenamento da nuvem do Amazon S3 - etapa de autenticação](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

   Para destinos SFTP, insira o local em **[!UICONTROL Folder path]** que os arquivos serão entregues.

   ![Conectar-se ao destino do armazenamento na nuvem SFTP - etapa de autenticação](/help/rtcdp/destinations/assets/sftp-destinations-setup-step.png)

1. Seu destino agora é criado. Você pode selecionar **[!UICONTROL Save & Exit]** se deseja ativar segmentos posteriormente ou selecionar **[!UICONTROL Next]** para continuar o fluxo de trabalho e selecionar segmentos para ativar. Em ambos os casos, consulte a próxima seção, [Ativar segmentos](#activate-segments), para que o restante do fluxo de trabalho exporte dados.

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos em um destino](/help/rtcdp/destinations/activate-destinations.md) para obter informações sobre o fluxo de trabalho da ativação de segmentos.