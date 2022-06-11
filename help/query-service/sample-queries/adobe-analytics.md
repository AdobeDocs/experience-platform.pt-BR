---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, consultas de amostra, consulta de amostra, adobe analytics;
solution: Experience Platform
title: Exemplos de consultas para dados do Adobe Analytics
topic-legacy: queries
description: Os dados dos conjuntos de relatórios selecionados do Adobe Analytics são transformados em XDM ExperienceEvents e assimilados no Adobe Experience Platform como conjuntos de dados. Este documento descreve uma série de casos de uso em que o Serviço de query usa esses dados e inclui consultas de amostra projetadas para funcionar com seus conjuntos de dados do Adobe Analytics.
exl-id: 96da3713-c7ab-41b3-9a9d-397756d9dd07
source-git-commit: e0cdfc514a9e1277134d4c0d5396fc0bdf9d9958
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 1%

---

# Exemplos de consultas para dados do Adobe Analytics

Os dados dos conjuntos de relatórios selecionados do Adobe Analytics são transformados em dados conformes ao [!DNL XDM ExperienceEvent] e assimiladas no Adobe Experience Platform como conjuntos de dados.

Este documento descreve vários casos de uso em que o Adobe Experience Platform [!DNL Query Service] usam esses dados. Consulte a documentação em [Mapeamento de campo do Analytics](../../sources/connectors/adobe-applications/mapping/analytics.md) para obter mais informações sobre mapeamento para [!DNL Experience Events].

Consulte a [documentação do caso de uso do analytics](../use-cases/analytics-insights.md) para saber como usar o Serviço de query para criar insights acionáveis a partir de dados assimilados do Adobe Analytics.

## Desduplicação

[!DNL Query Service] O suporta desduplicação de dados. Consulte a [Desduplicação de dados em [!DNL Query Service] documentação](../best-practices/deduplication.md) para obter informações sobre como gerar novos valores no momento do query [!DNL Experience Event] conjuntos de dados.

## Variáveis de merchandising (sintaxe do produto)

As seções a seguir fornecem campos XDM e consultas de amostra que você pode usar para acessar as variáveis de merchandising em seu [!DNL Analytics] conjunto de dados.

### Sintaxe do produto

No Adobe Analytics, os dados personalizados a nível de produto podem ser coletados por meio de variáveis configuradas especialmente chamadas variáveis de merchandising. Elas se baseiam em um eVar ou em eventos personalizados. A diferença entre essas variáveis e seu uso típico é que elas representam um valor separado para cada produto encontrado na ocorrência, em vez de apenas um valor único para a ocorrência.

Essas variáveis são chamadas de variáveis de merchandising de sintaxe de produto. Isso permite a coleta de informações, como um &quot;valor de desconto&quot; por produto ou informações sobre o &quot;local na página&quot; do produto nos resultados de pesquisa do cliente.

Para saber mais sobre o uso da sintaxe do produto, leia a documentação do Adobe Analytics em [implementação de eVars usando sintaxe de produto](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-product-syntax).

As seções abaixo destacam os campos XDM necessários para acessar as variáveis de comercialização em seu [!DNL Analytics] conjunto de dados:

#### eVars

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

- `#`: O índice da matriz que você está acessando.
- `evar#`: A variável de eVar específica que você está acessando.

#### Eventos personalizados

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

- `#`: O índice da matriz que você está acessando.
- `event#`: A variável de evento personalizada específica que você está acessando.

#### Exemplos de consultas

Esta é uma consulta de amostra que retorna um eVar de merchandising e um evento para o primeiro produto encontrado no `productListItems`.

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

Essa próxima query explora a variável `productListItems` e retorna cada eVar de merchandising e evento por produto. O `_id` é incluído para mostrar a relação com a ocorrência original. O `_id` é uma chave primária exclusiva para o conjunto de dados.

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
> Se você tentar recuperar um campo que não existe em seu conjunto de dados atual, o erro &quot;Nenhum campo de estrutura semelhante&quot; ocorrerá. Avalie o motivo retornado na mensagem de erro para identificar um campo disponível, atualize sua query e execute novamente.
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### Sintaxe de conversão

