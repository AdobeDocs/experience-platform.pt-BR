---
keywords: email; Email; email; destinos de email; oracle eloqua; oracle
title: Conexão Eloqua do Oracle
description: O Oracle Eloqua é uma plataforma de software como serviço (SaaS) para automação de marketing oferecida pelo Oracle, que tem como objetivo ajudar profissionais de marketing B2B e organizações a gerenciar campanhas de marketing e geração de líderes de vendas.
exl-id: 6eaa79ff-8874-423b-bdff-aa04f6101a53
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---

# [!DNL Oracle Eloqua] conexão

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) é uma plataforma de software como um serviço (SaaS) para automação de marketing oferecida pela  [!DNL Oracle] que tem como objetivo ajudar profissionais de marketing e organizações B2B a gerenciar campanhas de marketing e geração de líderes de vendas.

Para enviar dados de segmento para [!DNL Oracle Eloqua], primeiro você deve [conectar o destino](#connect-destination) no Adobe Experience Platform e [configurar uma importação de dados](#import-data-into-eloqua) do local de armazenamento para [!DNL Oracle Eloqua].

## Tipo de exportação {#export-type}

**Baseado em perfil**  - você está exportando todos os membros de um segmento, junto com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos do fluxo de trabalho de ativação de  [destino](../../ui/activate-destinations.md#select-attributes).

## LISTA DE PERMISSÕES de endereço IP {#allow-list}

Ao configurar destinos de marketing por email com o armazenamento SFTP, o Adobe recomenda adicionar determinados intervalos IP à lista de permissões.

Consulte [lista de permissões de endereço IP para destinos de armazenamento em nuvem](../cloud-storage/ip-address-allow-list.md) se precisar adicionar IPs Adobe à lista de permissões.

## Conecte-se ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

Esse destino oferece suporte aos seguintes tipos de conexão:

* **[!UICONTROL SFTP com senha]**
* **[!UICONTROL SFTP com chave SSH]**

### Parâmetros de conexão {#parameters}

Enquanto [configurar](../../ui/connect-destination.md) esse destino, você deve fornecer as seguintes informações:

* Para conexões **[!UICONTROL SFTP com senha]**, você deve fornecer:
   * [!UICONTROL Domínio]
   * [!UICONTROL Port]
   * [!UICONTROL Nome do usuário]
   * [!UICONTROL Password]
* Para conexões **[!UICONTROL SFTP com chave SSH]**, você deve fornecer:
   * [!UICONTROL Domínio]
   * [!UICONTROL Port]
   * [!UICONTROL Nome do usuário]
   * [!UICONTROL Chave SSH]

* Como opção, você pode anexar sua chave pública formatada em RSA para adicionar criptografia com PGP/GPG aos arquivos exportados na seção **[!UICONTROL Key]**. Sua chave pública deve ser gravada como uma sequência de caracteres [!DNL Base64] codificada.
* **[!UICONTROL Nome]**: Escolha um nome relevante para o seu destino.
* **[!UICONTROL Descrição]**: Insira uma descrição para o seu destino.
* **[!UICONTROL Caminho]** da pasta: Forneça o caminho no local de armazenamento onde a Platform depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
* **[!UICONTROL Formato]** de arquivo:  **** CSVou  **TAB_DELIMITED**. Selecione o formato de arquivo a ser exportado para o local de armazenamento.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

## Ativar segmentos para este destino {#activate}

Consulte [Ativar perfis e segmentos para um destino](../../ui/activate-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para destinos.

## Atributos de destino {#destination-attributes}

Quando [ativar segmentos](../../ui/activate-destinations.md) para esse destino, o Adobe recomenda selecionar um identificador exclusivo no [schema de união](../../../profile/home.md#profile-fragments-and-union-schemas). Selecione o identificador exclusivo e quaisquer outros campos XDM que deseja exportar para o destino. Para obter mais informações, consulte [Selecionar quais campos de esquema usar como atributos de destino em seus arquivos exportados](./overview.md#destination-attributes).

## Dados exportados {#exported-data}

Para destinos [!DNL Oracle Eloqua], a Platform cria um arquivo `.csv` delimitado por tabulação no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [Destinos de marketing por email e destinos de armazenamento na nuvem](../../ui/activate-destinations.md#esp-and-cloud-storage) no tutorial de ativação de segmento.

## Configurar importação de dados em [!DNL Oracle Eloqua] {#import-data-into-eloqua}

Depois de conectar [!DNL Platform] ao armazenamento [!DNL SFTP], você deve configurar a importação de dados do local de armazenamento para [!DNL Oracle Eloqua]. Para saber como fazer isso, consulte [Importando contatos ou contas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) no [!DNL Oracle Eloqua Help Center].
