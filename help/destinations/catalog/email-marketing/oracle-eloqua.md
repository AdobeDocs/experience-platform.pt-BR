---
keywords: email; Email; email; destinos de email; oracle eloqua; oracle
title: Conexão Eloqua do Oracle
description: O Oracle Eloqua é uma plataforma de software como serviço (SaaS) para automação de marketing oferecida pelo Oracle, que tem como objetivo ajudar profissionais de marketing B2B e organizações a gerenciar campanhas de marketing e geração de líderes de vendas.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---


# [!DNL Oracle Eloqua] conexão

## Visão geral {#overview}

[[!DNL Oracle Eloqua]](https://www.oracle.com/marketingcloud/products/marketing-automation/) é uma plataforma de software como um serviço (SaaS) para automação de marketing oferecida pela  [!DNL Oracle] que tem como objetivo ajudar profissionais de marketing e organizações B2B a gerenciar campanhas de marketing e geração de líderes de vendas.

Para enviar dados de segmento para [!DNL Oracle Eloqua], primeiro você deve [conectar o destino](#connect-destination) no Adobe Experience Platform e [configurar uma importação de dados](#import-data-into-eloqua) do local de armazenamento para [!DNL Oracle Eloqua].

## Tipo de exportação {#export-type}

**Baseado em perfil**  - você está exportando todos os membros de um segmento, junto com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos do fluxo de trabalho de ativação de  [destino](../../ui/activate-destinations.md#select-attributes).

## Conecte-se ao destino {#connect-destination}

Em **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selecione [!DNL Oracle Eloqua] e selecione **[!UICONTROL Connect destination]**.

[Conectar-se ao Eloqua](../../assets/catalog/email-marketing/oracle-eloqua/catalog.png)

Na etapa **[!UICONTROL Authentication]**, se você tiver configurado anteriormente uma conexão com o destino de armazenamento na nuvem, selecione **[!UICONTROL Existing Account]** e selecione uma das conexões existentes. Ou você pode selecionar **[!UICONTROL New Account]** para configurar uma nova conexão. Preencha as credenciais de autenticação da conta e selecione **[!UICONTROL Connect to destination]**. Para [!DNL Oracle Eloqua], você pode selecionar entre **[!UICONTROL SFTP with Password]** e **[!UICONTROL SFTP with SSH Key]**. Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Connect to destination]**.

Para conexões **[!UICONTROL SFTP with Password]**, você deve fornecer Domínio, Porta, Nome de usuário e Senha.
Para conexões **[!UICONTROL SFTP with SSH Key]**, você deve fornecer Domínio, Porta, Nome de usuário e Chave SSH.

![Configurar o assistente do Eloqua](../../assets/catalog/email-marketing/oracle-eloqua/account-info.png)

Na etapa **[!UICONTROL Setup]** , preencha as informações relevantes para o seu destino conforme mostrado abaixo:
- **[!UICONTROL Name]**: Escolha um nome relevante para o seu destino.
- **[!UICONTROL Description]**: Insira uma descrição para o seu destino.
- **[!UICONTROL Bucket name]**: Seu bucket do Amazon S3, onde a Platform depositará a exportação de dados. Sua entrada deve ter entre 3 e 63 caracteres. Deve começar e terminar com uma letra ou número. Deve conter somente letras minúsculas, números ou hífens ( - ). Não deve ser formatado como um endereço IP (por exemplo, 192.100.1.1).
- **[!UICONTROL Folder Path]**: Forneça o caminho no local de armazenamento onde a Platform depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
- **[!UICONTROL File Format]**:  **** CSVou  **TAB_DELIMITED**. Selecione o formato de arquivo a ser exportado para o local de armazenamento.
- **[!UICONTROL Marketing actions]**: As ações de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar ações de marketing definidas pelo Adobe ou criar sua própria ação de marketing. Para obter mais informações sobre ações de marketing, consulte a página [Governança de dados no Adobe Experience Platform](../../../data-governance/policies/overview.md) . Para obter informações sobre as ações de marketing individuais definidas pelo Adobe, consulte a [Visão geral das políticas de uso de dados](../../../data-governance/policies/overview.md).

![Informações básicas sobre o Eloqua](../../assets/catalog/email-marketing/oracle-eloqua/basic-information.png)

Clique em **[!UICONTROL Create destination]** após preencher os campos acima. Seu destino agora é criado e você pode [ativar segmentos](../../ui/activate-destinations.md) no destino.

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos para um destino](../../ui/activate-destinations.md) para obter informações sobre o fluxo de trabalho de ativação de segmentos.

## Atributos de destino {#destination-attributes}

Ao [ativar segmentos](../../ui/activate-destinations.md) para o destino [!DNL Oracle Eloqua], recomendamos selecionar um identificador exclusivo no [schema de união](../../../profile/home.md#profile-fragments-and-union-schemas). Selecione o identificador exclusivo e quaisquer outros campos XDM que deseja exportar para o destino. Para obter mais informações, consulte [Selecionar quais campos de esquema usar como atributos de destino em seus arquivos exportados](./overview.md#destination-attributes) em Destinos de marketing de email.

## Dados exportados {#exported-data}

Para destinos [!DNL Oracle Eloqua], a Platform cria um arquivo delimitado por tabulação `.txt` ou `.csv` no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [Destinos de marketing por email e destinos de armazenamento na nuvem](../../ui/activate-destinations.md#esp-and-cloud-storage) no tutorial de ativação de segmento.

## Configurar importação de dados em [!DNL Oracle Eloqua] {#import-data-into-eloqua}

Após conectar a Plataforma ao armazenamento Amazon S3 ou SFTP, é necessário configurar a importação de dados do local de armazenamento para [!DNL Oracle Eloqua]. Para saber como fazer isso, consulte [Importando contatos ou contas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) no [!DNL Oracle Eloqua Help Center].