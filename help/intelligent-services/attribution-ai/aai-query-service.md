---
keywords: insights;attribution ai;attribution ai insights;AAI query service;attribution queries;attribution scores
solution: Intelligent Services, Experience Platform
title: Guia de start rápido do Serviço de Query AAI
topic: Attribution AI queries
description: Este documento fornece um guia e modelos para usar o Serviço de Query para analisar suas pontuações de atribuição.
translation-type: tm+mt
source-git-commit: 32d49c9244414afeb2729ef44eb364fb2c609380
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 0%

---


# Guia de start rápido do Serviço de Query Adobe Experience Platform para analisar as pontuações de atribuição

Cada linha nos dados representa uma conversão, na qual as informações para pontos de contato relacionados são armazenadas como uma matriz de estruturas na coluna `touchpointsDetail`.

| Informações do ponto de contato | Coluna |
| ---------------------- | ------ |
| Nome do ponto de contato | `touchpointsDetail. touchpointName` |
| Canal de ponto de contato | `touchpointsDetail.touchPoint.mediaChannel` |
| Pontuações algorítmicas AAI de ponto de contato | <li>`touchpointsDetail.scores.algorithmicSourced`</li> <li> `touchpointsDetail.scores.algorithmicInfluenced` </li> |

## Como localizar seus caminhos de dados

Na interface do usuário do Adobe Experience Platform, selecione **[!UICONTROL Conjuntos de dados]** na navegação à esquerda. A página **[!UICONTROL Conjuntos de Dados]** é exibida. Em seguida, selecione a guia **[!UICONTROL Procurar]** e localize o conjunto de dados de saída para suas pontuações de Attribution AI.

![Acessar sua instância](./images/aai-query/datasets_browse.png)

Selecione seu conjunto de dados de saída. A página atividade do conjunto de dados é exibida.

![página atividade do conjunto de dados](./images/aai-query/select_preview.png)

Na página atividade do conjunto de dados, selecione **[!UICONTROL conjunto de dados de Pré-visualização]** no canto superior direito para pré-visualização dos dados e verificar se eles foram assimilados conforme esperado.

![Conjunto de dados de pré-visualização](./images/aai-query/preview_dataset.JPG)

Depois de visualizar seus dados, selecione o schema no painel direito. Um schema é exibido com o nome e a descrição do mesmo. Selecione o hiperlink do nome do schema para redirecionar para o schema de pontuação.

![selecione o schema](./images/aai-query/select_schema.png)

Usando o schema de pontuação, você pode selecionar ou procurar um valor. Depois de selecionado, o painel lateral **[!UICONTROL Propriedades do campo]** é aberto, permitindo que você copie o caminho para uso na criação de query.

![copiar o caminho](./images/aai-query/copy_path.png)

## Serviço de Query de acesso

Para acessar o Serviço de Query na interface do usuário da plataforma, selecione **[!UICONTROL Query]** no painel de navegação esquerdo e selecione a guia **[!UICONTROL Procurar]**. Uma lista dos query salvos anteriormente é carregada.

![Navegação pelo serviço de query](./images/aai-query/query_tab.png)

Em seguida, selecione **[!UICONTROL Criar query]** no canto superior direito. O Editor de Query é carregado. Usando o Editor de Query, você pode começar a criar query usando seus dados de pontuação.

![editor de query](./images/aai-query/query_example.png)

Para obter mais informações sobre o Editor de Query, visite o [guia do usuário do Editor de Query](../../query-service/ui/user-guide.md).

## Modelos de query para análise de pontuação de atribuição

Os query abaixo podem ser usados como modelo para diferentes cenários de análise de pontuação. É necessário substituir `_tenantId` e `your_score_output_dataset` pelos valores corretos encontrados no schema de saída de pontuação.

>[!NOTE]
>
> Dependendo de como seus dados foram ingeridos, os valores usados abaixo, como `timestamp`, podem estar em um formato diferente.

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

**Número total de eventos somente conversão (em uma janela de conversão)**

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

### Exemplos de análise de tendência

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

### Exemplos de análise de distribuição

**Quantidade de pontos de contato nos caminhos de conversão por tipo definido (em uma janela de conversão)**

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

### Exemplos de geração de insight

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

**Detalhamento de unidades incrementais por data de ponto de contato e ponto de contato (em uma janela de conversão)**

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

**Avançado - análise de comprimento do caminho**

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

Obtenha a distribuição do número de pontos de contato distintos em um caminho de conversão para cada tipo de evento de conversão:

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
