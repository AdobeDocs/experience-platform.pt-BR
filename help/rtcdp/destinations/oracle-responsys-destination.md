---
title: Destino do Oracle Responsys
seo-title: Destino do Oracle Responsys
description: A Responsys é uma ferramenta de marketing por email corporativo para campanhas de marketing entre canais oferecida pela Oracle para personalizar interações entre email, dispositivos móveis, exibição e redes sociais.
seo-description: A Responsys é uma ferramenta de marketing por email corporativo para campanhas de marketing entre canais oferecida pela Oracle para personalizar interações entre email, dispositivos móveis, exibição e redes sociais.
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---


# [!DNL Oracle Responsys]

## Visão geral

[A Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) é uma ferramenta de marketing por email empresarial para campanhas de marketing entre canais, oferecida pela [!DNL Oracle] para personalizar interações entre email, dispositivos móveis, vídeos e redes sociais.

Para enviar dados de segmento para [!DNL Oracle Responsys], é necessário primeiro [conectar-se ao destino](#connect-destination) no Adobe Real-time Customer Data Platform e, em seguida, [configurar uma importação](#import-data-into-responsys) de dados do local do armazenamento para [!DNL Oracle Responsys].

## Destino do Connect {#connect-destination}

1. Em **[!UICONTROL Conexões > Destinos]**, selecione [!DNL Oracle Responsys]e, em seguida, selecione destino **[!UICONTROL do]** Connect.

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

## Atributos de destino {#destination-attributes}

Ao [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) para o [!DNL Oracle Responsys] destino, recomendamos que você selecione um identificador exclusivo do seu schema [de](../../profile/home.md#profile-fragments-and-union-schemas)união. Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino. Para obter mais informações, consulte [Selecionar quais campos de schema usar como atributos de destino em seus arquivos](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportados em Destinos de marketing de email.

## Configurar importação de dados em [!DNL Oracle Responsys] {#import-data-into-responsys}

Depois de conectar o CDP em tempo real ao seu armazenamento Amazon S3 ou SFTP, você deve configurar a importação de dados do local do armazenamento para [!DNL Oracle Responsys]. Para saber como fazer isso, consulte [Importar contatos ou contas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) no [!DNL Oracle Responsys Help Center].