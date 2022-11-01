---
audience: user
user-guide-title: Ajuda do Serviço de consulta da Adobe Experience Platform
breadcrumb-title: Guia do Serviço de consulta
user-guide-description: Use o SQL padrão para consultar dados no data lake na Experience Platform.
feature: Queries
source-git-commit: 745cf377cebb6f612820d963d9207bfec3c12338
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 18%

---


# Serviço de query Adobe Experience Platform {#query}

- [Visão geral do Serviço de query](home.md)
- [Pacote do Serviço de Consulta](packages.md)
- [Medidas de proteção do serviço de consulta](guardrails.md)
- Distiller de dados {#data-distiller}
   - [Uso da licença](data-distiller/licence-usage.md)
- Introdução {#get-started}
   - [Pré-requisitos](get-started/prerequisites.md)
- Casos de uso {#use-cases}
   - [Navegador abandonado](use-cases/abandoned-browse.md)
   - [Análise de atividade com o Adobe Target](use-cases/activity-analysis-with-adobe-target.md)
   - [Análise de atribuição](use-cases/attribution-analysis.md)
   - [Filtragem de bot](use-cases/bot-filtering.md)
   - [Insights do Web e de análises móveis](use-cases/analytics-insights.md)
- API do serviço de consulta {#api}
   - [Introdução](api/getting-started.md)
   - [Consultas](api/queries.md)
   - [Parâmetros de conexão](api/connection-parameters.md)
   - [Consultas agendadas](api/scheduled-queries.md)
   - [É executado para consultas agendadas](api/runs-scheduled-queries.md)
   - [Templates de query](api/query-templates.md)
   - [Assinaturas de alertas](api/alert-subscriptions.md)
- Interface do usuário do serviço de query {#ui}
   - [Visão geral da interface do usuário](ui/overview.md)
   - [Guia do usuário do Editor de consultas](ui/user-guide.md)
   - [Templates de query](ui/query-templates.md)
   - [Usando credenciais do Serviço de Consulta](ui/credentials.md)
   - [Geração de conjuntos de dados a partir de resultados de query](ui/create-datasets.md)
- [Monitorar consultas](monitor-queries.md)
- Armazenamento acelerado de consulta{#query-accelerated-store}
   - [Modelo de dados de insights de relatórios](query-accelerated-store/reporting-insights-data-model.md)
- Práticas recomendadas {#best-practices}
   - [Orientações gerais para a execução de consultas](best-practices/writing-queries.md)
   - [Orientação para a organização de ativos de dados](./best-practices/organize-data-assets.md)
   - [Trabalhar com estruturas de dados aninhadas](best-practices/nested-data-structures.md)
   - [Nivelar estruturas de dados aninhadas](best-practices/flatten-nested-data.md)
   - [Bloco anônimo](best-practices/anonymous-block.md)
   - [Carregamento incremental](best-practices/incremental-load.md)
   - [Desduplicação de dados](best-practices/deduplication.md)
- Atributos derivados {#derived-attributes}
   - [Visão geral](derived-attributes/overview.md)
   - [Caso de uso de decodificações](derived-attributes/deciles-use-case.md)
- Consultas de exemplo {#sample-queries}
   - [Exemplos de consultas de eventos de experiência](sample-queries/experience-event.md)
   - [Exemplos de consultas do Adobe Analytics](sample-queries/adobe-analytics.md)
- Referência SQL {#sql}
   - [Visão geral do SQL](sql/overview.md)
   - [Sintaxe SQL](sql/syntax.md)
   - [Funções definidas por Adobe](sql/adobe-defined-functions.md)
   - [Funções SQL Spark](sql/spark-sql-functions.md)
   - [Comandos de metadados](sql/metadata.md)
   - [Instruções preparadas](sql/prepared-statements.md)
   - [Amostras do conjunto de dados](sql/dataset-samples.md)
- Conectar clientes ao Serviço de query {#clients}
   - [Visão geral das conexões do cliente](clients/overview.md)
   - [Modos SSL](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [DbVisualizer](./clients/dbvisulaizer.md)
   - [Notebook Júpiter](clients//jupyter-notebook.md)
   - [Looker](clients/looker.md)
   - [Postico](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [RStudio](clients/rstudio.md)
   - [Tableau](clients/tableau.md)
- Governança de dados {#data-governance}
   - [Visão geral](data-governance/overview.md)
   - [Guia de log de auditoria](data-governance/audit-log-guide.md)
   - [Identidades em conjuntos de dados de esquema ad hoc](data-governance/ad-hoc-schema-identities.md)
   - [Suporte ao controle de acesso baseado em atributos para esquemas ad hoc](./data-governance/ad-hoc-schema-labels.md)
- [Guia de solução de problemas](troubleshooting-guide.md)
- [Referência da API](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Notas de versão da plataforma](https://www.adobe.com/go/platform-release-notes-en)