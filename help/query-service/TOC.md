---
audience: user
user-guide-title: Ajuda do Serviço de consulta da Adobe Experience Platform
breadcrumb-title: Guia do Serviço de consulta
user-guide-description: Use o SQL padrão para consultar dados no data lake na Experience Platform.
feature: Queries
source-git-commit: a78f7499b55dcedbe379e917b94946948c66e6e5
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 20%

---


# Serviço de consulta Adobe Experience Platform {#query}

- [Visão geral do Serviço de consulta](home.md)
- [Empacotamento do Serviço de consulta](packages.md)
- [Proteções do serviço de consulta](guardrails.md)
- Introdução {#get-started}
   - [Pré-requisitos](get-started/prerequisites.md)
- Distiller de dados {#data-distiller}
   - [Visão geral](data-distiller/overview.md)
   - [Uso da licença](data-distiller/license-usage.md)
   - Consultar armazenamento acelerado {#query-accelerated-store}
      - [Enviar consultas aceleradas](data-distiller/query-accelerated-store/send-accelerated-queries.md)
      - [Guia do modelo de dados de insights de relatórios](data-distiller/query-accelerated-store/reporting-insights-data-model.md)
   - Atributos derivados {#derived-attributes}
      - [Visão geral](data-distiller/derived-attributes/overview.md)
      - [Fluxo SQL contínuo](data-distiller/derived-attributes/seamless-sql-flow.md)
      - [Criar atributos derivados baseados em decil](data-distiller/derived-attributes/decile-based-derived-attributes.md)
   - Pipelines de recursos de IA/ML {#ml-feature-pipelines}
      - [Visão geral](data-distiller/ml-feature-pipelines/overview.md)
      - [Conectar-se aos Jupyter Notebooks](data-distiller/ml-feature-pipelines/establish-connection.md)
      - [Análise exploratória de dados](data-distiller/ml-feature-pipelines/exploratory-analysis.md)
      - [Recursos do engenheiro para ML](data-distiller/ml-feature-pipelines/feature-engineering.md)
      - [Exportar dados para ambientes ML](data-distiller/ml-feature-pipelines/export-data.md)
      - [Fluxo de trabalho completo de enriquecimento do pipeline de dados de IA/ML](data-distiller/ml-feature-pipelines/end-to-end-notebook-workflow.md)
- Casos de uso {#use-cases}
   - [Navegação abandonada](use-cases/abandoned-browse.md)
   - [Análise de atribuição](use-cases/attribution-analysis.md)
   - [Filtragem de bots](use-cases/bot-filtering.md)
   - [Criar um relatório de tendências de eventos](use-cases/trended-report-of-events.md)
   - [Análise de consentimento](use-cases/consent-analysis.md)
   - [Valor vitalício do cliente](use-cases/customer-lifetime-value.md)
   - [Atributos derivados baseados em decis](use-cases/deciles-use-case.md)
   - [Correspondência difusa](use-cases/fuzzy-match.md)
   - [Listar as exibições de página de um usuário](use-cases/list-visitor-sessions.md)
   - [Listar visitantes por suas visualizações de página](use-cases/visitors-by-number-of-page-views.md)
   - [Pontuação de tendência](use-cases/propensity-score.md)
   - [SQLAlchemy](use-cases/sqlalchemy.md)
   - [Retornar e usar variáveis de merchandising dos dados de análise](use-cases/merchandising-variables.md)
   - [Exibir o relatório acumulado de um visitante](use-cases/roll-up-report-of-a-visitor.md)
   - [Insights de análise da Web e móvel](use-cases/analytics-insights.md)
- Conectar clientes ao Serviço de consulta {#clients}
   - [Visão geral de conexões de clientes](clients/overview.md)
   - [Modos SSL](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [DbVisualizer](./clients/dbvisulaizer.md)
   - [Jupyter Notebook](clients//jupyter-notebook.md)
   - [Pesquisador](clients/looker.md)
   - [Pótico](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [RStudio](clients/rstudio.md)
   - [Tableau](clients/tableau.md)
- Interface do usuário do serviço de consulta {#ui}
   - [Visão geral da interface do ](ui/overview.md)
   - [Guia do usuário do Editor de consultas](ui/user-guide.md)
   - [Modelos de consulta](ui/query-templates.md)
   - [Consultas parametrizadas](ui/parameterized-queries.md)
   - [Agendamentos de consulta](ui/query-schedules.md)
   - [Logs de consulta](ui/query-logs.md)
   - [Monitorar consultas programadas](ui/monitor-queries.md)
   - [Guia de credenciais](ui/credentials.md)
   - [Gerar conjuntos de dados de saída a partir dos resultados da consulta](ui/create-datasets.md)
- Endpoints da API do Serviço de consulta {#api}
   - [Introdução](api/getting-started.md)
   - [Consultas](api/queries.md)
   - [Parâmetros de conexão](api/connection-parameters.md)
   - [Agendamentos](api/scheduled-queries.md)
   - [Execução para consultas programadas](api/runs-scheduled-queries.md)
   - [Modelos de consulta](api/query-templates.md)
   - [Consultas aceleradas](api/accelerated-queries.md)
   - [Assinaturas de alerta](api/alert-subscriptions.md)
- Governança de dados {#data-governance}
   - [Visão geral](data-governance/overview.md)
   - [Guia de log de auditoria](data-governance/audit-log-guide.md)
   - [Identidades em conjuntos de dados de esquema ad hoc](data-governance/ad-hoc-schema-identities.md)
   - [Suporte de controle de acesso baseado em atributos para esquemas ad hoc](./data-governance/ad-hoc-schema-labels.md)
- Práticas recomendadas {#best-practices}
   - [Execução da consulta](best-practices/writing-queries.md)
   - [Organização do ativo de dados](./best-practices/organize-data-assets.md)
- Conceitos essenciais {#essential-concepts}
   - [Trabalho com estruturas de dados aninhadas](essential-concepts/nested-data-structures.md)
   - [Nivelar estruturas de dados aninhadas](essential-concepts/flatten-nested-data.md)
   - [Bloqueio anônimo](essential-concepts/anonymous-block.md)
   - [Modelo embutido](essential-concepts/inline-templates.md)
   - [Carregamento incremental](essential-concepts/incremental-load.md)
   - [Desduplicação de dados](essential-concepts/deduplication.md)
   - [Amostras de conjunto de dados](essential-concepts/dataset-samples.md)
   - [Cálculo das estatísticas do conjunto de dados](essential-concepts/dataset-statistics.md)
- Referência SQL {#sql}
   - [Visão geral de SQL](sql/overview.md)
   - [Sintaxe SQL](sql/syntax.md)
   - [Funções definidas pelo Adobe](sql/adobe-defined-functions.md)
   - [Funções do Spark SQL](sql/spark-sql-functions.md)
   - [Comandos de metadados](sql/metadata.md)
   - [Demonstrativos preparados](sql/prepared-statements.md)
- [Perguntas frequentes](troubleshooting-guide.md)
- [INCLUIR NA LISTA DE PERMISSÕES endereço IP](ip-address-allowlist.md)
- [Referência da API](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Notas de versão da Platform](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html?lang=pt-BR)
