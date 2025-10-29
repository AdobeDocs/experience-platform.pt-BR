---
title: Prever o churn do cliente com regressão logística baseada em SQL
description: Saiba como prever a rotatividade do cliente usando regressão logística baseada em SQL. Este guia aborda todo o processo, da criação de modelos à avaliação e previsão. Obtenha insights acionáveis do comportamento de compra do cliente para implementar estratégias de retenção proativas e otimizar as decisões de negócios.
exl-id: 3b18870d-104c-4dce-8549-a6818dc40d24
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 1%

---

# Prever o churn do cliente com regressão logística baseada em SQL

A previsão de churn do cliente ajuda as empresas a manter os clientes, otimizar recursos e aumentar a lucratividade melhorando a satisfação e a fidelidade por meio de insights acionáveis.

Descubra como usar a regressão logística baseada em SQL para prever a rotatividade do cliente. Use este guia SQL abrangente para transformar dados brutos de comércio eletrônico em insights significativos do cliente com base em métricas comportamentais fundamentais (como frequência de compra, valor médio de pedido e recenticidade da última compra). O documento abrange todo o processo, desde a preparação de dados e a engenharia de recursos até a criação, avaliação e previsão de modelos.

Use este guia para criar um eficiente modelo de previsão de churn que identifique clientes em risco, refine estratégias de retenção e conduza a melhores decisões de negócios. Ele inclui instruções passo a passo, consultas SQL e explicações detalhadas para ajudá-lo a aplicar com confiança as técnicas de aprendizado de máquina em seu ambiente de dados.

## Introdução

Antes de criar o modelo de churn, é importante explorar os principais recursos e requisitos de dados do cliente. As seções a seguir descrevem os atributos essenciais do cliente e os campos de dados necessários para um treinamento de modelo preciso.

### Definir recursos do cliente {#define-customer-features}

Para classificar com precisão o churn, o modelo analisa os hábitos e as tendências de compra. A tabela abaixo descreve os principais recursos de comportamento do cliente usados no modelo:

| Recurso | Descrição |
|---------------------------|-------------------------------------------------------|
| `total_purchases` | O número total de compras feitas pelo cliente. |
| `total_revenue` | A receita total gerada das compras do cliente. |
| `avg_order_value` | O valor médio das compras de um cliente. |
| `customer_lifetime` | O número de dias entre a primeira e a última compra do cliente. |
| `days_since_last_purchase` | O número de dias desde a última compra do cliente. |
| `purchase_frequency` | O número de meses distintos nos quais o cliente fez compras. |

### Premissas e campos obrigatórios {#assumptions-required-fields}

Para gerar previsões de churn do cliente, o modelo depende dos campos principais da tabela `webevents` que capturam os detalhes da transação do cliente. Seu conjunto de dados deve incluir os seguintes campos:

| Campo | Descrição |
|--------------------------------|----------------------------------------------------|
| `identityMap['ECID'][0].id` | Um identificador exclusivo usado para rastrear clientes nas sessões. |
| `productListItems.priceTotal[0]` | O custo total de itens comprados por transação. |
| `productListItems.quantity[0]` | O número total de itens em uma compra. |
| `timestamp` | A data e hora exatas de cada evento de compra. |
| `commerce.order.purchaseID` | Um valor necessário que confirma uma compra concluída. |

O conjunto de dados deve conter registros históricos estruturados de transações de clientes, com cada linha representando um evento de compra. Cada evento deve incluir carimbos de data e hora em um formato de data e hora apropriado compatível com a função SQL `DATEDIFF` (por exemplo, AAAA-MM-DD HH:MI:SS). Além disso, cada registro deve conter uma ID do Experience Cloud válida (`ECID`) no campo `identityMap` para identificar os clientes de forma exclusiva.

>[!TIP]
>
>O processamento de grandes conjuntos de dados com milhões de registros pode afetar significativamente o desempenho. Para otimizar a execução da consulta, particione o conjunto de dados da experiência por carimbo de data e hora, execute processamento incremental usando instantâneos e aplique funções de agregação eficientes conforme necessário. Além disso, filtre os dados antes da agregação para reduzir a sobrecarga de processamento.

## Criar um modelo {#create-a-model}

Para prever a rotatividade do cliente, você deve criar um modelo de regressão logística baseado em SQL que analise o histórico de compras do cliente e as métricas comportamentais. O modelo classifica os clientes como `churned` ou `not churned`, determinando se eles fizeram uma compra nos últimos 90 dias.

### Usar SQL para criar o modelo de previsão de churn {#sql-create-model}

