---
keywords: email; Email; email; destinos de email; salesforce; destino do salesforce
title: Conexão do Marketing Cloud Salesforce
seo-description: O Salesforce Marketing Cloud é um conjunto de marketing digital conhecido anteriormente como ExactTarget, que permite criar e personalizar jornadas para visitantes e clientes para personalizar sua experiência.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---


# [!DNL Salesforce Marketing Cloud] conexão

## Visão geral {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/) é um conjunto de marketing digital conhecido anteriormente como ExactTarget, que permite criar e personalizar jornadas para visitantes e clientes para personalizar sua experiência.

Para enviar dados de segmento para [!DNL Salesforce Marketing Cloud], primeiro você deve [conectar o destino](#connect-destination) na Plataforma e [configurar uma importação de dados](#import-data-into-salesforce) do local de armazenamento para [!DNL Salesforce Marketing Cloud].

## Tipo de exportação {#export-type}

**Baseado em perfil**  - você está exportando todos os membros de um segmento, junto com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos do fluxo de trabalho de ativação de  [destino](../../ui/activate-destinations.md#select-attributes).

## Conectar destino {#connect-destination}

Em **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selecione [!DNL Salesforce Marketing Cloud] e selecione **[!UICONTROL Connect destination]**.

![Conectar-se ao Salesforce](../../assets/catalog/email-marketing/salesforce/catalog.png)

Na etapa **[!UICONTROL Authentication]**, se você tiver configurado anteriormente uma conexão com o destino de armazenamento na nuvem, selecione **[!UICONTROL Existing Account]** e selecione uma das conexões existentes. Ou você pode selecionar **[!UICONTROL New Account]** para configurar uma nova conexão. Preencha as credenciais de autenticação da conta e selecione **[!UICONTROL Connect to destination]**. Para [!DNL Salesforce Marketing Cloud], você pode selecionar entre **[!UICONTROL SFTP with Password]** e **[!UICONTROL SFTP with SSH Key]**. Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Connect to destination]**.

Para conexões **[!UICONTROL SFTP with Password]**, você deve fornecer Domínio, Porta, Nome de usuário e Senha.

Para conexões **[!UICONTROL SFTP with SSH Key]**, você deve fornecer Domínio, Porta, Nome de usuário e Chave SSH.

![Preencha as informações do Salesforce](../../assets/catalog/email-marketing/salesforce/account-info.png)

Na etapa **[!UICONTROL Setup]** , preencha as informações relevantes para o seu destino conforme mostrado abaixo:
- **[!UICONTROL Name]**: Escolha um nome relevante para o seu destino.
- **[!UICONTROL Description]**: Insira uma descrição para o seu destino.
- **[!UICONTROL Bucket name]**: Seu bucket do Amazon S3, onde a Platform depositará a exportação de dados. Sua entrada deve ter entre 3 e 63 caracteres. Deve começar e terminar com uma letra ou número. Deve conter somente letras minúsculas, números ou hífens ( - ). Não deve ser formatado como um endereço IP (por exemplo, 192.100.1.1).
- **[!UICONTROL Folder Path]**: Forneça o caminho no local de armazenamento onde a Platform depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
- **[!UICONTROL File Format]**:  **** CSVou  **TAB_DELIMITED**. Selecione o formato de arquivo a ser exportado para o local de armazenamento.
- **[!UICONTROL Marketing actions]**: As ações de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar ações de marketing definidas pelo Adobe ou criar sua própria ação de marketing. Para obter mais informações sobre ações de marketing, consulte a página [Governança de dados no Adobe Experience Platform](../../../data-governance/policies/overview.md) . Para obter informações sobre as ações de marketing individuais definidas pelo Adobe, consulte a [Visão geral das políticas de uso de dados](../../../data-governance/policies/overview.md).

![Informações básicas do Salesforce](../../assets/catalog/email-marketing/salesforce/basic-information.png)

Clique em **[!UICONTROL Create destination]** após preencher os campos acima. Seu destino agora está conectado e você pode [ativar segmentos](../../ui/activate-destinations.md) no destino.

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos para um destino](../../ui/activate-destinations.md) para obter informações sobre o fluxo de trabalho de ativação de segmentos.

## Atributos de destino {#destination-attributes}

Ao [ativar segmentos](../../ui/activate-destinations.md) para o destino [!DNL Salesforce Marketing Cloud], recomendamos selecionar um identificador exclusivo no [schema de união](../../../profile/home.md#profile-fragments-and-union-schemas). Selecione o identificador exclusivo e quaisquer outros campos XDM que deseja exportar para o destino. Para obter mais informações, consulte [Selecionar quais campos de esquema usar como atributos de destino em seus arquivos exportados](./overview.md#destination-attributes) em Destinos de marketing de email.

## Dados exportados {#exported-data}

Para destinos [!DNL Salesforce Marketing Cloud], a Platform cria um arquivo delimitado por tabulação `.txt` ou `.csv` no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [Destinos de marketing por email e destinos de armazenamento na nuvem](../../ui/activate-destinations.md#esp-and-cloud-storage) no tutorial de ativação de segmento.

## Configurar importação de dados em [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

Depois de conectar a Platform ao seu armazenamento [!DNL Amazon S3] ou SFTP, você deve configurar a importação de dados do local de armazenamento para [!DNL Salesforce Marketing Cloud]. Para saber como fazer isso, consulte [Importando assinantes no Marketing Cloud de um arquivo](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) no [!DNL Salesforce Help Center].