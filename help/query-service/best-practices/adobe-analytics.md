---
keywords: Experience Platform;home;popular topics;query service;Query service;exemplo de query;exemplo de query;adobe analytics;
solution: Experience Platform
title: Query de amostra
topic: queries
description: Os dados de conjuntos de relatórios selecionados da Adobe Analytics são transformados em XDM ExperienceEvents e ingeridos no Adobe Experience Platform como conjuntos de dados para você. Este documento descreve vários casos de uso em que o Adobe Experience Platform Query Service usa esses dados e os query de amostra incluídos devem funcionar com seus conjuntos de dados Adobe Analytics.
translation-type: tm+mt
source-git-commit: e2c648829bb3268ab319da934f5cc6cc811290b3
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 1%

---


# Query de amostra para dados do Adobe Analytics

Os dados de conjuntos de relatórios selecionados da Adobe Analytics são transformados em dados em conformidade com a classe [!DNL XDM ExperienceEvent] e ingeridos no Adobe Experience Platform como conjuntos de dados.

Este documento descreve vários casos de uso em que a Adobe Experience Platform [!DNL Query Service] usa esses dados, incluindo query de amostra, devem funcionar com seus conjuntos de dados Adobe Analytics. Consulte a documentação em [Mapeamento de campos do Analytics](../../sources/connectors/adobe-applications/mapping/analytics.md) para obter mais informações sobre o mapeamento para [!DNL Experience Events].

## Introdução

Os exemplos SQL deste documento exigem que você edite o SQL e preencha os parâmetros esperados para seus query com base no conjunto de dados, no eVar, no evento ou no período em que você está interessado em avaliar. Forneça parâmetros onde quer que você veja `{ }` nos exemplos de SQL a seguir.

## Exemplos SQL usados com frequência

Os exemplos a seguir mostram query SQL comumente usados para analisar seus dados do Adobe Analytics.

### Contagem de visitantes por hora para um determinado dia

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count 
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

### As 10 principais páginas visualizadas de um determinado dia

```sql
SELECT web.webpagedetails.name AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY web.webpagedetails.name 
ORDER BY page_views DESC 
LIMIT  10;
```

### Os 10 usuários mais ativos

```sql
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### Dez cidades principais por atividade do usuário

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
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
       FROM   {TARGET_TABLE}
            WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
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
        FROM   {TARGET_TABLE} 
        WHERE  commerce.`order`.purchaseid IS NOT NULL 
                AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')

GROUP BY Purchase_ID 
ORDER BY total_order_revenue DESC 
LIMIT  10;
```

### Contagens de eventos por dia

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day, 
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Sum(_experience.analytics.event1to100.{TARGET_EVENT}.value) AS Event_Count
FROM   {TARGET_TABLE}
WHERE  _experience.analytics.event1to100.{TARGET_EVENT}.value IS NOT NULL 
        AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

## Variáveis de comercialização (sintaxe de produto)


### Sintaxe do produto

No Adobe Analytics, os dados personalizados no nível do produto podem ser coletados por meio de variáveis especialmente configuradas chamadas variáveis de comercialização. Eles são baseados em um eVar ou eventos personalizados. A diferença entre essas variáveis e seu uso padrão é que elas representam um valor separado para cada produto encontrado na ocorrência, em vez de apenas um valor para a ocorrência.

Essas variáveis são chamadas de variáveis de comercialização da sintaxe do produto. Isso permite a coleta de informações, como uma &quot;quantia de desconto&quot; por produto ou informações sobre a &quot;localização na página&quot; do produto nos resultados de pesquisa do cliente.

Para saber mais sobre o uso da sintaxe do produto, leia a documentação da Adobe Analytics em [implementação de eVars usando a sintaxe do produto](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-product-syntax).

As seções abaixo descrevem os campos XDM necessários para acessar as variáveis de comercialização no conjunto de dados [!DNL Analytics]:

#### eVars

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

- `#`: O índice do storage que você está acessando.
- `evar#`: A variável de eVar específica que você está acessando.

#### Eventos personalizados

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

- `#`: O índice do storage que você está acessando.
- `event#`: A variável de evento personalizada específica que você está acessando.

#### Query de amostra

Este é um exemplo de query que retorna um eVar e um evento de comercialização para o primeiro produto encontrado no `productListItems`.

