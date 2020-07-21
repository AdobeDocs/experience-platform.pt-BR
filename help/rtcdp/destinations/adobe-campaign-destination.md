---
title: Adobe Campaign
seo-title: Adobe Campaign
description: O Adobe Campaign é um conjunto de soluções que o ajudam a personalizar e fornecer campanhas em todos os canais online e offline.
seo-description: O Adobe Campaign é um conjunto de soluções que o ajudam a personalizar e fornecer campanhas em todos os canais online e offline.
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---


# Adobe Campaign

## Visão geral

O Adobe Campaign é um conjunto de soluções que o ajudam a personalizar e fornecer campanhas em todos os canais online e offline. Consulte [Sobre o Adobe Campaign Classic](https://docs.adobe.com/content/help/en/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) para obter mais informações.

Para enviar dados de segmento para o Adobe Campaign, é necessário primeiro [conectar o destino](#connect-destination) na Adobe Real-time Customer Data Platform e [configurar uma importação](#import-data-into-campaign) de dados do local do armazenamento para o Adobe Campaign.

## Destino do Connect {#connect-destination}

1. Em **[!UICONTROL Conexões > Destinos]**, selecione Adobe Campaign e, em seguida, selecione destino **[!UICONTROL do]** Connect.

   ![Conectar-se à adobe campanha](/help/rtcdp/destinations/assets/connect-adobe-campaign.png)

1. No fluxo de trabalho de destino do Connect, selecione o tipo **[!UICONTROL de]** conexão para o local do armazenamento. Para o Adobe Campaign, você pode selecionar entre **[!UICONTROL Amazon S3]**, **[!UICONTROL SFTP com senha]** e **[!UICONTROL SFTP com chave]** SSH. Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Connect (Conectar]**).

   ![Configurar o assistente de Campanhas](/help/rtcdp/destinations/assets/adobe-campaign-wizard.png)

   Para conexões **[!UICONTROL Amazon S3]** , você deve fornecer sua ID da chave de acesso e chave de acesso secreta.
Para **[!UICONTROL SFTP com conexões de senha]** , você deve fornecer Domínio, Porta, Nome de usuário e Senha.
Para **[!UICONTROL SFTP com conexões de chave]** SSH, você deve fornecer Domínio, Porta, Nome de usuário e Chave SSH.

   ![Preencher informações de Campanha](/help/rtcdp/destinations/assets/adobe-campaign-step2.png)

1. Em Informações **** básicas, preencha as informações relevantes para o seu destino, como mostrado abaixo:
   * **[!UICONTROL Nome]**: Escolha um nome relevante para o seu destino.
   * **[!UICONTROL Descrição]**: Insira uma descrição para o seu destino.
   * **[!UICONTROL Nome]** do grupo: *Para conexões* S3. Insira o local do bucket S3 no qual a CDP em tempo real depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
   * **[!UICONTROL Caminho]** da pasta: Forneça o caminho no local do armazenamento onde a CDP em tempo real depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
   * **[!UICONTROL Formato]** de arquivo: **CSV** ou **TAB_DELIMITED**. Selecione o formato de arquivo a ser exportado para o local do armazenamento.

   ![Informações básicas sobre Campanhas](/help/rtcdp/destinations/assets/adobe-campaign-basic-information.png)

1. Clique em **[!UICONTROL Criar]** após preencher os campos acima. Seu destino agora está conectado e você pode [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) no destino.

## Atributos de destino {#destination-attributes}

Ao [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) no destino do Adobe Campaign, recomendamos que você selecione um identificador exclusivo no schema [da](../../profile/home.md#profile-fragments-and-union-schemas)união. Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino. Para obter mais informações, consulte [Selecionar quais campos de schema usar como atributos de destino em seus arquivos](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportados em Destinos de marketing de email.


## Configurar importação de dados para o Adobe Campaign {#import-data-into-campaign}

Depois de conectar o CDP em tempo real ao seu armazenamento [!DNL Amazon S3] ou SFTP, é necessário configurar a importação de dados do local do armazenamento para o Adobe Campaign. Para saber como fazer isso, consulte [Importação de dados](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) na documentação Ajuda do Adobe Campaign.