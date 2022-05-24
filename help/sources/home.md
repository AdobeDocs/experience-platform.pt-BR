---
keywords: Experience Platform, home, tópicos populares, conectores de origem, conector de origem, fontes, fontes de dados, fonte de dados, conexão da fonte de dados
solution: Experience Platform
title: Visão geral dos conectores de origem
topic-legacy: overview
description: O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: 365e36351bf18864c677f53dffbc30b47f29b074
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 0%

---

# Visão geral dos conectores de origem

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamentos baseados em nuvem, bancos de dados e muitas outras.

[!DNL Flow Service] O é usado para coletar e centralizar dados do cliente de várias fontes diferentes no Platform. O serviço fornece uma interface de usuário e uma RESTful API que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar sistemas de terceiros, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

Com o Experience Platform, você pode centralizar dados coletados de fontes diferentes e usar os insights obtidos com ele para fazer mais.

## Tipos de fontes

As fontes no Experience Platform são agrupadas nas seguintes categorias:

### Aplicativos Adobe {#adobe-applications}

O Experience Platform permite que os dados sejam assimilados de outros aplicativos do Adobe, incluindo Adobe Analytics e Adobe Audience Manager. Consulte os seguintes documentos relacionados para obter mais informações:

- [Visão geral do conector Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
- [Criar uma conexão de origem do Adobe Audience Manager na interface do usuário](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Visão geral da conexão da fonte de dados Classificações Adobe Analytics](connectors/adobe-applications/classifications.md)
- [Criar uma conexão de fonte de dados de classificações do Adobe Analytics na interface do usuário](./tutorials/ui/create/adobe-applications/classifications.md)
- [Visão geral da conexão da fonte de dados do conjunto de relatórios do Adobe Analytics](connectors/adobe-applications/analytics.md)
- [Criar uma conexão de origem do Adobe Analytics na interface do usuário](./tutorials/ui/create/adobe-applications/analytics.md)
- [Coleta de dados do Adobe](connectors/adobe-applications/data-collection.md)
- [Criar uma conexão de origem de Atributos do cliente na interface do usuário](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage] visão geral do conector](connectors/adobe-applications/marketo/marketo.md)
- [Crie um [!DNL Marketo Engage] conexão de origem na interface do usuário](./tutorials/ui/create/adobe-applications/marketo.md)

### Advertising {#advertising}

O Experience Platform oferece suporte para assimilar dados de um sistema de publicidade de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL Google AdWords]](connectors/advertising/ads.md) conector

### Armazenamento na nuvem {#cloud-storage}

As fontes de armazenamento em nuvem podem trazer seus próprios dados para a plataforma sem precisar baixar, formatar ou fazer upload. Os dados assimilados podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho Fontes por meio da interface do usuário. Consulte os seguintes documentos relacionados para obter mais informações:

- [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob]](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3]](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md)
- [[!DNL FTP]](connectors/cloud-storage/ftp.md)
- [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md)
- [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md)
- [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md)
- [[!DNL SFTP]](connectors/cloud-storage/sftp.md)

### Consentimento e preferências {#consent}

O Experience Platform oferece suporte para assimilar dados de uma plataforma de gerenciamento de consentimento e preferências de terceiros. Consulte os seguintes documentos relacionados para obter mais informações:

- [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md)


### Gerenciamento de Relacionamento com o Cliente (CRM) {#customer-relationship-management}

Os sistemas CRM fornecem dados que podem ajudar a criar relações com o cliente, o que, por sua vez, cria fidelidade e impulsiona a retenção do cliente. O Experience Platform fornece suporte para assimilar dados do CRM de [!DNL Microsoft Dynamics 365] e [!DNL Salesforce]. Consulte os seguintes documentos relacionados para obter mais informações:

- [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce]](connectors/crm/salesforce.md)
- [[!DNL Veeva CRM]](connectors/crm/veeva.md)
- [[!DNL Zoho CRM]](connectors/crm/zoho.md)

### Sucesso do cliente {#customer-success}

O Experience Platform oferece suporte para assimilar dados de um aplicativo de terceiros com sucesso do cliente. Consulte os seguintes documentos relacionados para obter mais informações:

- [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow]](connectors/customer-success/servicenow.md)

### Banco de dados {#database}

