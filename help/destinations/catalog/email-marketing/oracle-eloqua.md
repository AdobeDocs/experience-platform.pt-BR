---
keywords: email; Email; email; destinos de email; oracle eloqua; oracle
title: Conexão Eloqua do Oracle
description: O Oracle Eloqua é uma plataforma de software como serviço (SaaS) para automação de marketing oferecida pelo Oracle, que tem como objetivo ajudar profissionais de marketing B2B e organizações a gerenciar campanhas de marketing e geração de líderes de vendas.
exl-id: 6eaa79ff-8874-423b-bdff-aa04f6101a53
source-git-commit: 70be44e919070df910d618af4507b600ad51123c
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# [!DNL Oracle Eloqua] conexão

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) é uma plataforma de software como um serviço (SaaS) para automação de marketing oferecida pela  [!DNL Oracle] que tem como objetivo ajudar profissionais de marketing e organizações B2B a gerenciar campanhas de marketing e geração de líderes de vendas.

Para enviar dados de segmento para [!DNL Oracle Eloqua], primeiro você deve [conectar o destino](#connect-destination) no Adobe Experience Platform e [configurar uma importação de dados](#import-data-into-eloqua) do local de armazenamento para [!DNL Oracle Eloqua].

## Tipo de exportação {#export-type}

**Baseado em perfil**  - você está exportando todos os membros de um segmento, junto com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos do fluxo de trabalho de ativação de  [destino](../../ui/activate-destinations.md#select-attributes).

## LISTA DE PERMISSÕES do endereço IP {#allow-list}

Ao configurar destinos de marketing por email com o armazenamento SFTP, o Adobe recomenda adicionar determinados intervalos IP à lista de permissões.

Consulte [lista de permissões de endereço IP para destinos de armazenamento em nuvem](../cloud-storage/ip-address-allow-list.md) se precisar adicionar IPs Adobe à lista de permissões.

## Conecte-se ao destino {#connect-destination}

Em **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]**, selecione [!DNL Oracle Eloqua] e selecione **[!UICONTROL Configurar]**.

>[!NOTE]
>
>Se uma conexão com esse destino já existir, você poderá ver um botão **[!UICONTROL Ativar]** no cartão de destino. Para obter mais informações sobre a diferença entre [!UICONTROL Ativate] e [!UICONTROL Configure], consulte a seção [Catalog](../../ui/destinations-workspace.md#catalog) da documentação do espaço de trabalho de destino.

![Conectar-se ao Eloqua](../../assets/catalog/email-marketing/oracle-eloqua/catalog.png)

Na etapa **[!UICONTROL Account]**, se você tiver configurado anteriormente uma conexão com o destino de armazenamento na nuvem, selecione **[!UICONTROL Existing Account]** e selecione uma de suas conexões existentes. Ou você pode selecionar **[!UICONTROL New Account]** para configurar uma nova conexão. Preencha as credenciais de autenticação da conta e selecione **[!UICONTROL Conectar ao destino]**. Para [!DNL Oracle Eloqua], você pode selecionar entre **[!UICONTROL SFTP com Senha]** e **[!UICONTROL SFTP com Chave SSH]**.

![Conexão da conta Eloqua](../../assets/catalog/email-marketing/oracle-eloqua/connection-type.png)

Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Conectar ao destino]**.

- Para **[!UICONTROL SFTP com conexões de senha]**, você deve fornecer [!UICONTROL Domínio], [!UICONTROL Porta], [!UICONTROL Nome de usuário] e [!UICONTROL Senha].
- Para **[!UICONTROL SFTP com conexões de chave SSH]**, você deve fornecer [!UICONTROL Domínio], [!UICONTROL Porta], [!UICONTROL Nome de usuário] e [!UICONTROL Chave SSH].

Como opção, você pode anexar sua chave pública formatada em RSA para adicionar criptografia com PGP/GPG aos arquivos exportados na seção **[!UICONTROL Key]**. Sua chave pública deve ser gravada como uma sequência de caracteres [!DNL Base64] codificada.

![Eloqua se conecta ao destino](../../assets/catalog/email-marketing/oracle-eloqua/account-info.png)

Na etapa **[!UICONTROL Authentication]**, preencha as informações relevantes para seu destino, conforme mostrado abaixo:
- **[!UICONTROL Nome]**: Escolha um nome relevante para o seu destino.
- **[!UICONTROL Descrição]**: Insira uma descrição para o seu destino.
- **[!UICONTROL Caminho]** da pasta: Forneça o caminho no local de armazenamento onde a Platform depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
- **[!UICONTROL Formato]** de arquivo:  **** CSVou  **TAB_DELIMITED**. Selecione o formato de arquivo a ser exportado para o local de armazenamento.
- **[!UICONTROL Ações]** de marketing: As ações de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar ações de marketing definidas pelo Adobe ou criar sua própria ação de marketing. Para obter mais informações sobre ações de marketing, consulte a [Visão geral das políticas de uso de dados](../../../data-governance/policies/overview.md).

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

![Informações básicas sobre o Eloqua](../../assets/catalog/email-marketing/oracle-eloqua/basic-information.png)

Clique em **[!UICONTROL Criar destino]** após preencher os campos acima. Seu destino agora é criado e você pode [ativar segmentos](../../ui/activate-destinations.md) no destino.

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos para um destino](../../ui/activate-destinations.md) para obter informações sobre o fluxo de trabalho de ativação de segmentos.

## Atributos de destino {#destination-attributes}

Quando [ativar segmentos](../../ui/activate-destinations.md) para o destino [!DNL Oracle Eloqua], o Adobe recomenda selecionar um identificador exclusivo no [esquema de união](../../../profile/home.md#profile-fragments-and-union-schemas). Selecione o identificador exclusivo e quaisquer outros campos XDM que deseja exportar para o destino. Para obter mais informações, consulte [Selecionar quais campos de esquema usar como atributos de destino em seus arquivos exportados](./overview.md#destination-attributes).

## Dados exportados {#exported-data}

Para destinos [!DNL Oracle Eloqua], a Platform cria um arquivo `.csv` delimitado por tabulação no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [Destinos de marketing por email e destinos de armazenamento na nuvem](../../ui/activate-destinations.md#esp-and-cloud-storage) no tutorial de ativação de segmento.

## Configurar importação de dados em [!DNL Oracle Eloqua] {#import-data-into-eloqua}

Depois de conectar [!DNL Platform] ao armazenamento [!DNL SFTP], você deve configurar a importação de dados do local de armazenamento para [!DNL Oracle Eloqua]. Para saber como fazer isso, consulte [Importando contatos ou contas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) no [!DNL Oracle Eloqua Help Center].
