---
title: Destino Oracle Eloqua
seo-title: Destino Oracle Eloqua
description: O Oracle Eloqua é uma plataforma de software como serviço (SaaS) para automação de marketing oferecida pela Oracle que tem como objetivo ajudar os comerciantes e organizações B2B a gerenciar campanhas de marketing e geração de leads de vendas.
seo-description: O Oracle Eloqua é uma plataforma de software como serviço (SaaS) para automação de marketing oferecida pela Oracle que tem como objetivo ajudar os comerciantes e organizações B2B a gerenciar campanhas de marketing e geração de leads de vendas.
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Oracle Eloqua

## Visão geral

[A Eloqua](https://www.oracle.com/marketingcloud/products/marketing-automation/) é uma plataforma de software como serviço (SaaS) para automação de marketing oferecida pela Oracle que tem como objetivo ajudar os comerciantes e organizações B2B a gerenciar campanhas de marketing e geração de leads de vendas.

Para enviar dados de segmento para o Oracle Eloqua, é necessário primeiro [conectar o destino](#connect-destination) na Plataforma de Dados de Cliente em Tempo Real da Adobe e [configurar uma importação](#import-data-into-eloqua) de dados do local de armazenamento para o Oracle Eloqua.

## Conectar ao destino {#connect-destination}

1. Em **[!UICONTROL Connections > Destinations]**, selecione Oracle Eloqua e, em seguida, selecione **[!UICONTROL Connect destination]**.

   ![Ligar à Eloqua](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

1. No assistente de destino do Connect, selecione o local **[!UICONTROL Connection type]** de armazenamento. No Oracle Eloqua, você pode selecionar entre **SFTP com Senha** e **SFTP com Chave** SSH. Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Connect]**.

   ![Configurar o assistente Eloqua](/help/rtcdp/destinations/assets/eloqua-wizard.png)

   Para **SFTP com conexões de senha** , você deve fornecer Domínio, Porta, Nome de usuário e Senha.
Para **SFTP com conexões de chave** SSH, você deve fornecer Domínio, Porta, Nome de usuário e Chave SSH.

   ![Preencha as informações de Eloqua](/help/rtcdp/destinations/assets/eloqua-step2.png)

1. Em Informações **** básicas, preencha as informações relevantes para o seu destino, conforme mostrado abaixo:
   * **Nome**: Escolha um nome relevante para o seu destino.
   * **Descrição**: Insira uma descrição para o seu destino.
   * **Caminho** da pasta: Forneça o caminho no local de armazenamento onde a CDP em tempo real depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
   * **Formato** de arquivo: **CSV** ou **TAB_DELIMITED**. Selecione o formato de arquivo a ser exportado para o local de armazenamento.
   ![Informações básicas sobre o Eloqua](/help/rtcdp/destinations/assets/eloqua-basic-information.png)

1. Clique em **Criar** após preencher os campos em Informações **básicas**. Seu destino agora está conectado e você pode [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) no destino.

## Atributos de destino

Ao [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) para o destino Oracle Eloqua, recomendamos que você selecione um identificador exclusivo do esquema [de](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)união. Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino. Para obter mais informações, consulte [Selecionar quais campos de esquema usar como atributos de destino em seus arquivos](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportados em Destinos de marketing de email.

## Configurar importação de dados para o Oracle Eloqua {#import-data-into-eloqua}

Depois de conectar o CDP em tempo real ao armazenamento Amazon S3 ou SFTP, você deve configurar a importação de dados do local de armazenamento para o Oracle Eloqua. Para saber como fazer isso, consulte [Importando contatos ou contas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) no Centro de Ajuda do Oracle Eloqua.