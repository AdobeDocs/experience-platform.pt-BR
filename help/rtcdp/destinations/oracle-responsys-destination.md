---
keywords: email;Email;e-mail;email destinations;oracle responsys destination
title: Destino do Oracle Responsys
seo-title: Destino do Oracle Responsys
description: A Responsys é uma ferramenta de marketing por email corporativo para campanhas de marketing entre canais oferecida pela Oracle para personalizar interações entre email, dispositivos móveis, exibição e redes sociais.
seo-description: A Responsys é uma ferramenta de marketing por email corporativo para campanhas de marketing entre canais oferecida pela Oracle para personalizar interações entre email, dispositivos móveis, exibição e redes sociais.
translation-type: tm+mt
source-git-commit: 15323134f0c626cad2c4e90b3e1c0662cf7e57dd
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---


# [!DNL Oracle Responsys]

## Visão geral

[A Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) é uma ferramenta de marketing por email empresarial para campanhas de marketing entre canais, oferecida pela [!DNL Oracle] para personalizar interações entre email, dispositivos móveis, vídeos e redes sociais.

Para enviar dados de segmento para [!DNL Oracle Responsys], é necessário primeiro [conectar-se ao destino](#connect-destination) na Plataforma de dados do cliente em tempo real do Adobe e [configurar uma importação](#import-data-into-responsys) de dados do local do armazenamento para [!DNL Oracle Responsys].

## Destino do Connect {#connect-destination}

1. Em **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]**, selecione [!DNL Oracle Responsys]e, em seguida, selecione o destino **[!UICONTROL do]** Connect.

   ![Conectar-se ao Responsys](/help/rtcdp/destinations/assets/connect-oracle-responsys.png)

2. Na etapa **[!UICONTROL Autenticação]** , se você tiver configurado anteriormente uma conexão com o destino do armazenamento na nuvem, selecione Conta **** existente e selecione uma de suas conexões existentes. Ou você pode selecionar **[!UICONTROL Nova conta]** para configurar uma nova conexão. Preencha as credenciais de autenticação de sua conta e selecione **[!UICONTROL Conectar ao destino]**. Para [!DNL Oracle Responsys], você pode selecionar entre **[!UICONTROL SFTP com senha]** e **[!UICONTROL SFTP com chave]** SSH. Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Conectar-se ao destino]**.

   Para **[!UICONTROL SFTP com conexões de senha]** , você deve fornecer Domínio, Porta, Nome de usuário e Senha.
Para **[!UICONTROL SFTP com conexões de chave]** SSH, você deve fornecer Domínio, Porta, Nome de usuário e Chave SSH.

   ![Preencha as informações do Responsys](/help/rtcdp/destinations/assets/responsys-authentication.png)

3. Na etapa **[!UICONTROL de configuração]** , preencha as informações relevantes para seu destino, conforme mostrado abaixo:
   * **[!UICONTROL Nome]**: Escolha um nome relevante para o seu destino.
   * **[!UICONTROL Descrição]**: Insira uma descrição para o seu destino.
   * **[!UICONTROL Caminho]** da pasta: Forneça o caminho no local do armazenamento onde a CDP em tempo real depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
   * **[!UICONTROL Formato]** de arquivo: **CSV** ou **TAB_DELIMITED**. Selecione o formato de arquivo a ser exportado para o local do armazenamento.

   ![Informações básicas sobre a resposta](/help/rtcdp/destinations/assets/responsys-basic-information.png)

4. Clique em **[!UICONTROL Criar destino]** após preencher os campos acima. Seu destino agora está conectado e você pode [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) no destino.

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos em um destino](/help/rtcdp/destinations/activate-destinations.md) para obter informações sobre o fluxo de trabalho da ativação de segmentos.

## Atributos de destino {#destination-attributes}

Ao [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) para o [!DNL Oracle Responsys] destino, recomendamos que você selecione um identificador exclusivo do seu schema [de](../../profile/home.md#profile-fragments-and-union-schemas)união. Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino. Para obter mais informações, consulte [Selecionar quais campos de schema usar como atributos de destino em seus arquivos](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportados em Destinos de marketing de email.

## Dados exportados {#exported-data}

Para [!DNL Oracle Responsys] destinos, o CDP Adobe em tempo real cria um arquivo delimitado por tabulação `.txt` ou `.csv` no local do armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte Destinos de marketing de [email e destinos](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) de armazenamentos da Cloud no tutorial de ativação de segmentos.

<!--

Expect a new file to be created in your storage location every day. The file format is:

`Oracle_Responsys_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
Oracle_Responsys_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Oracle_Responsys_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Oracle_Responsys_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->

## Configurar importação de dados em [!DNL Oracle Responsys] {#import-data-into-responsys}

Depois de conectar o CDP em tempo real ao seu armazenamento [!DNL Amazon S3] ou SFTP, você deve configurar a importação de dados do local do armazenamento para [!DNL Oracle Responsys]. Para saber como fazer isso, consulte [Importar contatos ou contas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) no [!DNL Oracle Responsys Help Center].