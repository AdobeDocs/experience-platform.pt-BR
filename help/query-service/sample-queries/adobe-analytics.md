---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Query de amostra
topic: queries
translation-type: tm+mt
source-git-commit: 38cb8eeae3ac0a1852c59e433d1cacae82b1c6c0
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 1%

---


# Query de amostra para dados do Adobe Analytics

Os dados de conjuntos de relatórios selecionados da Adobe Analytics são transformados em XDM [!DNL ExperienceEvents] e ingeridos no Adobe Experience Platform como conjuntos de dados para você. Este documento descreve vários casos de uso em que a Adobe Experience Platform [!DNL Query Service] usa esses dados e os query de amostra incluídos devem funcionar com seus conjuntos de dados Adobe Analytics. Consulte a documentação [de mapeamento de campo do](../../sources/connectors/adobe-applications/mapping/analytics.md) Analytics para obter mais informações sobre o mapeamento para XDM [!DNL ExperienceEvents].

## Introdução

Os exemplos SQL deste documento exigem que você edite o SQL e preencha os parâmetros esperados para seus query com base no conjunto de dados, no eVar, no evento ou no período em que você está interessado em avaliar. Forneça parâmetros onde quer que você veja `{ }` os exemplos de SQL a seguir.

## Exemplos SQL usados com frequência

### Contagem de visitantes por hora para um determinado dia

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count 
FROM   {target_table}
WHERE _acp_year = {target_year} 
      AND _acp_month = {target_month}  
      AND _acp_day = {target_day}
GROUP BY Day, Hour
ORDER BY Hour;
```

### As 10 principais páginas visualizadas de um determinado dia

```sql
SELECT web.webpagedetails.name AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP BY web.webpagedetails.name 
ORDER BY page_views DESC 
LIMIT  10;
```

### Os 10 usuários mais ativos

```sql
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp) AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### Dez cidades principais por atividade do usuário

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp) AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP BY state_city
ORDER BY Count DESC
LIMIT  10;
```

### Os 10 principais produtos visualizados

```sql
SELECT Product_SKU,
       Sum(Product_Views) AS Total_Product_Views
FROM  (SELECT Explode(productlistitems.sku) AS Product_SKU, 
              commerce.productviews.value   AS Product_Views 
       FROM   {target_table}
       WHERE  _acp_year = {target_year}
              AND _acp_month = {target_month}
              AND _acp_day = {target_day}
              AND commerce.productviews.value IS NOT NULL) 
GROUP BY Product_SKU 
ORDER BY Total_Product_Views DESC
LIMIT  10;
```

### 10 principais receitas totais da ordem

```sql
SELECT Purchase_ID, 
       Round(Sum(Product_Items.priceTotal * Product_Items.quantity), 2) AS Total_Order_Revenue 
FROM   (SELECT commerce.`order`.purchaseid AS Purchase_ID, 
               Explode(productlistitems)   AS Product_Items 
        FROM   {target_table} 
        WHERE  commerce.`order`.purchaseid IS NOT NULL 
               AND _acp_year = {target_year} 
               AND _acp_month = {target_month}  
               AND _acp_day = {target_day}) 
GROUP BY Purchase_ID 
ORDER BY total_order_revenue DESC 
LIMIT  10;
```

### Contagens de eventos por dia

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day, 
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Sum(_experience.analytics.event1to100.{target_event}.value) AS Event_Count
FROM   {target_table}
WHERE  _experience.analytics.event1to100.{target_event}.value IS NOT NULL 
        AND _acp_year = {target_year} 
        AND _acp_month = {target_month}  
        AND _acp_day = {target_day}
GROUP BY Day, Hour
ORDER BY Hour;
```

## Variáveis de comercialização (sintaxe de produto)

No Adobe Analytics, dados personalizados de nível de produto podem ser coletados por meio de variáveis especialmente configuradas chamadas de &quot;Variáveis de comercialização&quot;. Eles são baseados em um eVar ou Evento personalizado. A diferença entre essas variáveis e seu uso padrão é que elas representam um valor separado para cada produto encontrado na ocorrência, em vez de apenas um valor para a ocorrência. Essas variáveis são chamadas de Variáveis de comercialização de sintaxe de produto. Isso permite a coleta de informações como uma &quot;quantia de desconto&quot; por produto ou informações sobre a &quot;localização na página&quot; do produto nos resultados de pesquisa do cliente.

