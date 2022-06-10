---
title: 'Insights Do Analytics Para Interações Web E Móveis '
description: Este documento explica como usar o Serviço de query para criar insights acionáveis a partir de dados assimilados do Adobe Analytics.
source-git-commit: cdceba9caf035831f4c376edf34356f666b79aa8
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 1%

---

# Insights do Analytics para interações da Web e móveis

O Adobe Experience Platform permite assimilar dados de conjuntos de relatórios do Adobe Analytics usando campos do Experience Data Model (XDM) para preencher conjuntos de dados. O Serviço de query pode então usar esses dados de análise executando consultas SQL para gerar informações valiosas de um comportamento de usuários nas plataformas digitais.

Este documento fornece uma variedade de consultas SQL de amostra que demonstram casos de uso comuns ao criar insights de dados da Web e do Mobile Analytics.

Consulte a [Documentação de mapeamentos de campo do Analytics](../../sources/connectors/adobe-applications/mapping/analytics.md) para obter mais informações sobre assimilação e mapeamento de dados analíticos.

## Introdução

Para cada um dos seguintes casos de uso, um exemplo de consulta SQL parametrizado é fornecido como um template para você personalizar. Forneça parâmetros onde você visualizar `{ }` nos exemplos de SQL para o conjunto de dados, eVar, evento ou período que você está interessado em avaliar.

## Objetivos

Os exemplos a seguir mostram consultas SQL para casos de uso comuns para analisar seus dados do Adobe Analytics.

### Gerar a contagem de visitantes para cada hora em um determinado dia

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour,
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

### Identificar as 10 páginas mais visualizadas em um determinado dia

```SQL
SELECT web.webpagedetails.name AS Page_Name,
       Sum(web.webpagedetails.pageviews.value) AS Page_Views
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY web.webpagedetails.name
ORDER BY page_views DESC
LIMIT  10;
```

### Identificar os 10 usuários mais ativos

```sql
SELECT enduserids._experience.aaid.id AS aaid,
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### Identifique as 10 cidades mais desejadas com base na atividade do usuário

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city,
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY state_city
ORDER BY Count DESC
LIMIT  10;
```

### Identifique os 10 produtos mais vistos

```sql
SELECT Product_SKU,
       Sum(Product_Views) AS Total_Product_Views
FROM  (SELECT Explode(productlistitems.sku) AS Product_SKU,
              commerce.productviews.value   AS Product_Views
       FROM   {TARGET_TABLE}
            WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
              AND commerce.productviews.value IS NOT NULL)
GROUP BY Product_SKU
ORDER BY Total_Product_Views DESC
LIMIT  10;
```

### Identificar as 10 receitas de pedidos mais altas

```sql
SELECT Purchase_ID,
       Round(Sum(Product_Items.priceTotal * Product_Items.quantity), 2) AS Total_Order_Revenue
FROM   (SELECT commerce.`order`.purchaseid AS Purchase_ID,
               Explode(productlistitems)   AS Product_Items
        FROM   {TARGET_TABLE}
        WHERE  commerce.`order`.purchaseid IS NOT NULL
                AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')

GROUP BY Purchase_ID
ORDER BY total_order_revenue DESC
LIMIT  10;
```
