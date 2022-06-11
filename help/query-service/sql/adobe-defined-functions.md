---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, funções definidas pela adobe, sql;
solution: Experience Platform
title: Funções SQL Definidas pelo Adobe no Serviço de Consulta
topic-legacy: functions
description: Este documento fornece informações para funções definidas pelo Adobe disponíveis no Adobe Experience Platform Query Service.
exl-id: 275aa14e-f555-4365-bcd6-0dd6df2456b3
source-git-commit: e0cdfc514a9e1277134d4c0d5396fc0bdf9d9958
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 3%

---

# Funções SQL definidas pelo Adobe no Serviço de Consulta

As funções definidas pelo Adobe, aqui chamadas de ADFs, são funções pré-criadas no Serviço de Consulta da Adobe Experience Platform que ajudam a executar tarefas comerciais comuns em [!DNL Experience Event] dados. Essas incluem funções para [Sessões](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html) e [Atribuição](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html?lang=pt-BR) como os encontrados no Adobe Analytics.

Este documento fornece informações para as funções definidas pelo Adobe disponíveis em [!DNL Query Service].

## Funções da janela {#window-functions}

A maior parte da lógica de negócios requer reunir os pontos de contato para um cliente e solicitar por tempo. Esse suporte é fornecido por [!DNL Spark] SQL na forma de funções de janela. As funções Window fazem parte do SQL padrão e são compatíveis com muitos outros mecanismos SQL.

Uma função window atualiza um agregado e retorna um único item para cada linha no subconjunto ordenado. A função de agregação mais básica é `SUM()`. `SUM()` O pega suas linhas e oferece um total. Se, em vez disso, você aplicar `SUM()` para uma janela, transformando-a em uma função de janela, você recebe uma soma cumulativa com cada linha.

A maioria dos [!DNL Spark] Os auxiliar SQL são funções de janela que atualizam cada linha na janela, com o estado dessa linha adicionado.

**Sintaxe do query**

```sql
OVER ({PARTITION} {ORDER} {FRAME})
```

