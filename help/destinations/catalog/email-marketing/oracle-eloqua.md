---
keywords: email;E-mail;e-mail;destinos de e-mail;oracle eloqua;oracle
title: Destino oracle Eloqua
seo-title: Destino oracle Eloqua
description: A oracle Eloqua é uma plataforma de software como serviço (SaaS) para automação de marketing oferecida pela Oracle que tem como objetivo ajudar os comerciantes e organizações B2B a gerenciar campanhas de marketing e a geração de leads de vendas.
seo-description: A oracle Eloqua é uma plataforma de software como serviço (SaaS) para automação de marketing oferecida pela Oracle que tem como objetivo ajudar os comerciantes e organizações B2B a gerenciar campanhas de marketing e a geração de leads de vendas.
translation-type: tm+mt
source-git-commit: 7aadb4b7e7c36b659490d155ad4cfa7ef0a24306
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 0%

---


# [!DNL Oracle Eloqua]

## Visão geral

[[!DNL Oracle Eloqua]](https://www.oracle.com/marketingcloud/products/marketing-automation/) é uma plataforma de software como um serviço (SaaS) para automação de marketing oferecida por  [!DNL Oracle] que tem como objetivo ajudar os profissionais de marketing e organizações B2B a gerenciar campanhas de marketing e geração de leads de vendas.

Para enviar dados de segmento para [!DNL Oracle Eloqua], primeiro [conecte o destino](#connect-destination) no Adobe Experience Platform e, em seguida, [configure uma importação de dados](#import-data-into-eloqua) do local do armazenamento para [!DNL Oracle Eloqua].

## Tipo de exportação {#export-type}

**Baseado**  em perfis - você está exportando todos os membros de um segmento, juntamente com os campos de schema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela de atributos selecionados do fluxo de trabalho [ da ativação de ](../../ui/activate-destinations.md#select-attributes)destino.

## Conectar ao destino {#connect-destination}

Em **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]**, selecione [!DNL Oracle Eloqua] e **[!UICONTROL Ligar destino]**.

[Ligar à Eloqua](../../assets/catalog/email-marketing/oracle-eloqua/catalog.png)

Na etapa **[!UICONTROL Autenticação]**, se você tiver configurado anteriormente uma conexão com o destino do armazenamento na nuvem, selecione **[!UICONTROL Conta existente]** e selecione uma de suas conexões existentes. Ou você pode selecionar **[!UICONTROL Nova conta]** para configurar uma nova conexão. Preencha as credenciais de autenticação da sua conta e selecione **[!UICONTROL Ligar ao destino]**. Para [!DNL Oracle Eloqua], você pode selecionar entre **[!UICONTROL SFTP com Password]** e **[!UICONTROL SFTP com chave SSH]**. Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Conecte-se ao destino]**.

Para conexões **[!UICONTROL SFTP com Password]**, você deve fornecer Domínio, Porta, Nome de usuário e Senha.
Para conexões **[!UICONTROL SFTP com chave SSH]**, você deve fornecer Domínio, Porta, Nome de usuário e Chave SSH.

![Configurar o assistente Eloqua](../../assets/catalog/email-marketing/oracle-eloqua/account-info.png)

Na etapa **[!UICONTROL Setup]**, preencha as informações relevantes para seu destino, conforme mostrado abaixo:
- **[!UICONTROL Nome]**: Escolha um nome relevante para o seu destino.
- **[!UICONTROL Descrição]**: Insira uma descrição para o seu destino.
- **[!UICONTROL Caminho]** da pasta: Forneça o caminho no local do armazenamento onde a Plataforma depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
- **[!UICONTROL Formato]** de arquivo:  **** CSV ou  **TAB_DELIMITED**. Selecione o formato de arquivo a ser exportado para o local do armazenamento.

![Informações básicas sobre o Eloqua](../../assets/catalog/email-marketing/oracle-eloqua/basic-information.png)

Clique em **[!UICONTROL Criar destino]** depois de preencher os campos acima. Seu destino agora é criado e você pode [ativar segmentos](../../ui/activate-destinations.md) no destino.

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos em um destino](../../ui/activate-destinations.md) para obter informações sobre o fluxo de trabalho da ativação de segmentos.

## Atributos de destino {#destination-attributes}

Quando [ativar segmentos](../../ui/activate-destinations.md) no destino [!DNL Oracle Eloqua], recomendamos que você selecione um identificador exclusivo do seu [schema de união](../../../profile/home.md#profile-fragments-and-union-schemas). Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino. Para obter mais informações, consulte [Selecione quais campos de schema usar como atributos de destino em seus arquivos exportados](./overview.md#destination-attributes) em Destinos de marketing de email.

## Dados exportados {#exported-data}

Para destinos [!DNL Oracle Eloqua], a plataforma cria um arquivo `.txt` ou `.csv` delimitado por tabulação no local do armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [Destinos de e-mail Marketing e destinos do armazenamento Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) no tutorial de ativação de segmentos.

## Configurar importação de dados para [!DNL Oracle Eloqua] {#import-data-into-eloqua}

Depois de conectar a Plataforma ao seu armazenamento Amazon S3 ou SFTP, é necessário configurar a importação de dados do local do armazenamento para [!DNL Oracle Eloqua]. Para saber como fazer isso, consulte [Importando contatos ou contas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) no [!DNL Oracle Eloqua Help Center].