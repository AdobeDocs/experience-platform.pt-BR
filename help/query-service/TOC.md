---
audience: user
user-guide-title: Ajuda do Serviço de consulta da Adobe Experience Platform
breadcrumb-title: Guia do Serviço de consulta
user-guide-description: Use o SQL padrão para consulta de dados no Platform Data Lake.
feature: Queries
source-git-commit: d074ebaef19616f1556671f4c7307faeb954cd60
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 18%

---


# Serviço de query Adobe Experience Platform {#query}

- [Visão geral do Serviço de query](home.md)
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
- Interface do usuário do serviço de query {#ui}
   - [Visão geral da interface do usuário](ui/overview.md)
   - [Guia do usuário do Editor de consultas](ui/user-guide.md)
   - [Usando credenciais do Serviço de Consulta](ui/credentials.md)
   - [Geração de conjuntos de dados a partir de resultados de query](ui/create-datasets.md)
- Práticas recomendadas {#best-practices}
   - [Orientações gerais para a execução de consultas](best-practices/writing-queries.md)
   - [Orientação para a organização de ativos de dados](./best-practices/organize-data-assets.md)
   - [Trabalhar com estruturas de dados aninhadas](best-practices/nested-data-structures.md)
   - [Nivelar estruturas de dados aninhadas](best-practices/flatten-nested-data.md)
   - [Bloco anônimo](best-practices/anonymous-block.md)
   - [Carregamento incremental](best-practices/incremental-load.md)
   - [Desduplicação de dados](best-practices/deduplication.md)
- [Atributos derivados](derived-attributes.md)
- Consultas de exemplo {#sample-queries}
   - [Exemplos de consultas de eventos de experiência](sample-queries/experience-event.md)
   - [Exemplos de consultas do Adobe Analytics](sample-queries/adobe-analytics.md)
- Governança de dados {#data-governance}
   - [Guia de log de auditoria](data-governance/audit-log-guide.md)
   - [Identidades em conjuntos de dados de esquema ad hoc](data-governance/ad-hoc-schema-identities.md)
   - [Suporte ao controle de acesso baseado em atributos para esquemas ad hoc](./data-governance/ad-hoc-schema-labels.md)
- Referência SQL {#sql}
   - [Visão geral do SQL](sql/overview.md)
   - [Sintaxe SQL](sql/syntax.md)
   - [Funções definidas por Adobe](sql/adobe-defined-functions.md)
   - [Funções SQL Spark](sql/spark-sql-functions.md)
   - [Comandos de metadados](sql/metadata.md)
   - [Instruções preparadas](sql/prepared-statements.md)
- Conectar clientes ao Serviço de query {#clients}
   - [Visão geral das conexões do cliente](clients/overview.md)
   - [Modos SSL](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [Visualizador Db](./clients/dbvisulaizer.md)
   - [Looker](clients/looker.md)
   - [Postico](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [RStudio](clients/rstudio.md)
   - [Tableau](clients/tableau.md)
- [Guia de solução de problemas](troubleshooting-guide.md)
- [Referência da API](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Notas de versão da plataforma](https://www.adobe.com/go/platform-release-notes-en)