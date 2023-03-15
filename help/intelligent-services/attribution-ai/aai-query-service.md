---
keywords: insights;ia de atribuição;insights de ia de atribuição;serviço de consulta de AAI;consultas de atribuição;pontuações de atribuição
feature: Attribution AI
title: Análise de pontuações de atribuição usando o serviço de consulta
description: Saiba como usar o Serviço de consulta do Adobe Experience Platform para analisar pontuações do Attribution AI.
exl-id: 35d7f6f2-a118-4093-8dbc-cb020ec35e90
source-git-commit: 66d20dc1141ff33211635ba74d320350f8b27fb7
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# Análise de pontuações de atribuição usando o Serviço de consulta

Cada linha nos dados representa uma conversão, em que as informações de pontos de contato relacionados são armazenadas como uma matriz de structs no `touchpointsDetail` coluna.

| Informações do ponto de contato | Coluna |
| ---------------------- | ------ |
| Nome do ponto de contato | `touchpointsDetail. touchpointName` |
| Canal de ponto de contato | `touchpointsDetail.touchPoint.mediaChannel` |
| Pontuações Attribution AI do ponto de contato | <li>`touchpointsDetail.scores.algorithmicSourced`</li> <li> `touchpointsDetail.scores.algorithmicInfluenced` </li> |

## Encontrar seus caminhos de dados

Na interface do Adobe Experience Platform, selecione **[!UICONTROL Conjuntos de dados]** no painel de navegação esquerdo. A variável **[!UICONTROL Conjuntos de dados]** é exibida. Em seguida, selecione o **[!UICONTROL Procurar]** e localize o conjunto de dados de saída para suas pontuações do Attribution AI.

![Acesso ao seu modelo](./images/aai-query/datasets_browse.png)

Selecione o conjunto de dados de saída. A página de atividade do conjunto de dados é exibida.

![página de atividade do conjunto de dados](./images/aai-query/select_preview.png)

Na página de atividade do conjunto de dados, selecione **[!UICONTROL Visualizar conjunto de dados]** no canto superior direito para visualizar seus dados e verificar se foram assimilados conforme esperado.

![visualizar conjunto de dados](./images/aai-query/preview_dataset.JPG)

Depois de visualizar os dados, selecione o esquema no painel direito. Um popover é exibido com o nome e a descrição do esquema. Selecione o hiperlink do nome do esquema para redirecionar para o esquema de pontuação.

![selecionar o esquema](./images/aai-query/select_schema.png)

Usando o esquema de pontuação, você pode selecionar ou pesquisar um valor. Uma vez selecionado, o **[!UICONTROL Propriedades do campo]** as aberturas do painel lateral permitem copiar o caminho para uso na criação de consultas.

![copiar o caminho](./images/aai-query/copy_path.png)

## Serviço de consulta do Access

Para acessar o Serviço de consulta na interface do Platform, comece selecionando **[!UICONTROL Consultas]** na navegação à esquerda, selecione o **[!UICONTROL Procurar]** guia. Uma lista de consultas salvas anteriormente é carregada.

![procurar serviço de consulta](./images/aai-query/query_tab.png)

Em seguida, selecione **[!UICONTROL Criar consulta]** no canto superior direito. O Editor de consultas é carregado. Usando o Editor de consultas, você pode começar a criar consultas usando seus dados de pontuação.

![editor de consulta](./images/aai-query/query_example.png)

Para obter mais informações sobre o Editor de consultas, visite a [Guia do usuário do Editor de consultas](../../query-service/ui/user-guide.md).

## Modelos de consulta para análise de pontuação de atribuição

As consultas abaixo podem ser usadas como modelo para diferentes cenários de análise de pontuação. É necessário substituir o `_tenantId` e `your_score_output_dataset` com os valores adequados encontrados no esquema de saída de pontuação.

>[!NOTE]
>
> Dependendo de como seus dados foram assimilados, os valores usados abaixo, como `timestamp` O pode estar em um formato diferente.

### Exemplos de validação

**Número total de conversões por evento de conversão (em uma janela de conversão)**

