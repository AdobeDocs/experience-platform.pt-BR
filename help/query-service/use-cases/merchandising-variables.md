---
title: Retornar e usar variáveis de merchandising a partir de dados de análise
description: Saiba como fornecer campos XDM e consultas de amostra para acessar as variáveis de comercialização em seus conjuntos de dados do Analytics.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 4%

---

# Retornar e usar variáveis de merchandising a partir de dados de análise

Use o Serviço de query para gerenciar os dados assimilados do Adobe Analytics no Adobe Experience Platform como conjuntos de dados. As seções a seguir fornecem consultas de exemplo que podem ser usadas para acessar as variáveis de merchandising em seus conjuntos de dados do Analytics. Consulte a documentação para obter mais informações sobre [como assimilar e mapear dados do Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/analytics.html?lang=pt-BR) por meio da fonte do Analytics

## Variáveis de merchandising {#merchandising-variables}

As variáveis de merchandising podem seguir uma das duas sintaxes:

* **Sintaxe do produto**: Associa o valor do eVar a um produto. 
* **Sintaxe de variável de conversão**: Associa o eVar a um produto somente se um evento compulsório ocorrer. Você pode selecionar os eventos que atuam como eventos de vinculação.

## Sintaxe do produto {#product-syntax}

No Adobe Analytics, os dados personalizados a nível de produto podem ser coletados por meio de variáveis configuradas especialmente chamadas variáveis de merchandising. Elas se baseiam em um eVar ou em eventos personalizados. A diferença entre essas variáveis e seu uso típico é que elas representam um valor separado para cada produto encontrado na ocorrência, em vez de apenas um valor único para a ocorrência.

Essas variáveis são chamadas de variáveis de merchandising de sintaxe de produto. Isso permite a coleta de informações, como um &quot;valor de desconto&quot; por produto ou informações sobre o &quot;local na página&quot; do produto nos resultados de pesquisa do cliente.

Para saber mais sobre o uso da sintaxe do produto, leia a documentação do Adobe Analytics em [implementação de eVars usando sintaxe de produto](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-product-syntax).

As seções abaixo destacam os campos XDM necessários para acessar as variáveis de comercialização em seu [!DNL Analytics] conjunto de dados:

### eVars

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

* `#`: O índice da matriz que você está acessando.
* `evar#`: A variável de eVar específica que você está acessando.

### Eventos personalizados

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

* `#`: O índice da matriz que você está acessando.
* `event#`: A variável de evento personalizada específica que você está acessando.

## Casos de uso da sintaxe do produto {#product-use-cases}

Os seguintes casos de uso têm como foco a devolução de um eVar de merchandising do `productListItems` usando SQL.

### Retornar um eVar e evento de comercialização

A query abaixo retorna um eVar de merchandising e um evento para o primeiro produto encontrado no `productListItems` matriz.

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

### Explore a matriz productListItems e retorne o eVar de merchandising e o evento de cada produto.

Essa próxima query explora a variável `productListItems` e retorna cada eVar de merchandising e evento por produto. O `_id` é incluído para mostrar a relação com a ocorrência original. O `_id` é uma chave primária exclusiva para o conjunto de dados.

>[!NOTE]
>
>A função explode separa os elementos de uma matriz em várias linhas. Exclui valores nulos.

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
> Se você tentar recuperar um campo que não existe em seu conjunto de dados atual, ocorrerá o erro &quot;Nenhum campo de struct semelhante&quot;. Avalie o motivo retornado na mensagem de erro para identificar um campo disponível, atualize sua query e execute-a novamente.
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### Sintaxe da variável de conversão {#conversion-variable-syntax}

Outro tipo de variável de merchandising encontrada no Adobe Analytics é a sintaxe de variável de conversão. A sintaxe da variável de conversão é usada quando o valor do eVar não está disponível para ser definido na variável products . Normalmente, significa que sua página não tem o contexto do canal de merchandising ou do método de descoberta. Nesses casos, você deve definir a variável de merchandising antes que o usuário chegue à página do produto e o valor persiste até que o evento compulsório ocorra.

Por exemplo, o cenário de descoberta de produto abaixo ilustra como os dados necessários podem estar presentes em uma página antes da conversão ou evento relacionado ao produto ocorrer.

