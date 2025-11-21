---
audience: user
user-guide-title: Ajuda da Ingestão de dados da Adobe Experience Platform
breadcrumb-title: Guia da Ingestão de dados
user-guide-description: Traga seus dados para a Experience Platform por meio de uma ingestão em lote ou ingestão de transmissão.
feature: Data Ingestion
role: Developer
source-git-commit: f1d851afae5ad271e3c7d9d887f614058a262874
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 21%

---


# Assimilação de dados Adobe Experience Platform {#ingestion}

- [Visão geral da assimilação de dados](home.md)
- Assimilação por transmissão {#streaming}
   - [Visão geral](streaming-ingestion/overview.md)
   - [Conector Kafka](streaming-ingestion/kafka.md)
   - [Solução de problemas](streaming-ingestion/troubleshooting.md)
   - [Endereço IP ➡ Incluir na lista de permissões](streaming-ingestion/allowlisting.md)
- Assimilação em lote{#batch}
   - [Introdução às APIs de assimilação em lote](batch-ingestion/getting-started.md)
   - [Visão geral da API](batch-ingestion/overview.md)
   - [Guia do desenvolvedor de API](batch-ingestion/api-overview.md)
   - [Assimilação parcial de lote](batch-ingestion/partial.md)
   - [Solução de problemas](batch-ingestion/troubleshooting.md)
- Tutoriais {#tutorials}
   - Mapear um arquivo CSV para XDM {#map-csv}
      - [Visão geral](./tutorials/map-csv/overview.md)
      - [Mapear um arquivo CSV para um esquema existente](./tutorials/map-csv/existing-schema.md)
      - [Mapear um arquivo CSV usando recomendações geradas por IA](./tutorials/map-csv/recommendations.md)
   - [Assimilar dados em lote usando a interface do](tutorials/ingest-batch-data.md)
   - [Criar uma conexão de streaming autenticada](tutorials/create-authenticated-streaming-connection.md)
   - [Criar uma conexão de streaming (API)](tutorials/create-streaming-connection.md)
   - [Criar uma conexão de transmissão (UI)](tutorials/create-streaming-connection-ui.md)
   - [Transmissão de dados de registro](tutorials/streaming-record-data.md)
   - [Transmissão de dados de série temporal](tutorials/streaming-time-series-data.md)
   - [Transmissão de várias mensagens](tutorials/streaming-multiple-messages.md)
- Qualidade e monitoramento dos dados{#quality}
   - [Visão geral](quality/overview.md)
   - [Monitorar assimilação de dados](quality/monitor-data-ingestion.md)
   - [Recuperar diagnóstico de erro](quality/error-diagnostics.md)
   - [Recuperar lotes com falha](quality/retrieve-failed-batches.md)
   - [Validação de assimilação de streaming](quality/streaming-validation.md)
- [Medidas de proteção para assimilação de dados](guardrails.md)
- [Conectores do Source](source-connectors.md)
- [Referência da API de assimilação em lote](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)
- [Referência da API de assimilação de fluxo](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)
- [Notas de versão da Experience Platform](https://experienceleague.adobe.com/pt-br/docs/experience-platform/release-notes/latest)
