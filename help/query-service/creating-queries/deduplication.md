---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Dados desduplicação-duplicados
topic: queries
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 1%

---


# Dados desduplicação-duplicados no serviço de Query

O Serviço de Query Adobe Experience Platform suporta dados desduplicação-duplicados quando pode ser necessário remover uma linha inteira de um cálculo ou ignorar um conjunto específico de campos porque apenas parte dos dados na linha é um duplicado. O padrão comum de desduplicação-duplicado envolve o uso da `ROW_NUMBER()` função em uma janela para uma ID, ou par de IDs, ao longo do tempo ordenado (usando o campo Modelo de Dados de Experiência (XDM) `timestamp` ) para retornar um novo campo que representa o número de vezes que um duplicado foi detectado. Quando esse valor é `1`, refere-se à instância original e, na maioria dos casos, essa é a instância que você deseja usar, ignorando todas as outras instâncias. Isso será feito com mais frequência dentro de uma subseleção em que o desduplicação-duplicado é feito em um nível mais alto, `SELECT` como executar uma contagem de agregações.

## Casos de uso

Alguns casos de uso para desduplicação-duplicados são globais no intervalo de datas e alguns estão restritos a um único visitante ou ID de usuário final dentro do `identityMap`.

Este documento descreve exemplos de query de amostra completa e de subseleção para desduplicar três casos de uso comuns:
- [ExperienceEvents](#experienceevents)
- [Compras](#purchases)
- [Métricas](#metrics)

### ExperienceEvents {#experienceevents}

No caso de ExperienceEvents do duplicado, você provavelmente desejará ignorar a linha inteira.

>[!CAUTION]
>
>Muitos DataSets no Experience Platform, incluindo os produzidos pelo Adobe Analytics Data Connector, já têm o nível de ExperienceEvent desduplicação-duplicado aplicado. Portanto, reaplicar esse nível de desduplicação-duplicado é desnecessário e vai retardar seu query. É importante entender a fonte de seus DataSets e saber se desduplicação-duplicado no nível do ExperienceEvent já foi aplicado. Para todos os DataSets que são transmitidos (por exemplo, os de Adobe Target), será necessário aplicar o nível de ExperienceEvent desduplicação-duplicado, pois essas fontes de dados têm uma semântica de &#39;pelo menos uma vez&#39;.

**Âmbito:** Global

**Chave da janela:** id

#### Subseleção

```sql
SELECT *,
  ROW_NUMBER()
    OVER (PARTITION BY id
          ORDER BY timestamp ASC
    ) AS id_dup_num
FROM experience_events
```

#### Exemplo completo

```sql
SELECT COUNT(*) AS num_events FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num
  FROM experience_events
) WHERE id_dup_num = 1
```

### Compras {#purchases}

Se você tiver compras de duplicado, provavelmente desejará manter a maior parte da linha ExperienceEvent, mas ignorará os campos vinculados à compra (como a `commerce.orders` métrica). Para compras, há um campo especial para a ID de compra. Este campo é `commerce.order.purchaseID`.

**Âmbito:** Visitante

**Chave da janela:** identityMap[$NAMESPACE].id &amp; commerce.order.purchaseID

#### Subseleção

```sql
SELECT *,
  IF(LENGTH(commerce.`order`.purchaseID) > 0,
    ROW_NUMBER()
      OVER (PARTITION BY identityMap['ECID'].id, commerce.`order`.purchaseID
            ORDER BY timestamp ASC
      ),
    1) AS purchaseID_dup_num
FROM experience_events
```

#### Exemplo completo

```sql
SELECT SUM(commerce.purchases.value) AS num_purchases FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num,
    IF(LENGTH(commerce.`order`.purchaseID) > 0,
      ROW_NUMBER()
        OVER (PARTITION BY identityMap['ECID'].id, commerce.order.purchaseID
              ORDER BY timestamp ASC
        ),
      1) AS purchaseID_dup_num
  FROM experience_events
) WHERE id_dup_num = 1 AND purchaseID_dup_num = 1
```

### Métricas {#metrics}

Se você tiver uma métrica que esteja usando a ID exclusiva opcional e um duplicado dessa ID for exibido, você provavelmente desejará ignorar esse valor métrico e manter o restante do ExperienceEvent. No XDM, quase todas as métricas usam o tipo de `Measure` dados que inclui um `id` campo opcional que você poderia usar para o desduplicação-duplicado.

**Âmbito:** Visitante

**Chave da janela:** identityMap[$NAMESPACE].id e id do objeto Measurement

#### Subseleção

```sql
SELECT *,
  IF(LENGTH(application.launches.id) > 0,
    ROW_NUMBER()
      OVER (PARTITION BY identityMap['ECID'].id, application.launches.id
            ORDER BY timestamp ASC
      ),
    1) AS launchesID_dup_num
FROM experience_events
```

#### Exemplo completo

```sql
SELECT SUM(application.launches.value) AS num_launches FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num,
    IF(LENGTH(application.launches.id) > 0,
      ROW_NUMBER()
        OVER (PARTITION BY identityMap['ECID'].id, application.launches.id
              ORDER BY timestamp ASC
        ),
      1) AS launchesID_dup_num
  FROM experience_events
) WHERE id_dup_num = 1 AND launchesID_dup_num = 1
```
