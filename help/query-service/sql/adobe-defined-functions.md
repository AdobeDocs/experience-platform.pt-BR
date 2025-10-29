---
keywords: Experience Platform;página inicial;tópicos populares;serviço de consulta;Serviço de consulta;funções definidas pela adobe;sql;
solution: Experience Platform
title: Funções SQL Definidas pela Adobe no Serviço de Consulta
description: Este documento fornece informações para funções definidas pela Adobe disponíveis no Serviço de consulta da Adobe Experience Platform.
exl-id: 275aa14e-f555-4365-bcd6-0dd6df2456b3
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 2%

---

# Funções SQL definidas pela Adobe no Serviço de consulta

As funções definidas pelo Adobe, aqui chamadas de ADFs, são funções pré-criadas no Serviço de Consulta do Adobe Experience Platform que ajudam a executar tarefas comerciais comuns em dados do [!DNL Experience Event]. Isso inclui funções para [Sessionization](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html?lang=pt-BR) e [Attribution](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html?lang=pt-BR) como aquelas encontradas no Adobe Analytics.

Este documento fornece informações para funções definidas pela Adobe disponíveis em [!DNL Query Service].

>[!NOTE]
>
>A Experience Cloud ID (ECID) também é conhecida como MCID e continua a ser usada em namespaces.

## Funções de janela {#window-functions}

A maior parte da lógica de negócios requer a obtenção dos pontos de contato para um cliente e a solicitação deles por tempo. Este suporte é fornecido pelo SQL [!DNL Spark] na forma de funções de janela. As funções de janela são parte do SQL padrão e são suportadas por muitos outros mecanismos SQL.

Uma função de janela atualiza uma agregação e retorna um único item para cada linha no subconjunto ordenado. A função de agregação mais básica é `SUM()`. `SUM()` pega suas linhas e dá um total. Se, em vez disso, você aplicar `SUM()` a uma janela, transformando-a em uma função de janela, você receberá uma soma cumulativa com cada linha.

A maioria dos auxiliares de SQL [!DNL Spark] são funções de janela que atualizam cada linha da janela, com o estado dessa linha adicionado.

**Sintaxe de consulta**

```sql
OVER ({PARTITION} {ORDER} {FRAME})
```

