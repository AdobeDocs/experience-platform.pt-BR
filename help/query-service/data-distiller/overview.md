---
title: Visão geral da Distiller de dados
description: Um resumo dos limites de uso do Data Distiller para dados do Serviço de query em relação ao seu direito de licenciamento.
source-git-commit: ae4ecd43071a198592193a1a598a064cdc6be2f6
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 1%

---

# Visão geral do Data Distiller

O Data Distiller é uma oferta de pacote que inclui um subconjunto das funcionalidades do Adobe Experience Platform. Com o Data Distiller, você pode executar a preparação de dados pós-ingestão (como limpeza, modelagem e manipulação) para o perfil do cliente em tempo real ou casos de uso analítico executando consultas em lote no Serviço de query. O uso do Data Distiller depende de sua qualificação para aplicativos baseados na plataforma.

## Uso da licença {#license-usage}

O  [Painel de uso da licença do Data Distiller](./license-usage.md) O está disponível depois que você comprou o Data Distiller e as horas de computação. O painel de uso da licença ajuda você a monitorar o consumo das horas de computação autorizadas. Consulte a [Documento de uso da licença do Data Distiller](./license-usage.md) para exibir informações importantes sobre o uso da licença do Serviço de query de sua organização.

<!-- Update these descriptions post 23.3 release
## Scoping parameters {#scoping-parameters}

Scoping parameters are usage limits that relate to the scoping of your required set up, and are defined by your license capacity. Without add-ons, Data Distiller's scoping parameters are as follows: 

* **Compute Hours**: You can use PSQL or the Query Service API to run batch queries executed in any sandbox (scheduled or otherwise) to scan and write data. This uses your allotted Compute Hours per year as determined in the scoping process of your license agreement. Total Compute Hours is accumulated across all Sandboxes.
* **Data Ingested**: The data ingested into Adobe Experience Platform which can be queried using Data Distiller is subject to the limitations described in your then-current license to Adobe Real-Time Customer Data Platform, Customer Journey Analytics, and/or Adobe Journey Optimizer.
* **Data Lake Storage**: The data lake storage provided in your then-current license to Adobe Real-Time Customer Data Platform, Customer Journey Analytics, and/or Adobe Journey Optimizer may also be used with Data Distiller. Data Lake Storage is a shared feature.
* **Query Service Users**: The number of Query Service users detailed in your then-current license to Adobe Real-Time Customer Data Platform, Customer Journey Analytics, and/or Adobe Journey Optimizer may also be used with Data Distiller. Query Service Users is a shared feature. 
-->

## Medidas de proteção

Consulte a [Medidas de proteção do serviço de consulta](../guardrails.md) documento sobre limites de uso padrão para dados do Serviço de query em relação ao seu direito de licenciamento.

<!-- Update these descriptions post 23.3 release
## Static limits

A static limit is the usage limit that relates to the functional boundaries of Adobe Experience Platform Activation. [More information on Adobe Experience Platform Activation](https://helpx.adobe.com/ca/legal/product-descriptions/adobe-experience-platform0.html) can be found in the Adobe help documents. A summary of Data Distiller static limits are listed below, for more complete information please refer to the Query Service guardrail document.  

* **Batch Queries**: Scheduled batch queries time out after 24 hours.
* **Query Service**: You can use Query Service for the following purposes: 
    * To run SQL queries for data analysis and post ingestion data preparation (cleaning, shaping, and manipulation).
    * To run SQL queries to create roll-up metrics to surface directly into a BI tool.
    * To quickly inspect data within Adobe Experience Platform.
    * To generate meaningful insights from your data.
* **Reporting API Call**: To ensure queries run on aggregated data using the reporting API have enough resources to execute efficiently. This includes queries that enhance existing data models such as those provided by Real-Time Customer Data Platform. The reporting API tracks resource utilization by assigning concurrency slots to each query. A maximum of four reporting API calls are available concurrently. If you access the reporting API through a BI tool and require more concurrency slots, a BI server is required.
-->

