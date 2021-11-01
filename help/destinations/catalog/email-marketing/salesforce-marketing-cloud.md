---
keywords: email; Email; email; destinos de email; salesforce; destino do salesforce
title: Conexão do Marketing Cloud Salesforce
seo-description: Salesforce Marketing Cloud is a digital marketing suite formerly known as ExactTarget that allows you to build and customize journeys for visitors and customers to personalize their experience.
exl-id: e85049a7-eaed-4f8a-b670-9999d56928f8
source-git-commit: b4810dfef7b0d437744ca14a32bd4f5746e8d002
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 1%

---

# [!DNL Salesforce Marketing Cloud] conexão

## Visão geral {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/) é um conjunto de marketing digital conhecido anteriormente como ExactTarget, que permite criar e personalizar jornadas para visitantes e clientes para personalizar sua experiência.

Para enviar dados de segmento para [!DNL Salesforce Marketing Cloud], você deve primeiro [conectar o destino](#connect-destination) na Platform e, em seguida, [configurar uma importação de dados](#import-data-into-salesforce) do local de armazenamento para [!DNL Salesforce Marketing Cloud].

## Tipo de exportação {#export-type}

**Baseado em perfil** - estiver exportando todos os membros de um segmento, juntamente com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos do [fluxo de trabalho de ativação do público](../../ui/activate-batch-profile-destinations.md#select-attributes).

## LISTA DE PERMISSÕES de endereço IP {#allow-list}

Ao configurar destinos de marketing por email com o armazenamento SFTP, o Adobe recomenda adicionar determinados intervalos IP à lista de permissões.

Consulte [LISTA DE PERMISSÕES de endereço IP para destinos de armazenamento em nuvem](../cloud-storage/ip-address-allow-list.md) se você precisar adicionar IPs Adobe à lista de permissões.

## Conecte-se ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

Esse destino oferece suporte aos seguintes tipos de conexão:

* **[!UICONTROL SFTP com senha]**
* **[!UICONTROL SFTP com chave SSH]**

### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* Para **[!UICONTROL SFTP com senha]** , você deve fornecer:
   * [!UICONTROL Domínio]
   * [!UICONTROL Port]
   * [!UICONTROL Nome do usuário]
   * [!UICONTROL Senha]
* Para **[!UICONTROL SFTP com chave SSH]** , você deve fornecer:
   * [!UICONTROL Domínio]
   * [!UICONTROL Port]
   * [!UICONTROL Nome do usuário]
   * [!UICONTROL Chave SSH]

* Como opção, você pode anexar sua chave pública formatada em RSA para adicionar criptografia com PGP/GPG aos arquivos exportados sob a variável **[!UICONTROL Chave]** seção. Sua chave pública deve ser escrita como uma [!DNL Base64] sequência de caracteres codificada.
* **[!UICONTROL Nome]**: Escolha um nome relevante para o seu destino.
* **[!UICONTROL Descrição]**: Insira uma descrição para o seu destino.
* **[!UICONTROL Caminho da pasta]**: Forneça o caminho no local de armazenamento onde a Platform depositará seus dados de exportação como arquivos CSV.
* **[!UICONTROL Formato de arquivo]**: **CSV** ou **TAB_DELIMITED**. Selecione o formato de arquivo a ser exportado para o local de armazenamento.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

## Ativar segmentos para este destino {#activate}

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

### Atributos de destino {#destination-attributes}

Ao ativar segmentos para esse destino, o Adobe recomenda selecionar um identificador exclusivo de [schema de união](../../../profile/home.md#profile-fragments-and-union-schemas). Selecione o identificador exclusivo e quaisquer outros campos XDM que deseja exportar para o destino. Para obter mais informações, consulte [práticas recomendadas ao ativar públicos-alvo para destinos de marketing por email](overview.md#best-practices).

## Dados exportados {#exported-data}

Para [!DNL Salesforce Marketing Cloud] destinos, a Platform cria uma `.csv` no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [verificar ativação de segmento](../../ui/activate-batch-profile-destinations.md#verify) no tutorial de ativação de segmento.

## Configurar a importação de dados no [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

Depois de conectar [!DNL Platform] para [!DNL SFTP] você deve configurar a importação de dados do seu local de armazenamento para [!DNL Salesforce Marketing Cloud]. Para saber como fazer isso, consulte [Importação de assinantes para o Marketing Cloud a partir de um arquivo](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) no [!DNL Salesforce Help Center].