| Parâmetro | Descrição | Exemplo |
| --------- | ----------- | ------- |
| `{PARTITION}` | Um subgrupo de linhas com base em uma coluna ou campo disponível. | `PARTITION BY endUserIds._experience.mcid.id` |
| `{ORDER}` | Uma coluna ou campo disponível usado para ordenar o subconjunto ou as linhas. | `ORDER BY timestamp` |
| `{FRAME}` | Um subgrupo de linhas em uma partição. | `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## Sessões

Ao trabalhar com o [!DNL Experience Event] dados provenientes de um site, aplicativo móvel, sistema interativo de resposta de voz ou qualquer outro canal de interação do cliente, ajuda se os eventos puderem ser agrupados em torno de um período de atividade relacionado. Normalmente, você tem uma intenção específica de conduzir sua atividade, como pesquisar um produto, pagar uma conta, verificar o saldo da conta, preencher um aplicativo e assim por diante.

Esse agrupamento, ou sessão de dados, ajuda a associar os eventos para descobrir mais contexto sobre a experiência do cliente.

Para obter mais informações sobre sessões no Adobe Analytics, consulte a documentação em [sessões sensíveis ao contexto](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html).

**Sintaxe do query**

```sql
SESS_TIMEOUT({TIMESTAMP}, {EXPIRATION_IN_SECONDS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{TIMESTAMP}` | O campo de carimbo de data e hora encontrado no conjunto de dados. |
| `{EXPIRATION_IN_SECONDS}` | O número de segundos necessários entre eventos para qualificar o fim da sessão atual e o início de uma nova sessão. |

Uma explicação dos parâmetros no `OVER()` pode ser encontrada no [seção funções da janela](#window-functions).

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
----------------------------------+-----------------------+--------------------
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

Para a consulta de amostra fornecida, os resultados são fornecidos no `session` coluna. O `session` é composta pelos seguintes componentes:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parâmetros | Descrição |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | A diferença de tempo, em segundos, entre o registro atual e o registro anterior. |
| `{NUM}` | Um número de sessão exclusivo, começando em 1, para a chave definida no `PARTITION BY` da função window. |
| `{IS_NEW}` | Um booleano usado para identificar se um registro é o primeiro de uma sessão. |
| `{DEPTH}` | A profundidade do registro atual na sessão. |

### SESS_START_IF

Esse query retorna o estado da sessão para a linha atual, com base no carimbo de data e hora atual e na expressão fornecida, e inicia uma nova sessão com a linha atual.

**Sintaxe do query**

```sql
SESS_START_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{TIMESTAMP}` | O campo de carimbo de data e hora encontrado no conjunto de dados. |
| `{TEST_EXPRESSION}` | Uma expressão na qual você deseja verificar os campos dos dados. Por exemplo, `application.launches > 0`. |

Uma explicação dos parâmetros no `OVER()` pode ser encontrada no [seção funções da janela](#window-functions).

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
----------------------------------+-----------------------+----------+--------------------
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

Para a consulta de amostra fornecida, os resultados são fornecidos no `session` coluna. O `session` é composta pelos seguintes componentes:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parâmetros | Descrição |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | A diferença de tempo, em segundos, entre o registro atual e o registro anterior. |
| `{NUM}` | Um número de sessão exclusivo, começando em 1, para a chave definida no `PARTITION BY` da função window. |
| `{IS_NEW}` | Um booleano usado para identificar se um registro é o primeiro de uma sessão. |
| `{DEPTH}` | A profundidade do registro atual na sessão. |

### SESS_END_IF

Esse query retorna o estado da sessão para a linha atual, com base no carimbo de data e hora atual e na expressão fornecida, encerra a sessão atual e inicia uma nova sessão na próxima linha.

**Sintaxe do query**

```sql
SESS_END_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{TIMESTAMP}` | O campo de carimbo de data e hora encontrado no conjunto de dados. |
| `{TEST_EXPRESSION}` | Uma expressão na qual você deseja verificar os campos dos dados. Por exemplo, `application.launches > 0`. |

Uma explicação dos parâmetros no `OVER()` pode ser encontrada no [seção funções da janela](#window-functions).

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
----------------------------------+-----------------------+----------+--------------------
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

Para a consulta de amostra fornecida, os resultados são fornecidos no `session` coluna. O `session` é composta pelos seguintes componentes:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parâmetros | Descrição |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | A diferença de tempo, em segundos, entre o registro atual e o registro anterior. |
| `{NUM}` | Um número de sessão exclusivo, começando em 1, para a chave definida no `PARTITION BY` da função window. |
| `{IS_NEW}` | Um booleano usado para identificar se um registro é o primeiro de uma sessão. |
| `{DEPTH}` | A profundidade do registro atual na sessão. |


## Definição de caminho

A definição de caminho pode ser usada para entender a profundidade de engajamento do cliente, confirmar as etapas desejadas de uma experiência que estão funcionando conforme projetado e identificar possíveis pontos problemáticos que afetam o cliente.

Os seguintes ADFs são compatíveis com a definição de exibições de definição de caminho de seus relacionamentos anteriores e posteriores. Você poderá criar páginas anteriores e próximas ou percorrer vários eventos para criar a definição de caminho.

### Página anterior

Determina o valor anterior de um campo específico a um número definido de etapas na janela. Observe no exemplo que a variável `WINDOW` é configurada com um quadro de `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` definir o ADF para examinar a linha atual e todas as linhas subsequentes.

**Sintaxe do query**

```sql
PREVIOUS({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{KEY}` | A coluna ou campo do evento. |
| `{SHIFT}` | (Opcional) O número de eventos distantes do evento atual. Por padrão, o valor é 1. |
| `{IGNORE_NULLS}` | (Opcional) Um booleano que indica se é nulo `{KEY}` devem ser ignorados. Por padrão, o valor é `false`. |

Uma explicação dos parâmetros no `OVER()` pode ser encontrada no [seção funções da janela](#window-functions).

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
-----------------------------------+-----------------------+-------------------------------------+-----------------------------------------------------
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

Para a consulta de amostra fornecida, os resultados são fornecidos no `previous_page` coluna. O valor na variável `previous_page` é baseada na variável `{KEY}` usado no ADF.

### Próxima página

Determina o próximo valor de um campo específico a um número definido de etapas na janela. Observe no exemplo que a variável `WINDOW` é configurada com um quadro de `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` definir o ADF para examinar a linha atual e todas as linhas subsequentes.

**Sintaxe do query**

```sql
NEXT({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{KEY}` | A coluna ou campo do evento. |
| `{SHIFT}` | (Opcional) O número de eventos distantes do evento atual. Por padrão, o valor é 1. |
| `{IGNORE_NULLS}` | (Opcional) Um booleano que indica se é nulo `{KEY}` devem ser ignorados. Por padrão, o valor é `false`. |

Uma explicação dos parâmetros no `OVER()` pode ser encontrada no [seção funções da janela](#window-functions).

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
-----------------------------------+-----------------------+-------------------------------------+---------------------------------------
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

Para a consulta de amostra fornecida, os resultados são fornecidos no `previous_page` coluna. O valor na variável `previous_page` é baseada na variável `{KEY}` usado no ADF.

## Intervalo de tempo

O intervalo de tempo permite explorar o comportamento latente do cliente em um determinado período de tempo antes ou depois da ocorrência de um evento.

### Tempo entre a correspondência anterior

Este query retorna um número que representa a unidade de tempo desde que o evento correspondente anterior foi visualizado. Se nenhum evento correspondente foi encontrado, ele retorna null.

**Sintaxe do query**

```sql
TIME_BETWEEN_PREVIOUS_MATCH(
    {TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT})
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{TIMESTAMP}` | Um campo de carimbo de data e hora encontrado no conjunto de dados preenchido em todos os eventos. |
| `{EVENT_DEFINITION}` | A expressão para qualificar o evento anterior. |
| `{TIME_UNIT}` | A unidade de saída. O valor possível inclui dias, horas, minutos e segundos. Por padrão, o valor é segundos. |

Uma explicação dos parâmetros no `OVER()` pode ser encontrada no [seção funções da janela](#window-functions).

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
-----------------------------------+------------------------------------
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

Para a consulta de amostra fornecida, os resultados são fornecidos no `average_minutes_since_registration` coluna. O valor na variável `average_minutes_since_registration` é a diferença no tempo entre os eventos atual e anterior. A unidade de tempo foi definida anteriormente no `{TIME_UNIT}`.

### Tempo entre a próxima correspondência

Este query retorna um número negativo que representa a unidade de tempo por trás do próximo evento correspondente. Se um evento correspondente não for encontrado, null será retornado.

**Sintaxe do query**

```sql
TIME_BETWEEN_NEXT_MATCH({TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{TIMESTAMP}` | Um campo de carimbo de data e hora encontrado no conjunto de dados preenchido em todos os eventos. |
| `{EVENT_DEFINITION}` | A expressão para qualificar o evento seguinte. |
| `{TIME_UNIT}` | (Opcional) A unidade de saída. O valor possível inclui dias, horas, minutos e segundos. Por padrão, o valor é segundos. |

Uma explicação dos parâmetros no `OVER()` pode ser encontrada no [seção funções da janela](#window-functions).

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
-----------------------------------+------------------------------------------
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

Para a consulta de amostra fornecida, os resultados são fornecidos no `average_minutes_until_order_confirmation` coluna. O valor na variável `average_minutes_until_order_confirmation` é a diferença no tempo entre os eventos atual e seguinte. A unidade de tempo foi definida anteriormente no `{TIME_UNIT}`.

## Próximas etapas

Usando as funções descritas aqui, você pode gravar consultas para acessar suas próprias [!DNL Experience Event] conjuntos de dados usando [!DNL Query Service]. Para obter mais informações sobre a criação de consultas no [!DNL Query Service], consulte a documentação em [criação de queries](../best-practices/writing-queries.md).

## Recursos adicionais

O vídeo a seguir mostra como executar consultas na interface do Adobe Experience Platform e em um cliente PSQL. Além disso, o vídeo também usa exemplos envolvendo propriedades individuais em um objeto XDM, usando funções definidas pelo Adobe e usando CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)
