---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, funções definidas pela adobe, sql;
solution: Experience Platform
title: Funções SQL Definidas pelo Adobe no Serviço de Consulta
topic-legacy: functions
description: Este documento fornece informações para funções definidas pelo Adobe disponíveis no Adobe Experience Platform Query Service.
exl-id: 275aa14e-f555-4365-bcd6-0dd6df2456b3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2913'
ht-degree: 2%

---

# Funções SQL definidas pelo Adobe no Serviço de Consulta

As funções definidas pelo Adobe, aqui chamadas de ADFs, são funções pré-criadas no Serviço de Consulta da Adobe Experience Platform que ajudam a executar tarefas comerciais comuns em dados [!DNL Experience Event]. Isso inclui funções para [Sessões](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html) e [Atribuição](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html) como as encontradas no Adobe Analytics.

Este documento fornece informações para funções definidas pelo Adobe disponíveis em [!DNL Query Service].

## Funções da janela {#window-functions}

A maior parte da lógica de negócios requer reunir os pontos de contato para um cliente e solicitar por tempo. Esse suporte é fornecido pelo [!DNL Spark] SQL na forma de funções de janela. As funções Window fazem parte do SQL padrão e são compatíveis com muitos outros mecanismos SQL.

Uma função window atualiza um agregado e retorna um único item para cada linha no subconjunto ordenado. A função de agregação mais básica é `SUM()`. `SUM()` O pega suas linhas e oferece um total. Se, em vez disso, você aplicar `SUM()` a uma janela, transformando-a em uma função de janela, você receberá uma soma cumulativa com cada linha.

A maioria dos [!DNL Spark] auxiliar SQL são funções de janela que atualizam cada linha na janela, com o estado dessa linha adicionado.

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

Quando você está trabalhando com dados [!DNL Experience Event] provenientes de um site, aplicativo móvel, sistema interativo de resposta de voz ou qualquer outro canal de interação do cliente, ajuda se os eventos podem ser agrupados em torno de um período de atividade relacionado. Normalmente, você tem uma intenção específica de conduzir sua atividade, como pesquisar um produto, pagar uma conta, verificar o saldo da conta, preencher um aplicativo e assim por diante.

Esse agrupamento, ou sessão de dados, ajuda a associar os eventos para descobrir mais contexto sobre a experiência do cliente.

Para obter mais informações sobre sessões no Adobe Analytics, consulte a documentação sobre [sessões sensíveis ao contexto](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html).

**Sintaxe do query**

```sql
SESS_TIMEOUT({TIMESTAMP}, {EXPIRATION_IN_SECONDS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{TIMESTAMP}` | O campo de carimbo de data e hora encontrado no conjunto de dados. |
| `{EXPIRATION_IN_SECONDS}` | O número de segundos necessários entre eventos para qualificar o fim da sessão atual e o início de uma nova sessão. |