Estes são os campos XDM para acessar as variáveis de comercialização em seu [!DNL Analytics] conjunto de dados:

### eVars

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

Onde `[#]` é um índice de matriz e `evar#` é a variável de eVar específica.

### Eventos personalizados

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

Onde `[#]` é um índice de matriz e `event#` é a variável de evento personalizada específica.

### Query de amostra

Este é um query de amostra que retorna um eVar e um evento de comercialização para o primeiro produto encontrado no `productListItems`.

```sql
SELECT
  productListItems[0]._experience.analytics.customDimensions.evars.eVar1,
  productListItems[0]._experience.analytics.event1to100.event1.value
FROM adobe_analytics_midvalues
WHERE _ACP_YEAR=2019 AND _ACP_MONTH=7 AND _ACP_DAY=23
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
LIMIT 10
```

Esse próximo query &quot;explode&quot; o e retorna cada eVar de comercialização e evento por produto. `productListItems` O `_id` campo é incluído para mostrar a relação com a ocorrência original. O `_id` valor é uma chave primária exclusiva no [!DNL ExperienceEvent] conjunto de dados.

```sql
SELECT
  _id,
  productItem._experience.analytics.customDimensions.evars.eVar1,
  productItem._experience.analytics.event1to100.event1.value
FROM (
  SELECT
    _id,
    explode(productListItems) as productItem
  FROM adobe_analytics_midvalues
  WHERE _ACP_YEAR=2019 AND _ACP_MONTH=7 AND _ACP_DAY=23
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
)
LIMIT 20
```

### Erro comum ao implementar query de amostra

O erro &quot;Nenhum campo struct&quot; é encontrado quando você tenta recuperar um campo que não existe no conjunto de dados atual. Avalie o motivo retornado na mensagem de erro para identificar um campo disponível, atualize seu query e execute-o novamente.

```console
ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
```

## Variáveis de comercialização (sintaxe de conversão)

Outro tipo de Variável de comercialização encontrado no Adobe Analytics é Sintaxe de conversão. Com a Sintaxe do produto, o valor é coletado ao mesmo tempo que o produto, mas isso requer que os dados estejam presentes na mesma página. Há cenários em que os dados ocorrem em uma página antes da conversão ou do evento de interesse relacionado ao produto. Por exemplo, considere o caso de uso do relatórios Método de descoberta de produto.

1. Um usuário realiza uma pesquisa interna por &quot;chapéu de inverno&quot;, que define o eVar 6 de comercialização ativado pela Sintaxe de conversão como &quot;pesquisa interna:chapéu de inverno&quot;
2. O usuário clica em &quot;waffle beanie&quot; e chega à página de detalhes do produto.\
   a. Aterrissando aqui dispara um `Product View` evento para o &quot;waffle beanie&quot; por $12,99.\
   b. Como `Product View` está configurado como um evento de ligação, o produto &quot;waffle beanie&quot; agora está vinculado ao valor eVar6 de &quot;pesquisa interna:chapéu de inverno&quot;. Sempre que o produto &quot;waffle beanie&quot; for coletado, ele será associado a &quot;pesquisa interna:chapéu de inverno&quot; até que (1) a configuração de expiração seja atingida ou (2) um novo valor de eVar6 seja definido e o evento de vinculação ocorra novamente com esse produto.
3. O usuário adiciona o produto ao carrinho, disparando o `Cart Add` evento.
4. O usuário realiza outra pesquisa interna por &quot;camisa de verão&quot;, que define o eVar 6 de comercialização ativado pela Sintaxe de conversão como &quot;pesquisa interna:camisa de verão&quot;
5. O usuário clica em &quot;t-shirt esportiva&quot; e chega à página de detalhes do produto.\
   a. Aterrissando aqui dispara um `Product View` evento de &quot;camiseta esportiva por $19,99.\
   b. O `Product View` evento ainda é nosso evento de ligação, então agora o produto &quot;camiseta esportiva&quot; está vinculado ao valor eVar6 de &quot;pesquisa interna:camisa de verão&quot; e o produto anterior &quot;waffle beanie&quot; ainda está vinculado a um valor eVar6 de &quot;pesquisa interna:waffle beanie&quot;.
