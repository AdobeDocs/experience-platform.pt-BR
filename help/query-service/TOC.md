---
audience: user
user-guide-title: Ajuda do serviço de consulta da Adobe Experience Platform
breadcrumb-title: Guia do Serviço de consulta
user-guide-description: Use o SQL padrão para consultar dados no data lake na Experience Platform.
feature: Queries
role: User,Developer
source-git-commit: 8b33d9231aeebd454fd614a81b356a9e971b757c
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 25%

---


# Serviço de consulta Adobe Experience Platform {#query}

- [Visão geral do Serviço de consulta](home.md)
- [Empacotamento do Serviço de consulta](packaging.md)
- [Proteções do serviço de consulta](guardrails.md)
- Introdução {#get-started}
   - [Pré-requisitos](get-started/prerequisites.md)
- Destilador de dados {#data-distiller}
   - [Visão geral](data-distiller/overview.md)
   - [Uso da licença](data-distiller/license-usage.md)
   - Conjuntos de dados derivados {#derived-datasets}
      - [Visão geral](data-distiller/derived-datasets/overview.md)
      - [Criar conjuntos de dados derivados com SQL](data-distiller/derived-datasets/create-derived-datasets-with-sql.md)
      - [Criar conjuntos de dados derivados baseados em decil](data-distiller/derived-datasets/decile-based-derived-attributes.md)
   - SQL Insights para relatórios estendidos do aplicativo {#sql-insights}
      - [Visão geral](data-distiller/sql-insights/overview.md)
      - [Modo de consulta profissional](data-distiller/sql-insights/query-pro-mode.md)
      - [Visão geral da loja acelerada](data-distiller/sql-insights/accelerated-store-overview.md)
      - [Enviar consultas aceleradas](data-distiller/sql-insights/send-accelerated-queries.md)
      - [Guia do modelo de dados de insights de relatórios](data-distiller/sql-insights/reporting-insights-data-model.md)
   - Pipelines de recursos de IA/AM {#ml-feature-pipelines}
      - [Visão geral](data-distiller/ml-feature-pipelines/overview.md)
      - [Conectar-se aos Jupyter Notebooks](data-distiller/ml-feature-pipelines/establish-connection.md)
      - [Análise exploratória de dados](data-distiller/ml-feature-pipelines/exploratory-analysis.md)
      - [Recursos do engenheiro para ML](data-distiller/ml-feature-pipelines/feature-engineering.md)
      - [Exportar dados para ambientes ML](data-distiller/ml-feature-pipelines/export-data.md)
      - [Fluxo de trabalho completo de enriquecimento do pipeline de dados de IA/ML](data-distiller/ml-feature-pipelines/end-to-end-notebook-workflow.md)
   - [Sessão do Summit 2025](data-distiller/top-tips-to-maximize-value.md)
- Estatísticas do Data Distiller e aprendizado de máquina {#advanced-statistics}
   - [Visão geral](advanced-statistics/overview.md)
   - [Engenharia de recursos](advanced-statistics/feature-engineering.md)
   - [Modelos](advanced-statistics/models.md)
   - [Transformação de recursos](advanced-statistics/feature-transformation.md)
   - Implementar modelos {#implement-models}
      - [Implementar modelos](advanced-statistics/implement-models/implement-models.md)
      - [Regressão](advanced-statistics/implement-models/regression.md)
      - [Classificação](advanced-statistics/implement-models/classification.md)
      - [Geração de cluster](advanced-statistics/implement-models/clustering.md)
   - Exemplos {#examples}
      - [Filtragem de bot usando estatísticas e aprendizado de máquina](advanced-statistics/examples/statistics-and-ml-bot-filtering.md)
      - [Preveja o abandono do cliente usando regressão logística baseada em SQL](advanced-statistics/examples/predict-customer-churn.md)
- Públicos-alvo do Data Distiller {#data-distiller-audiences}
   - [Criar públicos-alvo externos usando SQL](data-distiller-audiences/overview.md)
- Exemplos {#use-cases}
   - [Visão geral](use-cases/overview.md)
   - [Navegação abandonada](use-cases/abandoned-browse.md)
   - [Análise de atribuição](use-cases/attribution-analysis.md)
   - [Filtragem de bot](use-cases/bot-filtering.md)
   - [Filtragem de bot usando estatísticas e introdução ao aprendizado de máquina](use-cases/statistics-and-ml-bot-filtering-stub.md)
   - [Criar um relatório de tendências de eventos](use-cases/trended-report-of-events.md)
   - [Análise de consentimento](use-cases/consent-analysis.md)
   - [Valor vitalício do cliente](use-cases/customer-lifetime-value.md)
   - [Exploração de dados](./use-cases/data-exploration.md)
   - [Conjuntos de dados derivados baseados em decis](use-cases/deciles-use-case.md)
   - [Correspondência difusa](use-cases/fuzzy-match.md)
   - [Listar as exibições de página de um usuário](use-cases/list-visitor-sessions.md)
   - [Listar visitantes por suas visualizações de página](use-cases/visitors-by-number-of-page-views.md)
   - [Prever a rotatividade do cliente usando o SQL](use-cases/predict-customer-churn-stub.md)
   - [Pontuação de propensão](use-cases/propensity-score.md)
   - [Recuperar registros semelhantes com funções de ordem superior](use-cases/retrieve-similar-records.md)
   - [Retornar e usar variáveis de merchandising dos dados de análise](use-cases/merchandising-variables.md)
   - [SQLAlchemy](use-cases/sqlalchemy.md)
   - [Exibir o relatório acumulado de um visitante](use-cases/roll-up-report-of-a-visitor.md)
   - [Insights de análise da Web e móvel](use-cases/analytics-insights.md)
- Principais conceitos {#key-concepts}
   - [Trabalho com estruturas de dados aninhadas](key-concepts/nested-data-structures.md)
   - [Nivelar estruturas de dados aninhadas](key-concepts/flatten-nested-data.md)
   - [Bloqueio anônimo](key-concepts/anonymous-block.md)
   - [Modelo embutido](key-concepts/inline-templates.md)
   - [Carregamento incremental](key-concepts/incremental-load.md)
   - [Desduplicação de dados](key-concepts/deduplication.md)
   - [Amostras de conjunto de dados](key-concepts/dataset-samples.md)
   - [Cálculo das estatísticas do conjunto de dados](key-concepts/dataset-statistics.md)
- Hipercubos de Distiller de dados {#hypercubes}
   - [Análise eficiente de big data com hipercubos](hypercubes/overview.md)
- Conectar clientes ao Serviço de consultas {#clients}
   - [Visão geral de conexões de clientes](clients/overview.md)
   - [Modos SSL](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [DbVisualizer](./clients/dbvisulaizer.md)
   - [GitHub Copilot](./clients/github-copilot.md)
   - [Jupyter Notebook](clients//jupyter-notebook.md)
   - [Pesquisador](clients/looker.md)
   - [Pótico](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [RStudio](clients/rstudio.md)
   - [Tableau](clients/tableau.md)
- Interface do usuário do serviço de consulta {#ui}
   - [Visão geral da interface](ui/overview.md)
   - [Guia do usuário do Editor de consultas](ui/user-guide.md)
   - [Modelos de consulta](ui/query-templates.md)
   - [Consultas parametrizadas](ui/parameterized-queries.md)
   - [Agendamentos de consulta](ui/query-schedules.md)
   - [Logs de consulta](ui/query-logs.md)
   - [Monitorar consultas programadas](ui/monitor-queries.md)
   - [Guia de credenciais](ui/credentials.md)
   - [Migrar JWT para credenciais do OAuth](ui/migrate-jwt-to-oauth.md)
   - [Gerar conjuntos de dados de saída a partir dos resultados da consulta](ui/create-datasets.md)
- API do serviço de consulta {#api}
   - [Introdução](api/getting-started.md)
   - [Consultas](api/queries.md)
   - [Parâmetros de conexão](api/connection-parameters.md)
   - [Programações](api/scheduled-queries.md)
   - [Execução para consultas programadas](api/runs-scheduled-queries.md)
   - [Modelos de consulta](api/query-templates.md)
   - [Consultas aceleradas](api/accelerated-queries.md)
   - [Assinaturas de alerta](api/alert-subscriptions.md)
- API de autorização do Data Distiller {#auth-api}
   - [Visão geral](auth-api/overview.md)
   - [Introdução](auth-api/getting-started.md)
   - [Acesso IP](auth-api/ip-access.md)
   - [Validar](auth-api/validate.md)
- Governança de dados {#data-governance}
   - [Visão geral](data-governance/overview.md)
   - [Guia de log de auditoria](data-governance/audit-log-guide.md)
   - [Identidades em conjuntos de dados de esquema ad hoc](data-governance/ad-hoc-schema-identities.md)
   - [Suporte de controle de acesso baseado em atributos para esquemas ad hoc](./data-governance/ad-hoc-schema-labels.md)
- Práticas recomendadas {#best-practices}
   - [Execução da consulta](best-practices/writing-queries.md)
   - [Organização do ativo de dados](./best-practices/organize-data-assets.md)
- Referência SQL {#sql}
   - [Visão geral de SQL](sql/overview.md)
   - [Sintaxe SQL](sql/syntax.md)
   - [Funções definidas pela Adobe](sql/adobe-defined-functions.md)
   - [Funções de ordem superior](sql/higher-order-functions.md)
   - [Funções do Spark SQL](sql/spark-sql-functions.md)
   - [Comandos de metadados](sql/metadata.md)
   - [Demonstrativos preparados](sql/prepared-statements.md)
- [Perguntas frequentes](troubleshooting-guide.md)
- [INCLUO NA LISTA DE PERMISSÕES de endereços IP](ip-address-allowlist.md)
- [Referência da API](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Notas de versão da Experience Platform](https://experienceleague.adobe.com/pt-br/docs/experience-platform/release-notes/latest)
