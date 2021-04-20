---
keywords: Experience Platform;início;tópicos populares;conectores de origem;conector de origem;fontes;fontes de dados;fonte de dados;conexão de fonte de dados
solution: Experience Platform
title: Visão geral dos conectores de origem
topic: overview
description: A Adobe Experience Platform permite que os dados sejam ingeridos de fontes externas e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamentos baseados em nuvem, bancos de dados e muitas outras.
translation-type: tm+mt
source-git-commit: 0e4fda4abf5c02df81b74f15d2fbcafb68548070
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 0%

---


# Visão geral dos conectores de origem

A Adobe Experience Platform permite que os dados sejam ingeridos de fontes externas e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamentos baseados em nuvem, bancos de dados e muitas outras.

[!DNL Flow Service] é usada para coletar e centralizar dados do cliente de várias fontes diferentes na Plataforma. O serviço fornece uma interface de usuário e uma RESTful API que permite configurar conexões de origem com facilidade para vários provedores de dados. Essas conexões de origem permitem autenticar sistemas de terceiros, definir horários para execuções de ingestão e gerenciar o throughput de ingestão de dados.

Com o Experience Platform, você pode centralizar os dados coletados de fontes diferentes e usar os insights obtidos com ele para fazer mais.

## Tipos de fontes

As fontes no Experience Platform são agrupadas nas seguintes categorias:

### aplicativos Adobe

O Experience Platform permite que os dados sejam assimilados de outros aplicativos Adobe, incluindo Adobe Analytics, Adobe Audience Manager e [!DNL Experience Platform Launch]. Consulte os seguintes documentos relacionados para obter mais informações:

- [Visão geral do conector Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
- [Criar uma conexão de origem Adobe Audience Manager na interface do usuário](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Visão geral do conector de dados de classificações Adobe Analytics](connectors/adobe-applications/classifications.md)
- [Criar uma conexão de fonte de dados de classificações da Adobe Analytics na interface do usuário](./tutorials/ui/create/adobe-applications/classifications.md)
- [Visão geral do conector de dados Adobe Analytics](connectors/adobe-applications/analytics.md)
- [Criar uma conexão de origem Adobe Analytics na interface do usuário](./tutorials/ui/create/adobe-applications/analytics.md)
- [Criar uma conexão de origem de Atributos do cliente na interface do usuário](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### Publicidade

O Experience Platform oferece suporte para assimilar dados de um sistema de publicidade de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL Google AdWords]](connectors/advertising/ads.md) conector

### Armazenamento em nuvem

As fontes de armazenamentos na nuvem podem trazer seus próprios dados para a Plataforma sem a necessidade de baixar, formatar ou fazer upload. Os dados ingeridos podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho Fontes usando a interface do usuário. Consulte os seguintes documentos relacionados para obter mais informações:

- [[!DNL Azure Data Lake Storage Gen2] conector](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob] conector](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis] conector](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3] conector](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS] conector](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs] conector](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage] conector](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL FTP] conector](connectors/cloud-storage/ftp.md)
- [[!DNL Google Cloud Storage] conector](connectors/cloud-storage/google-cloud-storage.md)
- [[!DNL Google PubSub] conector](connectors/cloud-storage/google-pubsub.md)
- [[!DNL Oracle Object Storage] conector](connectors/cloud-storage/oracle-object-storage.md)
- [[!DNL SFTP] conector](connectors/cloud-storage/sftp.md)

### Gerenciamento de Relacionamento com o Cliente (CRM)

Os sistemas CRM fornecem dados que podem ajudar a construir relações com os clientes, o que, por sua vez, cria fidelidade e impulsiona a retenção dos clientes. O Experience Platform oferece suporte para a assimilação de dados CRM de [!DNL Microsoft Dynamics 365] e [!DNL Salesforce]. Consulte os seguintes documentos relacionados para obter mais informações:

- [[!DNL Microsoft Dynamics] conector](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce] conector](connectors/crm/salesforce.md)

### Sucesso do cliente

O Experience Platform oferece suporte para a assimilação de dados de um aplicativo de terceiros com sucesso. Consulte os seguintes documentos relacionados para obter mais informações:

- [[!DNL Salesforce Service Cloud] conector](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow] conector](connectors/customer-success/servicenow.md)

### Banco de dados