O modelo baseado em SQL processa dados `webevents` agregando métricas principais e atribuindo rótulos de churn com base em uma regra de inatividade de 90 dias. Essa abordagem distingue clientes ativos de clientes em risco. A consulta SQL também executa a engenharia de recursos para melhorar a precisão do modelo e a classificação de churn. Esses insights capacitam sua empresa a implementar estratégias de retenção direcionadas, reduzir o abandono e maximizar o valor vitalício do cliente.

>[!NOTE]
>
>O modelo de previsão de churn usa um limite padrão de 90 dias para classificar os clientes como churn. Para ajustar esse limite para alinhar-se às suas metas comerciais e estratégias de retenção, modifique a condição `DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90` nas consultas SQL.

Use a seguinte instrução SQL para criar o modelo `retention_model_logistic_reg` com os recursos e rótulos especificados:

```sql
CREATE MODEL retention_model_logistic_reg
TRANSFORM (
  vector_assembler(array(total_purchases, total_revenue, avg_order_value, customer_lifetime, days_since_last_purchase, purchase_frequency)) features
  -- Combines selected customer metrics into a feature vector for model training
)
OPTIONS (
  MODEL_TYPE = 'logistic_reg',  -- Specifies logistic regression as the model type
  LABEL = 'churned'             -- Defines the target label for churn classification
)
AS
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,  -- Extract the unique customer ID from identityMap
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,  -- Calculates the average order value, and handles null values with COALESCE
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue, -- The sum of all purchase values per customer
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases,  -- The total number of items purchased by the customer
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,  -- The days between first and last recorded purchase
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,  -- The days since the last purchase event
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency  -- The count of unique months with purchases
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  -- Filters transactions with valid total price
      AND commerce.`order`.purchaseID <> ''  -- Ensures the order has a valid purchase ID
    GROUP BY customer_id 
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,  -- Extract the unique customer ID for labeling
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1  -- Marks the customer as churned if no purchase occurred in the last 90 days
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0) 
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id  
)
SELECT
    f.customer_id,
    f.total_purchases,
    f.total_revenue,
    f.avg_order_value,
    f.customer_lifetime,
    f.days_since_last_purchase,
    f.purchase_frequency,
    l.churned
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id  -- Join features with churn labels
ORDER BY RANDOM()  -- Shuffles rows randomly for training
LIMIT 500000;  -- Limit the dataset to 500,000 rows for model training
```

### Saída do modelo {#model-output}

O conjunto de dados de saída contém métricas relacionadas ao cliente e seu status de churn. Cada linha representa um cliente, seus valores de recurso e seu status de churn. Você pode usar esse resultado para analisar o comportamento do cliente, treinar modelos preditivos e desenvolver estratégias de retenção direcionadas para reter clientes em risco. Um exemplo de tabela de saída é mostrado abaixo:

```console
 customer_id  | total_purchases | total_revenue | avg_order_value  | customer_lifetime | days_since_last_purchase | purchase_frequency | churned |
|--------------+-----------------+---------------+------------------+-------------------+--------------------------+--------------------+----------
  100001      | 25              | 1250.00       | 50.00            | 540               | 20                       | 10                 | 0       
  100002      | 3               | 90.00         | 30.00            | 120               | 95                       | 1                  | 1       
  100003      | 60              | 7200.00       | 120.00           | 800               | 5                        | 24                 | 0       
  100004      | 15              | 750.00        | 50.00            | 365               | 60                       | 8                  | 0       
  100005      | 1               | 25.00         | 25.00            | 60                | 180                      | 1                  | 1       
```

| Coluna | Descrição |
|-----------|------------------------------------------------------------------------------------|
| `churned` | O valor indica se o cliente fez uma compra nos últimos 90 dias (0 = sem churn, 1 = com churn). |

## Usar SQL para avaliar o modelo {#model-evaluation}

Em seguida, avalie o modelo de previsão de churn para determinar sua eficácia na identificação de clientes em risco. Avalie o desempenho do modelo com métricas principais que medem a precisão e a confiabilidade.

Para medir a precisão do modelo `retention_model_logistic_reg` em prever o churn do cliente, use a função `model_evaluate`. O exemplo de SQL a seguir avalia o modelo usando um conjunto de dados estruturado como os dados de treinamento:

```sql
SELECT * 
FROM model_evaluate(retention_model_logistic_reg, 1,
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue,
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases, 
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency 
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)
      AND commerce.`order`.purchaseID <> ''
    GROUP BY customer_id
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1 
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0) 
      AND commerce.`order`.purchaseID <> '' 
    GROUP BY customer_id
)
SELECT
    f.customer_id,
    f.total_purchases,
    f.total_revenue,
    f.avg_order_value,
    f.customer_lifetime,
    f.days_since_last_purchase,
    f.purchase_frequency,
    l.churned
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id); -- Joins customer features with churn labels
```

### Saída de avaliação do modelo

