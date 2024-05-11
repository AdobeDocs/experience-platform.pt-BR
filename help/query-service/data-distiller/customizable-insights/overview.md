---
title: Insights personalizáveis
description: Saiba mais sobre os casos de uso, recursos essenciais e etapas necessárias para desenvolver um painel de insights personalizável com o Data Distiller. Descubra como o recurso de Insights personalizáveis no Data Distiller pode melhorar a transparência e obter insights operacionais em diferentes dimensões, como perfis, públicos, campanhas, jornadas, direitos e consentimento.
exl-id: f807d0fd-c8ec-42d4-96a0-5ffc5681943b
source-git-commit: bb95e0aa8ee92aee5a2f126d85e78308e652a061
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# Insights personalizáveis

Crie modelos de dados de relatórios sob medida para extrair insights mais profundos, otimizar estratégias e adaptar a análise para atender às necessidades específicas dos negócios com os insights personalizáveis do Data Distiller. Use o recurso Insights personalizáveis para melhorar a transparência e obter insights operacionais dos dados do Adobe Experience Platform em dimensões como perfis, públicos, campanhas, jornadas, direitos e consentimento. Esse recurso oferece uma solução versátil e adaptável para adaptar os modelos de dados de relatórios de sua organização às necessidades específicas de seus negócios.

Para [visualizar seus Insights Personalizáveis](../../../dashboards/data-distiller/overview.md) você pode usar [modo pro da consulta](../../../dashboards/data-distiller/customizable-insights/query-pro-mode.md) para realizar análises complexas com queries SQL personalizadas e transformar seus dados em gráficos de fácil interpretação. Use o modo query pro para criar insights e visualizações sob medida em seus painéis e atender a públicos técnicos e não técnicos baixando seus insights como arquivos CSV.

Este documento aborda os casos de uso, os recursos essenciais e as etapas necessárias para desenvolver um painel de insights personalizável com o Data Distiller.

## Pré-requisitos

Este tutorial usa painéis definidos pelo usuário para visualizar dados de seu modelo de dados personalizado na interface do usuário da Platform. Consulte a [documentação de painéis definida pelo usuário](../../../dashboards/user-defined-dashboards.md) para saber mais sobre este recurso.

## Introdução

