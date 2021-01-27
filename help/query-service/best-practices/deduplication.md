---
keywords: Experience Platform;home;popular topics;query service;Query service;data deduplication;deduplication;
solution: Experience Platform
title: Dados desduplicação-duplicados
topic: queries
type: Tutorial
description: Este documento descreve exemplos completos e de subseleção de query para desduplicar três casos de uso comuns de Eventos de experiência, compras e métricas.
translation-type: tm+mt
source-git-commit: e2c648829bb3268ab319da934f5cc6cc811290b3
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---


# Dados desduplicação-duplicados em [!DNL Query Service]

O Adobe Experience Platform [!DNL Query Service] suporta dados desduplicação-duplicados. Os dados desduplicação-duplicados podem ser feitos quando é necessário remover uma linha inteira de um cálculo ou ignorar um conjunto específico de campos, pois apenas parte dos dados na linha são informações de duplicado.

Desduplicação-duplicado geralmente envolve o uso da função `ROW_NUMBER()` em uma janela para uma ID (ou um par de IDs) durante o tempo solicitado, que retorna um novo campo que representa o número de vezes que um duplicado foi detectado. A hora é frequentemente representada usando o campo [!DNL Experience Data Model] (XDM) `timestamp`.

Quando o valor de `ROW_NUMBER()` é `1`, ele se refere à instância original. Geralmente, essa é a instância que você gostaria de usar. Isso será feito com mais frequência dentro de uma subseleção em que o desduplicação-duplicado é feito em um nível mais alto `SELECT`, como executar uma contagem de agregações.

Casos de uso desduplicação-duplicados podem ser globais ou restritos a uma única ID de usuário ou usuário final dentro de `identityMap`.

Este documento descreve o desempenho desduplicação-duplicado para três casos de uso comuns: Experimente Eventos, compras e métricas.

Cada exemplo inclui o escopo, a chave da janela, um outline do método desduplicação-duplicado, bem como o query SQL completo.

## Eventos de experiência {#experience-events}

No caso de Eventos de experiência de duplicado, você provavelmente desejará ignorar a linha inteira.

>[!CAUTION]
>
>Muitos conjuntos de dados em [!DNL Experience Platform], incluindo os produzidos pelo Adobe Analytics Data Connector, já têm desduplicação-duplicado nível de Evento da experiência aplicado. Portanto, reaplicar esse nível de desduplicação-duplicado é desnecessário e vai retardar seu query.
>
>É importante entender a fonte de seus conjuntos de dados e saber se o desduplicação-duplicado no nível do Evento da experiência já foi aplicado. Para qualquer conjunto de dados que seja transmitido (por exemplo, os da Adobe Target), você **** precisará aplicar o nível de Evento de experiência desduplicação-duplicado, já que essas fontes de dados têm semântica &quot;pelo menos uma vez&quot;.

**Escopo:** Global

**Chave da janela:** `id`

### exemplo desduplicação-duplicado

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

Se você tiver compras de duplicado, provavelmente desejará manter a maioria da linha Evento de experiência, mas ignorará os campos vinculados à compra (como a métrica `commerce.orders`). As compras contêm um campo especial para a ID de compra, que é `commerce.order.purchaseID`.

**Escopo:** Visitante

**Chave de janela:** identityMap[$NAMESPACE].id &amp; commerce.order.purchaseID

### exemplo desduplicação-duplicado

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

Se você tiver uma métrica que esteja usando a ID exclusiva opcional e um duplicado dessa ID for exibido, você provavelmente desejará ignorar esse valor métrico e manter o restante do Evento da experiência.

No XDM, quase todas as métricas usam o tipo de dados `Measure` que inclui um campo opcional `id` que você pode usar para desduplicação-duplicado.

**Escopo:** Visitante

**Chave de janela:** identityMap[$NAMESPACE].id e id do objeto de Medida

### exemplo desduplicação-duplicado

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

Este documento descreveu como executar dados desduplicação-duplicados dentro do Serviço de Query, bem como exemplos de dados desduplicação-duplicados. Para obter mais práticas recomendadas ao gravar query usando o Query Service, leia o [guia query de gravação](./writing-queries.md).