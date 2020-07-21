---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: O Salesforce Marketing Cloud é um conjunto de marketing digital conhecido anteriormente como ExactTarget que permite criar e personalizar viagens para visitantes e clientes para personalizar sua experiência.
seo-description: O Salesforce Marketing Cloud é um conjunto de marketing digital conhecido anteriormente como ExactTarget que permite criar e personalizar viagens para visitantes e clientes para personalizar sua experiência.
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---


# [!DNL Salesforce Marketing Cloud]

## Visão geral

[!DNL Salesforce Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/email-marketing/) é um conjunto de marketing digital conhecido anteriormente como ExactTarget que permite criar e personalizar viagens para visitantes e clientes para personalizar sua experiência.

Para enviar dados de segmento para [!DNL Salesforce Marketing Cloud], é necessário primeiro [conectar o destino](#connect-destination) na CDP em tempo real da Adobe e [configurar uma importação](#import-data-into-salesforce) de dados do local do armazenamento para [!DNL Salesforce Marketing Cloud].

## Destino do Connect {#connect-destination}

1. Em **[!UICONTROL Conexões > Destinos]**, selecione [!DNL Salesforce Marketing Cloud]e, em seguida, selecione destino **[!UICONTROL do]** Connect.

   ![Conectar-se ao Salesforce](/help/rtcdp/destinations/assets/connect-salesforce.png)

2. Na etapa **[!UICONTROL Autenticação]** , se você tiver configurado anteriormente uma conexão com o destino do armazenamento na nuvem, selecione Conta **** existente e selecione uma de suas conexões existentes. Ou você pode selecionar **[!UICONTROL Nova conta]** para configurar uma nova conexão. Preencha as credenciais de autenticação de sua conta e selecione **[!UICONTROL Conectar ao destino]**. Para [!DNL Salesforce Marketing Cloud], você pode selecionar entre **[!UICONTROL SFTP com senha]** e **[!UICONTROL SFTP com chave]** SSH. Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Conectar-se ao destino]**.

   Para **[!UICONTROL SFTP com conexões de senha]** , você deve fornecer Domínio, Porta, Nome de usuário e Senha.
Para **[!UICONTROL SFTP com conexões de chave]** SSH, você deve fornecer Domínio, Porta, Nome de usuário e Chave SSH.

   ![Preencha as informações do Salesforce](/help/rtcdp/destinations/assets/salesforce-authenticate.png)

3. Na etapa **[!UICONTROL de configuração]** , preencha as informações relevantes para seu destino, conforme mostrado abaixo:
   * **[!UICONTROL Nome]**: Escolha um nome relevante para o seu destino.
   * **[!UICONTROL Descrição]**: Insira uma descrição para o seu destino.
   * **[!UICONTROL Caminho]** da pasta: Forneça o caminho no local do armazenamento onde a CDP em tempo real depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
   * **[!UICONTROL Formato]** de arquivo: **[!UICONTROL CSV]** ou **[!UICONTROL TAB_DELIMITED]**. Selecione o formato de arquivo a ser exportado para o local do armazenamento.

   ![Informações básicas sobre o Salesforce](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

4. Clique em **[!UICONTROL Criar destino]** após preencher os campos acima. Seu destino agora está conectado e você pode [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) no destino.

## Atributos de destino {#destination-attributes}

Ao [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) para o [!DNL Salesforce Marketing Cloud] destino, recomendamos que você selecione um identificador exclusivo do seu schema [de](../../profile/home.md#profile-fragments-and-union-schemas)união. Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino. Para obter mais informações, consulte [Selecionar quais campos de schema usar como atributos de destino em seus arquivos](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportados em Destinos de marketing de email.

## Configurar importação de dados em [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

Depois de conectar o CDP em tempo real ao seu armazenamento Amazon S3 ou SFTP, você deve configurar a importação de dados do local do armazenamento para [!DNL Salesforce Marketing Cloud]. Para saber como fazer isso, consulte [Importar assinantes para a Marketing Cloud de um arquivo](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) no [!DNL Salesforce Help Center].