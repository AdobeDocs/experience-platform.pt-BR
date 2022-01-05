---
keywords: Experience Platform, home, tópicos populares, serviço de query, serviço de query, desduplicação de dados, desduplicação;
solution: Experience Platform
title: Desduplicação de dados no serviço de query
topic-legacy: queries
type: Tutorial
description: 'Este documento descreve exemplos de consulta de amostra completa e de subseleção para desduplicação de três casos de uso comuns: Eventos de experiência, compras e métricas.'
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
source-git-commit: b140037ed5f055a8e7c583540910cc6b18bbf0bd
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---

# Desduplicação de dados em [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] O suporta desduplicação de dados. A desduplicação de dados pode ser feita quando é necessário remover uma linha inteira de um cálculo ou ignorar um conjunto específico de campos porque apenas parte dos dados na linha são informações duplicadas.

A desduplicação geralmente envolve o uso da variável `ROW_NUMBER()` em uma janela para uma ID (ou um par de IDs) ao longo do tempo solicitado, que retorna um novo campo que representa o número de vezes que uma duplicata foi detectada. Muitas vezes, o tempo é representado usando o [!DNL Experience Data Model] (XDM) `timestamp` campo.

Quando o valor da variável `ROW_NUMBER()` é `1`, refere-se à instância original. Geralmente, essa é a instância que você deseja usar. Isso será feito com mais frequência dentro de uma subseleção em que a desduplicação é feita em um nível superior `SELECT` como executar uma contagem agregada.

Os casos de uso de desduplicação podem ser globais ou restritas a um único usuário ou ID de usuário final dentro da variável `identityMap`.

Este documento descreve como executar a desduplicação em três casos de uso comuns: Eventos de experiência, compras e métricas.

Cada exemplo inclui o escopo, a chave da janela e um outline do método de desduplicação, bem como a consulta SQL completa.

## Eventos de experiência {#experience-events}

No caso de Eventos de experiência duplicados, você provavelmente desejará ignorar a linha inteira.

>[!CAUTION]
>
>Muitos conjuntos de dados em [!DNL Experience Platform], incluindo aqueles produzidos pelo Adobe Analytics Data Connector, já têm a desduplicação no nível do Experience-Event aplicada. Portanto, reaplicar esse nível de desduplicação é desnecessário e retardará sua query.
>
>É importante entender a fonte de seus conjuntos de dados e saber se a desduplicação no nível do evento de experiência já foi aplicada. Para qualquer conjunto de dados que seja transmitido (por exemplo, os do Adobe Target), você **will** É necessário aplicar a desduplicação no nível do evento de experiência, pois essas fontes de dados têm uma semântica &quot;pelo menos uma vez&quot;.

**Âmbito de aplicação:** Global

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

Se você tiver compras duplicadas, é provável que queira manter a maioria das [!DNL Experience Event] , mas ignore os campos vinculados à compra (como `commerce.orders` métrica). As compras contêm um campo especial para a ID de compra, que é `commerce.order.purchaseID`.

Recomenda-se a utilização de `purchaseID` no escopo do visitante, pois é o campo semântico padrão para IDs de compra dentro do XDM. O escopo do visitante é recomendado para remover dados de compra duplicados, pois a consulta é mais rápida do que usar o escopo global e é improvável que uma ID de compra seja duplicada em várias IDs de visitante.

**Âmbito de aplicação:** Visitante

**Chave da janela:** identityMap[$NAMESPACE].id e commerce.order.purchaseID

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

>[!NOTE]
>
>Em alguns casos em que os dados originais do Analytics têm IDs de compra duplicadas nas IDs de visitante, você **pode** é necessário executar a contagem duplicada da ID de compra para todos os visitantes. Quando a ID de compra não está presente, esse método exige que você inclua uma condição que, em vez disso, use a ID de evento para manter a consulta o mais rápido possível.

### Exemplo completo

O exemplo abaixo usa uma cláusula de condição para usar a ID de evento caso a ID de compra não esteja presente.

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

No XDM, quase todas as métricas usam o `Measure` tipo de dados que inclui uma `id` campo que pode ser usado para desduplicação.

**Âmbito de aplicação:** Visitante

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

Este documento descrevia como executar a desduplicação de dados no Serviço de query, bem como exemplos de desduplicação de dados. Para obter mais práticas recomendadas ao gravar consultas usando o Serviço de query, leia o [guia de gravação de consultas](./writing-queries.md).