```sql
SELECT
  productListItems[0]._experience.analytics.customDimensions.evars.eVar1,
  productListItems[0]._experience.analytics.event1to100.event1.value
FROM adobe_analytics_midvalues
WHERE timestamp = to_timestamp('2019-07-23')
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
LIMIT 10
```

Este próximo query explora a matriz `productListItems` e retorna cada eVar e evento de comercialização por produto. O campo `_id` é incluído para mostrar a relação com a ocorrência original. O valor `_id` é uma chave primária exclusiva para o conjunto de dados.

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
  WHERE TIMESTAMP = to_timestamp('2019-07-23')
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
)
LIMIT 20
```

>[!NOTE]
>
> Se você tentar recuperar um campo que não existe no conjunto de dados atual, o erro &quot;Nenhum campo struct&quot; ocorrerá. Avalie o motivo retornado na mensagem de erro para identificar um campo disponível, atualize seu query e execute-o novamente.
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### Sintaxe de conversão

Outro tipo de variável de comercialização encontrado no Adobe Analytics é a sintaxe de conversão. Com a sintaxe do produto, o valor é coletado ao mesmo tempo que o produto, mas isso requer que os dados estejam presentes na mesma página. Há cenários em que os dados ocorrem em uma página antes da conversão ou do evento de interesse relacionado ao produto. Por exemplo, considere o caso de uso para o método de descoberta de produtos.

1. Um usuário realiza uma pesquisa interna por &quot;chapéu de inverno&quot;, que define o eVar 6 de comercialização ativado pela Sintaxe de conversão como &quot;pesquisa interna:chapéu de inverno&quot;
2. O usuário clica em &quot;waffle beanie&quot; e chega à página de detalhes do produto.\
   a. Aterrissando aqui dispara um evento `Product View` para o &quot;waffle beanie&quot; por $12.99.\
   b. Como `Product View` está configurado como um evento de vínculo, o produto &quot;waffle beanie&quot; agora está vinculado ao valor eVar6 de &quot;pesquisa interna:chapéu de inverno&quot;. Sempre que o produto &quot;waffle beanie&quot; for coletado, ele será associado a &quot;pesquisa interna:chapéu de inverno&quot; até que (1) a configuração de expiração seja atingida ou (2) um novo valor de eVar6 seja definido e o evento de vinculação ocorra novamente com esse produto.
3. O usuário adiciona o produto ao carrinho, disparando o evento `Cart Add`.
4. O usuário realiza outra pesquisa interna por &quot;camisa de verão&quot;, que define o eVar 6 de comercialização ativado pela Sintaxe de conversão como &quot;pesquisa interna:camisa de verão&quot;
5. O usuário clica em &quot;t-shirt esportiva&quot; e chega à página de detalhes do produto.\
   a. Aterrissando aqui dispara um evento de &quot;camiseta esportiva&quot; por $19,99.`Product View`\
   b. O evento `Product View` ainda é nosso evento de ligação, então agora o produto &quot;t-shirt esportiva&quot; está vinculado ao valor eVar6 de &quot;pesquisa interna:camisa de verão&quot; e o produto anterior &quot;waffle beanie&quot; ainda está vinculado a um valor eVar6 de &quot;pesquisa interna:waffle beanie&quot;.
6. O usuário adiciona o produto ao carrinho, disparando o evento `Cart Add`.
7. O usuário faz check-out com ambos os produtos.

No relatórios, os pedidos, a receita, as visualizações de produtos e as adições ao carrinho serão relatáveis em relação ao eVar6 e serão alinhados à atividade do produto vinculado.

| eVar6 (método de descoberta de produtos) | receita | ordens | visualizações de produtos | adição ao carrinho |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| pesquisa interna:camisa de verão | 19,99 | 1 | 1 | 3 |
| pesquisa interna:chapéu de inverno | 12,99 | 1 | 3 | 3 |

Para saber mais sobre como usar a sintaxe de conversão, leia a documentação da Adobe Analytics em [implementar eVars usando a sintaxe de conversão](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-conversion-variable-syntax).

Estes são os campos XDM para produzir a sintaxe de conversão no conjunto de dados [!DNL Analytics]:

#### eVars

```console
_experience.analytics.customDimensions.evars.evar#
```

- `evar#`: A variável de eVar específica que você está acessando.

#### Produto

```console
productListItems[#].sku
```

- `#`: O índice do storage que você está acessando.

#### Query de amostra

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
