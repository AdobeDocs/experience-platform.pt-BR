---
title: Retornar e usar variáveis de merchandising dos dados de análise
description: Saiba como fornecer campos XDM e consultas de exemplo para acessar as variáveis de merchandising em seus conjuntos de dados do Analytics.
exl-id: 1e2ae095-4152-446f-8b66-dae5512d690e
source-git-commit: 7cde32f841497edca7de0c995cc4c14501206b1a
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 1%

---

# Retornar e usar variáveis de merchandising dos dados de análise

Use o Serviço de consulta para gerenciar os dados assimilados da Adobe Analytics na Adobe Experience Platform como conjuntos de dados. As seções a seguir fornecem exemplos de consultas que você pode usar para acessar as variáveis de merchandising nos conjuntos de dados do Analytics. Consulte a documentação para obter mais informações sobre [como assimilar e mapear dados do Adobe Analytics](../../sources/connectors/adobe-applications/mapping/analytics.md) por meio da fonte do Analytics

## Variáveis de merchandising {#merchandising-variables}

As variáveis de merchandising podem seguir uma das duas sintaxes:

* **Sintaxe do Produto**: Associa o valor do eVar a um produto. 
* **Sintaxe de variável de conversão**: associa o eVar a um produto somente se um evento de associação ocorrer. Você pode selecionar os eventos que atuam como eventos de vinculação.

## Sintaxe do produto {#product-syntax}

No Adobe Analytics, os dados personalizados a nível de produto podem ser coletados por meio de variáveis especialmente configuradas, chamadas de variáveis de merchandising. Elas se baseiam em eventos de eVar ou personalizados. A diferença entre essas variáveis e seu uso típico é que elas representam um valor separado para cada produto encontrado na ocorrência, em vez de apenas um valor único para a ocorrência.

Essas variáveis são chamadas de variáveis de merchandising da sintaxe do produto. Isso permite a coleta de informações, como um &quot;valor de desconto&quot; por produto ou informações sobre o &quot;local na página&quot; do produto nos resultados de pesquisa do cliente.

Para saber mais sobre como usar a sintaxe do produto, leia a documentação do Adobe Analytics em [implementação de eVars usando a sintaxe do produto](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-product-syntax).

As seções abaixo descrevem os campos XDM necessários para acessar as variáveis de merchandising em seu conjunto de dados [!DNL Analytics]:

### eVars

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

* `#`: o índice da matriz que você está acessando.
* `evar#`: a variável de eVar específica que você está acessando.

### Eventos personalizados

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

* `#`: o índice da matriz que você está acessando.
* `event#`: a variável de evento personalizado específica que você está acessando.

## Casos de uso da sintaxe do produto {#product-use-cases}

Os seguintes casos de uso se concentram no retorno de um eVar de merchandising da matriz `productListItems` usando SQL.

### Devolver um eVar e um evento de merchandising

A consulta abaixo retorna um eVar de merchandising e um evento para o primeiro produto encontrado na matriz `productListItems`.

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

### Exploda a matriz productListItems e retorne o eVar e o evento de merchandising para cada produto.

A próxima consulta explode a matriz `productListItems` e retorna cada eVar e evento de merchandising por produto. O campo `_id` é incluído para mostrar a relação com a ocorrência original. O valor `_id` é uma chave primária exclusiva para o conjunto de dados.

