---
title: Fluxo de trabalho de destinos de armazenamentos na nuvem
seo-title: Fluxo de trabalho de destinos de armazenamentos na nuvem
description: Instruções para conectar-se aos locais dos armazenamentos na nuvem
seo-description: Instruções para conectar-se aos locais dos armazenamentos na nuvem
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---


# Fluxo de trabalho para criar destinos de armazenamentos na nuvem

## Visão geral

Esta página explica como você pode se conectar aos locais do armazenamento em nuvem na Adobe Real-time Customer Data Platform.

1. Em **[!UICONTROL Conexões > Destinos]**, selecione o destino preferencial do armazenamento na nuvem e selecione o destino **[!UICONTROL do]** Connect.

   ![Conectar-se ao destino do armazenamento na nuvem](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. Na etapa **[!UICONTROL Autenticação]** , se você tiver configurado anteriormente uma conexão com o destino do armazenamento na nuvem, selecione Conta **** existente e selecione a conexão existente. Ou você pode selecionar **[!UICONTROL Nova conta]** para configurar uma nova conexão com o destino do armazenamento na nuvem. Preencha as credenciais de autenticação de sua conta e selecione **[!UICONTROL Conectar ao destino]**. <br> Consulte destino [do Amazon S3](/help/rtcdp/destinations/amazon-s3-destination.md) , [!DNL Amazon Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md) destino, [!DNL Azure Event Hubs](/help/rtcdp/destinations/azure-event-hubs-destination.md) destino e destino [SFTP](/help/rtcdp/destinations/sftp-destination.md) para obter detalhes sobre as credenciais inseridas na etapa **Autenticação** .

   >[!NOTE]
   >
   >O Adobe Real-time CDP oferece suporte à validação de credenciais no processo de autenticação e exibe uma mensagem de erro se você inserir credenciais incorretas no local do armazenamento na nuvem. Isso garante que você não conclua o fluxo de trabalho com credenciais incorretas.

   ![Conectar ao destino do armazenamento na nuvem - etapa de autenticação](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. Na etapa **[!UICONTROL Configuração]** , digite um **[!UICONTROL Nome]** e uma **[!UICONTROL Descrição]** para o fluxo de ativação. <br>
Também nesta etapa, você pode selecionar qualquer caso **[!UICONTROL de uso de]** Marketing que deve ser aplicado a este destino. Os casos de uso de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar entre casos de uso de marketing definidos pela Adobe ou criar seu próprio caso de uso de marketing. Para obter mais informações sobre casos de uso de marketing, consulte a página [Data Governance em CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) em tempo real. Para obter informações sobre casos individuais de uso de marketing definidos pela Adobe, consulte a visão geral [das políticas de uso de](/help/data-governance/policies/overview.md#core-actions)dados. <br>
Para destinos do Amazon S3, insira o nome **[!UICONTROL do]** bucket e o caminho **[!UICONTROL da]** pasta no destino do armazenamento da nuvem onde os arquivos serão entregues. Selecione **[!UICONTROL Criar destino]** depois de preencher os campos acima.

   ![Conectar-se ao destino do armazenamento da nuvem do Amazon S3 - etapa de autenticação](/help/rtcdp/destinations/assets/amazon-s3-setup-step.png)

   Para destinos SFTP, insira o caminho **[!UICONTROL da]** pasta onde os arquivos serão entregues. Selecione **[!UICONTROL Criar destino]** depois de preencher os campos acima.

   ![Conectar-se ao destino do armazenamento na nuvem SFTP - etapa de autenticação](/help/rtcdp/destinations/assets/sftp-destinations-setup-step.png)

   Para [!DNL Amazon Kinesis] destinos, forneça o nome do seu fluxo de dados existente em sua [!DNL Amazon Kinesis] conta. A CDP em tempo real da Adobe exportará dados para esse fluxo. Selecione **[!UICONTROL Criar destino]** depois de preencher os campos acima.

   ![Conectar-se ao destino do armazenamento na nuvem do Kinesis - etapa de autenticação](/help/rtcdp/destinations/assets/kinesis-destinations-setup-step.png)

   Para [!DNL Azure Event Hubs] destinos, forneça o nome do seu fluxo de dados existente em sua [!DNL Amazon Kinesis] conta. A CDP em tempo real da Adobe exportará dados para esse fluxo. Selecione **[!UICONTROL Criar destino]** depois de preencher os campos acima.

   ![Conectar-se ao destino do armazenamento na nuvem do Kinesis - etapa de autenticação](/help/rtcdp/destinations/assets/eventhubs-destinations-setup-step.png)

4. Seu destino agora é criado. Você pode selecionar **[!UICONTROL Salvar e sair]** se quiser ativar segmentos posteriormente ou selecionar **[!UICONTROL Próximo]** para continuar o fluxo de trabalho e selecionar segmentos para ativar. Em ambos os casos, consulte a próxima seção, [Ativar segmentos](#activate-segments), para que o restante do fluxo de trabalho exporte dados.

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos em um destino](/help/rtcdp/destinations/activate-destinations.md) para obter informações sobre o fluxo de trabalho da ativação de segmentos.