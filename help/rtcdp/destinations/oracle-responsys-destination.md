---
title: Destino do Oracle Responsys
seo-title: Destino do Oracle Responsys
description: A Responsys é uma ferramenta de marketing por email corporativo para campanhas de marketing entre canais oferecida pela Oracle para personalizar interações entre email, dispositivos móveis, exibição e redes sociais.
seo-description: A Responsys é uma ferramenta de marketing por email corporativo para campanhas de marketing entre canais oferecida pela Oracle para personalizar interações entre email, dispositivos móveis, exibição e redes sociais.
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# Oracle Responsys

## Visão geral

[A Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) é uma ferramenta de marketing por email corporativo para campanhas de marketing entre canais oferecida pela Oracle para personalizar interações entre email, dispositivos móveis, exibição e redes sociais.

Para enviar dados de segmento ao Oracle Responsys, primeiro você deve [se conectar ao destino](#connect-destination) na Plataforma de Dados de Cliente em Tempo Real da Adobe e, em seguida, [configurar uma importação](#import-data-into-responsys) de dados da localização do armazenamento para o Oracle Responsys.

## Destino do Connect {#connect-destination}

1. Em **[!UICONTROL Connections > Destinations]**, selecione Oracle Responsys e, em seguida, selecione **[!UICONTROL Connect destination]**.

   ![Conectar-se ao Responsys](/help/rtcdp/destinations/assets/connect-oracle-responsys.png)

2. Na **[!UICONTROL Authentication]** etapa, se você tiver configurado anteriormente uma conexão com o destino do armazenamento na nuvem, selecione **[!UICONTROL Existing Account]** e selecione uma de suas conexões existentes. Ou você pode selecionar **[!UICONTROL New Account]** configurar uma nova conexão. Preencha as credenciais de autenticação da sua conta e selecione **[!UICONTROL Connect to destination]**. Para o Oracle Responsys, você pode selecionar entre **[!UICONTROL SFTP with Password]** e **[!UICONTROL SFTP with SSH Key]**. Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Connect to destination]**.

   Para **[!UICONTROL SFTP with Password]** conexões, você deve fornecer Domínio, Porta, Nome de usuário e Senha.
Para **[!UICONTROL SFTP with SSH Key]** conexões, você deve fornecer Domínio, Porta, Nome de usuário e Chave SSH.

   ![Preencha as informações do Responsys](/help/rtcdp/destinations/assets/responsys-authentication.png)

3. Na **[!UICONTROL Setup]** etapa, preencha as informações relevantes para o seu destino, conforme mostrado abaixo:
   * **[!UICONTROL Name]**: Escolha um nome relevante para o seu destino.
   * **[!UICONTROL Description]**: Insira uma descrição para o seu destino.
   * **[!UICONTROL Folder Path]**: Forneça o caminho no local do armazenamento onde a CDP em tempo real depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
   * **[!UICONTROL File Format]**: **CSV** ou **TAB_DELIMITED**. Selecione o formato de arquivo a ser exportado para o local do armazenamento.
   ![Informações básicas sobre a resposta](/help/rtcdp/destinations/assets/responsys-basic-information.png)

4. Clique **[!UICONTROL Create destination]** depois de preencher os campos acima. Seu destino agora está conectado e você pode [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) no destino.

## Atributos de destino {#destination-attributes}

Ao [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) para o destino do Oracle Responsys, recomendamos que você selecione um identificador exclusivo do seu schema [de](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)união. Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino. Para obter mais informações, consulte [Selecionar quais campos de schema usar como atributos de destino em seus arquivos](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportados em Destinos de marketing de email.

## Configurar importação de dados para o Oracle Responsys {#import-data-into-responsys}

Depois de conectar o CDP em tempo real ao seu armazenamento Amazon S3 ou SFTP, você deve configurar a importação de dados do local do armazenamento para o Oracle Responsys. Para saber como fazer isso, consulte [Importando contatos ou contas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) no Centro de Ajuda do Oracle Responsys.