| Parâmetro | Descrição | Exemplo |
| --------- | ----------- | ------- |
| `{PARTITION}` | Um subgrupo de linhas com base em uma coluna ou campo disponível. | `PARTITION BY endUserIds._experience.mcid.id` |
| `{ORDER}` | Uma coluna ou campo disponível usado para ordenar o subconjunto ou as linhas. | `ORDER BY timestamp` |
| `{FRAME}` | Um subgrupo das linhas em uma partição. | `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## Sessões

Ao trabalhar com dados do [!DNL Experience Event] originados de um site, aplicativo móvel, sistema de resposta de voz interativa ou qualquer outro canal de interação com o cliente, é útil que os eventos possam ser agrupados em torno de um período de atividade relacionado. Normalmente, você tem uma intenção específica ao orientar sua atividade, como pesquisar um produto, pagar uma fatura, verificar o saldo da conta, preencher um aplicativo e assim por diante.

Esse agrupamento ou sessão de dados ajuda a associar os eventos para descobrir mais contexto sobre a experiência do cliente.

Para obter mais informações sobre a sessão no Adobe Analytics, consulte a documentação em [sessões com reconhecimento de contexto](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html?lang=pt-BR).

**Sintaxe de consulta**

```sql
SESS_TIMEOUT({TIMESTAMP}, {EXPIRATION_IN_SECONDS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{TIMESTAMP}` | O campo de carimbo de data e hora encontrado no conjunto de dados. |
| `{EXPIRATION_IN_SECONDS}` | O número de segundos necessários entre eventos para qualificar o final da sessão atual e o início de uma nova sessão. |

Uma explicação dos parâmetros dentro da função `OVER()` pode ser encontrada na [seção de funções da janela](#window-functions).

**Exemplo de consulta**

```sql
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp,
  SESS_TIMEOUT(timestamp, 60 * 30)
    OVER (PARTITION BY endUserIds._experience.mcid.id
        ORDER BY timestamp
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
    AS session
FROM experience_events
ORDER BY id, timestamp ASC
LIMIT 10
```

**Resultados**

```console
                id                |       timestamp       |      session       
|----------------------------------+-----------------------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | (40,1,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | (55,1,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | (1361821,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | (54,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | (49,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | (33,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | (31,2,false,5)
(10 rows)
```

Para o exemplo de consulta fornecido, os resultados são fornecidos na coluna `session`. A coluna `session` é composta dos seguintes componentes:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parâmetros | Descrição |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | A diferença no tempo, em segundos, entre o registro atual e o registro anterior. |
| `{NUM}` | Um número de sessão exclusivo, começando em 1, para a chave definida no `PARTITION BY` da função de janela. |
| `{IS_NEW}` | Um booleano usado para identificar se um registro é o primeiro de uma sessão. |
| `{DEPTH}` | A profundidade do registro atual na sessão. |

### SESS_START_IF

Esta consulta retorna o estado da sessão para a linha atual, com base no carimbo de data e hora atual e na expressão fornecida, e inicia uma nova sessão com a linha atual.

**Sintaxe de consulta**

```sql
SESS_START_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{TIMESTAMP}` | O campo de carimbo de data e hora encontrado no conjunto de dados. |
| `{TEST_EXPRESSION}` | Uma expressão em que você deseja verificar os campos dos dados. Por exemplo, `application.launches > 0`. |

Uma explicação dos parâmetros dentro da função `OVER()` pode ser encontrada na [seção de funções da janela](#window-functions).

**Exemplo de consulta**

```sql
SELECT
    endUserIds._experience.mcid.id AS id,
    timestamp,
    IF(application.launches.value > 0, true, false) AS isLaunch,
    SESS_START_IF(timestamp, application.launches.value > 0)
        OVER (PARTITION BY endUserIds._experience.mcid.id
            ORDER BY timestamp
            ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
        AS session
    FROM experience_events
    ORDER BY id, timestamp ASC
    LIMIT 10
```

**Resultados**

```console
                id                |       timestamp       | isLaunch |      session       
|----------------------------------+-----------------------+----------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | true     | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | false    | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | false    | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | true     | (40,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | false    | (55,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | false    | (1361821,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | false    | (54,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | false    | (49,2,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | false    | (33,2,false,6)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | false    | (31,2,false,7)
(10 rows)
```

Para o exemplo de consulta fornecido, os resultados são fornecidos na coluna `session`. A coluna `session` é composta dos seguintes componentes:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parâmetros | Descrição |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | A diferença no tempo, em segundos, entre o registro atual e o registro anterior. |
| `{NUM}` | Um número de sessão exclusivo, começando em 1, para a chave definida no `PARTITION BY` da função de janela. |
| `{IS_NEW}` | Um booleano usado para identificar se um registro é o primeiro de uma sessão. |
| `{DEPTH}` | A profundidade do registro atual na sessão. |

### SESS_END_IF

Esta consulta retorna o estado da sessão para a linha atual, com base no carimbo de data e hora atual e na expressão fornecida, encerra a sessão atual e inicia uma nova sessão na linha seguinte.

**Sintaxe de consulta**

```sql
SESS_END_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{TIMESTAMP}` | O campo de carimbo de data e hora encontrado no conjunto de dados. |
| `{TEST_EXPRESSION}` | Uma expressão em que você deseja verificar os campos dos dados. Por exemplo, `application.launches > 0`. |

Uma explicação dos parâmetros dentro da função `OVER()` pode ser encontrada na [seção de funções da janela](#window-functions).

**Exemplo de consulta**

```sql
SELECT
    endUserIds._experience.mcid.id AS id,
    timestamp,
    IF(application.applicationCloses.value > 0 OR application.crashes.value > 0, true, false) AS isExit,
    SESS_END_IF(timestamp, application.applicationCloses.value > 0 OR application.crashes.value > 0)
        OVER (PARTITION BY endUserIds._experience.mcid.id
            ORDER BY timestamp
            ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
        AS session
    FROM experience_events
    ORDER BY id, timestamp ASC
    LIMIT 10
```

**Resultados**

```console
                id                |       timestamp       | isExit   |      session       
|----------------------------------+-----------------------+----------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | false    | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | false    | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | true     | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | false    | (40,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | false    | (55,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | false    | (1361821,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | false    | (54,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | false    | (49,2,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | false    | (33,2,false,6)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | false    | (31,2,false,7)
(10 rows)
```

Para o exemplo de consulta fornecido, os resultados são fornecidos na coluna `session`. A coluna `session` é composta dos seguintes componentes:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parâmetros | Descrição |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | A diferença no tempo, em segundos, entre o registro atual e o registro anterior. |
| `{NUM}` | Um número de sessão exclusivo, começando em 1, para a chave definida no `PARTITION BY` da função de janela. |
| `{IS_NEW}` | Um booleano usado para identificar se um registro é o primeiro de uma sessão. |
| `{DEPTH}` | A profundidade do registro atual na sessão. |


## Definição de caminho

A definição de caminho pode ser usada para entender a profundidade do engajamento do cliente, confirmar se as etapas desejadas de uma experiência estão funcionando como projetado e identificar possíveis pontos problemáticos que afetam o cliente.

Os ADFs a seguir são compatíveis com o estabelecimento de exibições de definição de caminho a partir de suas relações anteriores e seguintes. Você poderá criar páginas anteriores e próximas páginas, ou percorrer vários eventos para criar a definição de caminho.

### Página anterior

Determina o valor anterior de um campo específico em um número definido de etapas na janela. Observe no exemplo que a função `WINDOW` está configurada com um quadro de `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` definindo o ADF para examinar a linha atual e todas as linhas subsequentes.

**Sintaxe de consulta**

```sql
PREVIOUS({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{KEY}` | A coluna ou o campo do evento. |
| `{SHIFT}` | (Opcional) O número de eventos distante do evento atual. Por padrão, o valor é 1. |
| `{IGNORE_NULLS}` | (Opcional) Um booleano que indica se valores `{KEY}` nulos devem ser ignorados. O valor padrão é `false`. |

Uma explicação dos parâmetros dentro da função `OVER()` pode ser encontrada na [seção de funções da janela](#window-functions).

**Exemplo de consulta**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, web.webPageDetails.name
    PREVIOUS(web.webPageDetails.name, 3)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Resultados**

```console
                id                 |       timestamp       |                 name                |                    previous_page                    
|-----------------------------------+-----------------------+-------------------------------------+-----------------------------------------------------
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:15:28.0 |                                     | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:05.0 | Home                                | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:45.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 19:22:34.0 |                                     | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:12.0 | Home                                | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:57.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:03:36.0 | Search Results                      | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:04:30.0 | Product Details: Pemmican Power Bar | (Search Results)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:05:27.0 | Shopping Cart: Cart Details         | (Product Details: Pemmican Power Bar)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:06:07.0 | Shopping Cart: Shipping Information | (Shopping Cart: Cart Details)
(10 rows)
```

Para o exemplo de consulta fornecido, os resultados são fornecidos na coluna `previous_page`. O valor na coluna `previous_page` é baseado no `{KEY}` usado no ADF.

### Próxima página

Determina o próximo valor de um campo específico em um número definido de etapas na janela. Observe no exemplo que a função `WINDOW` está configurada com um quadro de `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` definindo o ADF para examinar a linha atual e todas as linhas subsequentes.

**Sintaxe de consulta**

```sql
NEXT({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{KEY}` | A coluna ou o campo do evento. |
| `{SHIFT}` | (Opcional) O número de eventos distante do evento atual. Por padrão, o valor é 1. |
| `{IGNORE_NULLS}` | (Opcional) Um booleano que indica se valores `{KEY}` nulos devem ser ignorados. O valor padrão é `false`. |

Uma explicação dos parâmetros dentro da função `OVER()` pode ser encontrada na [seção de funções da janela](#window-functions).

**Exemplo de consulta**

```sql
SELECT endUserIds._experience.aaid.id, timestamp, web.webPageDetails.name,
    NEXT(web.webPageDetails.name, 1, true)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
      AS next_page
FROM experience_events
ORDER BY endUserIds._experience.aaid.id, timestamp ASC
LIMIT 10
```

**Resultados**

```console
                id                 |       timestamp       |                name                 |             previous_page             
|-----------------------------------+-----------------------+-------------------------------------+---------------------------------------
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:15:28.0 |                                     | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:05.0 | Home                                | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:45.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 19:22:34.0 |                                     | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:12.0 | Home                                | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:57.0 | Kids                                | (Search Results)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:03:36.0 | Search Results                      | (Product Details: Pemmican Power Bar)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:04:30.0 | Product Details: Pemmican Power Bar | (Shopping Cart: Cart Details)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:05:27.0 | Shopping Cart: Cart Details         | (Shopping Cart: Shipping Information)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:06:07.0 | Shopping Cart: Shipping Information | (Shopping Cart: Billing Information)
(10 rows)
```

Para o exemplo de consulta fornecido, os resultados são fornecidos na coluna `previous_page`. O valor na coluna `previous_page` é baseado no `{KEY}` usado no ADF.

## Intervalo

O intervalo de tempo permite explorar o comportamento latente do cliente em um determinado período antes ou depois da ocorrência de um evento.

### Tempo entre a correspondência anterior

Esta consulta retorna um número que representa a unidade de tempo desde que o evento correspondente anterior foi visto. Se nenhum evento correspondente for encontrado, ele retornará um valor nulo.

**Sintaxe de consulta**

```sql
TIME_BETWEEN_PREVIOUS_MATCH(
    {TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT})
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{TIMESTAMP}` | Um campo de carimbo de data e hora foi encontrado no conjunto de dados preenchido em todos os eventos. |
| `{EVENT_DEFINITION}` | A expressão para qualificar o evento anterior. |
| `{TIME_UNIT}` | A unidade de saída. Os valores possíveis incluem dias, horas, minutos e segundos. Por padrão, o valor é segundos. |

Uma explicação dos parâmetros dentro da função `OVER()` pode ser encontrada na [seção de funções da janela](#window-functions).

**Exemplo de consulta**

```sql
SELECT 
  page_name,
  SUM (time_between_previous_match) / COUNT(page_name) as average_minutes_since_registration
FROM
(
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp, web.webPageDetails.name as page_name, 
  TIME_BETWEEN_PREVIOUS_MATCH(timestamp, web.webPageDetails.name='Account Registration|Confirmation', 'minutes')
    OVER(PARTITION BY endUserIds._experience.mcid.id
       ORDER BY timestamp
       ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
    AS time_between_previous_match
FROM experience_events
)
WHERE time_between_previous_match IS NOT NULL
GROUP BY page_name
ORDER BY average_minutes_since_registration
LIMIT 10
```

**Resultados**

```console
             page_name             | average_minutes_since_registration 
|-----------------------------------+------------------------------------
                                   |                                   
 Account Registration|Confirmation |                                0.0
 Seasonal                          |                   5.47029702970297
 Equipment                         |                  6.532110091743119
 Women                             |                  7.287081339712919
 Men                               |                  7.640918580375783
 Product List                      |                  9.387459807073954
 Unlimited Blog|February           |                  9.954545454545455
 Product Details|Buffalo           |                 13.304347826086957
 Unlimited Blog|June               |                  770.4285714285714
(10 rows)
```

Para o exemplo de consulta fornecido, os resultados são fornecidos na coluna `average_minutes_since_registration`. O valor na coluna `average_minutes_since_registration` é a diferença de tempo entre os eventos atual e anterior. A unidade de tempo foi definida anteriormente no `{TIME_UNIT}`.

### Tempo entre a próxima correspondência

Esta consulta retorna um número negativo que representa a unidade de tempo atrás do próximo evento correspondente. Se um evento correspondente não for encontrado, null será retornado.

**Sintaxe de consulta**

```sql
TIME_BETWEEN_NEXT_MATCH({TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{TIMESTAMP}` | Um campo de carimbo de data e hora foi encontrado no conjunto de dados preenchido em todos os eventos. |
| `{EVENT_DEFINITION}` | A expressão para qualificar o próximo evento. |
| `{TIME_UNIT}` | (Opcional) A unidade de saída. Os valores possíveis incluem dias, horas, minutos e segundos. Por padrão, o valor é segundos. |

Uma explicação dos parâmetros dentro da função `OVER()` pode ser encontrada na [seção de funções da janela](#window-functions).

**Exemplo de consulta**

```sql
SELECT 
  page_name,
  SUM (time_between_next_match) / COUNT(page_name) as average_minutes_until_order_confirmation
FROM
(
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp, web.webPageDetails.name as page_name, 
  TIME_BETWEEN_NEXT_MATCH(timestamp, web.webPageDetails.name='Shopping Cart|Order Confirmation', 'minutes')
    OVER(PARTITION BY endUserIds._experience.mcid.id
       ORDER BY timestamp
       ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
    AS time_between_next_match
FROM experience_events
)
WHERE time_between_next_match IS NOT NULL
GROUP BY page_name
ORDER BY average_minutes_until_order_confirmation DESC
LIMIT 10
```

**Resultados**

```console
             page_name             | average_minutes_until_order_confirmation 
|-----------------------------------+------------------------------------------
 Shopping Cart|Order Confirmation  |                                      0.0
 Men                               |                       -9.465295629820051
 Equipment                         |                       -9.682098765432098
 Product List                      |                       -9.690661478599221
 Women                             |                       -9.759459459459459
 Seasonal                          |                                  -10.295
 Shopping Cart|Order Review        |                      -366.33567364956144
 Unlimited Blog|February           |                       -615.0327868852459
 Shopping Cart|Billing Information |                       -775.6200495367711
 Product Details|Buffalo           |                      -1274.9571428571428
(10 rows)
```

Para o exemplo de consulta fornecido, os resultados são fornecidos na coluna `average_minutes_until_order_confirmation`. O valor na coluna `average_minutes_until_order_confirmation` é a diferença de tempo entre os eventos atuais e seguintes. A unidade de tempo foi definida anteriormente no `{TIME_UNIT}`.

## Próximas etapas

Usando as funções descritas aqui, você pode gravar consultas para acessar seus próprios conjuntos de dados do [!DNL Experience Event] usando o [!DNL Query Service]. Para obter mais informações sobre a criação de consultas em [!DNL Query Service], consulte a documentação em [criando consultas](../best-practices/writing-queries.md).

## Recursos adicionais

O vídeo a seguir mostra como executar queries na interface do Adobe Experience Platform e em um cliente PSQL. Além disso, o vídeo também usa exemplos envolvendo propriedades individuais em um objeto XDM, usando funções definidas pelo Adobe e usando CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/33393?captions=por_br&quality=12&learn=on)
