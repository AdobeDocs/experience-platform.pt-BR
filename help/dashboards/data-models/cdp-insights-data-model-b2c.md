---
title: Edição B2C do modelo de dados do Real-time Customer Data Platform Insights
description: Saiba como usar consultas SQL com os Modelos de dados do Real-time Customer Data Platform Insights (B2C Edition) para personalizar seus próprios relatórios do Real-Time CDP para seus casos de uso de marketing e KPI.
badgeB2B: label="Edição B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="Edição B2P" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 61bc7f23-9f79-4c75-a515-85dd9dda2d02
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 0%

---

# Edição B2C do modelo de dados do Real-time Customer Data Platform Insights

O Modelo de Dados do Real-time Customer Data Platform Insights para o [B2C Edition](../../rtcdp/overview.md#rtcdp-b2c) expõe os modelos de dados e o SQL que potencializam os insights para vários widgets de perfil, destino e segmentação. Você pode personalizar esses modelos de consulta SQL para criar relatórios do Real-Time CDP para seus casos de uso de marketing e KPI (indicador chave de desempenho). Esses insights podem ser usados como widgets personalizados para seus painéis definidos pelo usuário. Consulte a documentação dos insights de relatório do repositório acelerado de consulta para saber [como criar um modelo de dados de insights de relatório por meio do Serviço de consulta para uso com dados de repositório acelerados e painéis definidos pelo usuário](../../query-service/data-distiller/sql-insights/reporting-insights-data-model.md).

>[!NOTE]
>
>O termo &quot;segmento&quot; foi atualizado para &quot;público-alvo&quot; em todos os sistemas Adobe Experience Platform. Algumas referências a segmentos permanecem em uso para caminhos de arquivos e convenções de nomenclatura de conjuntos de dados.

## Pré-requisitos

Este guia requer uma compreensão funcional do [recurso de painéis definido pelo usuário](../standard-dashboards.md). Leia a documentação antes de continuar com este guia.

## Relatórios e casos de uso do Real-Time CDP Insights

Os relatórios do Real-Time CDP fornecem insights sobre os dados do perfil e sua relação com públicos e destinos. Vários modelos de esquema estrela foram desenvolvidos para responder a uma variedade de casos de uso comuns de marketing e cada modelo de dados pode suportar vários casos de uso.

>[!IMPORTANT]
>
>Os dados usados para os relatórios do Real-Time CDP são precisos para uma política de mesclagem escolhida e do instantâneo diário mais recente.

### Modelo de perfil {#profile-model}

O modelo de perfil é composto de três conjuntos de dados:

- `adwh_dim_date`
- `adwh_fact_profile`
- `adwh_dim_merge_policies`

A imagem abaixo contém os campos de dados relevantes em cada conjunto de dados.

![Um ERD do modelo de perfil.](../images/cdp-insights/profile-model.png)

#### O caso de uso de contagem de perfis {#profile-count}

A lógica usada para o widget [!UICONTROL Contagem de perfis] retorna o número total de perfis mesclados no armazenamento Perfil no momento em que o instantâneo foi tirado. Consulte a [[!UICONTROL documentação do widget Contagem de perfis]](../guides/profiles.md#profile-count) para obter mais informações.

O SQL que gera o widget [!UICONTROL Contagem de perfis] é visto na seção que pode ser recolhida abaixo.

+++Consulta SQL

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

+++

#### O caso de uso de perfis de identidade únicos {#single-identity-profiles}

A lógica usada pelo widget [!UICONTROL Perfis de identidade única] fornece uma contagem dos perfis da sua organização que têm apenas um tipo de ID que cria a identidade. Consulte a documentação do widget [[!UICONTROL Perfis de identidade únicos]](../guides/profiles.md#single-identity-profiles) para obter mais informações.

O SQL que gera o widget [!UICONTROL Perfis de identidade única] é visto na seção que pode ser recolhida abaixo.

+++Consulta SQL

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_Single_Identity_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

+++

### Modelo de namespace {#namespace-model}

O modelo de namespace é composto pelos seguintes conjuntos de dados:

- `adwh_dim_date`
- `adwh_fact_profile_by_namespace`
- `adwh_dim_merge_policies`
- `adwh_dim_namespaces`

A imagem abaixo contém os campos de dados relevantes em cada conjunto de dados.

![Um ERD do modelo de namespace.](../images/cdp-insights/namespace-model.png)

#### Caso de uso de perfis por identidade {#profiles-by-identity}

O widget [!UICONTROL Perfis por identidade] exibe o detalhamento de identidades em todos os perfis mesclados em seu repositório de perfis. Consulte a [[!UICONTROL documentação do widget Perfis por identidade]](../guides/profiles.md#profiles-by-identity) para obter mais informações.

O SQL que gera o widget [!UICONTROL Perfis por identidade] é visto na seção que pode ser recolhida abaixo.

+++Consulta SQL

```sql
SELECT qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.count_of_profiles) count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
  AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
          qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id,
          qsaccel.profile_agg.adwh_dim_namespaces.namespace_description
  ORDER BY count_of_profiles DESC;
```

+++

#### Caso de uso de perfis de identidade únicos por identidade {#single-identity-profiles-by-identity}

A lógica usada pelo widget [!UICONTROL Perfis de identidade únicos por identidade] ilustra o número total de perfis identificados com apenas um identificador exclusivo. Consulte a [Documentação de widget de identidade de perfis de identidade únicos por identidade](../guides/profiles.md#single-identity-profiles-by-identity) para obter mais informações.

O SQL que gera o widget [!UICONTROL Perfis de identidade únicos por identidade] é visto na seção recolhível abaixo.

+++Consulta SQL

```sql
SELECT qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.count_of_Single_Identity_profiles) count_of_Single_Identity_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
  AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
          qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id,
          qsaccel.profile_agg.adwh_dim_namespaces.namespace_description;
```

+++

### Modelo de público {#audience-model}

O modelo de público-alvo é composto pelos seguintes conjuntos de dados:

- `adwh_dim_date`
- `adwh_fact_profile_by_segment`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

A imagem abaixo contém os campos de dados relevantes em cada conjunto de dados.

![Um ERD do modelo de público-alvo.](../images/cdp-insights/audience-model.png)

#### Caso de uso de tamanho do público {#audience-size}

A lógica usada para o widget [!UICONTROL Tamanho do público-alvo] retorna o número total de perfis mesclados no público-alvo selecionado no momento do instantâneo mais recente. Consulte a documentação do widget [[!UICONTROL Tamanho do público]](../guides/audiences.md#audience-size) para obter mais informações.

O SQL que gera o widget [!UICONTROL Tamanho do público-alvo] é visto na seção que pode ser recolhida abaixo.

+++Consulta SQL

```sql
SELECT
  sum(
    qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.count_of_profiles
  ) count_of_profiles
FROM
  qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id = qsaccel.profile_agg.adwh_dim_segments.segment_id
WHERE
  qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id = -1323307941
  AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 1914917902
  AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-12';
```

+++

#### Caso de uso de tendência de alteração de tamanho do público {#audience-size-change-trend}

A lógica usada para o widget [!UICONTROL Tendência de alteração de tamanho de público] fornece uma ilustração de gráfico de linha da diferença no número total de perfis qualificados para um determinado público-alvo entre os instantâneos diários mais recentes. Consulte a [[!UICONTROL Documentação do widget Tendência de alteração de tamanho do público]](../guides/audiences.md#audience-size-change-trend) para obter mais informações.

O SQL que gera o widget [!UICONTROL Tendência de alteração de tamanho de público] é visto na seção que pode ser recolhida abaixo.

+++Consulta SQL

```sql
SELECT date_key,
      Profiles_added
  FROM
    (SELECT rn_num,
            date_key,
            (count_of_profiles-lag(count_of_profiles, 1, 0) over(
                                                                ORDER BY date_key))Profiles_added
    FROM
      (SELECT date_key,
              sum(x.count_of_profiles)count_of_profiles,
              row_number() OVER (
                                  ORDER BY date_key) rn_num
        FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
        INNER JOIN
          (SELECT MAX(process_date) last_process_date,
                  merge_policy_id
          FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
          WHERE process_name = 'FACT_TABLES_PROCESSING'
            AND process_status = 'SUCCESSFUL'
          GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
        WHERE segment_id = 1333234510
          AND x.date_key >= dateadd(DAY, -30 -1, y.last_process_date)
        GROUP BY x.date_key) a)b
  WHERE rn_num > 1;
```

+++

#### Caso de uso de destinos mais usados {#most-used-destinations}

A lógica usada no widget [!UICONTROL Destinos mais usados] lista os destinos mais usados de sua organização de acordo com o número de públicos-alvo mapeados para eles. Essa classificação fornece insight sobre quais destinos estão sendo utilizados, além de mostrar os que podem estar subutilizados. Consulte a documentação no [[!UICONTROL Widget Destinos mais usados]](../guides/destinations.md#most-used-destinations) para obter mais informações.

O SQL que gera o widget [!UICONTROL Destinos mais usados] é visto na seção que pode ser recolhida abaixo.

+++Consulta SQL

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

#### Caso de uso de públicos ativado recentemente {#recently-activated-audiences}

A lógica do widget [!UICONTROL Públicos-alvo recentemente ativados] fornece uma lista dos públicos-alvo mapeados mais recentemente para um destino. Esta lista fornece um instantâneo dos públicos-alvo e destinos que estão ativamente em uso no sistema e pode ajudar a solucionar problemas de mapeamentos incorretos. Consulte a [[!UICONTROL Documentação do widget Públicos recentemente ativados]](../guides/destinations.md#recently-activated-audiences) para obter mais informações.

O SQL que gera o widget [!UICONTROL Públicos-alvo recentemente ativados] é visto na seção que pode ser recolhida abaixo.

+++Consulta SQL

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

### Modelo de namespace-público {#namespace-audience-model}

O modelo de namespace-público é composto pelos seguintes conjuntos de dados:

- `adwh_dim_date`
- `adwh_dim_namespaces`
- `adwh_fact_profile_by_segment_and_namespace`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

A imagem abaixo contém os campos de dados relevantes em cada conjunto de dados.

![Um ERD do modelo de público-alvo de namespace.](../images/cdp-insights/namespace-audience-model.png)

#### Perfis por identidade para um caso de uso de público-alvo {#audience-profiles-by-identity}

A lógica usada no widget [!UICONTROL Perfis por identidade] fornece um detalhamento de identidades em todos os perfis mesclados no repositório de perfis de um determinado público-alvo. Consulte a [[!UICONTROL documentação do widget Perfis por identidade]](../guides/audiences.md#profiles-by-identity) para obter mais informações.

O SQL que gera o widget [!UICONTROL Perfis por identidade] é visto na seção que pode ser recolhida abaixo.

+++Consulta SQL

```sql
SELECT qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.count_of_profiles) count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
  AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.segment_id = 1333234510
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = 1709997014
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.date_key = '2024-01-10'
  GROUP BY qsaccel.profile_agg.adwh_dim_namespaces.namespace_description
  ORDER BY count_of_profiles DESC;
```

+++

### Sobrepor modelo de namespace

O modelo de namespace de sobreposição é composto pelos seguintes conjuntos de dados:

- `adwh_dim_date`
- `adwh_dim_overlap_namespaces`
- `adwh_fact_profile_overlap_of_namespace`
- `adwh_dim_merge_policies`

A imagem abaixo contém os campos de dados relevantes em cada conjunto de dados.

![Um ERD do modelo de namespace de sobreposição.](../images/cdp-insights/overlap-namespace-model.png)

#### Caso de uso de sobreposição de identidade (perfis) {#profiles-identity-overlap}

A lógica usada no widget [!UICONTROL Sobreposição de identidade] exibe a sobreposição de perfis no seu **Repositório de perfis** que contém as duas identidades selecionadas. Para obter mais informações, consulte a seção widget [[!UICONTROL Sobreposição de identidade] da documentação do painel [!UICONTROL Perfis]](../guides/profiles.md#identity-overlap).

O SQL que gera o widget [!UICONTROL Sobreposição de identidade] é visto na seção que pode ser recolhida abaixo.

+++Consulta SQL

```sql
SELECT Sum(overlap_col1) overlap_col1,
        Sum(overlap_col2) overlap_col2,
        coalesce(Sum(overlap_count), 0) overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            Sum(count_of_profiles) overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace.overlap_id IN
        (SELECT a.overlap_id
          FROM
            (SELECT qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id overlap_id,
                    count(*) cnt_num
            FROM qsaccel.profile_agg.adwh_dim_overlap_namespaces
            WHERE qsaccel.profile_agg.adwh_dim_overlap_namespaces.merge_policy_id = 2027892989
              AND qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_namespaces in ('avid',
                                                                                          'crmid')
            GROUP BY qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id)a
          WHERE a.cnt_num>1 )
    UNION ALL SELECT count_of_profiles overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'avid'
    UNION ALL SELECT 0 overlap_col1,
                      count_of_profiles overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'crmid' )a;
```

+++

### Sobrepor namespace por modelo de público {#overlap-namespace-by-audience-model}

O namespace de sobreposição por modelo de público é composto pelos seguintes conjuntos de dados:

- `adwh_dim_date`
- `adwh_dim_overlap_namespaces`
- `adwh_fact_profile_overlap_of_namespace_by_segment`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

A imagem abaixo contém os campos de dados relevantes em cada conjunto de dados.

![Um ERD do namespace de sobreposição por modelo de público-alvo.](../images/cdp-insights/overlap-namespace-by-audience-model.png)

#### Caso de uso de sobreposição de identidade (públicos-alvo) {#audiences-identity-overlap}

A lógica usada no widget [!UICONTROL Públicos-alvo] do painel [!UICONTROL Sobreposição de identidade] ilustra a sobreposição de perfis que contém as duas identidades selecionadas para um público-alvo específico. Para obter mais informações, consulte a seção widget [[!UICONTROL Sobreposição de identidade] da documentação do painel [!UICONTROL Públicos-alvo]](../guides/audiences.md#identity-overlap).

O SQL que gera o widget [!UICONTROL Sobreposição de identidade] é visto na seção que pode ser recolhida abaixo.

+++Consulta SQL

```sql
SELECT Sum(overlap_col1) overlap_col1,
        Sum(overlap_col2) overlap_col2,
        Sum(overlap_count) Overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            Sum(count_of_profiles) Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.segment_id = 1333234510
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.merge_policy_id = 1709997014
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.overlap_id IN
        (SELECT a.overlap_id
          FROM
            (SELECT qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id overlap_id,
                    count(*) cnt_num
            FROM qsaccel.profile_agg.adwh_dim_overlap_namespaces
            WHERE qsaccel.profile_agg.adwh_dim_overlap_namespaces.merge_policy_id = 1709997014
              AND qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_namespaces in ('crmid',
                                                                                          'email')
            GROUP BY qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id)a
          WHERE a.cnt_num>1 )
    UNION ALL SELECT count_of_profiles overlap_col1,
                      0 overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines
    LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'crmid'
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.segment_id = 1333234510
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = 1709997014
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.date_key = '2024-01-10'
    UNION ALL SELECT 0 overlap_col1,
                      count_of_profiles overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines
    LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'email'
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.segment_id = 1333234510
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = 1709997014
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.date_key = '2024-01-10' ) a;
```

+++

<!-- Commented out as Anil wanted to add something but did not provide information yet:
### Overlap Namespace-Audience model {#overlap-namespace-audience-model}

The overlap namespace-audience model is comprised of the following datasets: 

- `adwh_fact_profile_overlap_by_namespace_and_segment`
- `adwh_dim_date`
- `adwh_dim_namespace`
- `adwh_dim_overlap_namespaces`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

![An ERD of the overlap namespace-audience model.](../images/cdp-insights/overlap-namespace-audience-model.png) -->

<!-- What insights are gathered from this particular data model? -->

<!-- Commented out as Anil wanted to add something but did not provide information yet:
### AI model {#ai-model}

The AI model is comprised of the following datasets: 

- `adwh_fact_profile_ai_models`
- `adwh_dim_date`
- `adwh_dim_merge_policies`
- `adwh_dim_ai_models`

![An ERD of the AI model.](./images/cdp-insights/ai-model.png) -->

<!-- What insights are gathered from this particular data model? -->

