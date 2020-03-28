---
title: Adobe Campaign
seo-title: Adobe Campaign
description: O Adobe Campaign é um conjunto de soluções que o ajudam a personalizar e fornecer campanhas em todos os canais online e offline.
seo-description: O Adobe Campaign é um conjunto de soluções que o ajudam a personalizar e fornecer campanhas em todos os canais online e offline.
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# Adobe Campaign

## Visão geral

O Adobe Campaign é um conjunto de soluções que o ajudam a personalizar e fornecer campanhas em todos os canais online e offline. Consulte [Sobre o Adobe Campaign Classic](https://docs.adobe.com/content/help/en/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) para obter mais informações.

Para enviar dados de segmento para o Adobe Campaign, é necessário primeiro [conectar o destino](#connect-destination) na Plataforma de dados do cliente em tempo real da Adobe e [configurar uma importação](#import-data-into-campaign) de dados do local do armazenamento para o Adobe Campaign.

## Destino do Connect {#connect-destination}

1. Em **[!UICONTROL Connections > Destinations]**, selecione Adobe Campaign e, em seguida, selecione **[!UICONTROL Connect destination]**.

   ![Conectar-se à adobe campanha](/help/rtcdp/destinations/assets/connect-adobe-campaign.png)

1. No fluxo de trabalho de destino do Connect, selecione o local **[!UICONTROL Connection type]** do seu armazenamento. Para Adobe Campaign, você pode selecionar entre **[!UICONTROL Amazon S3]**, **[!UICONTROL SFTP with Password]** e **[!UICONTROL SFTP with SSH Key]**. Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Connect]**.

   ![Configurar o assistente de Campanhas](/help/rtcdp/destinations/assets/adobe-campaign-wizard.png)

   Para **[!UICONTROL Amazon S3]** conexões, você deve fornecer sua ID da chave de acesso e sua chave de acesso secreta.
Para **[!UICONTROL SFTP with Password]** conexões, você deve fornecer Domínio, Porta, Nome de usuário e Senha.
Para **[!UICONTROL SFTP with SSH Key]** conexões, você deve fornecer Domínio, Porta, Nome de usuário e Chave SSH.

   ![Preencher informações de Campanha](/help/rtcdp/destinations/assets/adobe-campaign-step2.png)

1. Em **[!UICONTROL Basic Information]**, preencha as informações relevantes para o seu destino, como mostrado abaixo:
   * **[!UICONTROL Name]**: Escolha um nome relevante para o seu destino.
   * **[!UICONTROL Description]**: Insira uma descrição para o seu destino.
   * **[!UICONTROL Bucket Name]**: *Para conexões* S3. Insira o local do bucket S3 no qual a CDP em tempo real depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
   * **[!UICONTROL Folder Path]**: Forneça o caminho no local do armazenamento onde a CDP em tempo real depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
   * **[!UICONTROL File Format]**: **CSV** ou **TAB_DELIMITED**. Selecione o formato de arquivo a ser exportado para o local do armazenamento.
   ![Informações básicas sobre Campanhas](/help/rtcdp/destinations/assets/adobe-campaign-basic-information.png)

1. Clique **[!UICONTROL Create]** depois de preencher os campos acima. Seu destino agora está conectado e você pode [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) no destino.

## Atributos de destino {#destination-attributes}

Ao [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) no destino do Adobe Campaign, recomendamos que você selecione um identificador exclusivo no schema [da](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)união. Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino. Para obter mais informações, consulte [Selecionar quais campos de schema usar como atributos de destino em seus arquivos](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportados em Destinos de marketing de email.


## Configurar importação de dados para o Adobe Campaign {#import-data-into-campaign}

Depois de conectar o CDP em tempo real ao seu armazenamento Amazon S3 ou SFTP, é necessário configurar a importação de dados do local do armazenamento para o Adobe Campaign. Para saber como fazer isso, consulte [Importação de dados](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) na documentação Ajuda do Adobe Campaign.