O Experience Platform oferece suporte para assimilar dados de um banco de dados de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL Amazon Redshift]](connectors/databases/redshift.md)
- [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md)
- [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md)
- [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md)
- [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md)
- [[!DNL Azure Table Storage]](connectors/databases/ats.md)
- [[!DNL Couchbase]](connectors/databases/couchbase.md)
- [[!DNL Google BigQuery]](connectors/databases/bigquery.md)
- [[!DNL GreenPlum]](connectors/databases/greenplum.md)
- [[!DNL HP Vertica]](connectors/databases/hp-vertica.md)
- [[!DNL IBM DB2]](connectors/databases/ibm-db2.md)
- [[!DNL MariaDB]](connectors/databases/mariadb.md)
- [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md)
- [[!DNL MySQL]](connectors/databases/mysql.md)
- [[!DNL Oracle]](connectors/databases/oracle.md)
- [[!DNL Phoenix]](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL]](connectors/databases/postgres.md)
- [[!DNL Snowflake]](connectors/databases/snowflake.md)

### eCommerce {#ecommerce}

O Experience Platform oferece suporte para assimilar dados de um sistema de comércio eletrônico de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### Sistema local {#local-system}

O Experience Platform oferece suporte para assimilar dados do sistema local. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [Upload de arquivo local](connectors/local-system/local-file-upload.md)

### Automação de marketing {#marketing-automation}

O Experience Platform oferece suporte para assimilar dados de um sistema de automação de marketing de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md)
- [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md)
- [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md)
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md)

### Pagamentos {#payments}

O Experience Platform fornece suporte para assimilação de dados de um sistema de pagamentos de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL PayPal]](connectors/payments/paypal.md)
- [[!DNL Square]](connectors/payments/square.md)

### Streaming {#streaming}

O Experience Platform oferece suporte para assimilar dados de fontes de transmissão. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL HTTP API]](connectors/streaming/http.md)

### Protocolos {#protocols}

O Experience Platform oferece suporte para assimilação de dados de um sistema de protocolos de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL Generic OData]](connectors/protocols/odata.md)
- [[!DNL Generic REST API]](connectors/protocols/generic-rest.md)

## Controle de acesso para fontes na assimilação de dados

As permissões para fontes na assimilação de dados podem ser gerenciadas na Adobe Admin Console. Você pode acessar permissões por meio do **[!UICONTROL Permissões]** em um perfil de produto específico. No **[!UICONTROL Editar permissões]** , você pode acessar as permissões pertencentes às fontes por meio do **[!UICONTROL ingestão de dados]** entrada do menu. O **[!UICONTROL Exibir fontes]** a permissão concede acesso somente leitura a fontes disponíveis no **[!UICONTROL Catálogo]** e fontes autenticadas na **[!UICONTROL Procurar]** enquanto a guia **[!UICONTROL Gerenciar fontes]** a permissão concede acesso total para ler, criar, editar e desativar fontes.

A tabela a seguir descreve como a interface do usuário se comporta com base em diferentes combinações dessas permissões:

| Nível de permissão | Descrição |
| ---- | ----|
| **[!UICONTROL Exibir fontes]** Ligado | Conceda acesso somente leitura a fontes em cada tipo-fonte na guia Catálogo , bem como nas guias Procurar, Contas e Fluxo de dados. |
| **[!UICONTROL Gerenciar fontes]** Ligado | Além das funções incluídas em **[!UICONTROL Exibir fontes]**, concede acesso a **[!UICONTROL Fonte do Connect]** em **[!UICONTROL Catálogo]** e **[!UICONTROL Selecionar dados]** em **[!UICONTROL Procurar]**. **[!UICONTROL Gerenciar fontes]** O também permite ativar ou desativar o **[!UICONTROL DataFlows]** e edite suas programações. |
| **[!UICONTROL Exibir fontes]** Desligado e **[!UICONTROL Gerenciar fontes]** Desligado | Revogar todo o acesso às fontes. |

Para obter mais informações sobre as permissões disponíveis concedidas por meio do Admin Console, incluindo essas quatro fontes, consulte o [visão geral do controle de acesso](../access-control/home.md).

## Termos e condições {#terms-and-conditions}

Ao usar qualquer uma das Fontes rotuladas como beta (&quot;Beta&quot;), Você reconhece que o Beta é fornecido ***&quot;no estado em que se encontra&quot; sem garantia de qualquer tipo***.

O Adobe não deve ter a obrigação de manter, corrigir, atualizar, alterar, modificar ou de qualquer outra forma suportar o Beta. Recomenda-se que tenha cuidado e não se baseie de forma alguma no correto funcionamento ou desempenho desses materiais Beta e/ou de acompanhamento. O Beta é considerado Informações Confidenciais do Adobe.

Qualquer &quot;Feedback&quot; (informações relacionadas ao Beta, incluindo, mas não se limitando a problemas ou defeitos que você encontra ao usar o Beta, sugestões, melhorias e recomendações) fornecidas por Você ao Adobe é atribuído ao Adobe, incluindo todos os direitos, título e interesse em e para tal Feedback.

Envie Feedback aberto ou crie um Tíquete de suporte para compartilhar suas sugestões ou relatar um erro, e procure um aprimoramento de recurso.
