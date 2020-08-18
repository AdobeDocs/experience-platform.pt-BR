---
keywords: Experience Platform;home;popular topics;source connectors;source connector;sources;data sources;data source;data source connection
solution: Experience Platform
title: Visão geral dos Conectores de origem Adobe Experience Platform
topic: overview
description: A Adobe Experience Platform permite que os dados sejam ingeridos de fontes externas e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamentos baseados em nuvem, bancos de dados e muitas outras.
translation-type: tm+mt
source-git-commit: c15f582eeaa895f03441b2f488686a9a48942f3d
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 0%

---


# Visão geral dos conectores de origem

A Adobe Experience Platform permite que os dados sejam ingeridos de fontes externas e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamentos baseados em nuvem, bancos de dados e muitas outras.

[!DNL Experience Platform] fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem com vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar sistemas de terceiros, definir horários para execuções de ingestão e gerenciar o throughput de ingestão de dados.

Com [!DNL Experience Platform]isso, você pode centralizar os dados coletados de fontes diferentes e usar os insights obtidos com eles para fazer mais.

## Tipos de fontes

As fontes em [!DNL Experience Platform] são agrupadas nas seguintes categorias:

### aplicativos Adobe

[!DNL Experience Platform] permite que os dados sejam assimilados de outros aplicativos Adobe, incluindo Adobe Analytics, Adobe Audience Manager e [!DNL Experience Platform Launch]. Consulte os seguintes documentos relacionados para obter mais informações:

- [Visão geral do conector Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
- [Criar um conector de origem Adobe Audience Manager na interface do usuário](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Visão geral do conector de dados Adobe Analytics](connectors/adobe-applications/analytics.md)
- [Criar um conector de origem Adobe Analytics na interface do usuário](./tutorials/ui/create/adobe-applications/analytics.md)
- [Criar um conector de origem de Atributos do cliente na interface do usuário](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### Publicidade

[!DNL Experience Platform] fornece suporte para assimilar dados de um sistema de publicidade de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [!DNL Google AdWords](connectors/advertising/ads.md) conector

### Armazenamento em nuvem

As fontes de armazenamentos na nuvem podem inserir seus próprios dados [!DNL Platform] sem a necessidade de baixar, formatar ou fazer upload. Os dados ingeridos podem ser formatados como XDM JSON, XDM parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho Fontes usando a interface do usuário. Consulte os seguintes documentos relacionados para obter mais informações:

- [!DNL Azure Data Lake Storage Gen2](connectors/cloud-storage/adls-gen2.md) conector
- [!DNL Azure Blob](connectors/cloud-storage/blob.md) conector
- [!DNL Amazon Kinesis](connectors/cloud-storage/kinesis.md) conector
- [!DNL Amazon S3](connectors/cloud-storage/s3.md) conector
- [!DNL Apache HDFS](connectors/cloud-storage/hdfs.md) conector
- [!DNL Azure Event Hubs](connectors/cloud-storage/eventhub.md) conector
- [!DNL Azure File Storage](connectors/cloud-storage/azure-file-storage.md) conector
- [!DNL FTP and SFTP](connectors/cloud-storage/ftp-sftp.md) conector
- [!DNL Google Cloud Storage](connectors/cloud-storage/google-cloud-storage.md) conector

### Gerenciamento de Relacionamento com o Cliente (CRM)

Os sistemas CRM fornecem dados que podem ajudar a construir relações com os clientes, o que, por sua vez, cria fidelidade e impulsiona a retenção dos clientes. [!DNL Experience Platform] fornece suporte para assimilar dados do CRM de [!DNL Microsoft Dynamics 365] e [!DNL Salesforce]. Consulte os seguintes documentos relacionados para obter mais informações:

- [!DNL Microsoft Dynamics](connectors/crm/ms-dynamics.md) conector
- [!DNL Salesforce](connectors/crm/salesforce.md) conector

### Sucesso do cliente

[!DNL Experience Platform] fornece suporte para assimilar dados de um aplicativo de cliente bem-sucedido de terceiros. Consulte os seguintes documentos relacionados para obter mais informações:

- [!DNL Salesforce Service Cloud](connectors/customer-success/salesforce-service-cloud.md) conector
- [!DNL ServiceNow](connectors/customer-success/servicenow.md) conector

### Banco de dados

[!DNL Experience Platform] fornece suporte para assimilar dados de um banco de dados de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [!DNL Amazon Redshift](connectors/databases/redshift.md) conector
- [!DNL Apache Hive on Azure HDInsights](connectors/databases/hive.md) conector
- [!DNL Apache Spark on Azure HDInsights](connectors/databases/spark.md) conector
- [!DNL Azure Data Explorer](connectors/databases/data-explorer.md) conector
- [!DNL Azure Synapse Analytics](connectors/databases/synapse-analytics.md) conector
- [!DNL Azure Table Storage](connectors/databases/ats.md) conector
- [!DNL Couchbase](connectors/databases/couchbase.md) conector
- [!DNL Google BigQuery](connectors/databases/bigquery.md) conector
- [!DNL GreenPlum](connectors/databases/greenplum.md) conector
- [!DNL HP Vertica](connectors/databases/hp-vertica.md) conector
- [!DNL IBM DB2](connectors/databases/ibm-db2.md) conector
- [!DNL Microsoft SQL Server](connectors/databases/sql-server.md) conector
- [!DNL MySQL](connectors/databases/mysql.md) conector
- [!DNL Oracle](connectors/databases/oracle.md) conector
- [!DNL Phoenix](connectors/databases/phoenix.md) conector
- [!DNL PostgreSQL](connectors/databases/postgres.md) conector

### Automação de marketing

[!DNL Experience Platform] fornece suporte para assimilar dados de um sistema de automação de marketing de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [!DNL HubSpot](connectors/marketing-automation/hubspot.md) conector

### Pagamentos

[!DNL Experience Platform] fornece suporte para a assimilação de dados de um sistema de pagamentos de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [!DNL PayPal](connectors/payments/paypal.md) conector

### Protocolos

[!DNL Experience Platform] fornece suporte para assimilar dados de um sistema de protocolos de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [!DNL Generic OData](connectors/protocols/odata.md) conector

## Controle de acesso para fontes na ingestão de dados

As permissões para fontes na ingestão de dados podem ser gerenciadas no Adobe Admin Console. Você pode acessar permissões por meio da guia *[!UICONTROL Permissões]* em um perfil de produto específico. No painel **[!UICONTROL Editar permissões]** , é possível acessar as permissões pertencentes às fontes por meio da entrada do menu de ingestão *[!UICONTROL de]* dados. A permissão Fontes **[!UICONTROL de]** Visualização concede acesso somente leitura a fontes disponíveis na guia *[!UICONTROL Catálogo]* e a fontes autenticadas na guia *[!UICONTROL Procurar]* , enquanto a permissão **[!UICONTROL Gerenciar fontes]** concede acesso total a fontes de leitura, criação, edição e desativação.

A tabela a seguir descreve como a interface se comporta com base em diferentes combinações dessas permissões:

| Nível de permissão | Descrição |
| ---- | ----|
| **[!UICONTROL Fontes]** de visualização ativadas | Conceda acesso somente leitura às fontes em cada tipo de fonte na guia *Catálogo* , bem como nas guias *Procurar*, *Contas* e *DataFlow* . |
| **[!UICONTROL Gerenciar fontes]** em | Além das funções incluídas nas Fontes **[!UICONTROL de]** Visualização, concede acesso à opção Fonte *[!UICONTROL do]* Connect no *[!UICONTROL Catálogo]* e à opção *[!UICONTROL Selecionar dados]* na *[!UICONTROL Navegação]*. **[!UICONTROL Gerenciar fontes]** também permite ativar ou desativar *[!UICONTROL DataFlows]* e editar seus agendamentos. |
| **[!UICONTROL Fontes]** de visualização desativadas e **[!UICONTROL gerenciamento de fontes]** desativadas | Revogar todo o acesso às fontes. |

Para obter mais informações sobre as permissões disponíveis concedidas através do Admin Console, incluindo essas quatro fontes, consulte a visão geral [do](../access-control/home.md)controle de acesso.

## Termos e condições {#terms-and-conditions}

Ao usar qualquer uma das Fontes rotuladas como beta (&quot;Beta&quot;), Você reconhece pela presente que o Beta é fornecido ***&quot;no estado em que se encontra&quot; sem garantia de qualquer tipo***.

O Adobe não tem a obrigação de manter, corrigir, atualizar, alterar, modificar ou suportar o Beta. Recomenda-se que tenha cuidado e que não se baseie de forma alguma no funcionamento ou desempenho corretos desses materiais Beta e/ou associados. O Beta é considerado Informações Confidenciais do Adobe.

Qualquer &quot;Feedback&quot; (informações relacionadas ao Beta incluindo, mas não se limitando a, problemas ou defeitos encontrados durante a utilização do Beta, sugestões, melhorias e recomendações) fornecido por Você ao Adobe é atribuído ao Adobe, incluindo todos os direitos, título e interesse em e para tal Feedback.

Enviar feedback em aberto ou criar um tíquete de suporte para compartilhar suas sugestões ou relatar um erro, busque um aprimoramento de recurso.