O Experience Platform oferece suporte para assimilar dados de um banco de dados de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL Amazon Redshift] conector](connectors/databases/redshift.md)
- [[!DNL Apache Hive on Azure HDInsights] conector](connectors/databases/hive.md)
- [[!DNL Apache Spark on Azure HDInsights] conector](connectors/databases/spark.md)
- [[!DNL Azure Data Explorer] conector](connectors/databases/data-explorer.md)
- [[!DNL Azure Synapse Analytics] conector](connectors/databases/synapse-analytics.md)
- [[!DNL Azure Table Storage] conector](connectors/databases/ats.md)
- [[!DNL Couchbase] conector](connectors/databases/couchbase.md)
- [[!DNL Google BigQuery] conector](connectors/databases/bigquery.md)
- [[!DNL GreenPlum] conector](connectors/databases/greenplum.md)
- [[!DNL HP Vertica] conector](connectors/databases/hp-vertica.md)
- [[!DNL IBM DB2] conector](connectors/databases/ibm-db2.md)
- [[!DNL Microsoft SQL Server] conector](connectors/databases/sql-server.md)
- [[!DNL MySQL] conector](connectors/databases/mysql.md)
- [[!DNL Oracle] conector](connectors/databases/oracle.md)
- [[!DNL Phoenix] conector](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL] conector](connectors/databases/postgres.md)

### eCommerce

O Experience Platform oferece suporte para assimilar dados de um sistema de comércio eletrônico de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### Automação de marketing

O Experience Platform oferece suporte para assimilar dados de um sistema de automação de marketing de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL HubSpot] conector](connectors/marketing-automation/hubspot.md)

### Pagamentos

O Experience Platform oferece suporte para assimilar dados de um sistema de pagamentos de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL PayPal] conector](connectors/payments/paypal.md)

### Protocolos

O Experience Platform oferece suporte para assimilar dados de um sistema de protocolos de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL Generic OData] conector](connectors/protocols/odata.md)

## Controle de acesso para fontes na ingestão de dados

As permissões para fontes na ingestão de dados podem ser gerenciadas no Adobe Admin Console. Você pode acessar permissões por meio da guia **[!UICONTROL Permissões]** em um perfil de produto específico. No painel **[!UICONTROL Editar permissões]**, você pode acessar as permissões pertencentes às fontes por meio da entrada de menu **[!UICONTROL ingestão de dados]**. A permissão **[!UICONTROL Fontes de Visualização]** concede acesso somente leitura às fontes disponíveis na guia **[!UICONTROL Catálogo]** e às fontes autenticadas na guia **[!UICONTROL Procurar]**, enquanto a permissão **[!UICONTROL Gerenciar fontes]** concede acesso total às fontes de leitura, criação, edição e desativação.

A tabela a seguir descreve como a interface se comporta com base em diferentes combinações dessas permissões:

| Nível de permissão | Descrição |
| ---- | ----|
| **[!UICONTROL Fontes]** de visualização ativadas | Conceda acesso somente leitura às fontes em cada tipo de fonte na guia Catálogo, bem como nas guias Navegar, Contas e Fluxo de dados. |
| **[!UICONTROL Gerenciar]** fontesOn | Além das funções incluídas em **[!UICONTROL Fontes de Visualização]**, concede acesso à opção **[!UICONTROL Origem do Connect]** em **[!UICONTROL Catálogo]** e à opção **[!UICONTROL Selecionar Dados]** em **[!UICONTROL Procurar]**. **[!UICONTROL Gerenciar]** fontes também permite ativar ou desativar  **** DataFlowes e editar seus agendamentos. |
| **[!UICONTROL Fontes]** de visualização Desligadas e  **[!UICONTROL Gerenciar]** fontes Desligadas | Revogar todo o acesso às fontes. |

Para obter mais informações sobre as permissões disponíveis concedidas pelo Admin Console, incluindo essas quatro fontes, consulte a [visão geral do controle de acesso](../access-control/home.md).

## Termos e condições {#terms-and-conditions}

Ao usar qualquer uma das Fontes rotuladas como beta (&quot;Beta&quot;), Você reconhece que o Beta é fornecido ***&quot;no estado em que se encontra&quot; sem garantia de qualquer tipo***.

O Adobe não tem a obrigação de manter, corrigir, atualizar, alterar, modificar ou suportar o Beta. Recomenda-se que tenha cuidado e que não se baseie de forma alguma no funcionamento ou desempenho corretos desses materiais Beta e/ou associados. O Beta é considerado Informações Confidenciais do Adobe.

Qualquer &quot;Feedback&quot; (informações relacionadas ao Beta incluindo, mas não se limitando a, problemas ou defeitos encontrados durante a utilização do Beta, sugestões, melhorias e recomendações) fornecido por Você ao Adobe é atribuído ao Adobe, incluindo todos os direitos, título e interesse em e para tal Feedback.

Enviar feedback em aberto ou criar um tíquete de suporte para compartilhar suas sugestões ou relatar um erro, busque um aprimoramento de recurso.