```sql
    SELECT conversionName,
           SUM(scores.firstTouch) as total_conversions,
           SUM(scores.algorithmicSourced) as total_attributed_conversions
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName
                    as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16'
      AND
        conversion_timestamp <  '2020-10-14'
    GROUP BY
        conversionName
```

**Número total de eventos somente de conversão (em uma janela de conversão)**

```sql
    SELECT
        _tenantId.your_score_output_dataset.conversionName as conversionName,
        COUNT(1) as convOnly_cnt
    FROM
        your_score_output_dataset
    WHERE
        _tenantId.your_score_output_dataset.touchpointsDetail.touchpointName[0] IS NULL AND
        timestamp >= '2020-07-16' AND
        timestamp <  '2020-10-14'
    GROUP BY
        conversionName
```

### Exemplo de análise de tendência

**Número de conversões por dia**

```sql
    SELECT conversionName,
           DATE(conversion_timestamp) as conversion_date,
           SUM(scores.firstTouch) as convertion_cnt
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    GROUP BY
        conversionName, DATE(conversion_timestamp)
    ORDER BY
        conversionName, DATE(conversion_timestamp)
    LIMIT 20
```

### Exemplo de análise de distribuição

**Quantidade de pontos de contato em caminhos de conversão por tipo definido (em uma janela de conversão)**

```sql
    SELECT conversionName,
           touchpointName,
           COUNT(1) as tp_count
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14' AND
        touchpointName IS NOT NULL
    GROUP BY
        conversionName, touchpointName
    ORDER BY
        conversionName, tp_count DESC
```

### Exemplos de geração de insights

**Detalhamento de unidades incrementais por ponto de contato e data de conversão (em uma janela de conversão)**

```sql
    SELECT conversionName,
           touchpointName,
           DATE(conversion_timestamp) as conversion_date,
           SUM(scores.algorithmicSourced) as incremental_units
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14'  AND
        touchpointName IS NOT NULL
    GROUP BY
        conversionName, touchpointName, DATE(conversion_timestamp)
    ORDER BY
        conversionName, touchpointName, DATE(conversion_timestamp)
```

**Detalhamento de unidades incrementais por ponto de contato e data de ponto de contato (em uma janela de conversão)**

```sql
    SELECT conversionName,
           touchpointName,
           DATE(touchpoint.timestamp) as touchpoint_date,
           SUM(scores.algorithmicSourced) as incremental_units
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14'  AND
        touchpointName IS NOT NULL
    GROUP BY
        conversionName, touchpointName, DATE(touchpoint.timestamp)
    ORDER BY
        conversionName, touchpointName, DATE(touchpoint.timestamp)
    LIMIT 20
```

**Pontuações agregadas para um determinado tipo de ponto de contato para todos os modelos de pontuação (em uma janela de conversão)**

```sql
    SELECT
           conversionName,
           touchpointName,
           SUM(scores.algorithmicSourced) as total_incremental_units,
           SUM(scores.algorithmicInfluenced) as total_influenced_units,
           SUM(scores.uShape) as total_uShape_units,
           SUM(scores.decayUnits) as total_decay_units,
           SUM(scores.linear) as total_linear_units,
           SUM(scores.lastTouch) as total_lastTouch_units,
           SUM(scores.firstTouch) as total_firstTouch_units
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14'  AND
        touchpointName = 'display'
    GROUP BY
        conversionName, touchpointName
    ORDER BY
        conversionName, touchpointName
```

**Avançado - análise de comprimento de caminho**

Obtenha uma distribuição de comprimento de caminho para cada tipo de evento de conversão:

```sql
    WITH agg_path AS (
          SELECT
            _tenantId.your_score_output_dataset.conversionName as conversionName,
            sum(size(_tenantId.your_score_output_dataset.touchpointsDetail)) as path_length
          FROM
            your_score_output_dataset
          WHERE
            _tenantId.your_score_output_dataset.touchpointsDetail.touchpointName[0] IS NOT NULL AND
            timestamp >= '2020-07-16' AND
            timestamp <  '2020-10-14'
          GROUP BY
            _tenantId.your_score_output_dataset.conversionName,
            eventMergeId
    )
    SELECT
        conversionName,
        path_length,
        count(1) as conversionPath_count
    FROM
        agg_path
    GROUP BY
        conversionName, path_length
    ORDER BY
        conversionName, path_length
```

