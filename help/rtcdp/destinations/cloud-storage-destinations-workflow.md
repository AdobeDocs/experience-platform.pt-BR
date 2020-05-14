---
title: Fluxo de trabalho de destinos de armazenamentos na nuvem
seo-title: Fluxo de trabalho de destinos de armazenamentos na nuvem
description: Instruções para conectar-se aos locais dos armazenamentos na nuvem
seo-description: Instruções para conectar-se aos locais dos armazenamentos na nuvem
translation-type: tm+mt
source-git-commit: 37c51435ce8330dbd61857bda408df03ff21a491
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---


# Fluxo de trabalho para criar destinos de armazenamentos na nuvem

## Visão geral

Esta página explica como você pode se conectar aos locais do armazenamento em nuvem na Plataforma de dados do cliente em tempo real da Adobe.

1. Em **[!UICONTROL Conexões > Destinos]**, selecione o destino preferencial do armazenamento na nuvem e selecione o destino **[!UICONTROL do]** Connect.

   ![Conectar-se ao destino do armazenamento na nuvem](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. Na etapa **[!UICONTROL Autenticação]** , se você tiver configurado anteriormente uma conexão com o destino do armazenamento na nuvem, selecione Conta **** existente e selecione a conexão existente. Ou você pode selecionar **[!UICONTROL Nova conta]** para configurar uma nova conexão com o destino do armazenamento na nuvem. Preencha as credenciais de autenticação de sua conta e selecione **[!UICONTROL Conectar ao destino]**. <br> Consulte destino [do Amazon S3](/help/rtcdp/destinations/amazon-s3-destination.md) , destino do [Amazon Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md) , destino dos Hubs [do Evento do](/help/rtcdp/destinations/azure-event-hubs-destination.md) Azure e destino [SFTP](/help/rtcdp/destinations/sftp-destination.md) para obter detalhes sobre as credenciais inseridas na etapa **Autenticação** .

   >[!NOTE]
   >
   >O Adobe Real-time CDP oferece suporte à validação de credenciais no processo de autenticação e exibe uma mensagem de erro se você inserir credenciais incorretas no local do armazenamento na nuvem. Isso garante que você não conclua o fluxo de trabalho com credenciais incorretas.

   ![Conectar ao destino do armazenamento na nuvem - etapa de autenticação](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. Na etapa **[!UICONTROL Configuração]** , digite um **[!UICONTROL Nome]** e uma **[!UICONTROL Descrição]** para o fluxo de ativação. <br>
Para destinos do Amazon S3, insira o nome **[!UICONTROL do]** bucket e o caminho **[!UICONTROL da]** pasta no destino do armazenamento da nuvem onde os arquivos serão entregues. Selecione **[!UICONTROL Criar destino]** depois de preencher os campos acima.

   ![Conectar-se ao destino do armazenamento da nuvem do Amazon S3 - etapa de autenticação](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

   Para destinos SFTP, insira o caminho **[!UICONTROL da]** pasta onde os arquivos serão entregues.

   ![Conectar-se ao destino do armazenamento na nuvem SFTP - etapa de autenticação](/help/rtcdp/destinations/assets/sftp-destinations-setup-step.png)

4. Seu destino agora é criado. Você pode selecionar **[!UICONTROL Salvar e sair]** se quiser ativar segmentos posteriormente ou selecionar **[!UICONTROL Próximo]** para continuar o fluxo de trabalho e selecionar segmentos para ativar. Em ambos os casos, consulte a próxima seção, [Ativar segmentos](#activate-segments), para que o restante do fluxo de trabalho exporte dados.

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos em um destino](/help/rtcdp/destinations/activate-destinations.md) para obter informações sobre o fluxo de trabalho da ativação de segmentos.