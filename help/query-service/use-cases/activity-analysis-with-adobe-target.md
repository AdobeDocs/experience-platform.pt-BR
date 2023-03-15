---
title: Análise De Atividades Com O Adobe Target
description: Este documento explica como usar o Serviço de consulta para criar insights acionáveis de conjuntos de dados criados com seus dados do Adobe Target.
exl-id: a5181ee2-1e1c-405d-8dfe-5a32c28ac9f1
source-git-commit: d573c01a0aa9989f581796a0be4aec6904ffc569
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 3%

---

# Análise de atividades com o Adobe Target

O Adobe Experience Platform permite assimilar dados da Adobe Target usando campos do Experience Data Model (XDM) para criar conjuntos de dados para uso com o Serviço de consulta. Como o Adobe Target foi projetado para personalizar o conteúdo e personalizar as experiências do usuário, as consultas executadas nesses conjuntos de dados permitem insights altamente personalizados e focalizados, analisando a atividade do usuário por meio do SQL.

Este documento fornece uma variedade de exemplos de consultas SQL que demonstram casos de uso comuns com base nos comportamentos e características dos clientes.

## Introdução

Para cada um dos seguintes casos de uso, um exemplo de consulta SQL parametrizada é fornecido como um template para você personalizar. Forneça parâmetros onde quer que você veja `{ }` nos exemplos SQL que você está interessado em avaliar.

## Mapeamento de campo XDM parcial de alto nível

A tabela a seguir lista os campos comuns do Target e os campos XDM correspondentes para os quais eles mapeiam.

>[!NOTE]
>
>A utilização de `[ ]` no campo XDM indica uma matriz.

| Nome do campo de destino | Nome do campo XDM | Notas |
|---|---|---|
| `mboxName` | `_experience.target.mboxname` | N/D |
| ID da atividade | `_experience.target.activities.activityID` | N/D |
| ID da experiência | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID` | N/D |
| ID do segmento | `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id` | N/D |
| Escopo do Evento | `_experience.target.activities[].activityEvents[].eventScope` | Este campo rastreia novos visitantes e visitas. |
| ID da etapa | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID` | Esse campo é uma ID de etapa personalizada para o Adobe Campaign. |
| Preço total | commerce.order.priceTotal | N/D |

>[!IMPORTANT]
>
>O nome de um conjunto de dados criado automaticamente usando dados do Target é &quot;Eventos de experiência do Adobe Target&quot;. Ao usar esse conjunto de dados com consultas, use o nome `adobe_target_experience_events`.

## Objetivos

Ao analisar as atividades do usuário, você pode personalizar o conteúdo para um público-alvo específico e testar diferentes versões do conteúdo para uma entidade individual. Além disso, ao analisar uma atividade específica durante um determinado período de tempo ou para usuários individuais, o desempenho de cada atividade individual pode ser mais claramente compreendido. Os resultados dessa análise combinada podem ser utilizados para entender o desempenho de cada atividade individual.

Os seguintes casos de uso de personalização são criados usando dados do Adobe Target e se concentram nas atividades do usuário para criar insights valiosos sobre o comportamento dos clientes em aplicativos de negócios.

Este guia ilustra os principais conceitos a seguir por meio dos exemplos de casos de uso:

* Para entender o desempenho de uma ID de atividade em um determinado dia, como contagem, detalhes e IDs de experiência associadas.
* Para determinar o escopo de visitante e evento de uma atividade.
* Para coletar informações sobre a contagem de visitantes, visitas e impressões da Experience ID, Segment ID e Activity ID.

### Gerar contagem de atividades por hora para um determinado dia

```sql
SELECT
  Hour,
  ActivityID,
  COUNT(ActivityID) AS Instances
FROM
(
  SELECT
    date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
    EXPLODE(_experience.target.activities.activityID) AS ActivityID
  FROM adobe_target_experience_events
  WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, ActivityID
ORDER BY Hour DESC, Instances DESC
LIMIT 24
```

### Gerar detalhes por hora para um específico

```sql
SELECT
  date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
  _experience.target.activities.activityID AS ActivityID,
  COUNT(ActivityID) AS Instances
FROM adobe_target_experience_events
WHERE
  array_contains( _experience.target.activities.activityID, {Activity ID} ) AND
    TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
  _experience.target.activities IS NOT NULL
GROUP BY Hour, ActivityID
ORDER BY Hour DESC
LIMIT 24
```

### Determine a lista de IDs de experiência para uma atividade específica em um determinado dia

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  COUNT(ExperienceID) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents._experience.target.activity.activityevent.context.experienceID) AS ExperienceID
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE
      TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

### Retorne uma lista de Escopos de Evento (visitante, visita, impressão) por instâncias por ID de Atividade em um determinado dia

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  COUNT(ExperienceID) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents._experience.target.activity.activityevent.context.experienceID) AS ExperienceID
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE
      TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

### Determine a contagem de visitantes, visitas e impressões por atividade para um determinado dia

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  COUNT(ExperienceID) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents._experience.target.activity.activityevent.context.experienceID) AS ExperienceID
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE
      TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

### Determine visitantes, visitas e impressões para a Experience ID, Segment ID e EventScope para um determinado dia

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  SegmentID._id,
  SUM(CASE WHEN ActivityEvent.eventScope = 'visitor' THEN 1 END) as Visitors,
  SUM(CASE WHEN ActivityEvent.eventScope = 'visit' THEN 1 END) as Visits,
  SUM(CASE WHEN ActivityEvent.eventScope = 'impression' THEN 1 END) as Impressions
FROM
(
  SELECT
    Day,
    Activities,
    ActivityEvent,
    ActivityEvent._experience.target.activity.activityevent.context.experienceID AS ExperienceID,
    EXPLODE(ActivityEvent.segmentEvents.segmentID) AS SegmentID
  FROM
  (
    SELECT
      Day,
      Activities,
      EXPLODE(Activities.activityEvents) AS ActivityEvent
    FROM
    (
      SELECT
        date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
        EXPLODE(_experience.target.activities) AS Activities
      FROM adobe_target_experience_events
      WHERE
        TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
        _experience.target.activities IS NOT NULL
      LIMIT 1000000
    )
    LIMIT 1000000
  )
  LIMIT 1000000
)
GROUP BY Day, Activities.activityID, ExperienceID, SegmentID._id
ORDER BY Day DESC, Activities.activityID, ExperienceID ASC, SegmentID._id ASC, Visitors DESC
LIMIT 20
```

### Retorna nomes de mbox e contagem de registros para um determinado dia

```sql
SELECT
  _experience.target.mboxname,
  COUNT(timestamp) AS records
FROM
  adobe_target_experience_events
WHERE
  TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
  GROUP BY _experience.target.mboxname ORDER BY records DESC
LIMIT 100
```
