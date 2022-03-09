---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, consultas de amostra, consulta de amostra, adobe target;
solution: Experience Platform
title: Exemplos de consultas para dados do Adobe Target
topic-legacy: queries
description: Os dados do Adobe Target são transformados em esquema XDM do Evento de experiência e assimilados no Experience Platform como conjuntos de dados para você. Este documento contém consultas de amostra para usar o Serviço de query com seus conjuntos de dados do Adobe Target.
exl-id: 0ab3cd6e-25ed-43dc-b8f0-a2b71621ae50
source-git-commit: c0e7ae8f65aa0373d35a55d4da46e0ffcb0e60f9
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 1%

---

# Exemplos de consultas para dados do Adobe Target

Os dados do Adobe Target são transformados em esquema XDM do Evento de experiência e assimilados no Adobe Experience Platform como conjuntos de dados para você. Há muitos casos de uso para o Serviço de query do Adobe Experience Platform com esses dados e as seguintes consultas de amostra devem funcionar com seus conjuntos de dados do Adobe Target.

No Experience Platform, o nome do conjunto de dados criado automaticamente é &quot;Adobe Target Experience Events&quot;. Ao usar esse conjunto de dados com queries, você deve usar o nome `adobe_target_experience_events`.

## Mapeamento de campo XDM parcial de alto nível

A lista a seguir mostra os campos do Target que são mapeados para os campos XDM correspondentes.

>[!NOTE]
>
> O uso de `[ ]` no campo XDM significa uma matriz.

- mboxName: `_experience.target.mboxname`
- ID da atividade: `_experience.target.activities.activityID`
- ID da experiência: `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID`
- ID do segmento: `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id`
- Escopo do evento: `_experience.target.activities[].activityEvents[].eventScope`
   - Este campo rastreia novos visitantes e visitas.
- ID da etapa: `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID`
   - Este campo é uma ID de etapa personalizada para o Adobe Campaign.
- Preço total: `commerce.order.priceTotal`

## Exemplos de consultas

As consultas a seguir mostram exemplos de consultas usadas com frequência com o Adobe Target.

Nos exemplos a seguir, será necessário editar o SQL para preencher os parâmetros esperados de suas consultas com base no conjunto de dados, nas variáveis ou no período de tempo que você está interessado em avaliar. Forneça parâmetros onde você visualizar `{ }` no SQL.

### Contagens de atividades por hora para um determinado dia

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

### Detalhes por hora para uma atividade específica em um determinado dia

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

### IDs de experiência para uma atividade específica de um determinado dia

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

### Retorne uma lista de escopos de evento (visitante, visita, impressão) por instâncias por ID de atividade para um determinado dia

```sql
SELECT
  Day,
  Activities.activityID,
  EventScope,
  COUNT(EventScope) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents.eventScope) AS EventScope
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
)
GROUP BY Day, Activities.activityID, EventScope
ORDER BY Day DESC, Instances DESC
LIMIT 30
```

### Contagem de retorno de visitantes, visitas, impressões por atividade para um determinado dia

```sql
SELECT
  Hour,
  Activities.activityid,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'visitor' ) THEN 1 END) as Visitors,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'visit' ) THEN 1 END) as Visits,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'impression' ) THEN 1 END) as Impressions
FROM
(
  SELECT
    date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
    EXPLODE(_experience.target.activities) AS Activities
  FROM adobe_target_experience_events
  WHERE
    TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, Activities.activityid
ORDER BY Hour DESC, Visitors DESC
LIMIT 30
```

### Retornar visitantes, visitas, impressões para Experience ID, ID de segmento e EventScope para um determinado dia

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

### Retornar nomes de mbox e contagem de registros de um determinado dia

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
