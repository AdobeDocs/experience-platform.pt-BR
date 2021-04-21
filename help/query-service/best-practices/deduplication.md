---
keywords: Experience Platform, home, tópicos populares, serviço de query, serviço de query, desduplicação de dados, desduplicação;
solution: Experience Platform
title: Desduplicação de dados no serviço de query
topic-legacy: queries
type: Tutorial
description: 'Este documento descreve exemplos de consulta de amostra completa e de subseleção para desduplicação de três casos de uso comuns: Eventos de experiência, compras e métricas.'
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# Desduplicação de dados em [!DNL Query Service]

O Adobe Experience Platform [!DNL Query Service] oferece suporte à desduplicação de dados. A desduplicação de dados pode ser feita quando é necessário remover uma linha inteira de um cálculo ou ignorar um conjunto específico de campos porque apenas parte dos dados na linha são informações duplicadas.

A desduplicação geralmente envolve o uso da função `ROW_NUMBER()` em uma janela para uma ID (ou um par de IDs) durante o tempo solicitado, que retorna um novo campo que representa o número de vezes que uma duplicata foi detectada. O tempo é frequentemente representado usando o campo [!DNL Experience Data Model] (XDM) `timestamp`.

Quando o valor de `ROW_NUMBER()` é `1`, ele se refere à instância original. Geralmente, essa é a instância que você deseja usar. Isso será feito com mais frequência dentro de uma subseleção em que a desduplicação é feita em um `SELECT` nível superior, como executar uma contagem agregada.

Os casos de uso de desduplicação podem ser globais ou restritas a um único usuário ou ID de usuário final dentro do `identityMap`.

Este documento descreve como executar a desduplicação em três casos de uso comuns: Eventos de experiência, compras e métricas.

Cada exemplo inclui o escopo, a chave da janela e um outline do método de desduplicação, bem como a consulta SQL completa.

## Eventos de experiência {#experience-events}

No caso de Eventos de experiência duplicados, você provavelmente desejará ignorar a linha inteira.

>[!CAUTION]
>
>Muitos conjuntos de dados em [!DNL Experience Platform], incluindo os produzidos pelo Conector de dados do Adobe Analytics, já têm a desduplicação no nível do evento de experiência aplicada. Portanto, reaplicar esse nível de desduplicação é desnecessário e retardará sua query.
>
>É importante entender a fonte de seus conjuntos de dados e saber se a desduplicação no nível do evento de experiência já foi aplicada. Para todos os conjuntos de dados que são transmitidos (por exemplo, os do Adobe Target), você **precisará** aplicar a desduplicação no nível do Evento da Experiência, pois essas fontes de dados têm uma semântica &quot;pelo menos uma vez&quot;.

**Escopo:** global

**Chave da janela:** `id`

### Exemplo de desduplicação

```sql
SELECT *,
  ROW_NUMBER()
    OVER (PARTITION BY id
          ORDER BY timestamp ASC
    ) AS id_dup_num
FROM experience_events
```

### Exemplo completo

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

## Compras {#purchases}

Se você tiver compras duplicadas, provavelmente desejará manter a maior parte da linha Evento de experiência , mas ignorar os campos vinculados à compra (como a métrica `commerce.orders` ). As compras contêm um campo especial para a ID de compra, que é `commerce.order.purchaseID`.

**Escopo:** Visitante

**Chave da janela:** identityMap[$NAMESPACE].id &amp; commerce.order.purchaseID

### Exemplo de desduplicação

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

### Exemplo completo

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

## Métricas {#metrics}

Se você tiver uma métrica que esteja usando a ID exclusiva opcional e uma duplicata dessa ID for exibida, provavelmente desejará ignorar esse valor métrico e manter o restante do evento de experiência.

No XDM, quase todas as métricas usam o tipo de dados `Measure` que inclui um campo opcional `id` que pode ser usado para desduplicação.

**Escopo:** Visitante

**Chave da janela:** identityMap[$NAMESPACE].id e id do objeto Measure

### Exemplo de desduplicação

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

### Exemplo completo

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

## Próximas etapas

Este documento descrevia como executar a desduplicação de dados no Serviço de query, bem como exemplos de desduplicação de dados. Para obter mais práticas recomendadas ao gravar consultas usando o Serviço de query, leia o [guia de consultas de gravação](./writing-queries.md).
