---
title: Destino Oracle Eloqua
seo-title: Destino Oracle Eloqua
description: O Oracle Eloqua é uma plataforma de software como serviço (SaaS) para automação de marketing oferecida pela Oracle que tem como objetivo ajudar os comerciantes e organizações B2B a gerenciar campanhas de marketing e geração de leads de vendas.
seo-description: O Oracle Eloqua é uma plataforma de software como serviço (SaaS) para automação de marketing oferecida pela Oracle que tem como objetivo ajudar os comerciantes e organizações B2B a gerenciar campanhas de marketing e geração de leads de vendas.
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# Oracle Eloqua

## Visão geral

[A Eloqua](https://www.oracle.com/marketingcloud/products/marketing-automation/) é uma plataforma de software como serviço (SaaS) para automação de marketing oferecida pela Oracle que tem como objetivo ajudar os comerciantes e organizações B2B a gerenciar campanhas de marketing e a geração de leads de vendas.

Para enviar dados de segmento para o Oracle Eloqua, é necessário primeiro [conectar o destino](#connect-destination) na Plataforma de Dados de Cliente em Tempo Real da Adobe e [configurar uma importação](#import-data-into-eloqua) de dados da localização do armazenamento para o Oracle Eloqua.

## Conectar ao destino {#connect-destination}

1. Em **[!UICONTROL Connections > Destinations]**, selecione Oracle Eloqua e, em seguida, selecione **[!UICONTROL Connect destination]**.

   ![Ligar à Eloqua](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

2. Na **[!UICONTROL Authentication]** etapa, se você tiver configurado anteriormente uma conexão com o destino do armazenamento na nuvem, selecione **[!UICONTROL Existing Account]** e selecione uma de suas conexões existentes. Ou você pode selecionar **[!UICONTROL New Account]** configurar uma nova conexão. Preencha as credenciais de autenticação da sua conta e selecione **[!UICONTROL Connect to destination]**. Para o Oracle Eloqua, você pode selecionar entre **[!UICONTROL SFTP with Password]** e **[!UICONTROL SFTP with SSH Key]**. Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Connect to destination]**.

   Para **[!UICONTROL SFTP with Password]** conexões, você deve fornecer Domínio, Porta, Nome de usuário e Senha.
Para **[!UICONTROL SFTP with SSH Key]** conexões, você deve fornecer Domínio, Porta, Nome de usuário e Chave SSH.

   ![Configurar o assistente Eloqua](/help/rtcdp/destinations/assets/eloqua-authentication.png)

3. Na **[!UICONTROL Setup]** etapa, preencha as informações relevantes para o seu destino, conforme mostrado abaixo:
   * **[!UICONTROL Name]**: Escolha um nome relevante para o seu destino.
   * **[!UICONTROL Description]**: Insira uma descrição para o seu destino.
   * **[!UICONTROL Folder Path]**: Forneça o caminho no local do armazenamento onde a CDP em tempo real depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
   * **[!UICONTROL File Format]**: **CSV** ou **TAB_DELIMITED**. Selecione o formato de arquivo a ser exportado para o local do armazenamento.
   ![Informações básicas sobre o Eloqua](/help/rtcdp/destinations/assets/eloqua-basic-information.png)

4. Clique **[!UICONTROL Create destination]** depois de preencher os campos acima. Seu destino agora é criado e você pode [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) no destino.

## Atributos de destino

Ao [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) para o destino Oracle Eloqua, recomendamos que você selecione um identificador exclusivo do seu schema [de](../../profile/home.md#profile-fragments-and-union-schemas)união. Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino. Para obter mais informações, consulte [Selecionar quais campos de schema usar como atributos de destino em seus arquivos](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportados em Destinos de marketing de email.

## Configurar importação de dados para o Oracle Eloqua {#import-data-into-eloqua}

Depois de conectar o CDP em tempo real ao seu armazenamento Amazon S3 ou SFTP, você deve configurar a importação de dados do local do armazenamento para o Oracle Eloqua. Para saber como fazer isso, consulte [Importando contatos ou contas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) no Centro de Ajuda do Oracle Eloqua.