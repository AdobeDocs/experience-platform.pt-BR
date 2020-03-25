---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: O Salesforce Marketing Cloud é um conjunto de marketing digital conhecido anteriormente como ExactTarget que permite criar e personalizar viagens para visitantes e clientes para personalizar sua experiência.
seo-description: O Salesforce Marketing Cloud é um conjunto de marketing digital conhecido anteriormente como ExactTarget que permite criar e personalizar viagens para visitantes e clientes para personalizar sua experiência.
translation-type: tm+mt
source-git-commit: afe8032be1d96a63a3d43c5a552a0d6152e14552

---


# Salesforce Marketing Cloud

## Visão geral

[O Salesforce Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/email-marketing/) é um conjunto de marketing digital conhecido anteriormente como ExactTarget que permite criar e personalizar viagens para visitantes e clientes para personalizar sua experiência.

Para enviar dados de segmento para a Salesforce Marketing Cloud, primeiro é necessário [conectar o destino](#connect-destination) na Adobe Real-time CDP e [configurar uma importação](#import-data-into-salesforce) de dados da localização do armazenamento para a Salesforce Marketing Cloud.

## Destino do Connect {#connect-destination}

1. Em **[!UICONTROL Connections > Destinations]**, selecione Salesforce Marketing Cloud e, em seguida, selecione **[!UICONTROL Connect destination]**.

   ![Conectar-se ao Salesforce](/help/rtcdp/destinations/assets/connect-salesforce.png)

1. Na etapa **Autenticação** , se você tiver configurado anteriormente uma conexão com o destino do armazenamento na nuvem, selecione **[!UICONTROL Existing Account]** e selecione a conexão existente. Ou você pode selecionar **[!UICONTROL New Account]** configurar uma nova conexão. Preencha as credenciais de autenticação da sua conta e selecione **[!UICONTROL Connect to destination]**. Para a Salesforce Marketing Cloud, você pode selecionar entre **SFTP com senha** e **SFTP com chave** SSH. Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Connect to destination]**.

   Para **SFTP com conexões de senha** , você deve fornecer Domínio, Porta, Nome de usuário e Senha.
Para **SFTP com conexões de chave** SSH, você deve fornecer Domínio, Porta, Nome de usuário e Chave SSH.

   ![Preencha as informações do Salesforce](/help/rtcdp/destinations/assets/salesforce-authenticate.png)

1. Na etapa **de configuração** , preencha as informações relevantes para seu destino, conforme mostrado abaixo:
   * **Nome**: Escolha um nome relevante para o seu destino.
   * **Descrição**: Insira uma descrição para o seu destino.
   * **Caminho** da pasta: Forneça o caminho no local do armazenamento onde a CDP em tempo real depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
   * **Formato** de arquivo: **CSV** ou **TAB_DELIMITED**. Selecione o formato de arquivo a ser exportado para o local do armazenamento.
   ![Informações básicas sobre o Salesforce](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

1. Clique em **Criar destino** após preencher os campos em Informações **básicas**. Seu destino agora está conectado e você pode [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) no destino.

## Atributos de destino {#destination-attributes}

Ao [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) no destino da Salesforce Marketing Cloud, recomendamos que você selecione um identificador exclusivo do seu schema [de](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)união. Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino. Para obter mais informações, consulte [Selecionar quais campos de schema usar como atributos de destino em seus arquivos](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportados em Destinos de marketing de email.

## Configurar a importação de dados para o Salesforce Marketing Cloud {#import-data-into-salesforce}

Depois de conectar o CDP em tempo real ao seu armazenamento Amazon S3 ou SFTP, é necessário configurar a importação de dados do local do armazenamento para o Salesforce Marketing Cloud. Para saber como fazer isso, consulte [Importar assinantes para a Marketing Cloud de um arquivo](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&type=5) no Centro de ajuda do Salesforce.