**Avançado - número distinto de pontos de contato na análise de caminhos de conversão**

Obtenha a distribuição para o número de pontos de contato distintos em um caminho de conversão para cada tipo de evento de conversão:

```sql
    WITH agg_path AS (
      SELECT
        _tenantId.your_score_output_dataset.conversionName as conversionName,
        size(array_distinct(flatten(collect_list(_tenantId.your_score_output_dataset.touchpointsDetail.touchpointName)))) as num_dist_tp
      FROM
        your_score_output_dataset
      WHERE
        _tenantId.your_score_output_dataset.touchpointsDetail.touchpointName[0] IS NOT NULL AND
        timestamp >= '2020-07-16' AND
        timestamp <  '2020-10-14'
      GROUP BY
        _tenantId.your_score_output_dataset.conversionName,
        eventMergeId
    )
    SELECT
        conversionName,
        num_dist_tp,
        count(1) as conversionPath_count
    FROM
     agg_path
    GROUP BY
        conversionName, num_dist_tp
    ORDER BY
        conversionName, num_dist_tp
```

### Exemplo de achatamento e explosão de esquema

Essa consulta nivela a coluna struct em várias colunas singulares e explode matrizes em várias linhas. Isso ajuda a transformar as pontuações de atribuição em um formato CSV. A saída dessa consulta tem uma conversão e um dos pontos de contato correspondentes a essa conversão em cada linha.

>[!TIP]
>
> Neste exemplo, você precisa substituir `{COLUMN_NAME}` além de `_tenantId` e `your_score_output_dataset`. A variável `COLUMN_NAME` pode receber os valores de nomes opcionais de colunas de passagem (colunas de relatórios) que foram adicionados durante a configuração do seu modelo de Attribution AI. Revise seu esquema de saída de pontuação para encontrar o `{COLUMN_NAME}` valores necessários para concluir esta consulta.

```sql
SELECT 
  segmentation,
  conversionName,
  scoreCreatedTime,
  aaid, _id, eventMergeId,
  conversion.eventType as conversion_eventType,
  conversion.quantity as conversion_quantity,
  conversion.eventSource as conversion_eventSource,
  conversion.priceTotal as conversion_priceTotal,
  conversion.timestamp as conversion_timestamp,
  conversion.geo as conversion_geo,
  conversion.receivedTimestamp as conversion_receivedTimestamp,
  conversion.dataSource as conversion_dataSource,
  conversion.productType as conversion_productType,
  conversion.passThrough.{COLUMN_NAME} as conversion_passThru_column,
  conversion.skuId as conversion_skuId,
  conversion.product as conversion_product,
  touchpointName,
  touchPoint.campaignGroup as tp_campaignGroup, 
  touchPoint.mediaType as tp_mediaType,
  touchPoint.campaignTag as tp_campaignTag,
  touchPoint.timestamp as tp_timestamp,
  touchPoint.geo as tp_geo,
  touchPoint.receivedTimestamp as tp_receivedTimestamp,
  touchPoint.passThrough.{COLUMN_NAME} as tp_passThru_column,
  touchPoint.campaignName as tp_campaignName,
  touchPoint.mediaAction as tp_mediaAction,
  touchPoint.mediaChannel as tp_mediaChannel,
  touchPoint.eventid as tp_eventid,
  scores.*
FROM (
  SELECT
        _tenantId.your_score_output_dataset.segmentation,
        _tenantId.your_score_output_dataset.conversionName,
        _tenantId.your_score_output_dataset.scoreCreatedTime,
        _tenantId.your_score_output_dataset.conversion,
        _id,
        eventMergeId,
        map_values(identityMap)[0][0].id as aaid,
        inline(_tenantId.your_score_output_dataset.touchpointsDetail)
  FROM
        your_score_output_dataset
)
```
