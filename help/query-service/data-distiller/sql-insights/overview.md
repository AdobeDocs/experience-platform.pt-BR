---
title: Insights SQL
description: Saiba mais sobre os casos de uso, os recursos essenciais e as etapas necessárias para desenvolver um painel de insights SQL com o Data Distiller. Descubra como o recurso SQL Insights no Data Distiller pode melhorar a transparência e obter insights operacionais em diferentes dimensões, como perfis, públicos, campanhas, jornadas, direitos e consentimento.
exl-id: f807d0fd-c8ec-42d4-96a0-5ffc5681943b
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# Insights SQL

Crie modelos de dados de relatórios sob medida para extrair insights mais profundos, otimizar estratégias e adaptar a análise para atender às necessidades específicas dos negócios com os insights de SQL da Data Distiller. Use o recurso Insights SQL para melhorar a transparência e obter insights operacionais dos dados do Adobe Experience Platform em dimensões como perfis, públicos, campanhas, jornadas, direitos e consentimento. Esse recurso oferece uma solução versátil e adaptável para adaptar os modelos de dados de relatórios de sua organização às necessidades específicas de seus negócios.

Para [visualizar seus Insights de SQL](../../../dashboards/sql-insights-query-pro-mode/overview.md), você pode usar o [modo profissional de consulta](../../../dashboards/sql-insights-query-pro-mode/overview.md) para realizar análises complexas com consultas SQL personalizadas e transformar seus dados em gráficos de fácil interpretação. Use o modo query pro para criar insights e visualizações sob medida em seus painéis e atender a públicos técnicos e não técnicos baixando seus insights como arquivos CSV.

Este documento aborda os casos de uso, os recursos essenciais e as etapas necessárias para desenvolver um painel de insights SQL com o Data Distiller.

## Pré-requisitos

Este tutorial usa painéis definidos pelo usuário para visualizar dados de seu modelo de dados personalizado na interface do usuário da Platform. Consulte a [documentação de painéis definidos pelo usuário](../../../dashboards/standard-dashboards.md) para saber mais sobre este recurso.

## Introdução