6. O usuário adiciona o produto ao carrinho, disparando o `Cart Add` evento.
7. O usuário faz check-out com ambos os produtos.

No relatórios, os pedidos, a receita, as visualizações de produtos e as adições ao carrinho serão relatáveis em relação ao eVar6 e serão alinhados à atividade do produto vinculado.

| eVar6 (Método de descoberta do produto) | receita | ordens | visualizações de produtos | adição ao carrinho |
|---|---|---|---|---|
| pesquisa interna:camisa de verão | 19.99 | 1 | 1 | 1 |
| pesquisa interna:chapéu de inverno | 12.99 | 1 | 1 | 1 |

Estes são os campos XDM para produzir a Sintaxe de conversão no seu [!DNL Analytics] conjunto de dados:

### eVars

```console
_experience.analytics.customDimensions.evars.evar#
```

Onde `evar#` está a variável de eVar específica.

### Produto

```console
productListItems[#].sku
```

Onde `[#]` está um índice de matriz.

### Query de amostra

Este é um exemplo de query que vincula o valor ao produto específico e ao par de eventos, neste caso o evento da visualização do produto.

```sql
SELECT
  endUserIds._experience.aaid.id AS AAID,
  timestamp,
  CASE WHEN commerce.productViews.value = 1 THEN ATTRIBUTION_LAST_TOUCH(timestamp, 'bindConversionSyntaxMerchVariable_eVar1', _experience.analytics.customDimensions.eVars.eVar1)
  OVER(PARTITION BY endUserIds._experience.aaid.id
       ORDER BY timestamp
       ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
  END AS eVar1Bind,
  EXPLODE(productListItems) AS Product_List,
  commerce.productViews.value AS prodView,
  commerce.purchases.value AS purchase
FROM adobe_analytics_midvalues
WHERE commerce.productViews.value = 1 OR commerce.purchases.value = 1 OR _experience.analytics.customDimensions.eVars.eVar1 IS NOT NULL
LIMIT 100
```

Este é um query de exemplo que persiste o valor vinculado às ocorrências subsequentes do respectivo produto. O subquery mais baixo estabelece a relação de valores com o produto no evento de vínculo declarado. O próximo subquery executa a atribuição desse valor vinculado nas interações subsequentes com o respectivo produto. E a seleção de nível superior agregação os resultados para produzir o relatórios.

```sql
SELECT
  Product_List.SKU,
  eVar1101ConversionSyntax,
  SUM(prodView) AS Product_Views,
  SUM(purchase) AS Purchases
FROM
(
  SELECT
    Product_List,
    ATTRIBUTION_LAST_TOUCH(timestamp, 'ConversionSyntax_eVar1', eVar1Bind)
      OVER(PARTITION BY AAID, Product_List.SKU
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
    AS eVar1ConversionSyntax,
    prodView,
    purchase
  FROM
  (
    SELECT
      endUserIds._experience.aaid.id AS AAID,
      timestamp,
      CASE WHEN commerce.productViews.value = 1 THEN ATTRIBUTION_LAST_TOUCH(timestamp, 'bindConversionSyntaxMerchVariable_eVar1', _experience.analytics.customDimensions.eVars.eVar1)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
      END AS eVar1Bind,
      EXPLODE(productListItems) AS Product_List,
      commerce.productViews.value AS prodView,
      commerce.purchases.value AS purchase
    FROM adobe_analytics_midvalues
    WHERE commerce.productViews.value = 1 OR commerce.purchases.value = 1 OR _experience.analytics.customDimensions.eVars.eVar1 IS NOT NULL
  )
)
WHERE eVar1ConversionSyntax IS NOT NULL
GROUP BY 1, 2
ORDER BY 3 DESC
LIMIT 100
```
