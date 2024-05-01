---
title: Insights de destinos
description: Descubra o SQL que capacita seus insights de destino e use essas consultas para gerar insights personalizados e explorar ainda mais a ativação de dados do Adobe Experience Platform.
exl-id: 762a9960-e7a5-4796-80c7-ef745157cc04
source-git-commit: d4baf6cfaa772e5d46cef470fb35818c7af868b1
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 2%

---

# Insights de destinos

Os insights derivados da análise do modelo de dados tornam os dados do Adobe Real-time Customer Data Platform mais acessíveis, compreensíveis e impactantes para a tomada de decisões.

Entenda seus insights de destino acessando o SQL que os capacita e gere seus próprios insights para explorar ainda mais a ativação de dados do Adobe Experience Platform para suas plataformas de destino. Transforme seus dados brutos em novos insights acionáveis usando o SQL modelo de dados do Real-Time CDP existente como inspiração para criar consultas para suas necessidades comerciais exclusivas.

Consulte a [Exibir documentação SQL](../view-sql.md) para obter mais informações sobre como adaptar o SQL dos seus insights diretamente pela interface do Platform.

Os seguintes insights estão disponíveis para você usar como parte da [Painel de destinos](../guides/destinations.md) ou um personalizado [painel definido pelo usuário](../user-defined-dashboards.md). Consulte a [visão geral da personalização](../customize/overview.md) para obter instruções sobre como personalizar seu painel ou [criar e editar novos widgets](../customize/custom-widgets.md) na biblioteca de widgets e [painel definido pelo usuário](../user-defined-dashboards.md#create-widget).

## Públicos ativados {#activated-audiences}

Perguntas respondidas por este insight:

- Qual é a contagem total de públicos ativados filtrados por um destino específico?
- Qual é a contagem de público ativada por destino?

+++Selecione para revelar o SQL que gera esse insight

```sql
SELECT
  COUNT(segment_id) AS Activated_Audiences_Count
FROM
  qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE
  (
    SELECT
      MAX(process_date)
    FROM
      qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE
      process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
  ) BETWEEN start_date AND end_date
  AND destination_id = 1458738325;
```

+++

Consulte a [Documentação do widget Públicos ativados](../guides/destinations.md#activated-audiences) para obter informações sobre a aparência e a funcionalidade desse insight.

## Públicos ativados em todos os destinos {#activated-audiences-across-all-destinations}

Perguntas respondidas por este insight:

- Quantos públicos-alvo são ativados em todos os destinos?
- Qual é a contagem total de públicos ativados?

+++Selecione para revelar o SQL que gera esse insight

```sql
SELECT count(segment_id) AS Activated_Audiences_Count
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE
    (SELECT MAX(process_date)
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL' ) BETWEEN start_date AND end_date;
```

+++

Consulte a [Documentação do widget Públicos ativados em todos os destinos](../guides/destinations.md#activated-audiences-across-all-destinations) para obter informações sobre a aparência e a funcionalidade desse insight.

## Destinos ativos por plataforma de destino {#active-destinations-by-destination-platform}

Perguntas respondidas por este insight:

- Quantos destinos estão ativos?
- Qual é o detalhamento de destinos ativos por plataforma de destino?
- Qual é a contagem de destinos ativos dividida por plataforma de destino?

+++Selecione para revelar o SQL que gera esse insight

```sql
SELECT destination_platform_name AS Destination_Platform_Name,
       COUNT(destination_id) AS Active_Destinations_Count
  FROM qsaccel.profile_agg.adwh_dim_destination a
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination_platform b ON a.destination_platform_id = b.destination_platform_id
  WHERE destination_status='enabled'
  GROUP BY destination_platform_name
  ORDER BY Active_Destinations_Count DESC
  LIMIT 20;
```

+++

Consulte a [Documentação do widget Destinos ativos por plataforma de destino](../guides/destinations.md#active-destinations-by-destination-platform) para obter informações sobre a aparência e a funcionalidade desse insight.

## Tendência de tamanho do público-alvo {#audience-size-trend}

Perguntas respondidas por este insight:

- Como o tamanho do público mudou com o tempo, incluindo anomalias para um público mapeado para um destino?
- Como descobrir a tendência geral no tamanho do público-alvo, por destino, durante os períodos especificados de 30 dias, 90 dias e 12 meses?
- Quais são as principais características do público-alvo contribuindo para o tamanho, por exemplo, picos em relação a campanhas de marketing por email?

+++Selecione para revelar o SQL que gera esse insight

```sql
SELECT d.destination_name,
        d.destination,
        d.destination_id,
        b.segment_name,
        b.segment,
        c.segment_id,
        a.date_key,
        sum(a.count_of_profiles) AS profile_count
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations c ON a.segment_id = c.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination d ON c.destination_id = d.destination_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) f ON a.merge_policy_id = f.merge_policy_id
  WHERE a.date_key >= dateadd(DAY, -30-1, f.last_process_date)
    AND d.destination_id = -1275507046
    AND c.segment_id = -1452100519
  GROUP BY d.destination_name,
          d.destination,
          d.destination_id,
          b.segment_name,
          b.segment,
          c.segment_id,
          a.date_key;
```

+++

Consulte a [Documentação do widget de tendência de tamanho do público](../guides/destinations.md#audience-size-trend) para obter informações sobre a aparência e a funcionalidade desse insight.

## Públicos-alvo comuns {#common-audiences}

Perguntas respondidas por este insight:

- Quais são os públicos-alvo comuns entre dois destinos diferentes?
- Quantos perfis cada um dos públicos-alvo comuns entre dois destinos diferentes tem?
- Qual é o maior público-alvo para o qual dois destinos são mapeados?

+++Selecione para revelar o SQL que gera esse insight

```sql
SELECT k.destination_name1,
       k.destination_1,
       k.destination_id1,
       k.destination_name2,
       k.destination_2,
       k.destination_id2,
       b.segment_name,
       b.segment,
       b.segment_id,
       sum(a.count_of_profiles) AS profile_count
  FROM
    (SELECT i.destination_name AS destination_name1,
            i.destination AS destination_1,
            i.destination_id AS destination_id1,
            j.destination_name AS destination_name2,
            j.destination AS destination_2,
            j.destination_id AS destination_id2,
            i.segment_id
     FROM
       (SELECT b.destination_name,
               b.destination,
               b.destination_id,
               a.segment_id
        FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
        INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id=b.destination_id
        WHERE b.destination_id=1458738325) AS i
     INNER JOIN
       (SELECT b.destination_name,
               b.destination,
               b.destination_id,
               a.segment_id
        FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
        INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id=b.destination_id
        WHERE b.destination_id=-635802802) AS j ON i.segment_id=j.segment_id) AS k
  INNER JOIN qsaccel.profile_agg.adwh_fact_profile_by_segment a ON a.segment_id = k.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON b.segment_id = k.segment_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL'
     GROUP BY merge_policy_id) c ON a.merge_policy_id = c.merge_policy_id
  WHERE a.date_key = c.last_process_date
  GROUP BY k.destination_name1,
           k.destination_1,
           k.destination_id1,
           k.destination_name2,
           k.destination_2,
           k.destination_id2,
           b.segment_name,
           b.segment,
           b.segment_id
  ORDER BY profile_count DESC
  LIMIT 20;
```

+++

Consulte a [Documentação do widget Públicos-alvo comuns](../guides/destinations.md#common-audiences) para obter informações sobre a aparência e a funcionalidade desse insight.

## Status do destino {#destination-status}

Perguntas respondidas por este insight:

- Qual é o número total de destinos habilitados para uso?
- Qual é o número total de destinos que estão desabilitados?
- Qual é a divisão de porcentagem entre destinos habilitados e desabilitados?

+++Selecione para revelar o SQL que gera esse insight

```sql
SELECT COUNT(CASE
                 WHEN destination_status='enabled' THEN 1
             END) AS count_of_active_destinations,
       COUNT(CASE
                 WHEN destination_status='disabled' THEN 1
             END) AS count_of_inactive_destinations
FROM qsaccel.profile_agg.adwh_dim_destination;
```

+++

Consulte a [Documentação do widget de status de destino](../guides/destinations.md#destination-status) para obter informações sobre a aparência e a funcionalidade desse insight.

## Contagem de destinos {#destinations-count}

Perguntas respondidas por este insight:

- Quantos destinos estão configurados no momento?
- Como a contagem total de destinos mudou ao longo do tempo?

+++Selecione para revelar o SQL que gera esse insight

```sql
SELECT count(destination_id) AS total_number_of_destinations
  FROM qsaccel.profile_agg.adwh_dim_destination;
```

+++

Consulte a [Documentação do widget de contagem de destinos](../guides/destinations.md#destinations-count) para obter informações sobre a aparência e a funcionalidade desse insight.

## Integridade do público mapeado {#mapped-audience-health}

Perguntas respondidas por este insight:

- Quais públicos-alvo mapeados para um destino têm variações significativas nos últimos 30 dias?
- Qual é o tamanho mais recente de um público-alvo mapeado e se ele mudou no último mês?
- Como faço para listar todos os públicos mapeados para um destino com base na gravidade de suas alterações de tamanho no último mês?

+++Selecione para revelar o SQL que gera esse insight

```sql
SELECT destination_name,
        SEGMENT,
        segment_id,
        segment_name,
        avg_profile_count,
        latest_profile_count,
        stddev_profile_count,
        profile_count_z_factor
  FROM
    (SELECT b.destination_name,
            f.segment_id,
            c.segment_name,
            c.segment,
            f.avg_profile_count,
            f.latest_profile_count,
            f.stddev_profile_count,
            CASE
                WHEN stddev_profile_count = 0 THEN 0 ELSE(f.latest_profile_count - f.avg_profile_count)/f.stddev_profile_count
            END AS profile_count_z_factor
    FROM
      (SELECT segment_id,
              avg(profile_count) AS avg_profile_count,
              sum(CASE
                      WHEN last_process_date = date_key THEN profile_count
                      ELSE 0
                  END) AS latest_profile_count,
              stdevp(profile_count) AS stddev_profile_count
        FROM
          (SELECT x.date_key,
                  x.segment_id,
                  d.last_process_date,
                  sum(x.count_of_profiles) AS profile_count
          FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
          INNER JOIN
            (SELECT MAX(process_date) last_process_date,
                    merge_policy_id
              FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
              WHERE process_name = 'FACT_TABLES_PROCESSING'
                AND process_status = 'SUCCESSFUL'
              GROUP BY merge_policy_id) d ON x.merge_policy_id = d.merge_policy_id
          WHERE x.date_key >= dateadd (DAY, -30, d.last_process_date)
          GROUP BY x.date_key,
                    x.segment_id,
                    d.last_process_date) AS t
        GROUP BY segment_id) AS f
    INNER JOIN qsaccel.profile_agg.adwh_dim_segments c ON f.segment_id = c.segment_id
    INNER JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations a ON a.segment_id = c.segment_id
    INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id = b.destination_id
    WHERE b.destination_id = 1458738325) AS m
  WHERE abs(m.profile_count_z_factor) >= 1
  ORDER BY m.latest_profile_count DESC
  LIMIT 20;
```

+++

Consulte a [Documentação do widget de integridade do público mapeado](../guides/destinations.md#mapped-audience-health) para obter informações sobre a aparência e a funcionalidade desse insight.

## Públicos mapeados {#mapped-audiences}

Perguntas respondidas por este insight:

- Quantos públicos-alvo são mapeados para um destino específico?
- Como a contagem de públicos mapeados mudou ao longo do tempo?
- Onde posso comparar dois destinos para ver a sobreposição de público mapeada para cada destino?

+++Selecione para revelar o SQL que gera esse insight

```sql
SELECT COUNT(segment_id) AS mapped_audiences_count
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE destination_id = 1458738325;
```

+++

Consulte a [Documentação do widget Públicos mapeados](../guides/destinations.md#mapped-audiences) para obter informações sobre a aparência e a funcionalidade desse insight.

<!-- Commented out until the Jan release as the SQL IS MISSING:
## Mapped audiences by identity {#mapped-audiences-by-identity}

Questions answered by this insight:

- How do I find a list of audiences that are mapped to a destination?
- What is the count of identities for audiences mapped to a destination?
- Which audiences have the highest count of identities mapped to a particular destination?

+++Select to reveal the SQL that generates this insight

```sql
```

+++

See the [Mapped audiences by identity widget documentation](../guides/destinations.md#mapped-audiences-by-identity) for information on the appearance and functionality of this insight.
-->

## Destinos mais usados {#most-used-destinations}

Perguntas respondidas por este insight:

- Quais são os destinos mais usados?
- Quantos públicos-alvo são mapeados para cada destino, classificados da maioria para a menor?
- Como o mapeamento de públicos-alvo para destinos muda de um instantâneo para outro?

+++Selecione para revelar o SQL que gera esse insight

```sql
SELECT qsaccel.profile_agg.adwh_dim_destination.destination_name,
       qsaccel.profile_agg.adwh_dim_destination.destination_id,
       qsaccel.profile_agg.adwh_dim_destination.destination,
       count(DISTINCT qsaccel.profile_agg.adwh_dim_br_segment_destinations.segment_id) segment_count
  FROM qsaccel.profile_agg.adwh_dim_destination
  JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations ON qsaccel.profile_agg.adwh_dim_destination.destination_id = qsaccel.profile_agg.adwh_dim_br_segment_destinations.destination_id
  WHERE qsaccel.profile_agg.adwh_dim_destination.destination_name IS NOT NULL
  GROUP BY qsaccel.profile_agg.adwh_dim_destination.destination_name,
           qsaccel.profile_agg.adwh_dim_destination.destination,
           qsaccel.profile_agg.adwh_dim_destination.destination_id
  ORDER BY segment_count DESC
  LIMIT 20;
```

+++

Consulte a [Documentação do widget de destinos mais usados](../guides/destinations.md#most-used-destinations) para obter informações sobre a aparência e a funcionalidade desse insight.

## Públicos-alvo ativados recentemente {#recently-activated-audiences}

Perguntas respondidas por este insight:

- Para qual destino um público-alvo foi ativado mais recentemente?
- Como faço para encontrar uma lista de todos os destinos classificados pela data da última atualização?
- Como posso comparar dois destinos com base nas ativações mais recentes?

+++Selecione para revelar o SQL que gera esse insight

```sql
SELECT
  segment_name,
  segment,
  destination_name,
  a.create_time create_time
FROM
  qsaccel.profile_agg.adwh_dim_br_segment_destinations a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id = c.destination_id
ORDER BY
  create_time DESC,
  segment
LIMIT
  20;
```

+++

Consulte a [Documentação do widget Públicos ativados recentemente](../guides/destinations.md#recently-activated-audiences) para obter informações sobre a aparência e a funcionalidade desse insight.

## Públicos-alvo ativados recentemente por destino {#recently-activated-audiences-by-destination}

Perguntas respondidas por este insight:

- Quais são os públicos-alvo ativados para um destino específico?
- Como faço para encontrar uma lista de públicos ativada por um público específico da mais para a menos recente?
- Como encontrar uma lista de públicos-alvo pela data em que foi ativada para um destino específico?

+++Selecione para revelar o SQL que gera esse insight

```sql
SELECT c.destination_name,
       c.destination,
       c.destination_id,
       b.segment_name,
       b.segment,
       b.segment_id,
       a.create_time activated
  FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id=b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id=c.destination_id
  WHERE c.destination_id=-1275507046
  ORDER BY a.create_time DESC,
           a.segment_id
  LIMIT 20;
```

+++

Consulte a [Documentação de widgets Públicos ativados recentemente por destino](../guides/destinations.md#recently-activated-audiences-by-destination) para obter informações sobre a aparência e a funcionalidade desse insight.

## Destinos criados recentemente {#recently-created-destinations}

Perguntas respondidas por este insight:

- Quais são os destinos criados mais recentemente?
- Como faço para encontrar uma lista de destinos com a data em que foram criados?
- Que novo destino foi criado recentemente?

+++Selecione para revelar o SQL que gera esse insight

```sql
SELECT DISTINCT
  destination,
  destination_name,
  create_time
FROM
  qsaccel.profile_agg.adwh_dim_destination
WHERE
  destination_status = 'enabled'
ORDER BY
  create_time DESC
LIMIT
  20;
```

+++

Consulte a [Documentação de widget de destinos criados recentemente](../guides/destinations.md#recently-created-destinations) para obter informações sobre a aparência e a funcionalidade desse insight.

<!-- Commented out until the Jan release as SQL MISSING FROM WIKI:

## Unmapped audiences by identity {#unmapped-audiences-by-identity}

Questions answered by this insight:

- How do I find a list of audiences that are not mapped to a destination?
- What is the count of identities for audiences that are not mapped to a destination?
- Which audiences have the highest count of identities not mapped to a particular destination?

+++Select to reveal the SQL that generates this insight

```sql
```

+++

See the [Unmapped audiences by identity widget documentation](../guides/destinations.md#unmapped-audiences-by-identity) for information on the appearance and functionality of this insight.

-->

## Próximas etapas {#next-steps}

Ao ler este documento, você agora entende o SQL que gera insights de painel e quais perguntas comuns essa análise resolve. Agora você pode editar e iterar essas consultas SQL para gerar seus próprios insights.

Consulte a [Exibir documentação SQL](../view-sql.md) para obter mais informações sobre como adaptar o SQL dos seus insights diretamente pela interface do Platform.

Você também pode ler e entender o SQL que gera insights para o [Perfis](./profiles.md), [Perfis de conta](./account-profiles.md) e [Públicos-alvo](./audiences.md) painéis.