O SKU do Data Distiller é necessário para criar um modelo de dados personalizado para seus insights de relatório e estender os modelos de dados do Real-Time CDP que contêm dados enriquecidos da Platform. Consulte a documentação de [empacotamento](../../packaging.md), [medidas de proteção](../../guardrails.md#query-accelerated-store) e [licenciamento](../../data-distiller/license-usage.md) relacionada à SKU do Data Distiller. Se você não tiver o Data Distiller SKU, entre em contato com o representante do serviço de atendimento ao cliente da Adobe para obter mais informações.

## Casos de uso do SQL Insights {#use-cases}

Abaixo estão casos de uso comuns que podem ser efetivamente tratados por meio do SQL Insights no Data Distiller.

### Transparência de uso de perfil e público {#usage-transparency}

**Desafio:** como detalhar os KPIs (Indicadores-chave de desempenho) por critérios específicos, como unidades de negócios, status de fidelidade ou Valor vitalício do cliente (CLTV).

**Solução do SQL Insights:** O Data Distiller habilita a extensão de modelos de dados de relatórios no Adobe Experience Platform, facilitando [a adição de atributos de perfil personalizados, como CLTV](../../use-cases/customer-lifetime-value.md) ou status de fidelidade.

### Rastreamento de anomalias de consentimento {#consent-anomaly-tracking}

**Desafio:** como aplicar sobreposição de público-alvo e dimensionar relatórios de linha de tendência a atributos de consentimento personalizados para canais como email, SMS e telefone.

**Solução do SQL Insights:** O modelo de dados de relatórios pode ser estendido para rastrear alterações nas preferências de consentimento ao longo do tempo. Isso envolve a criação de tabelas de fatos e dimensões adicionais para as preferências de consentimento de tendência e o agendamento de [atualização de dados incremental](../../key-concepts/incremental-load.md).

### Otimizar a estratégia de segmentação de público {#optimize-audience-segmentation-strategy}

**Desafio:** como integrar pontuações de propensão geradas por modelo de aprendizado de máquina (ML) aos relatórios de KPI de público-alvo.

**Solução do SQL Insights:** O Data Distiller permite a inclusão de [pontuações de propensão de modelos de ML personalizados](../../use-cases/propensity-score.md), facilitando o cálculo de pontuações agregadas no nível do público-alvo. Esses dados podem ser relatados junto com KPIs padrão.

### Expansão de público {#audience-expansion}

**Desafio:** como adquirir mais do que apenas contagens de perfil nos relatórios de sobreposição de público e obter dados demográficos adicionais ou preferências para orientar estratégias de expansão de público.

**Solução do SQL Insights:** ao estender o modelo de dados de relatórios, os usuários podem incorporar atributos de perfil adicionais, enriquecendo o relatório de sobreposição de público-alvo com dados demográficos e preferências relevantes.

## Principais recursos para gerar Insights SQL {#key-capabilities}

A ilustração abaixo destaca vários recursos essenciais para gerar Insights SQL. Esses recursos incluem:

1. **Visualizações de dados:** incorporação de elementos visuais, como tendências e gráficos de barras, para obter uma visão abrangente das tendências de dados.
1. **Criação de painéis:** habilitando a criação de painéis personalizados adaptados a casos de uso específicos, proporcionando uma experiência de análise mais personalizada e direcionada.
1. **Modelagem flexível de dados SQL:** use uma abordagem versátil de modelagem de dados SQL que permite aos usuários combinar e manipular facilmente diferentes conjuntos de dados, melhorando a adaptabilidade e a profundidade analítica.
1. **Armazenamento acelerado:** implementação de um mecanismo de armazenamento acelerado para fornecer insights agregados de maneira eficiente por meio do SQL, garantindo acesso rápido e simplificado a informações valiosas.
1. **Conectividade de BI:** facilita a integração perfeita com ferramentas populares de Business Intelligence (BI), incluindo Power BI, Tableau, Looker e Apache Superset. Essa conectividade garante a compatibilidade com diversos ambientes de BI, oferecendo aos usuários a flexibilidade de usar sua ferramenta de escolha para análises e relatórios detalhados.

![Representações visuais dos principais recursos dos Insights SQL da Data Distiller.](../../images/data-distiller/sql-insights/key-capabilities-of-customizable-insights.png)

## Etapas para criar insights SQL {#steps-to-create}

Para desenvolver um painel de Insights SQL no Data Distiller, siga as instruções passo a passo abaixo.

1. **Exploração de consulta ad hoc:** Comece executando consultas ad hoc `SELECT` para explorar dados brutos no data lake. Isso permite a análise de dados exploratórios e instantâneos para testar e valida dados em que os resultados das consultas não são armazenados no data lake.
1. **Utilização de consulta em lote:** use consultas em lote para [criar trabalhos agendados](../../api/scheduled-queries.md#create-a-new-scheduled-query) para gerar tabelas agregadas de insights, garantindo uma abordagem sistemática e automatizada para o processamento de dados. As consultas em lote executam consultas `INSERT TABLE AS SELECT` e `CREATE TABLE AS SELECT` para limpar, moldar, manipular e enriquecer dados. Os resultados dessas consultas são armazenados no data lake.
1. **Carregamento de insights agregados:** carregue os insights agregados gerados no repositório acelerado e use o SQL para testar consultas e garantir a precisão e a eficiência da recuperação de dados. Para saber como [fazer consultas sem estado ao repositório acelerado](../../api/accelerated-queries.md), consulte a documentação.
1. **Acesso e integração:** acesse os insights armazenados no repositório acelerado facilmente ao integrar com o Adobe Experience Platform [Painéis definidos pelo usuário](../../../dashboards/standard-dashboards.md) ou outras ferramentas de Business Intelligence (BI) preferenciais. Essas integrações com clientes de terceiros facilitam uma experiência coesa e intuitiva para os usuários.

![Um infográfico que ilustra as quatro etapas do SQL Insights no Data Distiller.](../../images/data-distiller/sql-insights/steps-to-customizable-insights.png)

## Próximas etapas

Ao ler este documento, agora você tem uma melhor compreensão dos casos de uso, recursos essenciais e etapas necessárias para desenvolver um painel de insights SQL com o Data Distiller. Para continuar aprendendo como criar modelos de dados de relatórios por medida, consulte o [guia do modelo de dados de insights de relatórios](./reporting-insights-data-model.md).
