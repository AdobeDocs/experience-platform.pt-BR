---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: O Salesforce Marketing Cloud é um conjunto de marketing digital conhecido anteriormente como ExactTarget que permite criar e personalizar viagens para visitantes e clientes para personalizar sua experiência.
seo-description: O Salesforce Marketing Cloud é um conjunto de marketing digital conhecido anteriormente como ExactTarget que permite criar e personalizar viagens para visitantes e clientes para personalizar sua experiência.
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# Salesforce Marketing Cloud

## Visão geral

[O Salesforce Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/email-marketing/) é um conjunto de marketing digital conhecido anteriormente como ExactTarget que permite criar e personalizar viagens para visitantes e clientes para personalizar sua experiência.

Para enviar dados de segmento para a Salesforce Marketing Cloud, primeiro é necessário [conectar o destino](#connect-destination) na Adobe Real-time CDP e [configurar uma importação](#import-data-into-salesforce) de dados da localização do armazenamento para a Salesforce Marketing Cloud.

## Destino do Connect {#connect-destination}

1. Em **[!UICONTROL Connections > Destinations]**, selecione Salesforce Marketing Cloud e, em seguida, selecione **[!UICONTROL Connect destination]**.

   ![Conectar-se ao Salesforce](/help/rtcdp/destinations/assets/connect-salesforce.png)

2. Na **[!UICONTROL Authentication]** etapa, se você tiver configurado anteriormente uma conexão com o destino do armazenamento na nuvem, selecione **[!UICONTROL Existing Account]** e selecione uma de suas conexões existentes. Ou você pode selecionar **[!UICONTROL New Account]** configurar uma nova conexão. Preencha as credenciais de autenticação da sua conta e selecione **[!UICONTROL Connect to destination]**. Para o Salesforce Marketing Cloud, você pode selecionar entre **[!UICONTROL SFTP with Password]** e **[!UICONTROL SFTP with SSH Key]**. Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Connect to destination]**.

   Para **[!UICONTROL SFTP with Password]** conexões, você deve fornecer Domínio, Porta, Nome de usuário e Senha.
Para **[!UICONTROL SFTP with SSH Key]** conexões, você deve fornecer Domínio, Porta, Nome de usuário e Chave SSH.

   ![Preencha as informações do Salesforce](/help/rtcdp/destinations/assets/salesforce-authenticate.png)

3. Na **[!UICONTROL Setup]** etapa, preencha as informações relevantes para o seu destino, conforme mostrado abaixo:
   * **[!UICONTROL Name]**: Escolha um nome relevante para o seu destino.
   * **[!UICONTROL Description]**: Insira uma descrição para o seu destino.
   * **[!UICONTROL Folder Path]**: Forneça o caminho no local do armazenamento onde a CDP em tempo real depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
   * **[!UICONTROL File Format]**: **[!UICONTROL CSV]** ou **[!UICONTROL TAB_DELIMITED]**. Selecione o formato de arquivo a ser exportado para o local do armazenamento.
   ![Informações básicas sobre o Salesforce](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

4. Clique **[!UICONTROL Create destination]** depois de preencher os campos acima. Seu destino agora está conectado e você pode [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) no destino.

## Atributos de destino {#destination-attributes}

Ao [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) no destino da Salesforce Marketing Cloud, recomendamos que você selecione um identificador exclusivo do seu schema [de](../../profile/home.md#profile-fragments-and-union-schemas)união. Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino. Para obter mais informações, consulte [Selecionar quais campos de schema usar como atributos de destino em seus arquivos](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportados em Destinos de marketing de email.

## Configurar a importação de dados para o Salesforce Marketing Cloud {#import-data-into-salesforce}

Depois de conectar o CDP em tempo real ao seu armazenamento Amazon S3 ou SFTP, é necessário configurar a importação de dados do local do armazenamento para o Salesforce Marketing Cloud. Para saber como fazer isso, consulte [Importar assinantes para a Marketing Cloud de um arquivo](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&type=5) no Centro de ajuda do Salesforce.