Outro tipo de variável de merchandising encontrada no Adobe Analytics é a sintaxe de conversão. Com a sintaxe do produto, o valor é coletado ao mesmo tempo que o produto, mas isso requer que os dados estejam presentes na mesma página. Há cenários em que os dados ocorrem em uma página antes da conversão ou do evento de interesse relacionado ao produto. Por exemplo, considere o caso de uso do método de descoberta de produto.

1. Um usuário realiza uma pesquisa interna por &quot;chapéu de inverno&quot;, que define o eVar 6 da Sintaxe de conversão habilitada para Merchandising como &quot;pesquisa interna:chapéu de inverno&quot;
2. O usuário clica em &quot;waffle beanie&quot; e chega à página de detalhes do produto.\
   a. Aterrissando aqui dispara uma `Product View` evento para &quot;waffle beanie&quot; por US$ 12,99.\
   b. Since `Product View` for configurado como um evento compulsório, o produto &quot;waffle beanie&quot; agora é vinculado ao valor de eVar6 de &quot;pesquisa interna:chapéu de inverno&quot;. Sempre que o produto &quot;waffle beanie&quot; for coletado, ele será associado a &quot;pesquisa interna:chapéu de inverno&quot; até que (1) a configuração de expiração seja alcançada ou (2) um novo valor de eVar6 seja definido e o evento de vinculação ocorra novamente com esse produto.
3. O usuário adiciona o produto ao carrinho, acionando o `Cart Add` evento.
4. O usuário realiza outra pesquisa interna por &quot;camisa de verão&quot;, que define o eVar 6 da Sintaxe de conversão habilitada para Merchandising como &quot;pesquisa interna:camisa de verão&quot;
5. O usuário clica em &quot;t-shirt do esporte&quot; e chega à página de detalhes do produto.\
   a. Aterrissando aqui dispara uma `Product View` evento para &quot;camiseta esportiva por US$ 19,99.\
   b. O `Product View` O evento ainda é nosso evento compulsório, então agora o produto &quot;camiseta esportiva&quot; está vinculado ao valor de eVar6 de &quot;pesquisa interna: camisa de verão&quot; e o produto anterior &quot;waffle beanie&quot; ainda está vinculado a um valor de eVar6 de &quot;pesquisa interna:waffle beanie&quot;.
6. O usuário adiciona o produto ao carrinho, acionando o `Cart Add` evento.
7. O usuário faz o check-out com ambos os produtos.

Nos relatórios, os pedidos, a receita, as visualizações de produtos e as inclusões no carrinho serão relatáveis em relação ao eVar6 e serão alinhadas à atividade do produto vinculado.

| eVar6 (método de descoberta do produto) | Receita | ordens | exibições de produto | adições ao carrinho |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| pesquisa interna:camisa de verão | 19,99 | 1 | 1 | 1 |
| pesquisa interna:chapéu de inverno | 12,99 | 1 | 1 | 1 |

Para saber mais sobre o uso da sintaxe de conversão, leia a documentação do Adobe Analytics em [implementação de eVars usando sintaxe de conversão](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-conversion-variable-syntax).

Estes são os campos XDM para produzir a sintaxe de conversão em [!DNL Analytics] conjunto de dados:

#### eVars

```console
_experience.analytics.customDimensions.evars.evar#
```

- `evar#`: A variável de eVar específica que você está acessando.

#### Produto

```console
productListItems[#].sku
```

- `#`: O índice da matriz que você está acessando.

#### Exemplos de consultas

Aqui está uma consulta de amostra que vincula o valor ao par de produto e evento específico, neste caso o evento de exibição de produto.

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

Aqui está uma consulta de amostra que persiste o valor vinculado às ocorrências subsequentes do respectivo produto. O subquery mais baixo estabelece a relação de valores com o produto no evento de vínculo declarado. O próximo subquery executa a atribuição desse valor vinculado em interações subsequentes com o respectivo produto. E a seleção de nível superior agrega os resultados para produzir o relatório.

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