Os resultados da avaliação incluem as principais métricas de desempenho, como AUC-ROC, precisão, e recuperação. Essas métricas fornecem insights sobre a eficácia do modelo que você pode usar para refinar estratégias de retenção e tomar decisões orientadas por dados.

>[!NOTE]
>
>Os valores de desempenho variam de 0 a 1, onde 1,0 representa o desempenho perfeito.

```console
 auc_roc | accuracy | precision | recall 
|---------+----------+-----------+--------
1        | 0.99998  |  1        |  1      
```

| Métrica | Descrição |
|------------|-------------------------------------------------------------------------|
| `auc_roc` | Essa métrica indica a capacidade do modelo de distinguir entre clientes com e sem churn. Um valor mais próximo a 1 indica melhor desempenho. |
| `accuracy` | A métrica de precisão representa a proporção de previsões corretas, fornecendo uma medida geral do desempenho do modelo. |
| `precision` | A precisão mostra a proporção de clientes com churn identificados corretamente e indica a confiabilidade na previsão de churn. Um valor alto significa menos falsos positivos. |
| `recall` | A recuperação mede a capacidade do modelo de identificar todos os clientes reais com churn. Um valor alto de recuperação indica menos clientes com churn perdido. |

>[!NOTE]
>
>As pontuações quase perfeitas neste exemplo são para fins de demonstração. Na prática, os dados do mundo real podem produzir valores mais baixos devido ao ruído e à variabilidade.

## Previsão de modelo {#model-prediction}

Depois que o modelo for avaliado, use `model_predict` para aplicá-lo a um novo conjunto de dados e fazer a previsão do churn do cliente. Você pode usar essas previsões para identificar clientes em risco e implementar estratégias de retenção direcionadas.

### Usar SQL para gerar previsões de churn {#sql-model-predict}

A consulta SQL abaixo usa o modelo `retention_model_logistic_reg` para prever o cancelamento do cliente com um conjunto de dados estruturado como os dados de treinamento:

```sql
SELECT * 
FROM model_predict(retention_model_logistic_reg, 1,  -- Applies the trained model for churn prediction
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,  
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue, 
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases,  
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,  
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,  
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency  
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  -- Ensures only valid purchase data is considered
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,  
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1  -- Identify customers who have not purchased in the last 90 days
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id
)
SELECT
    f.customer_id,  
    f.total_purchases,  
    f.total_revenue,  
    f.avg_order_value,  
    f.customer_lifetime,  
    f.days_since_last_purchase,  
    f.purchase_frequency,  
    l.churned  
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id);  -- Matches features with their churn labels for prediction
```

### Saída de previsão de modelo {#prediction-output}

O conjunto de dados de saída inclui os principais recursos do cliente e seu status de churn previsto, o que indica se é provável que um cliente faça churn. Use esses insights para implementar estratégias de retenção proativas e reduzir a rotatividade do cliente.

```console
 total_purchases | total_revenue | avg_order_value | customer_lifetime | days_since_last_purchase | purchase_frequency | churned | prediction
|-----------------+---------------+-----------------+-------------------+--------------------------+--------------------+---------+------------
 2               | 299           | 149.5           | 0                 | 13                        | 1                  | 0       | 0
 1               | 710           | 710.00          | 0                 | 149                       | 1                  | 1       | 1
 1               | 19.99         | 19.99           | 0                 | 30                        | 1                  | 0       | 0
 1               | 4528          | 4528.00         | 0                 | 26                        | 1                  | 0       | 0
 1               | 21.84         | 21.84           | 0                 | 90                        | 1                  | 0       | 0
 1               | 16.64         | 16.64           | 0                 | 268                       | 1                  | 1       | 1
```

| Coluna | Descrição |
|---------------|-------------------------------------------------------------------------------|
| `prediction` | O status de churn previsto do cliente com base no modelo (0 = sem churn, 1 = churn). |

## Próximas etapas

Agora você aprendeu a criar, avaliar e usar um modelo baseado em SQL para prever o cancelamento do cliente. Com essa base, você pode analisar o comportamento do cliente, identificar clientes em risco e implementar estratégias de retenção proativas para melhorar a retenção do cliente. Para aprimorar e aplicar ainda mais seu modelo de previsão de churn, considere as seguintes etapas:

- Automatizar o processo: integre o modelo em um pipeline de dados para monitoramento contínuo e insights em tempo real. [Saiba como verificar e processar conjuntos de dados com o SQL](../../../dashboards/query.md).
- Monitorar o desempenho do modelo: avalie continuamente o modelo com novos dados para manter a precisão e a relevância.  Use o [Assistente de IA](../../../ai-assistant/landing.md) na interface do Adobe Experience Platform para monitorar as principais alterações de desempenho e [prever tendências de público-alvo](../../../ai-assistant/new-features/audience-forecasting.md).
