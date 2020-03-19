---
title: Destino do Oracle Responsys
seo-title: Destino do Oracle Responsys
description: A Responsys é uma ferramenta de marketing de email corporativo para campanhas de marketing entre canais, oferecida pela Oracle para personalizar interações em email, dispositivos móveis, exibição e redes sociais.
seo-description: A Responsys é uma ferramenta de marketing de email corporativo para campanhas de marketing entre canais, oferecida pela Oracle para personalizar interações em email, dispositivos móveis, exibição e redes sociais.
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Oracle Responsys

## Visão geral

[A Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) é uma ferramenta de marketing de email corporativo para campanhas de marketing entre canais, oferecida pela Oracle para personalizar interações em email, dispositivos móveis, exibição e redes sociais.

Para enviar dados de segmento ao Oracle Responsys, primeiro você deve [conectar o destino](#connect-destination) na Plataforma de Dados de Cliente em Tempo Real da Adobe e [configurar uma importação](#import-data-into-responsys) de dados do local de armazenamento para o Oracle Responsys.

## Destino do Connect {#connect-destination}

1. Em **[!UICONTROL Conexões > Destinos]**, selecione Oracle Responsys e, em seguida, selecione o destino **[!UICONTROL do]** Connect.

   ![Conectar-se ao Responsys](/help/rtcdp/destinations/assets/connect-oracle-responsys.png)

1. No assistente de destino do Connect, selecione o tipo **[!UICONTROL de]** conexão para seu local de armazenamento. Para o Oracle Responsys, você pode selecionar entre **SFTP com Senha** e **SFTP com chave** SSH. Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Connect (Conectar]**).

   ![Configurar assistente de respostas](/help/rtcdp/destinations/assets/responsys-wizard.png)

   Para **SFTP com conexões de senha** , você deve fornecer Domínio, Porta, Nome de usuário e Senha.
Para **SFTP com conexões de chave** SSH, você deve fornecer Domínio, Porta, Nome de usuário e Chave SSH.

   ![Preencha as informações do Responsys](/help/rtcdp/destinations/assets/responsys-step2.png)

1. Em Informações **** básicas, preencha as informações relevantes para o seu destino, como mostrado abaixo:
   * **Nome**: Escolha um nome relevante para o seu destino.
   * **Descrição**: Insira uma descrição para o seu destino.
   * **Caminho** da pasta: Forneça o caminho no local de armazenamento onde a CDP em tempo real depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
   * **Formato** de arquivo: **CSV** ou **TAB_DELIMITED**. Selecione o formato de arquivo a ser exportado para o local de armazenamento.
   ![Informações básicas sobre a resposta](/help/rtcdp/destinations/assets/responsys-basic-information.png)

1. Clique em **Criar** após preencher os campos em Informações **básicas**. Seu destino agora está conectado e você pode [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) no destino.

## Atributos de destino {#destination-attributes}

Ao [ativar segmentos](/help/rtcdp/destinations/activate-destinations.md) para o destino do Oracle Responsys, recomendamos que você selecione um identificador exclusivo do esquema [de](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)união. Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino. Para obter mais informações, consulte [Selecionar quais campos de esquema usar como atributos de destino em seus arquivos](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) exportados em Destinos de marketing de email.

## Configurar importação de dados para o Oracle Responsys {#import-data-into-responsys}

Depois de conectar o CDP em tempo real ao armazenamento Amazon S3 ou SFTP, você deve configurar a importação de dados do local de armazenamento para o Oracle Responsys. Para saber como fazer isso, consulte [Importando contatos ou contas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) no Centro de Ajuda do Oracle Responsys.