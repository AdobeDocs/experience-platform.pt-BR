---
product: experience-platform
audience: user
user-guide-title: Ajuda para ingestão de dados da Adobe Experience Platform
user-guide-description: Adobe Experience Platform brings data from multiple sources together in order to help marketers better understand the behavior of their customers. Adobe Experience Platform Data Ingestion represents the multiple methods by which Platform ingests data from these sources, as well as how that data is persisted within the Data Lake for use by downstream Platform services.
translation-type: tm+mt
source-git-commit: bd3c31e7d39f7f66d755356a3dbb754e97c196fb
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 7%

---


# Adobe Experience Platform Data Ingestion {#ingestion}

- [Visão geral da ingestão de dados](home.md)
- Streaming ingestion {#streaming}
   - [Visão geral](streaming-ingestion/overview.md)
   - [Conector Kafka](streaming-ingestion/kafka.md)
   - [Solução de problemas](streaming-ingestion/troubleshooting.md)
- Ingestão em lote{#batch}
   - [Visão geral](batch-ingestion/overview.md)
   - [API de ingestão em lote](batch-ingestion/api-overview.md)
   - [Ingestão parcial em lote](batch-ingestion/partial.md)
   - [Solução de problemas](batch-ingestion/troubleshooting.md)
- Tutoriais {#tutorials}
   - [Mapear um arquivo CSV para XDM](tutorials/map-a-csv-file.md)
   - [Ingressar dados em lote usando a interface do usuário](tutorials/ingest-batch-data.md)
   - [Criar uma conexão de streaming autenticada](tutorials/create-authenticated-streaming-connection.md)
   - [Criar uma conexão de streaming (API)](tutorials/create-streaming-connection.md)
   - [Criar uma conexão de streaming (UI)](tutorials/create-streaming-connection-ui.md)
   - [Transmissão de dados de registro](tutorials/streaming-record-data.md)
   - [Transmissão de dados de séries temporais](tutorials/streaming-time-series-data.md)
   - [Transmissão de várias mensagens](tutorials/streaming-multiple-messages.md)
- Qualidade e monitorização da ingestão de dados{#quality}
   - [Visão geral](quality/overview.md)
   - [Monitorar fluxos de dados](quality/monitor-data-flows.md)
   - [Recuperar lotes com falha](quality/retrieve-failed-batches.md)
   - [Validação de ingestão de fluxo](quality/streaming-validation.md)
   - [Assinar eventos de ingestão de dados](quality/subscribe-events.md)
- [Conectores de origem](source-connectors.md)
- [Referência da API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)
- [Notas de versão da plataforma](https://www.adobe.com/go/platform-release-notes-en)