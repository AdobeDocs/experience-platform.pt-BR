---
audience: user
user-guide-title: Ajuda do Serviço de consulta da Adobe Experience Platform
breadcrumb-title: Guia do Serviço de consulta
user-guide-description: Use o SQL padrão para consultar dados no data lake na Experience Platform.
feature: Queries
source-git-commit: 9df75958d3945a52c219e96f18f9fc07f8036076
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 18%

---


# Serviço de query Adobe Experience Platform {#query}

- [Visão geral do Serviço de query](home.md)
- [Pacote do Serviço de Consulta](packages.md)
- [Medidas de proteção do serviço de consulta](guardrails.md)
- Introdução {#get-started}
   - [Pré-requisitos](get-started/prerequisites.md)
- Distiller de dados {#data-distiller}
   - [Visão geral](data-distiller/overview.md)
   - [Uso da licença](data-distiller/license-usage.md)
   - Armazenamento acelerado de consulta {#query-accelerated-store}
      - [Enviar consultas aceleradas](data-distiller/query-accelerated-store/send-accelerated-queries.md)
      - [Guia do modelo de dados de insights de relatórios](data-distiller/query-accelerated-store/reporting-insights-data-model.md)
   - Atributos derivados {#derived-attributes}
      - [Visão geral](data-distiller/derived-attributes/overview.md)
      - [Fluxo SQL contínuo](data-distiller/derived-attributes/seamless-sql-flow.md)
      - [Criar atributos derivados com base em decis](data-distiller/derived-attributes/decile-based-derived-attributes.md)
- Casos de uso {#use-cases}
   - [Navegador abandonado](use-cases/abandoned-browse.md)
   - [Análise de atividade com o Adobe Target](use-cases/activity-analysis-with-adobe-target.md)
   - [Análise de atribuição](use-cases/attribution-analysis.md)
   - [Filtragem de bot](use-cases/bot-filtering.md)
   - [Criar um relatório de tendências de eventos](use-cases/trended-report-of-events.md)
   - [Atributos derivados baseados em decis](use-cases/deciles-use-case.md)
   - [Correspondência difusa](use-cases/fuzzy-match.md)
   - [Listar as exibições de página de um usuário](use-cases/list-visitor-sessions.md)
   - [Listar visitantes por suas exibições de página](use-cases/visitors-by-number-of-page-views.md)
   - [Pontuação de propensão](use-cases/propensity-score.md)
   - [SQLAlchemy](use-cases/sqlalchemy.md)
   - [Retornar e usar variáveis de merchandising a partir de dados de análise](use-cases/merchandising-variables.md)
   - [Exibir o relatório de roll-up de um visitante](use-cases/roll-up-report-of-a-visitor.md)
   - [Insights do Web e de análises móveis](use-cases/analytics-insights.md)
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
- Interface do usuário do serviço de query {#ui}
   - [Visão geral da interface do usuário](ui/overview.md)
   - [Guia do usuário do Editor de consultas](ui/user-guide.md)
   - [Templates de query](ui/query-templates.md)
   - [Agendamentos de query](ui/query-schedules.md)
   - [Logs de consulta](ui/query-logs.md)
   - [Monitorar consultas agendadas](ui/monitor-queries.md)
   - [Guia de credenciais](ui/credentials.md)
   - [Gerar conjuntos de dados de saída a partir de resultados de consulta](ui/create-datasets.md)
- Pontos de extremidade da API do Serviço de query {#api}
   - [Introdução](api/getting-started.md)
   - [Consultas](api/queries.md)
   - [Parâmetros de conexão](api/connection-parameters.md)
   - [Agendamentos](api/scheduled-queries.md)
   - [É executado para consultas agendadas](api/runs-scheduled-queries.md)
   - [Templates de query](api/query-templates.md)
   - [Consultas aceleradas](api/accelerated-queries.md)
   - [Assinaturas de alertas](api/alert-subscriptions.md)
- Governança de dados {#data-governance}
   - [Visão geral](data-governance/overview.md)
   - [Guia de log de auditoria](data-governance/audit-log-guide.md)
   - [Identidades em conjuntos de dados de esquema ad hoc](data-governance/ad-hoc-schema-identities.md)
   - [Suporte ao controle de acesso baseado em atributos para esquemas ad hoc](./data-governance/ad-hoc-schema-labels.md)
- Práticas recomendadas {#best-practices}
   - [Execução da consulta](best-practices/writing-queries.md)
   - [Organização do ativo de dados](./best-practices/organize-data-assets.md)
- Conceitos essenciais {#essential-concepts}
   - [Trabalhar com estruturas de dados aninhadas](essential-concepts/nested-data-structures.md)
   - [Nivelar estruturas de dados aninhadas](essential-concepts/flatten-nested-data.md)
   - [Bloco anônimo](essential-concepts/anonymous-block.md)
   - [Carregamento incremental](essential-concepts/incremental-load.md)
   - [Desduplicação de dados](essential-concepts/deduplication.md)
   - [Amostras do conjunto de dados](essential-concepts/dataset-samples.md)
- Referência SQL {#sql}
   - [Visão geral do SQL](sql/overview.md)
   - [Sintaxe SQL](sql/syntax.md)
   - [Funções definidas por Adobe](sql/adobe-defined-functions.md)
   - [Funções SQL Spark](sql/spark-sql-functions.md)
   - [Comandos de metadados](sql/metadata.md)
   - [Instruções preparadas](sql/prepared-statements.md)
- [Perguntas frequentes](troubleshooting-guide.md)
- [Referência da API](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Notas de versão da plataforma](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html?lang=pt-BR)
