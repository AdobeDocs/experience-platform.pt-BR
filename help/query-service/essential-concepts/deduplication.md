---
keywords: Experience Platform;página inicial;tópicos populares;serviço de consulta;serviço de consulta;desduplicação de dados;desduplicação;
solution: Experience Platform
title: Eliminação de duplicação de dados no serviço de consulta
type: Tutorial
description: 'Este documento descreve exemplos de consulta de amostra completa e de subseleção para desduplicação de três casos de uso comuns: Eventos de experiência, compras e métricas.'
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# Desduplicação de dados em [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] O oferece suporte à desduplicação de dados. A desduplicação de dados pode ser feita quando é necessário remover uma linha inteira de um cálculo ou ignorar um conjunto específico de campos, pois apenas parte dos dados na linha é informação duplicada.

A desduplicação geralmente envolve o uso de `ROW_NUMBER()` em uma janela, para uma ID (ou um par de IDs) ao longo do tempo solicitado, que retorna um novo campo que representa o número de vezes que uma duplicata foi detectada. Muitas vezes, o tempo é representado pelo uso do [!DNL Experience Data Model] (XDM) `timestamp` campo.

Quando o valor de `ROW_NUMBER()` é `1`, ele se refere à instância original. Geralmente, essa é a instância que você desejaria usar. Na maioria das vezes, isso será feito dentro de uma subseleção em que a desduplicação é feita em um nível superior `SELECT` como executar uma contagem agregada.

Os casos de uso de desduplicação podem ser globais ou restritos a um único usuário ou ID de usuário final na `identityMap`.

Este documento descreve como executar a desduplicação em três casos de uso comuns: Eventos de experiência, compras e métricas.

Cada exemplo inclui o escopo, a chave da janela, um outline do método de desduplicação, bem como a consulta SQL completa.

## Eventos de experiência {#experience-events}

No caso de Eventos de experiência duplicados, você provavelmente desejará ignorar toda a linha.

>[!CAUTION]
>
>Vários conjuntos de dados no [!DNL Experience Platform], incluindo aqueles produzidos pelo Conector de dados do Adobe Analytics, já têm a desduplicação em nível de evento de experiência aplicada. Portanto, a reaplicação desse nível de desduplicação é desnecessária e retardará seu query.
>
>É importante entender a origem de seus conjuntos de dados e saber se a desduplicação no nível do evento de experiência já foi aplicada. Para qualquer conjunto de dados transmitido (por exemplo, aqueles do Adobe Target), você **irá** É necessário aplicar a desduplicação em nível de evento de experiência, já que essas fontes de dados têm semântica &quot;pelo menos uma vez&quot;.

**Escopo:** Global

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

Se você tiver compras duplicadas, é provável que queira manter a maioria dos [!DNL Experience Event] linha, mas ignore os campos vinculados à compra (como o campo `commerce.orders` métrica). As compras contêm um campo especial para a ID de compra, que é `commerce.order.purchaseID`.

É recomendável usar `purchaseID` no escopo do visitante, pois é o campo semântico padrão para IDs de compra no XDM. O escopo do visitante é recomendado para remover dados de compra duplicados, pois a consulta é mais rápida do que o uso do escopo global e é improvável que uma ID de compra seja duplicada em várias IDs de visitante.

**Escopo:** Visitante

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
>Em alguns casos em que os dados originais do Analytics têm IDs de compra duplicadas nas IDs de visitante, você **maio** É necessário executar a contagem duplicada da ID de compra em todos os visitantes. Quando a ID de compra não está presente, esse método exige que você inclua uma condição que, em vez disso, use a ID de evento para manter a consulta o mais rápido possível.

### Exemplo completo

O exemplo abaixo usa uma cláusula de condição para usar a ID de evento no caso de a ID de compra não estar presente.

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

Se você tiver uma métrica que esteja usando a ID exclusiva opcional e uma duplicata dessa ID for exibida, você provavelmente desejará ignorar esse valor de métrica e manter o restante do Evento de experiência.

No XDM, quase todas as métricas usam a variável `Measure` tipo de dados que inclui uma `id` que pode ser usado para desduplicação.

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

Este documento forneceu exemplos de desduplicação de dados e descreveu como executar a desduplicação de dados no Serviço de consulta. Para obter mais práticas recomendadas ao gravar consultas usando o Serviço de consulta, leia o [guia de criação de consultas](../best-practices/writing-queries.md).