O SKU do Data Distiller é necessário para criar um modelo de dados personalizado para seus insights de relatório e estender os modelos de dados do Real-Time CDP que contêm dados enriquecidos da Platform. Consulte a [empacotamento](../../packaging.md), [grades de proteção](../../guardrails.md#query-accelerated-store), e  [licenciamento](../../data-distiller/license-usage.md) Documentação relacionada ao Data Distiller SKU. Se você não tiver o Data Distiller SKU, entre em contato com o representante do serviço de atendimento ao cliente da Adobe para obter mais informações.

## Casos de uso de insights personalizáveis {#use-cases}

Abaixo estão casos de uso comuns que podem ser efetivamente abordados por meio de Insights personalizáveis no Data Distiller.

### Transparência de uso de perfil e público {#usage-transparency}

**Desafio** Como detalhar os Indicadores-chave de desempenho (KPIs) por critérios específicos, como unidades de negócios, status de fidelidade ou Valor vitalício do cliente (CLTV).

**Solução de insights personalizáveis:** O Data Distiller permite a extensão de modelos de dados de relatórios no Adobe Experience Platform, facilitando [a adição de atributos de perfil personalizados, como CLTV](../../use-cases/customer-lifetime-value.md) ou de fidelidade.

### Rastreamento de anomalias de consentimento {#consent-anomaly-tracking}

**Desafio** Como aplicar sobreposição de público-alvo e relatórios de linha de tendência de tamanho a atributos de consentimento personalizados para canais como email, SMS e telefone.

**Solução de insights personalizáveis:** O modelo de dados de relatórios pode ser estendido para rastrear alterações nas preferências de consentimento ao longo do tempo. Isso envolve a criação de tabelas de fatos e dimensões adicionais para analisar a tendência das preferências de consentimento e do agendamento [atualização de dados incremental](../../key-concepts/incremental-load.md).

### Otimizar a estratégia de segmentação de público {#optimize-audience-segmentation-strategy}

**Desafio** Como integrar pontuações de propensão geradas pelo modelo de aprendizado de máquina (ML) aos relatórios de KPI do público-alvo.

**Solução de insights personalizáveis:** O Data Distiller permite a inclusão de [pontuações de propensão de modelos de ML personalizados](../../use-cases/propensity-score.md), facilitando o cálculo de pontuações agregadas no nível do público-alvo. Esses dados podem ser relatados junto com KPIs padrão.

### Expansão de público {#audience-expansion}

**Desafio** Como adquirir mais do que apenas contagens de perfil nos relatórios de sobreposição de público e obter dados demográficos adicionais ou preferências para orientar estratégias de expansão de público.

**Solução de insights personalizáveis:** Estendendo o modelo de dados de relatórios, os usuários podem incorporar atributos de perfil adicionais, enriquecendo o relatório de sobreposição de público-alvo com dados demográficos e preferências relevantes.

## Principais recursos para gerar insights personalizáveis {#key-capabilities}

A ilustração abaixo destaca vários recursos essenciais para gerar Insights Personalizáveis. Esses recursos incluem:

1. **Visualizações de dados:** Incorporação de elementos visuais, como tendências e gráficos de barras, para obter uma visualização abrangente das tendências de dados.
1. **Criação do painel:** Ativação da criação de painéis personalizados adaptados a casos de uso específicos, fornecendo uma experiência de análise mais personalizada e direcionada.
1. **Modelagem de dados SQL flexível:** Use uma abordagem versátil de modelagem de dados SQL que permita aos usuários combinar e manipular facilmente diferentes conjuntos de dados, melhorando a adaptabilidade e a profundidade analítica.
1. **Armazenamento acelerado:** Implementar um mecanismo de armazenamento acelerado para fornecer insights agregados com eficiência por meio do SQL, garantindo acesso simplificado e rápido a informações valiosas.
1. **Conectividade de BI:** Facilitando a integração perfeita com ferramentas populares de Business Intelligence (BI), incluindo Power BI, Tableau, Looker e Apache Superset. Essa conectividade garante a compatibilidade com diversos ambientes de BI, oferecendo aos usuários a flexibilidade de usar sua ferramenta de escolha para análises e relatórios detalhados.

![Representações visuais dos principais recursos dos Insights personalizáveis do Data Distiller.](../../images/data-distiller/customizable-insights/key-capabilities-of-customizable-insights.png)

## Etapas para criar insights personalizáveis {#steps-to-create}

Para desenvolver um painel de Insights personalizáveis no Data Distiller, siga as instruções passo a passo abaixo.

1. **Exploração de query ad hoc:** Comece executando a ad hoc `SELECT` consultas para explorar dados brutos no data lake. Isso permite a análise de dados exploratórios e instantâneos para testar e valida dados em que os resultados das consultas não são armazenados no data lake.
1. **Utilização de consulta em lote:** Use consultas em lote para [criar trabalhos agendados](../../api/scheduled-queries.md#create-a-new-scheduled-query) para gerar tabelas agregadas de insights, garantindo uma abordagem sistemática e automatizada ao processamento de dados. Execução de consultas em lote `INSERT TABLE AS SELECT` e `CREATE TABLE AS SELECT` consultas para limpar, moldar, manipular e enriquecer dados. Os resultados dessas consultas são armazenados no data lake.
1. **Carregamento de insights agregados:** Carregue os insights agregados gerados no armazenamento acelerado e use o SQL para testar consultas e garantir a precisão e a eficiência da recuperação de dados. Para saber como [fazer consultas sem estado ao repositório acelerado](../../api/accelerated-queries.md), consulte a documentação.
1. **Acesso e integração:** Acesse os insights armazenados no armazenamento acelerado de maneira contínua ao integrar com o Adobe Experience Platform [Painéis definidos pelo usuário](../../../dashboards/user-defined-dashboards.md) ou outras ferramentas de Business Intelligence (BI) preferenciais. Essas integrações com clientes de terceiros facilitam uma experiência coesa e intuitiva para os usuários.

![Um infográfico que ilustra as quatro etapas para Personalizar insights no Data Distiller.](../../images/data-distiller/customizable-insights/steps-to-customizable-insights.png)

## Próximas etapas

Ao ler este documento, agora você tem uma melhor compreensão dos casos de uso, recursos essenciais e etapas necessárias para desenvolver um painel de insights personalizável com o Data Distiller. Para continuar aprendendo sobre como criar modelos de dados de relatórios por medida, consulte a [guia do modelo de dados do reporting insights](./reporting-insights-data-model.md).
