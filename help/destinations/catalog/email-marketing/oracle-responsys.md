---
keywords: email; Email; email; destinos de email; destino da responsys do oracle
title: Conexão Oracle Responsys
description: O Responsys é uma ferramenta de marketing por email corporativo para campanhas de marketing entre canais oferecidas pelo Oracle para personalizar interações em email, dispositivos móveis, exibição e redes sociais.
translation-type: tm+mt
source-git-commit: 02754055e2be8a45a0699386cb559dad8f25717c
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---


# [!DNL Oracle Responsys] conexão

## Visão geral {#overview}

[](https://www.oracle.com/cx/marketing/campaign-management/) O Responsyis é uma ferramenta de marketing por email corporativo para campanhas de marketing entre canais oferecidas pelo  [!DNL Oracle] para personalizar interações entre email, celular, exibição e redes sociais.

Para enviar dados de segmento para [!DNL Oracle Responsys], primeiro você deve [se conectar ao destino](#connect-destination) no Adobe Experience Platform e [configurar uma importação de dados](#import-data-into-responsys) do local de armazenamento para [!DNL Oracle Responsys].

## Tipo de exportação {#export-type}

**Baseado em perfil**  - você está exportando todos os membros de um segmento, junto com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos do fluxo de trabalho de ativação de  [destino](../../ui/activate-destinations.md#select-attributes).

## Conectar destino {#connect-destination}

Em **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selecione [!DNL Oracle Responsys] e selecione **[!UICONTROL Connect destination]**.

![Conecte-se ao Responsys](../../assets/catalog/email-marketing/oracle-responsys/catalog.png)

Na etapa **[!UICONTROL Account]**, se você tiver configurado anteriormente uma conexão com o destino de armazenamento na nuvem, selecione **[!UICONTROL Existing Account]** e selecione uma das conexões existentes. Ou você pode selecionar **[!UICONTROL New Account]** para configurar uma nova conexão. Preencha as credenciais de autenticação da conta e selecione **[!UICONTROL Connect to destination]**. Para [!DNL Oracle Responsys], você pode selecionar entre **[!UICONTROL SFTP with Password]** e **[!UICONTROL SFTP with SSH Key]**.

![Conta do Connect Responsys](../../assets/catalog/email-marketing/oracle-responsys/connection-type.png)

Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Configure]**.

- Para conexões **[!UICONTROL SFTP with Password]**, você deve fornecer [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username] e [!UICONTROL Password].
- Para conexões **[!UICONTROL SFTP with SSH Key]**, você deve fornecer [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username] e [!UICONTROL SSH Key].

Como opção, você pode anexar sua chave pública formatada em RSA para adicionar criptografia com PGP/GPG aos arquivos exportados na seção **[!UICONTROL Key]**. Sua chave pública deve ser gravada como uma sequência de caracteres [!DNL Base64] codificada.

![Preencha as informações do Responsys](../../assets/catalog/email-marketing/oracle-responsys/account-info.png)

Na etapa **[!UICONTROL Authentication]** , preencha as informações relevantes para o seu destino conforme mostrado abaixo:
- **[!UICONTROL Name]**: Escolha um nome relevante para o seu destino.
- **[!UICONTROL Description]**: Insira uma descrição para o seu destino.
- **[!UICONTROL Folder Path]**: Forneça o caminho no local de armazenamento onde a Platform depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
- **[!UICONTROL File Format]**:  **** CSVou  **TAB_DELIMITED**. Selecione o formato de arquivo a ser exportado para o local de armazenamento.
- **[!UICONTROL Marketing actions]**: As ações de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar ações de marketing definidas pelo Adobe ou criar sua própria ação de marketing. Para obter mais informações sobre ações de marketing, consulte a [Visão geral das políticas de uso de dados](../../../data-governance/policies/overview.md).

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

![Informações básicas do Responsys](../../assets/catalog/email-marketing/oracle-responsys/basic-information.png)

Clique em **[!UICONTROL Create destination]** após preencher os campos acima. Seu destino agora está conectado e você pode [ativar segmentos](../../ui/activate-destinations.md) no destino.

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos para um destino](../../ui/activate-destinations.md) para obter informações sobre o fluxo de trabalho de ativação de segmentos.

## Atributos de destino {#destination-attributes}

Quando [ativar segmentos](../../ui/activate-destinations.md) para o destino [!DNL Oracle Responsys], o Adobe recomenda selecionar um identificador exclusivo no [esquema de união](../../../profile/home.md#profile-fragments-and-union-schemas). Selecione o identificador exclusivo e quaisquer outros campos XDM que deseja exportar para o destino. Para obter mais informações, consulte [Selecionar quais campos de esquema usar como atributos de destino em seus arquivos exportados](./overview.md#destination-attributes).

## Dados exportados {#exported-data}

Para destinos [!DNL Oracle Responsys], a Platform cria um arquivo delimitado por tabulação `.txt` ou `.csv` no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [Destinos de marketing por email e destinos de armazenamento na nuvem](../../ui/activate-destinations.md#esp-and-cloud-storage) no tutorial de ativação de segmento.

## Configurar importação de dados em [!DNL Oracle Responsys] {#import-data-into-responsys}

Depois de conectar [!DNL Platform] ao armazenamento SFTP, você deve configurar a importação de dados do local de armazenamento para [!DNL Oracle Responsys]. Para saber como fazer isso, consulte [Importando contatos ou contas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) no [!DNL Oracle Responsys Help Center].