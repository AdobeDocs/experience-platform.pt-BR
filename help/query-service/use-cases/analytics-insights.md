---
title: Insights do Analytics para interações da Web e móveis
description: Este documento explica como usar o Serviço de consulta para criar insights acionáveis de dados assimilados do Adobe Analytics.
exl-id: f64e61ef-0157-4f0a-88f8-bbe4f9aa83f0
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 1%

---

# Insights do Analytics para interações da Web e móveis

O Adobe Experience Platform permite assimilar dados dos conjuntos de relatórios do Adobe Analytics usando campos do Experience Data Model (XDM) para preencher conjuntos de dados. Esses dados de análise foram modificados para estarem em conformidade com a [!DNL XDM ExperienceEvent] classe. O Serviço de consulta pode então usar esses dados executando consultas SQL para gerar insights valiosos do comportamento de um usuário nas plataformas digitais.

Este documento fornece uma variedade de exemplos de consultas SQL que demonstram casos de uso comuns ao criar insights de dados da Web e de dispositivos móveis do Analytics.

Consulte a [Documentação de mapeamentos de campo do Analytics](../../sources/connectors/adobe-applications/mapping/analytics.md) para obter mais informações sobre assimilação e mapeamento de dados do analytics.

## Introdução

Para cada um dos seguintes casos de uso, um exemplo de consulta SQL parametrizada é fornecido como um template para você personalizar. Forneça parâmetros onde quer que você veja `{ }` nos exemplos SQL do conjunto de dados, eVar, evento ou intervalo de tempo que você está interessado em avaliar.

## Objetivos

Os exemplos a seguir mostram consultas SQL para casos de uso comuns para analisar os dados do Adobe Analytics.

### Gera a contagem de visitantes para cada hora em um determinado dia

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

### Identificar as 10 cidades mais desejadas com base na atividade do usuário

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city,
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY state_city
ORDER BY Count DESC
LIMIT  10;
```

### Identificar os 10 produtos mais visualizados

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

### Identificar as 10 receitas mais altas de pedidos

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
