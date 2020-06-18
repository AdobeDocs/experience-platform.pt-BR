---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visão geral dos conectores de origem de Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: a9ce046d6ee8622e23f31edbbf777b045109c13b
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 0%

---


# Visão geral dos conectores de origem

O Adobe Experience Platform permite que os dados sejam ingeridos de fontes externas e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços Platform. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamentos baseados em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece uma RESTful API e uma interface de usuário interativa que permite configurar conexões de origem com vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar sistemas de terceiros, definir horários para execuções de ingestão e gerenciar o throughput de ingestão de dados.

Com o Experience Platform, você pode centralizar os dados coletados de fontes diferentes e usar os insights obtidos com ele para fazer mais.

## Tipos de fontes

As fontes no Experience Platform são agrupadas nas seguintes categorias:

### Aplicativos da Adobe

O Experience Platform permite que os dados sejam assimilados de outros aplicativos da Adobe, incluindo Adobe Analytics, Adobe Audience Manager e Experience Platform Launch. Consulte os seguintes documentos relacionados para obter mais informações:

- [Visão geral do conector Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
- [Criar um conector de fonte de Adobe Audience Manager na interface do usuário](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Visão geral do conector de dados Analytics](connectors/adobe-applications/analytics.md)
- [Criar um conector de origem do Adobe Analytics na interface do usuário](./tutorials/ui/create/adobe-applications/analytics.md)
- [Criar um conector de origem de Atributos do cliente na interface do usuário](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### Publicidade

O Experience Platform oferece suporte para assimilar dados de um sistema de publicidade de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [Conector Google AdWords](connectors/advertising/ads.md)

### Armazenamento em nuvem

As fontes de armazenamentos na nuvem podem trazer seus próprios dados para o Platform sem a necessidade de baixar, formatar ou fazer upload. Os dados ingeridos podem ser formatados como XDM JSON, XDM parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho Fontes usando a interface do usuário. Consulte os seguintes documentos relacionados para obter mais informações:

- [Conector Gen2 do Armazenamento Azure Data Lake](connectors/cloud-storage/adls-gen2.md)
- [Conector Azure Blob e Amazon S3](connectors/cloud-storage/blob-s3.md)
- [Conector Amazon Kinesis](connectors/cloud-storage/kinesis.md)
- [Conector HDFS Apache](connectors/cloud-storage/hdfs.md)
- [Conector Hubs de Evento do Azure](connectors/cloud-storage/eventhub.md)
- [Conector do Armazenamento de Arquivo do Azure](connectors/cloud-storage/azure-file-storage.md)
- [Conector FTP e SFTP](connectors/cloud-storage/ftp-sftp.md)
- [Conector de Armazenamento do Google Cloud](connectors/cloud-storage/google-cloud-storage.md)

### Gerenciamento de Relacionamento com o Cliente (CRM)

Os sistemas CRM fornecem dados que podem ajudar a construir relações com os clientes, o que, por sua vez, cria fidelidade e impulsiona a retenção dos clientes. O Experience Platform oferece suporte para a assimilação de dados do CRM do Microsoft Dynamics 365 e do Salesforce. Consulte os seguintes documentos relacionados para obter mais informações:

- [Conector do Microsoft Dynamics](connectors/crm/ms-dynamics.md)
- [Conector Salesforce](connectors/crm/salesforce.md)

### Sucesso do cliente

O Experience Platform oferece suporte para a assimilação de dados de um aplicativo de terceiros com sucesso. Consulte os seguintes documentos relacionados para obter mais informações:

- [Conector da Salesforce Service Cloud](connectors/customer-success/salesforce-service-cloud.md)
- [Conector ServiceNow](connectors/customer-success/servicenow.md)

### Banco de dados

O Experience Platform oferece suporte para assimilar dados de um banco de dados de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [Conector Amazon Redshift](connectors/databases/redshift.md)
- [Apache Hive no conector Azure HDInsights](connectors/databases/hive.md)
- [Apache Spark no conector Azure HDInsights](connectors/databases/spark.md)
- [Conector do Azure Data Explorer](connectors/databases/data-explorer.md)
- [Conector Analytics do Azure Synapse](connectors/databases/synapse-analytics.md)
- [Conector de Armazenamento de Tabela do Azure](connectors/databases/ats.md)
- [Conector Couchbase](connectors/databases/couchbase.md)
- [Conector Google BigQuery](connectors/databases/bigquery.md)
- [Conector GreenPlum](connectors/databases/greenplum.md)
- [Conector HP Vertica](connectors/databases/hp-vertica.md)
- [Conector IBM DB2](connectors/databases/ibm-db2.md)
- [Conector MariaDB](connectors/databases/mariadb.md)
- [Conector do Microsoft SQL Server](connectors/databases/sql-server.md)
- [Conector MySQL](connectors/databases/mysql.md)
- [Conector Oracle](connectors/databases/oracle.md)
- [Conector Phoenix](connectors/databases/phoenix.md)
- [Conector PostgreSQL](connectors/databases/postgres.md)

### Automação de marketing

O Experience Platform oferece suporte para assimilar dados de um sistema de automação de marketing de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [Conector HubSpot](connectors/marketing-automation/hubspot.md)

### Pagamentos

O Experience Platform oferece suporte para assimilar dados de um sistema de pagamentos de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [Conector PayPal](connectors/payments/paypal.md)

### Protocolos

O Experience Platform oferece suporte para assimilar dados de um sistema de protocolos de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [Conector OData genérico](connectors/protocols/odata.md)

## Controle de acesso para fontes na ingestão de dados

As permissões para fontes na ingestão de dados podem ser gerenciadas no Adobe Admin Console. Você pode acessar permissões por meio da guia *Permissões* em um perfil de produto específico. No painel **Editar permissões** , é possível acessar as permissões pertencentes às fontes por meio da entrada do menu de ingestão *de* dados. A permissão Fontes **de** Visualização concede acesso somente leitura a fontes disponíveis na guia *Catálogo* e a fontes autenticadas na guia *Procurar* , enquanto a permissão **Gerenciar fontes** concede acesso total a fontes de leitura, criação, edição e desativação.

A tabela a seguir descreve como a interface se comporta com base em diferentes combinações dessas permissões:

| Nível de permissão | Descrição |
| ---- | ----|
| **Fontes** de Visualização ativadas | Conceda acesso somente leitura às fontes em cada tipo de fonte na guia *Catálogo* , bem como nas guias *Procurar*, *Contas* e *DataFlow* . |
| **Gerenciar fontes** em | Além das funções incluídas nas Fontes **de** Visualização, concede acesso à opção Fonte *do* Connect no *Catálogo* e à opção *Selecionar dados* na *Navegação*. **Gerenciar fontes** também permite ativar ou desativar *DataFlows* e editar seus agendamentos. |
| **Fontes** de Visualização desativadas e **gerenciamento de fontes** desativadas | Revogar todo o acesso às fontes. |

Para obter mais informações sobre as permissões disponíveis concedidas pela Admin Console, incluindo essas quatro fontes, consulte a visão geral [do](../access-control/home.md)controle de acesso.

## Termos e condições {#terms-and-conditions}

Ao usar qualquer uma das Fontes rotuladas como beta (&quot;Beta&quot;), Você reconhece pela presente que o Beta é fornecido ***&quot;no estado em que se encontra&quot; sem garantia de qualquer tipo***.

A Adobe não tem a obrigação de manter, corrigir, atualizar, alterar, modificar ou, de outra forma, suportar o Beta. Recomenda-se que tenha cuidado e que não se baseie de forma alguma no funcionamento ou desempenho corretos desses materiais Beta e/ou associados. O Beta é considerado Informações confidenciais da Adobe.

Qualquer &quot;Feedback&quot; (informações relacionadas ao Beta, incluindo, mas não se limitando a, problemas ou defeitos que você encontrar ao usar o Beta, sugestões, melhorias e recomendações) fornecido por Você à Adobe é atribuído à Adobe, incluindo todos os direitos, título e interesse em e para tal Feedback.

Enviar feedback em aberto ou criar um tíquete de suporte para compartilhar suas sugestões ou relatar um erro, busque um aprimoramento de recurso.
