---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: O Salesforce Marketing Cloud é um conjunto de marketing digital conhecido anteriormente como ExactTarget que permite criar e personalizar viagens para visitantes e clientes para personalizar sua experiência.
seo-description: O Salesforce Marketing Cloud é um conjunto de marketing digital conhecido anteriormente como ExactTarget que permite criar e personalizar viagens para visitantes e clientes para personalizar sua experiência.
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Salesforce Marketing Cloud

## Visão geral

[O Salesforce Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/email-marketing/) é um conjunto de marketing digital conhecido anteriormente como ExactTarget que permite criar e personalizar viagens para visitantes e clientes para personalizar sua experiência.

Para enviar dados de segmento para a Salesforce Marketing Cloud, primeiro é necessário [conectar o destino](#connect-destination) na Adobe Real-time CDP e [configurar uma importação](#import-data-into-salesforce) de dados do local de armazenamento para a Salesforce Marketing Cloud.

## Destino do Connect {#connect-destination}

1. Em **[!UICONTROL Conexões > Destinos]**, selecione Salesforce Marketing Cloud e, em seguida, selecione o destino **[!UICONTROL do]** Connect.

   ![Conectar-se ao Salesforce](/help/rtcdp/destinations/assets/connect-salesforce.png)

1. No assistente de destino do Connect, selecione o tipo **[!UICONTROL de]** conexão para seu local de armazenamento. Para a Salesforce Marketing Cloud, você pode selecionar entre **SFTP com senha** e **SFTP com chave** SSH. Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Connect (Conectar]**).

   ![Configurar o assistente do Salesforce](/help/rtcdp/destinations/assets/salesforce-step1.png)

   Para **SFTP com conexões de senha** , você deve fornecer Domínio, Porta, Nome de usuário e Senha.
Para **SFTP com conexões de chave** SSH, você deve fornecer Domínio, Porta, Nome de usuário e Chave SSH.

   ![Preencha as informações do Salesforce](/help/rtcdp/destinations/assets/salesforce-wizard.png)

1. Em Informações **** básicas, preencha as informações relevantes para o seu destino, como mostrado abaixo:
   * **Nome**: Escolha um nome relevante para o seu destino.
   * **Descrição**: Insira uma descrição para o seu destino.
   * **Caminho** da pasta: Forneça o caminho no local de armazenamento onde a CDP em tempo real depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
   * **Formato** de arquivo: **CSV** ou **TAB_DELIMITED**. Selecione o formato de arquivo a ser exportado para o local de armazenamento.
   ![Informações básicas sobre o Salesforce](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

1. Clique em **Criar** após preencher os campos em Informações **básicas**. Seu destino agora está conectado e você pode [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) no destino.

## Atributos de destino {#destination-attributes}

Ao [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) no destino da Salesforce Marketing Cloud, recomendamos que você selecione um identificador exclusivo do esquema [de](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)união. Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino. Para obter mais informações, consulte [Selecionar quais campos de esquema usar como atributos de destino em seus arquivos](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportados em Destinos de marketing de email.

## Configurar a importação de dados para o Salesforce Marketing Cloud {#import-data-into-salesforce}

Depois de conectar o CDP em tempo real ao armazenamento Amazon S3 ou SFTP, é necessário configurar a importação de dados do local de armazenamento para o Salesforce Marketing Cloud. Para saber como fazer isso, consulte [Importar assinantes para a Marketing Cloud de um arquivo](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&type=5) no Centro de ajuda do Salesforce.