Uma explicação dos parâmetros dentro da função `OVER()` pode ser encontrada na seção [window functions](#window-functions).

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

Para a consulta de amostra fornecida, os resultados são fornecidos na coluna `session` . A coluna `session` é composta dos seguintes componentes:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parâmetros | Descrição |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | A diferença de tempo, em segundos, entre o registro atual e o registro anterior. |
| `{NUM}` | Um número de sessão exclusivo, começando em 1, para a chave definida em `PARTITION BY` da função da janela. |
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

Uma explicação dos parâmetros dentro da função `OVER()` pode ser encontrada na seção [window functions](#window-functions).

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

Para a consulta de amostra fornecida, os resultados são fornecidos na coluna `session` . A coluna `session` é composta dos seguintes componentes:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parâmetros | Descrição |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | A diferença de tempo, em segundos, entre o registro atual e o registro anterior. |
| `{NUM}` | Um número de sessão exclusivo, começando em 1, para a chave definida em `PARTITION BY` da função da janela. |
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

Uma explicação dos parâmetros dentro da função `OVER()` pode ser encontrada na seção [window functions](#window-functions).

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

Para a consulta de amostra fornecida, os resultados são fornecidos na coluna `session` . A coluna `session` é composta dos seguintes componentes:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parâmetros | Descrição |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | A diferença de tempo, em segundos, entre o registro atual e o registro anterior. |
| `{NUM}` | Um número de sessão exclusivo, começando em 1, para a chave definida em `PARTITION BY` da função da janela. |
| `{IS_NEW}` | Um booleano usado para identificar se um registro é o primeiro de uma sessão. |
| `{DEPTH}` | A profundidade do registro atual na sessão. |

## Atribuição

Associar ações do cliente ao sucesso é uma parte importante da compreensão dos fatores que influenciam as experiências do cliente. Os seguintes ADFs são compatíveis com atribuição de primeiro e último toque com diferentes configurações de expiração.

Para obter mais informações sobre atribuição no Adobe Analytics, consulte a [Visão geral do Attribution IQ](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html) no guia do painel Atribuição [!DNL Analytics].

### Atribuição de primeiro toque

Essa consulta retorna o valor da atribuição de primeiro toque e os detalhes de um único canal no conjunto de dados [!DNL Experience Event] de destino. A consulta retorna um objeto `struct` com o valor do primeiro toque, o carimbo de data e hora e a atribuição para cada linha retornada para o canal selecionado.

Esse query é útil se você quiser ver qual interação levou a uma série de ações do cliente. No exemplo mostrado abaixo, a responsabilidade pelo código de rastreamento inicial (`em:946426`) nos dados [!DNL Experience Event] é atribuída a 100% (`1.0`) das ações do cliente, pois foi a primeira interação.

**Sintaxe do query**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{TIMESTAMP}` | O campo de carimbo de data e hora encontrado no conjunto de dados. |
| `{CHANNEL_NAME}` | O rótulo do objeto retornado. |
| `{CHANNEL_VALUE}` | A coluna ou campo que é o canal de destino do query. |

Uma explicação dos parâmetros em `OVER()` pode ser encontrada na seção [funções de janela](#window-functions).

**Exemplo de consulta**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH(timestamp, 'Paid First', marketing.trackingCode)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
LIMIT 10
```

**Resultados**

```console
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:06:12.0 | em:946426    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:07:02.0 | em:946426    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:07:55.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:08:44.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:50:10.0 | em:513526    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:50:43.0 | em:513526    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:53:02.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-26 20:37:12.0 | sms:70175    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-26 20:37:57.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2019-01-02 19:41:38.0 | em:526702    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
(10 rows)
```

Para a consulta de amostra fornecida, os resultados são fornecidos na coluna `first_touch` . A coluna `first_touch` é composta dos seguintes componentes:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{NAME}` | O `{CHANNEL_NAME}`, que foi inserido como um rótulo no ADF. |
| `{VALUE}` | O valor de `{CHANNEL_VALUE}` que é o primeiro toque em [!DNL Experience Event] |
| `{TIMESTAMP}` | O carimbo de data e hora de [!DNL Experience Event] onde o primeiro contato ocorreu. |
| `{FRACTION}` | A atribuição do primeiro toque, expressa como uma fração decimal. |

### Atribuição de último toque

Essa consulta retorna o valor da atribuição de último toque e os detalhes de um único canal no conjunto de dados [!DNL Experience Event] de destino. A consulta retorna um objeto `struct` com o valor do último toque, o carimbo de data e hora e a atribuição para cada linha retornada para o canal selecionado.

Esse query é útil se você quiser ver a interação final em uma série de ações do cliente. No exemplo mostrado abaixo, o código de rastreamento no objeto retornado é a última interação em cada registro [!DNL Experience Event]. A cada código é atribuída uma responsabilidade de 100% (`1.0`) pelas ações do cliente, pois foi a última interação.

**Sintaxe do query**

```sql
ATTRIBUTION_LAST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{TIMESTAMP}` | O campo de carimbo de data e hora encontrado no conjunto de dados. |
| `{CHANNEL_NAME}` | O rótulo do objeto retornado. |
| `{CHANNEL_VALUE}` | A coluna ou campo que é o canal de destino do query. |

Uma explicação dos parâmetros em `OVER()` pode ser encontrada na seção [funções de janela](#window-functions).

**Exemplo de consulta**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH(timestamp, 'trackingCode', marketing.trackingCode)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Resultados**

```console
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:06:12.0 | em:946426    | (Paid Last,em:946426,2017-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:07:02.0 | em:946426    | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:07:55.0 |              | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:08:44.0 |              | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:50:10.0 | em:513526    | (Paid Last,em:513526,2017-12-23 17:50:10.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:50:43.0 | em:513526    | (Paid Last,em:513526,2017-12-23 17:50:43.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:53:02.0 |              | (Paid Last,em:513526,2017-12-23 17:50:43.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-26 20:37:12.0 | sms:70175    | (Paid Last,sms:70175,2017-12-26 20:37:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-26 20:37:57.0 |              | (Paid Last,sms:70175,2017-12-26 20:37:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-01-02 19:41:38.0 | em:526702    | (Paid Last,em:526702,2018-01-02 19:41:38.0,1.0)
(10 rows)
```

Para a consulta de amostra fornecida, os resultados são fornecidos na coluna `last_touch` . A coluna `last_touch` é composta dos seguintes componentes:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parâmetros | Descrição |
| ---------- | ----------- |
| `{NAME}` | O `{CHANNEL_NAME}`, que foi inserido como um rótulo no ADF. |
| `{VALUE}` | O valor de `{CHANNEL_VALUE}` que é o último toque em [!DNL Experience Event] |
| `{TIMESTAMP}` | O carimbo de data e hora de [!DNL Experience Event] onde `channelValue` foi usado. |
| `{FRACTION}` | A atribuição do último toque, expressa como uma fração decimal. |

### Atribuição de primeiro toque com condição de expiração

Esse query retorna o valor de atribuição de primeiro toque e os detalhes de um único canal no conjunto de dados [!DNL Experience Event] de destino, que expira após ou antes de uma condição. A consulta retorna um objeto `struct` com o valor do primeiro toque, o carimbo de data e hora e a atribuição para cada linha retornada para o canal selecionado.

Esse query é útil se você quiser ver qual interação levou a uma série de ações do cliente em uma parte do conjunto de dados [!DNL Experience Event] determinada por uma condição de sua escolha. No exemplo mostrado abaixo, uma compra é registrada (`commerce.purchases.value IS NOT NULL`) em cada um dos quatro dias mostrados nos resultados (15 de julho, 21, 23 e 29) e o código de rastreamento inicial em cada dia é atribuído à responsabilidade 100% (`1.0`) pelas ações do cliente.

**Sintaxe do query**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{TIMESTAMP}` | O campo de carimbo de data e hora encontrado no conjunto de dados. |
| `{CHANNEL_NAME}` | O rótulo do objeto retornado. |
| `{CHANNEL_VALUE}` | A coluna ou campo que é o canal de destino do query. |
| `{EXP_CONDITION}` | A condição que determina o ponto de expiração do canal. |
| `{EXP_BEFORE}` | Um booleano que indica se o canal expira antes ou depois da condição especificada, `{EXP_CONDITION}`, é atendida. Isso é ativado principalmente para as condições de expiração de uma sessão, para garantir que o primeiro toque não seja selecionado em uma sessão anterior. Por padrão, esse valor é definido como `false`. |

Uma explicação dos parâmetros dentro da função `OVER()` pode ser encontrada na seção [window functions](#window-functions).

**Exemplo de consulta**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, 'Paid First', marketing.trackingCode, commerce.purchases.value IS NOT NULL, false)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Resultados**

```console
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:05.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid First,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

Para a consulta de amostra fornecida, os resultados são fornecidos na coluna `first_touch` . A coluna `first_touch` é composta dos seguintes componentes:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parâmetros | Descrição |
| ---------- | ----------- |
| `{NAME}` | O `{CHANNEL_NAME}`, que foi inserido como um rótulo no ADF. |
| `{VALUE}` | O valor de `CHANNEL_VALUE}` que é o primeiro toque em [!DNL Experience Event], antes de `{EXP_CONDITION}`. |
| `{TIMESTAMP}` | O carimbo de data e hora de [!DNL Experience Event] onde o primeiro contato ocorreu. |
| `{FRACTION}` | A atribuição do primeiro toque, expressa como uma fração decimal. |

### Atribuição de primeiro toque com tempo limite de expiração

Esse query retorna o valor da atribuição de primeiro toque e os detalhes de um único canal no conjunto de dados de destino [!DNL Experience Event] por um período de tempo especificado. A consulta retorna um objeto `struct` com o valor do primeiro toque, o carimbo de data e hora e a atribuição para cada linha retornada para o canal selecionado.

Esse query é útil se você quiser ver qual interação, em um intervalo de tempo selecionado, levou a uma ação do cliente. No exemplo mostrado abaixo, o primeiro contato retornado para cada ação do cliente é a interação mais antiga nos sete dias anteriores (`expTimeout = 86400 * 7`).

**Especificação**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{TIMESTAMP}` | O campo de carimbo de data e hora encontrado no conjunto de dados. |
| `{CHANNEL_NAME}` | O rótulo do objeto retornado. |
| `{CHANNEL_VALUE}` | A coluna ou campo que é o canal de destino do query. |
| `{EXP_TIMEOUT}` | A janela de tempo antes do evento do canal, em segundos, que a query pesquisa por um evento de primeiro toque. |

Uma explicação dos parâmetros dentro da função `OVER()` pode ser encontrada na seção [window functions](#window-functions).

**Exemplo de consulta**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(timestamp, 'Paid First', marketing.trackingCode, 86400 * 7)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Resultados**

```console
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:05.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid First,em:483339,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid First,em:483339,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid First,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

Para a consulta de amostra fornecida, os resultados são fornecidos na coluna `first_touch` . A coluna `first_touch` é composta dos seguintes componentes:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parâmetros | Descrição |
| ---------- | ----------- |
| `{NAME}` | O `{CHANNEL_NAME}`, que foi inserido como um rótulo no ADF. |
| `{VALUE}` | O valor de `CHANNEL_VALUE}` que é o primeiro contato dentro do intervalo `{EXP_TIMEOUT}` especificado. |
| `{TIMESTAMP}` | O carimbo de data e hora de [!DNL Experience Event] onde o primeiro contato ocorreu. |
| `{FRACTION}` | A atribuição do primeiro toque, expressa como uma fração decimal. |

### Atribuição de último toque com condição de expiração

Esse query retorna o valor de atribuição de último toque e os detalhes de um único canal no conjunto de dados [!DNL Experience Event] de destino, que expira após ou antes de uma condição. A consulta retorna um objeto `struct` com o valor do último toque, o carimbo de data e hora e a atribuição para cada linha retornada para o canal selecionado.

Esse query é útil se você quiser ver a última interação em uma série de ações do cliente em uma parte do conjunto de dados [!DNL Experience Event] determinada por uma condição de sua escolha. No exemplo mostrado abaixo, uma compra é registrada (`commerce.purchases.value IS NOT NULL`) em cada um dos quatro dias mostrados nos resultados (15 de julho, 21, 23 e 29) e o último código de rastreamento em cada dia é atribuído à responsabilidade 100% (`1.0`) pelas ações do cliente.

**Sintaxe do query**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{TIMESTAMP}` | O campo de carimbo de data e hora encontrado no conjunto de dados. |
| `{CHANNEL_NAME}` | O rótulo do objeto retornado. |
| `{CHANNEL_VALUE}` | A coluna ou campo que é o canal de destino do query. |
| `{EXP_CONDITION}` | A condição que determina o ponto de expiração do canal. |
| `{EXP_BEFORE}` | Um booleano que indica se o canal expira antes ou depois da condição especificada, `{EXP_CONDITION}`, é atendida. Isso é ativado principalmente para as condições de expiração de uma sessão, para garantir que o primeiro toque não seja selecionado em uma sessão anterior. Por padrão, esse valor é definido como `false`. |

**Exemplo de consulta**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH_EXP_IF(timestamp, 'trackingCode', marketing.trackingCode, commerce.purchases.value IS NOT NULL, false)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Exemplo de resultados**

```console
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 | em:1024841   | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 | em:550984    | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid Last,em:380097,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 | em:380097    | (Paid Last,em:380097,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

Para a consulta de amostra fornecida, os resultados são fornecidos na coluna `last_touch` . A coluna `last_touch` é composta dos seguintes componentes:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parâmetros | Descrição |
| ---------- | ----------- |
| `{NAME}` | O `{CHANNEL_NAME}`, que foi inserido como um rótulo no ADF. |
| `{VALUE}` | O valor de `{CHANNEL_VALUE}` que é o último toque em [!DNL Experience Event], antes de `{EXP_CONDITION}`. |
| `{TIMESTAMP}` | O carimbo de data e hora de [!DNL Experience Event] onde o último contato ocorreu. |
| `{FRACTION}` | A atribuição do último toque, expressa como uma fração decimal. |

### Atribuição de último toque com tempo limite de expiração

Esta consulta retorna o valor da atribuição de último toque e os detalhes de um único canal no conjunto de dados [!DNL Experience Event] de destino por um período de tempo especificado. A consulta retorna um objeto `struct` com o valor do último toque, o carimbo de data e hora e a atribuição para cada linha retornada para o canal selecionado.

Essa consulta é útil se você quiser ver a última interação em um intervalo de tempo selecionado. No exemplo mostrado abaixo, o último toque retornado para cada ação do cliente é a interação final dentro dos sete dias seguintes (`expTimeout = 86400 * 7`).

**Sintaxe do query**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{TIMESTAMP}` | O campo de carimbo de data e hora encontrado no conjunto de dados. |
| `{CHANNEL_NAME}` | O rótulo do objeto retornado |
| `{CHANNEL_VALUE}` | A coluna ou campo que é o canal de destino do query |
| `{EXP_TIMEOUT}` | A janela de tempo após o evento de canal, em segundos, que a query pesquisa por um evento de último toque. |

Uma explicação dos parâmetros dentro da função `OVER()` pode ser encontrada na seção [window functions](#window-functions).

**Exemplo de consulta**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(timestamp, 'trackingCode', marketing.trackingCode, 86400 * 7)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Resultados**

```console
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 | em:1024841   | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

Para a consulta de amostra fornecida, os resultados são fornecidos na coluna `last_touch` . A coluna `last_touch` é composta dos seguintes componentes:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parâmetros | Descrição |
| ---------- | ----------- |
| `{NAME}` | O `{CHANNEL_NAME}`, inserido como um rótulo no ADF. |
| `{VALUE}` | O valor de `{CHANNEL_VALUE}` que é o último toque dentro do intervalo `{EXP_TIMEOUT}` especificado |
| `{TIMESTAMP}` | O carimbo de data e hora de [!DNL Experience Event] onde o último contato ocorreu |
| `{FRACTION}` | A atribuição do último toque, expressa como uma fração decimal. |

## Definição de caminho

A definição de caminho pode ser usada para entender a profundidade de engajamento do cliente, confirmar as etapas desejadas de uma experiência que estão funcionando conforme projetado e identificar possíveis pontos problemáticos que afetam o cliente.

Os seguintes ADFs são compatíveis com a definição de exibições de definição de caminho de seus relacionamentos anteriores e posteriores. Você poderá criar páginas anteriores e próximas ou percorrer vários eventos para criar a definição de caminho.

### Página anterior

Determina o valor anterior de um campo específico a um número definido de etapas na janela. Observe no exemplo que a função `WINDOW` está configurada com um quadro de `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` definindo o ADF para observar a linha atual e todas as linhas subsequentes.

**Sintaxe do query**

```sql
PREVIOUS({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{KEY}` | A coluna ou campo do evento. |
| `{SHIFT}` | (Opcional) O número de eventos distantes do evento atual. Por padrão, o valor é 1. |
| `{IGNORE_NULLS}` | (Opcional) Um booleano que indica se valores `{KEY}` nulos devem ser ignorados. Por padrão, o valor é `false`. |

Uma explicação dos parâmetros dentro da função `OVER()` pode ser encontrada na seção [window functions](#window-functions).

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

Para a consulta de amostra fornecida, os resultados são fornecidos na coluna `previous_page` . O valor na coluna `previous_page` é baseado no `{KEY}` usado no ADF.

### Próxima página

Determina o próximo valor de um campo específico a um número definido de etapas na janela. Observe no exemplo que a função `WINDOW` está configurada com um quadro de `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` definindo o ADF para observar a linha atual e todas as linhas subsequentes.

**Sintaxe do query**

```sql
NEXT({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{KEY}` | A coluna ou campo do evento. |
| `{SHIFT}` | (Opcional) O número de eventos distantes do evento atual. Por padrão, o valor é 1. |
| `{IGNORE_NULLS}` | (Opcional) Um booleano que indica se valores `{KEY}` nulos devem ser ignorados. Por padrão, o valor é `false`. |

Uma explicação dos parâmetros dentro da função `OVER()` pode ser encontrada na seção [window functions](#window-functions).

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

Para a consulta de amostra fornecida, os resultados são fornecidos na coluna `previous_page` . O valor na coluna `previous_page` é baseado no `{KEY}` usado no ADF.

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

Uma explicação dos parâmetros dentro da função `OVER()` pode ser encontrada na seção [window functions](#window-functions).

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

Para a consulta de amostra fornecida, os resultados são fornecidos na coluna `average_minutes_since_registration` . O valor na coluna `average_minutes_since_registration` é a diferença de tempo entre os eventos atual e anterior. A unidade de tempo foi definida anteriormente no `{TIME_UNIT}`.

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

Uma explicação dos parâmetros dentro da função `OVER()` pode ser encontrada na seção [window functions](#window-functions).

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

Para a consulta de amostra fornecida, os resultados são fornecidos na coluna `average_minutes_until_order_confirmation` . O valor na coluna `average_minutes_until_order_confirmation` é a diferença de tempo entre os eventos atual e seguinte. A unidade de tempo foi definida anteriormente no `{TIME_UNIT}`.

## Próximas etapas

Usando as funções descritas aqui, você pode gravar consultas para acessar seus próprios conjuntos de dados [!DNL Experience Event] usando [!DNL Query Service]. Para obter mais informações sobre a criação de consultas em [!DNL Query Service], consulte a documentação sobre [criação de consultas](../best-practices/writing-queries.md).

## Recursos adicionais

O vídeo a seguir mostra como executar consultas na interface do Adobe Experience Platform e em um cliente PSQL. Além disso, o vídeo também usa exemplos envolvendo propriedades individuais em um objeto XDM, usando funções definidas pelo Adobe e usando CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)
