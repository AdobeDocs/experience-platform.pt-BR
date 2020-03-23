---
title: Adobe Campaign
seo-title: Adobe Campaign
description: O Adobe Campaign é um conjunto de soluções que ajudam a personalizar e fornecer campanhas em todos os canais online e offline.
seo-description: O Adobe Campaign é um conjunto de soluções que ajudam a personalizar e fornecer campanhas em todos os canais online e offline.
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Adobe Campaign

## Visão geral

O Adobe Campaign é um conjunto de soluções que ajudam a personalizar e fornecer campanhas em todos os canais online e offline. Consulte [Sobre o Adobe Campaign Classic](https://docs.adobe.com/content/help/en/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) para obter mais informações.

Para enviar dados de segmento para o Adobe Campaign, primeiro é necessário [conectar o destino](#connect-destination) na Plataforma de dados do cliente em tempo real da Adobe e [configurar uma importação](#import-data-into-campaign) de dados do local de armazenamento para o Adobe Campaign.

## Destino do Connect {#connect-destination}

1. Em **[!UICONTROL Connections > Destinations]**, selecione Adobe Campaign e, em seguida, selecione **[!UICONTROL Connect destination]**.

   ![Conectar-se à campanha da Adobe](/help/rtcdp/destinations/assets/connect-adobe-campaign.png)

1. No assistente de destino do Connect, selecione o local **[!UICONTROL Connection type]** de armazenamento. Para o Adobe Campaign, você pode selecionar entre **Amazon S3**, **SFTP com senha** e **SFTP com chave** SSH. Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Connect]**.

   ![Configurar o assistente de campanha](/help/rtcdp/destinations/assets/adobe-campaign-wizard.png)

   Para conexões **S3** , é necessário fornecer a ID da chave de acesso e a chave de acesso secreta.
Para **SFTP com conexões de senha** , você deve fornecer Domínio, Porta, Nome de usuário e Senha.
Para **SFTP com conexões de chave** SSH, você deve fornecer Domínio, Porta, Nome de usuário e Chave SSH.

   ![Preencha as informações da campanha](/help/rtcdp/destinations/assets/adobe-campaign-step2.png)

1. Em Informações **** básicas, preencha as informações relevantes para o seu destino, como mostrado abaixo:
   * **Nome**: Escolha um nome relevante para o seu destino.
   * **Descrição**: Insira uma descrição para o seu destino.
   * **Nome** do grupo: *Para conexões* S3. Insira o local do bucket S3 no qual a CDP em tempo real depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
   * **Caminho** da pasta: Forneça o caminho no local de armazenamento onde a CDP em tempo real depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
   * **Formato** de arquivo: **CSV** ou **TAB_DELIMITED**. Selecione o formato de arquivo a ser exportado para o local de armazenamento.
   ![Informações básicas da campanha](/help/rtcdp/destinations/assets/adobe-campaign-basic-information.png)

1. Clique em **Criar** após preencher os campos em Informações **básicas**. Seu destino agora está conectado e você pode [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) no destino.

## Atributos de destino {#destination-attributes}

Ao [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) no destino do Adobe Campaign, recomendamos que você selecione um identificador exclusivo do esquema [de](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)união. Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino. Para obter mais informações, consulte [Selecionar quais campos de esquema usar como atributos de destino em seus arquivos](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportados em Destinos de marketing de email.


## Configurar importação de dados para o Adobe Campaign {#import-data-into-campaign}

Depois de conectar o CDP em tempo real ao armazenamento Amazon S3 ou SFTP, é necessário configurar a importação de dados do local de armazenamento para o Adobe Campaign. Para saber como fazer isso, consulte [Importação de dados](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) na documentação da Ajuda do Adobe Campaign.