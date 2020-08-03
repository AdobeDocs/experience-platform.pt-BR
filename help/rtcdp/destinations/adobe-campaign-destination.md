---
title: Adobe Campaign
seo-title: Adobe Campaign
description: O Adobe Campaign é um conjunto de soluções que o ajudam a personalizar e fornecer campanhas em todos os canais online e offline.
seo-description: O Adobe Campaign é um conjunto de soluções que o ajudam a personalizar e fornecer campanhas em todos os canais online e offline.
translation-type: tm+mt
source-git-commit: 570c627672439a5ee0f4215b7bf7915ec3dd2bb3
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 1%

---


# Adobe Campaign

## Visão geral

O Adobe Campaign é um conjunto de soluções que o ajudam a personalizar e fornecer campanhas em todos os canais online e offline. Consulte [Sobre o Adobe Campaign Classic](https://docs.adobe.com/content/help/en/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) para obter mais informações.

Para enviar dados de segmento para o Adobe Campaign, é necessário primeiro [conectar o destino](#connect-destination) no Adobe Real-time Customer Data Platform e [configurar uma importação](#import-data-into-campaign) de dados do local do armazenamento para o Adobe Campaign.

## Destino do Connect {#connect-destination}

1. Em **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]**, selecione Adobe Campaign e, em seguida, selecione destino **[!UICONTROL do]** Connect.

   ![Conectar-se à adobe campanha](/help/rtcdp/destinations/assets/connect-adobe-campaign.png)

1. No fluxo de trabalho de destino do Connect, selecione o tipo **[!UICONTROL de]** conexão para o local do armazenamento. Para o Adobe Campaign, você pode selecionar entre **[!UICONTROL Amazon S3]**, **[!UICONTROL SFTP com senha]** e **[!UICONTROL SFTP com chave]** SSH. Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Connect (Conectar]**).

   ![Configurar o assistente de Campanhas](/help/rtcdp/destinations/assets/adobe-campaign-wizard.png)

   Para conexões com o **[!UICONTROL Amazon S3]** , é necessário fornecer a ID da chave de acesso e a chave de acesso secreta.
Para **[!UICONTROL SFTP com conexões de senha]** , você deve fornecer Domínio, Porta, Nome de usuário e Senha.
Para **[!UICONTROL SFTP com conexões de chave]** SSH, você deve fornecer Domínio, Porta, Nome de usuário e Chave SSH.

   ![Preencher informações de Campanha](/help/rtcdp/destinations/assets/adobe-campaign-step2.png)

1. Em Informações **** básicas, preencha as informações relevantes para o seu destino, como mostrado abaixo:
   * **[!UICONTROL Nome]**: Escolha um nome relevante para o seu destino.
   * **[!UICONTROL Descrição]**: Insira uma descrição para o seu destino.
   * **[!UICONTROL Nome]** do grupo: *Para conexões* S3. Insira o local do bucket S3 no qual a CDP em tempo real depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
   * **[!UICONTROL Caminho]** da pasta: Forneça o caminho no local do armazenamento onde a CDP em tempo real depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
   * **[!UICONTROL Formato]** de arquivo: **CSV** ou **TAB_DELIMITED**. Selecione o formato de arquivo a ser exportado para o local do armazenamento.

   ![Informações básicas sobre Campanhas](/help/rtcdp/destinations/assets/adobe-campaign-basic-information.png)

1. Clique em **[!UICONTROL Criar]** após preencher os campos acima. Seu destino agora está conectado e você pode [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) no destino.

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos em um destino](/help/rtcdp/destinations/activate-destinations.md) para obter informações sobre o fluxo de trabalho da ativação de segmentos.

## Atributos de destino {#destination-attributes}

Ao [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) no destino do Adobe Campaign, recomendamos que você selecione um identificador exclusivo no schema [da](../../profile/home.md#profile-fragments-and-union-schemas)união. Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino. Para obter mais informações, consulte [Selecionar quais campos de schema usar como atributos de destino em seus arquivos](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportados em Destinos de marketing de email.

## Dados exportados {#exported-data}

Para [!DNL Adobe Campaign] destinos, o CDP Adobe em tempo real cria um arquivo delimitado por tabulação `.txt` ou `.csv` no local do armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte Destinos de marketing de [email e destinos](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) de armazenamentos da Cloud no tutorial de ativação de segmentos.

<!--

Expect a new file to be created in your storage location every day. The file format is:

`Adobe_Campaign_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
Adobe_Campaign_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Adobe_Campaign_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Adobe_Campaign_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->

## Configurar importação de dados para o Adobe Campaign {#import-data-into-campaign}

Depois de conectar o CDP em tempo real ao seu armazenamento [!DNL Amazon S3] ou SFTP, é necessário configurar a importação de dados do local do armazenamento para o Adobe Campaign. Para saber como fazer isso, consulte [Importação de dados](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) na documentação Ajuda do Adobe Campaign.