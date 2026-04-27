---
title: Explorar, solucionar problemas e verificar a assimilação em lote com o SQL
description: Saiba como entender e gerenciar o processo de assimilação de dados no Adobe Experience Platform. Este documento inclui como verificar lotes e consultar dados assimilados.
exl-id: 8f49680c-42ec-488e-8586-50182d50e900
source-git-commit: 7fac5ebd3f81e6f4b9f601ab1d9252402cad52b6
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 0%

---

# Explore, solucione problemas e verifique a assimilação em lote com o SQL

Este documento explica como verificar e validar registros em lotes assimilados com o SQL. Este documento ensina como:

- Acessar metadados em lote do conjunto de dados
- Solucionar problemas e garantir a integridade dos dados consultando lotes

>[!NOTE]
>
>Algumas capturas de tela neste guia foram tiradas de [!DNL DBVisualizer]. Para saber como [conectar o Serviço de Consulta com DBVisualizer](../clients/dbvisulaizer.md) ou outras [ferramentas de BI de terceiros](../clients/overview.md), consulte a documentação vinculada.

## Pré-requisitos

Para ajudar na compreensão dos conceitos discutidos neste documento, você deve ter conhecimento dos seguintes tópicos:

- **Assimilação de dados**: consulte a [visão geral da assimilação de dados](../../ingestion/home.md) para saber as noções básicas de como os dados são assimilados na Experience Platform, incluindo os diferentes métodos e processos envolvidos.
- **Assimilação em lote**: consulte a [visão geral da API de assimilação em lote](../../ingestion/batch-ingestion/overview.md) para saber mais sobre os conceitos básicos de assimilação em lote. Especificamente, o que é um &quot;lote&quot; e como ele funciona no processo de assimilação de dados da Experience Platform.
- **Metadados do sistema em conjuntos de dados**: consulte a [visão geral do Serviço de Catálogo](../../catalog/home.md) para saber como os campos de metadados do sistema são usados para rastrear e consultar dados assimilados.
- **Experience Data Model (XDM)**: consulte a [visão geral da interface do usuário de esquemas](../../xdm/ui/overview.md) e as [&#39;noções básicas da composição de esquema&#39;](../../xdm/schema/composition.md) para saber mais sobre esquemas XDM e como eles representam e validam a estrutura e o formato dos dados assimilados na Experience Platform.

## Acessar metadados em lote do conjunto de dados {#access-dataset-batch-metadata}

Para garantir que as colunas do sistema (colunas de metadados) sejam incluídas nos resultados da consulta, use o comando SQL `set drop_system_columns=false` no Editor de Consultas. Isso configura o comportamento da sessão de consulta SQL. Esta entrada deve ser repetida se você iniciar uma nova sessão.

Em seguida, para exibir os campos de sistema do conjunto de dados, execute uma instrução SELECT all para exibir os resultados do conjunto de dados, por exemplo `select * from movie_data`. Os resultados incluem duas novas colunas no lado direito `_acp_system_metadata` e `_ACP_BATCHID`. As colunas de metadados `_acp_system_metadata` e `_ACP_BATCHID` ajudam a identificar as partições lógica e física dos dados assimilados.

![A interface do usuário do DBVisualizer com a tabela movie_data e suas colunas de metadados exibidas e realçadas.](../images/use-cases/movie_data-table-with-metadata-columns.png)

Quando os dados são assimilados na Experience Platform, ela recebe uma partição lógica com base nos dados recebidos. This logical partition is represented by `_acp_system_metadata.acp_sourceBatchId`. This ID helps to group and identify the data batches logically before they are processed and stored.

After the data is processed and ingested into the data lake, it is assigned a physical partition represented by `_ACP_BATCHID`. This ID reflects the actual storage partition in the data lake where the ingested data resides.

### Use SQL to understand logical and physical partitions {#understand-partitions}

To help understand how the data is grouped and distributed after ingestion, use the following query to count the number of distinct physical partitions (`_ACP_BATCHID`) for each logical partition (`_acp_system_metadata.acp_sourceBatchId`).

```SQL
SELECT  _acp_system_metadata, COUNT(DISTINCT _ACP_BATCHID) FROM movie_data
GROUP BY _acp_system_metadata
```

The results of this query are shown in the image below.

![The results of a query to show the number of distinct physical partitions for each logical partition.](../images/use-cases/logical-and-physical-partition-count.png)

These results demonstrate that the number of input batches does not necessarily match the number of output batches, as the system determines the most efficient way to batch and store the data in the data lake.

For the purpose of this example, it is assumed that you have ingested a CSV file into Experience Platform and created a dataset called `drug_checkout_data`.

The `drug_checkout_data` file is a deeply nested set of 35,000 records. Use the SQL statement `SELECT * FROM drug_orders;` to preview of the first set of records in the JSON-based `drug_orders` dataset.

The image below shows a preview of the file and its records.

![A preview of the first set of records in the JSON-based drug_orders dataset.](../images/use-cases/drug-orders-preview.png)

### Use SQL to generate insights on batch ingestion process {#sql-insights-on-batch-ingestion}

Use the SQL statement below to provide insights into how the data ingestion process has grouped and processed the input records into batches.

```sql
SELECT _acp_system_metadata,
       Count(DISTINCT _acp_batchid) AS numoutputbatches,
       Count(_acp_batchid)          AS recordcount
FROM   drug_orders
GROUP  BY _acp_system_metadata 
```

The query results are seen in the image below.

![A table showing the distribution of how input batches were mastered at a time with record counts.](../images/use-cases/distribution-of-input-batches.png)

The results demonstrate the efficiency and behavior of the data ingestion process. Although three input batches were created -- each containing 2000, 24000, and 9000 records -- when the records were combined and deduplicated, only one unique batch remained.

>[!NOTE]
>
>All the records that are visible within a dataset are the ones that were successfully ingested. A successful batch ingestion does not mean that all the records that were sent from the source input are present. You must check for data ingestion failures to find the batches/records that did not make it in.

## Validate a batch with SQL {#validate-a-batch-with-SQL}

Next, validate and verify the records that have been ingested into the dataset with SQL.

>[!TIP]
>
>To retrieve the batch ID and query records associated with that batch ID, you must first  create a batch within Experience Platform. If you want to test the process yourself, you can ingest CSV data into Experience Platform. Read the guide on how to [map a CSV file to an existing XDM schema using AI-generated recommendations](../../ingestion/tutorials/map-csv/recommendations.md).

Once you have ingested a batch, you must navigate to the [!UICONTROL Datasets activity tab] for the dataset you ingested data into.

In the Experience Platform UI, select **[!UICONTROL Datasets]** in the left-navigation to open the [!UICONTROL Datasets] dashboard. Next, select the name of the dataset from the [!UICONTROL Browse] tab to access the [!UICONTROL Dataset activity] screen.

![The Experience Platform UI Datasets dashboard with Datasets highlighted in left navigation.](../images/use-cases/datasets-workspace.png)

The [!UICONTROL Dataset activity] view appears. This view contains details of your selected dataset. It includes any ingested batches which are displayed in a table format.

Select a batch from the list of available batches and copy the [!UICONTROL Batch ID] from the details panel on the right.

![The Experience Platform Datasets UI showing the ingested records with a batch ID highlighted.](../images/use-cases/batch-id.png)

Next, use the following query to retrieve all the records that were included in the dataset as part of that batch:

```sql
SELECT * FROM movie_data
WHERE  _acp_batchid='01H00BKCTCADYRFACAAKJTVQ8P' 
LIMIT 1;
```

The `_ACP_BATCHID` keyword is used to filter the [!UICONTROL Batch ID].

>[!TIP]
>
>The `LIMIT` clause is helpful if you want to restrict the number of rows displayed, but a filter condition is more desirable.

When you execute this query in the Query Editor, the results are truncated to 100 rows. The Query Editor is designed for quick previews and investigation. To retrieve up to 50,000 rows, you can use a third-party tool like DBVisualizer or DBeaver.

## Próximas etapas {#next-steps}

By reading this document, you learned the essentials of verifying and validating records in ingested batches as part of the data ingestion process. You also gained insights into accessing dataset batch metadata, understanding logical and physical partitions, and querying specific batches using SQL commands. This knowledge can help you ensure data integrity and optimize your data storage on Experience Platform.

Next, you should practice data ingestion to apply the concepts learned. Ingest a sample dataset into Experience Platform with either the provided sample files or your own data. If you have not done so already, read the tutorial on how to [ingest data into Adobe Experience Platform](../../ingestion/tutorials/ingest-batch-data.md).

Alternatively, you could learn how to [connect and verify Query Service with a variety of desktop client applications](../clients/overview.md) to enhance your data analysis capabilities.
