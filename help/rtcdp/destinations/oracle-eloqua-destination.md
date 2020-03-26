---
title: Destino Oracle Eloqua
seo-title: Destino Oracle Eloqua
description: O Oracle Eloqua é uma plataforma de software como serviço (SaaS) para automação de marketing oferecida pela Oracle que tem como objetivo ajudar os comerciantes e organizações B2B a gerenciar campanhas de marketing e geração de leads de vendas.
seo-description: O Oracle Eloqua é uma plataforma de software como serviço (SaaS) para automação de marketing oferecida pela Oracle que tem como objetivo ajudar os comerciantes e organizações B2B a gerenciar campanhas de marketing e geração de leads de vendas.
translation-type: tm+mt
source-git-commit: c3fe5753fb23f99076f9c85b4e07af2d25a121a9

---


# Oracle Eloqua

## Visão geral

[A Eloqua](https://www.oracle.com/marketingcloud/products/marketing-automation/) é uma plataforma de software como serviço (SaaS) para automação de marketing oferecida pela Oracle que tem como objetivo ajudar os comerciantes e organizações B2B a gerenciar campanhas de marketing e a geração de leads de vendas.

Para enviar dados de segmento para o Oracle Eloqua, é necessário primeiro [conectar o destino](#connect-destination) na Plataforma de Dados de Cliente em Tempo Real da Adobe e [configurar uma importação](#import-data-into-eloqua) de dados da localização do armazenamento para o Oracle Eloqua.

## Conectar ao destino {#connect-destination}

1. Em **[!UICONTROL Connections > Destinations]**, selecione Oracle Eloqua e, em seguida, selecione **[!UICONTROL Connect destination]**.

   ![Ligar à Eloqua](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

2. Na etapa **Autenticação** , se você tiver configurado anteriormente uma conexão com o destino do armazenamento na nuvem, selecione **[!UICONTROL Existing Account]** e selecione uma de suas conexões existentes. Ou você pode selecionar **[!UICONTROL New Account]** configurar uma nova conexão. Preencha as credenciais de autenticação da sua conta e selecione **[!UICONTROL Connect to destination]**. No Oracle Eloqua, você pode selecionar entre **SFTP com Senha** e **SFTP com Chave** SSH. Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Connect to destination]**.

   Para **SFTP com conexões de senha** , você deve fornecer Domínio, Porta, Nome de usuário e Senha.
Para **SFTP com conexões de chave** SSH, você deve fornecer Domínio, Porta, Nome de usuário e Chave SSH.

   ![Configurar o assistente Eloqua](/help/rtcdp/destinations/assets/eloqua-authentication.png)

3. Na etapa **de configuração** , preencha as informações relevantes para seu destino, conforme mostrado abaixo:
   * **Nome**: Escolha um nome relevante para o seu destino.
   * **Descrição**: Insira uma descrição para o seu destino.
   * **Caminho** da pasta: Forneça o caminho no local do armazenamento onde a CDP em tempo real depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
   * **Formato** de arquivo: **CSV** ou **TAB_DELIMITED**. Selecione o formato de arquivo a ser exportado para o local do armazenamento.
   ![Informações básicas sobre o Eloqua](/help/rtcdp/destinations/assets/eloqua-basic-information.png)

4. Clique em **Criar destino** após preencher os campos acima. Seu destino agora é criado e você pode [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) no destino.

## Atributos de destino

Ao [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) para o destino Oracle Eloqua, recomendamos que você selecione um identificador exclusivo do seu schema [de](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)união. Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino. Para obter mais informações, consulte [Selecionar quais campos de schema usar como atributos de destino em seus arquivos](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportados em Destinos de marketing de email.

## Configurar importação de dados para o Oracle Eloqua {#import-data-into-eloqua}

Depois de conectar o CDP em tempo real ao seu armazenamento Amazon S3 ou SFTP, você deve configurar a importação de dados do local do armazenamento para o Oracle Eloqua. Para saber como fazer isso, consulte [Importando contatos ou contas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) no Centro de Ajuda do Oracle Eloqua.