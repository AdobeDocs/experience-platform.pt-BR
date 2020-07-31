---
title: Destino Oracle Eloqua
seo-title: Destino Oracle Eloqua
description: O Oracle Eloqua é uma plataforma de software como serviço (SaaS) para automação de marketing oferecida pela Oracle que tem como objetivo ajudar os comerciantes e organizações B2B a gerenciar campanhas de marketing e geração de leads de vendas.
seo-description: O Oracle Eloqua é uma plataforma de software como serviço (SaaS) para automação de marketing oferecida pela Oracle que tem como objetivo ajudar os comerciantes e organizações B2B a gerenciar campanhas de marketing e geração de leads de vendas.
translation-type: tm+mt
source-git-commit: 098dd31be4d6ee6971cd87bcbfe0f686e34918e1
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---


# [!DNL Oracle Eloqua]

## Visão geral

[A Eloqua](https://www.oracle.com/marketingcloud/products/marketing-automation/) é uma plataforma de software como serviço (SaaS) para automação de marketing oferecida por [!DNL Oracle] ela, que tem como objetivo ajudar os comerciantes e organizações B2B a gerenciar campanhas de marketing e a geração de leads de vendas.

Para enviar dados de segmento para [!DNL Oracle Eloqua], é necessário primeiro [conectar o destino](#connect-destination) na Adobe Real-time Customer Data Platform e [configurar uma importação](#import-data-into-eloqua) de dados do local do armazenamento para [!DNL Oracle Eloqua].

## Conectar ao destino {#connect-destination}

1. Em **[!UICONTROL Conexões > Destinos]**, selecione [!DNL Oracle Eloqua]e, em seguida, selecione destino **[!UICONTROL do]** Connect.

   ![Ligar à Eloqua](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

2. Na etapa **[!UICONTROL Autenticação]** , se você tiver configurado anteriormente uma conexão com o destino do armazenamento na nuvem, selecione Conta **** existente e selecione uma de suas conexões existentes. Ou você pode selecionar **[!UICONTROL Nova conta]** para configurar uma nova conexão. Preencha as credenciais de autenticação de sua conta e selecione **[!UICONTROL Conectar ao destino]**. Para [!DNL Oracle Eloqua], você pode selecionar entre **[!UICONTROL SFTP com senha]** e **[!UICONTROL SFTP com chave]** SSH. Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Conectar-se ao destino]**.

   Para **[!UICONTROL SFTP com conexões de senha]** , você deve fornecer Domínio, Porta, Nome de usuário e Senha.
Para **[!UICONTROL SFTP com conexões de chave]** SSH, você deve fornecer Domínio, Porta, Nome de usuário e Chave SSH.

   ![Configurar o assistente Eloqua](/help/rtcdp/destinations/assets/eloqua-authentication.png)

3. Na etapa **[!UICONTROL de configuração]** , preencha as informações relevantes para seu destino, conforme mostrado abaixo:
   * **[!UICONTROL Nome]**: Escolha um nome relevante para o seu destino.
   * **[!UICONTROL Descrição]**: Insira uma descrição para o seu destino.
   * **[!UICONTROL Caminho]** da pasta: Forneça o caminho no local do armazenamento onde a CDP em tempo real depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
   * **[!UICONTROL Formato]** de arquivo: **CSV** ou **TAB_DELIMITED**. Selecione o formato de arquivo a ser exportado para o local do armazenamento.

   ![Informações básicas sobre o Eloqua](/help/rtcdp/destinations/assets/eloqua-basic-information.png)

4. Clique em **[!UICONTROL Criar destino]** após preencher os campos acima. Seu destino agora é criado e você pode [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) no destino.

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos em um destino](/help/rtcdp/destinations/activate-destinations.md) para obter informações sobre o fluxo de trabalho da ativação de segmentos.

## Atributos de destino {#destination-attributes}

Ao [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) para o [!DNL Oracle Eloqua] destino, recomendamos que você selecione um identificador exclusivo do seu schema [de](../../profile/home.md#profile-fragments-and-union-schemas)união. Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino. Para obter mais informações, consulte [Selecionar quais campos de schema usar como atributos de destino em seus arquivos](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportados em Destinos de marketing de email.

## Dados exportados {#exported-data}

Para [!DNL Oracle Eloqua] destinos, o CDP Adobe em tempo real cria um arquivo delimitado por tabulação `.txt` ou `.csv` no local do armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte Destinos de marketing de [email e destinos](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) de armazenamentos da Cloud no tutorial de ativação de segmentos.

<!--

Expect a new file to be created in your storage location every day. The file format is:

`Oracle_Eloqua_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
Oracle_Eloqua_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Oracle_Eloqua_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Oracle_Eloqua_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->

## Configurar importação de dados em [!DNL Oracle Eloqua] {#import-data-into-eloqua}

Depois de conectar o CDP em tempo real ao seu armazenamento Amazon S3 ou SFTP, você deve configurar a importação de dados do local do armazenamento para [!DNL Oracle Eloqua]. Para saber como fazer isso, consulte [Importar contatos ou contas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) no [!DNL Oracle Eloqua Help Center].