1. Um usuário realiza uma pesquisa interna por &quot;chapéu de inverno&quot; que define o eVar6 de merchandising com sintaxe de conversão ativada como &quot;pesquisa interna:chapéu de inverno&quot;.
2. O usuário clica em &quot;waffle beanie&quot; e chega à página de detalhes do produto.\
   a. Aterrissando aqui dispara uma `Product View` evento para &quot;waffle beanie&quot; por US$ 12,99.\
   b. Since `Product View` for configurado como um evento compulsório, o produto &quot;waffle beanie&quot; agora é vinculado ao valor de eVar6 de &quot;pesquisa interna:chapéu de inverno&quot;. Sempre que o produto &quot;waffle beanie&quot; é coletado, ele é associado a &quot;pesquisa interna:chapéu de inverno&quot;. Isso acontece até que a configuração de expiração do eVar seja atingida ou que um novo valor de eVar6 seja definido e o evento de vinculação ocorra com esse produto novamente.
3. O usuário adiciona o produto ao carrinho, acionando o `Cart Add` evento.
4. O usuário realiza outra pesquisa interna por &quot;camisa de verão&quot;, que define o eVar de merchandising habilitado para a sintaxe de conversão como &quot;pesquisa interna: camisa de verão&quot;.
5. O usuário seleciona &quot;t-shirt do esportivo&quot; e chega à página de detalhes do produto.\
   a. Aterrissando aqui dispara uma `Product View` evento para &quot;camiseta esportiva por US$ 19,99.\
   b. Como `Product View` for o evento compulsório, a &quot;camiseta do esportivo&quot; do produto agora é vinculada ao valor de eVar6 de &quot;pesquisa interna: camiseta de verão&quot;. O produto anterior &quot;waffle beanie&quot; ainda está vinculado a um valor de eVar6 de &quot;pesquisa interna:waffle beanie&quot;.
6. O usuário adiciona o produto ao carrinho, acionando o `Cart Add` evento.
7. O usuário faz o check-out com ambos os produtos.

Nos relatórios, os pedidos, a receita, as visualizações de produtos e as adições ao carrinho são relatáveis em relação ao eVar6 e estão alinhadas à atividade do produto vinculado.

| eVar6 (método de descoberta do produto) | Receita | ordens | exibições de produto | adições ao carrinho |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| pesquisa interna:camisa de verão | 19,99 | 1 | 1 | 1 |
| pesquisa interna:chapéu de inverno | 12.99 | 1 | 1 | 1 |

Para saber mais sobre o uso da sintaxe da variável de conversão, leia a documentação do Adobe Analytics em [implementação de eVars usando a sintaxe da variável de conversão](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-conversion-variable-syntax).

Os campos XDM são exibidos abaixo para produzir a sintaxe da variável de conversão em [!DNL Analytics] conjunto de dados:

#### eVars

```console
_experience.analytics.customDimensions.evars.evar#
```

* `evar#`: A variável de eVar específica que você está acessando.

#### Produto

```console
productListItems[#].sku
```

* `#`: O índice da matriz que você está acessando.

## Casos de uso da variável de conversão {#conversion-variable-use-cases}

Os casos de uso abaixo refletem cenários que exigem a sintaxe da variável de conversão.

### Vincule o valor ao par de produto e evento específico

A query abaixo vincula o valor ao produto específico e ao par de eventos. Neste exemplo, o valor está vinculado ao evento de exibição de produto.

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

A consulta de amostra abaixo persiste o valor vinculado às ocorrências subsequentes do respectivo produto. O subquery mais baixo estabelece a relação do valor com o produto no evento de vínculo declarado. O próximo subquery executa a atribuição desse valor vinculado em interações subsequentes com o respectivo produto. O SELECT de nível superior agrega os resultados para produzir o relatório.

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

Ao ler este documento, você deve ter uma melhor compreensão de como retornar um eVar de merchandising usando a sintaxe do produto e vincular um valor a um produto específico com a sintaxe da variável de conversão.

Se ainda não o fez, leia a [Documentação de insights do Analytics para interações da Web e móveis](./analytics-insights.md) em seguida. Ela fornece casos de uso comuns e demonstra como usar o Serviço de query para criar insights acionáveis da Web e dados móveis do Adobe Analytics.