>[!NOTE]
>
>A função de explosão separa os elementos de uma matriz em várias linhas. Isso exclui valores nulos.

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
> Se você tentar recuperar um campo que não existe no conjunto de dados atual, o erro &quot;Campo de estrutura inexistente&quot; ocorrerá. Avalie o motivo retornado na mensagem de erro para identificar um campo disponível, atualize sua consulta e execute-a novamente.
>
>```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### Sintaxe de variável de conversão {#conversion-variable-syntax}

Outro tipo de variável de merchandising encontrada no Adobe Analytics é a sintaxe de variável de conversão. A sintaxe da variável de conversão é usada quando o valor de eVar não está disponível para ser definido na variável products. Normalmente, significa que sua página não tem o contexto do canal de merchandising ou do método de descoberta. Nesses casos, você deve definir a variável de merchandising antes que o usuário chegue à página do produto e o valor persiste até que o evento compulsório ocorra.

Por exemplo, o cenário de busca de produtos abaixo ilustra como os dados necessários podem estar presentes em uma página antes que a conversão ou o evento relacionado ao produto ocorra.

1. Um usuário realiza uma pesquisa interna para &quot;winter hat&quot;, que define a sintaxe de conversão ativada para o eVar de merchandising6 como &quot;pesquisa interna:winter hat&quot;.
2. O usuário clica em &quot;waffle beanie&quot; e chega à página de detalhes do produto.\
   a. Pousar aqui dispara um evento `Product View` para o &quot;waffle beanie&quot; por US$ 12,99.\
   b. Como `Product View` é configurado como um evento compulsório, o produto &quot;waffle beanie&quot; agora é vinculado ao valor eVar6 de &quot;internal search:winter hat&quot;. Sempre que o produto &quot;waffle beanie&quot; é coletado, ele é associado com &quot;pesquisa interna: chapéu de inverno&quot;. Isso acontece até que a configuração de expiração do eVar seja atingida ou até que um novo valor de eVar 6 seja definido e o evento compulsório ocorra com esse produto novamente.
3. O usuário adiciona o produto ao carrinho, acionando o evento `Cart Add`.
4. O usuário executa outra pesquisa interna para &quot;camisa de verão&quot;, que define a sintaxe de conversão ativada para eVar de merchandising6 como &quot;pesquisa interna:camisa de verão&quot;.
5. O usuário seleciona &quot;camiseta esportiva&quot; e acessa a página de detalhes do produto.\
   a. Lançar aqui dispara um evento `Product View` para camiseta esportiva por $19,99.\
   b. Como o evento `Product View` é o evento compulsório, o produto &quot;camiseta esportiva&quot; agora é vinculado ao valor de eVar 6 de &quot;pesquisa interna:camiseta de verão&quot;. O produto anterior &quot;waffle beanie&quot; ainda está vinculado a um valor de eVar 6 de &quot;pesquisa interna:waffle beanie&quot;.
6. O usuário adiciona o produto ao carrinho, acionando o evento `Cart Add`.
7. O usuário faz check-out de ambos os produtos.

Nos relatórios, os pedidos, a receita, as visualizações do produto e as adições ao carrinho são reportáveis em relação ao eVar6 e se alinham à atividade do produto vinculado.

| eVar 6 (método de descoberta de produtos) | Receita | pedidos | visualizações de produto | adições ao carrinho |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| pesquisa interna:camisa de verão | 19,99 | 1 | 1 | 1 |
| pesquisa interna:chapéu de inverno | 12,99 | 1 | 1 | 1 |

Para saber mais sobre como usar a sintaxe da variável de conversão, leia a documentação do Adobe Analytics em [implementação de eVars usando a sintaxe da variável de conversão](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-conversion-variable-syntax).

Os campos XDM são exibidos abaixo para produzir a sintaxe da variável de conversão no conjunto de dados [!DNL Analytics]:

#### eVars

```console
_experience.analytics.customDimensions.evars.evar#
```

* `evar#`: a variável de eVar específica que você está acessando.

#### Produto

```console
productListItems[#].sku
```

* `#`: o índice da matriz que você está acessando.

## Casos de uso de variável de conversão {#conversion-variable-use-cases}

Os casos de uso abaixo refletem cenários que exigem sintaxe de variável de conversão.

### Vincular o valor ao produto específico e ao par de eventos

A consulta abaixo vincula o valor ao produto específico e ao par de eventos. Neste exemplo, o valor é vinculado ao evento de visualização do produto.

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

### Manter o valor vinculado às ocorrências subsequentes do respectivo produto

O exemplo de consulta abaixo persiste o valor vinculado às ocorrências subsequentes do respectivo produto. A subconsulta mais baixa estabelece a relação do valor com o produto no evento compulsório declarado. A próxima subconsulta executa a atribuição desse valor vinculado em interações subsequentes com o respectivo produto. A opção SELECT de nível superior agrega os resultados para produzir os relatórios.

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

## Próximas etapas

Ao ler este documento, você deve entender melhor como retornar um eVar de merchandising usando a sintaxe do produto e vincular um valor a um produto específico com a sintaxe da variável de conversão.

Se ainda não tiver feito isso, você deverá ler a seguir a [documentação de insights do Analytics para interações da Web e móveis](./analytics-insights.md). Ele fornece casos de uso comuns e demonstra como usar o Serviço de consulta para criar insights acionáveis de dados da Web e do Adobe Analytics móvel.
