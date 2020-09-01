---
keywords: Experience Platform;home;popular topics;query service;Query service;adobe defined functions;sql;
solution: Experience Platform
title: funções definidas pelo Adobe
topic: functions
translation-type: tm+mt
source-git-commit: c5d3be4706ca6d6a30e203067db6ddc894b9bfb4
workflow-type: tm+mt
source-wordcount: '2156'
ht-degree: 4%

---


# funções definidas pelo Adobe

As funções definidas pelo Adobe (ADFs) são funções pré-criadas em [!DNL Query Service] que ajudam a executar tarefas comuns relacionadas aos negócios nos [!DNL ExperienceEvent] dados. Incluem funções para Sessões e Atribuição, como as encontradas no Adobe Analytics. Consulte a documentação [da](https://docs.adobe.com/content/help/pt-BR/analytics/landing/home.html) Adobe Analytics para obter mais informações sobre a Adobe Analytics e os conceitos por trás dos ADFs definidos nesta página. Este documento fornece informações para as funções definidas pelo Adobe, disponíveis em [!DNL Query Service].

## Funções da janela

A maior parte da lógica comercial exige a coleta de pontos de contato para um cliente e a solicitação desses pontos por tempo. Esse suporte é fornecido pelo [!DNL Spark] SQL na forma de funções de janela. As funções de janela fazem parte do SQL padrão e são suportadas por muitos outros mecanismos SQL.

Uma função de janela atualiza uma agregação e retorna um único item para cada linha no subconjunto solicitado. A função de agregação mais básica é `SUM()`. `SUM()` leva suas linhas e oferece um total. Se você aplicar `SUM()` a uma janela, transformando-a em uma função de janela, você receberá uma soma cumulativa com cada linha.

A maioria dos [!DNL Spark] auxiliares SQL são funções de janela que atualizam cada linha na janela, com o estado dessa linha adicionado.

### Especificação

Sintaxe: `OVER ([partition] [order] [frame])`

| Parâmetro | Descrição |
| --- | --- |
| [partição] | Um subgrupo das linhas com base em uma coluna ou campo disponível. Exemplo, `PARTITION BY endUserIds._experience.mcid.id` |
| [ordem] | Uma coluna ou campo disponível usado para ordenar o(s) subconjunto(s). Exemplo, `ORDER BY timestamp` |
| [quadro] | Um subgrupo das linhas em uma partição. Exemplo, `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## Sessões

Quando você trabalha com [!DNL ExperienceEvent] dados originários de um site, aplicativo móvel, sistema de resposta de voz interativo ou qualquer outro canal de interação do cliente, isso ajuda se os eventos puderem ser agrupados em um período relacionado de atividade. Normalmente, você tem uma intenção específica de conduzir sua atividade como pesquisar um produto, pagar uma conta, verificar o saldo da conta, preencher um aplicativo e assim por diante. Esse agrupamento ajuda a associar os eventos para descobrir mais contexto sobre a experiência do cliente.

Para obter mais informações sobre sessões no Adobe Analytics, consulte a documentação sobre sessões [sensíveis ao](https://docs.adobe.com/content/help/en/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html)contexto.

### Especificação

Sintaxe: `SESS_TIMEOUT(timestamp, expirationInSeconds) OVER ([partition] [order] [frame])`

| Parâmetro | Descrição |
| --- | --- |
| `timestamp` | Campo de carimbo de data e hora encontrado no conjunto de dados |
| `expirationInSeconds` | Número de segundos necessários entre os eventos para qualificar o término da sessão atual e o start de uma nova sessão |

| Parâmetros de objeto retornados | Descrição |
| ---------------------- | ------------- |
| `timestamp_diff` | Tempo em segundos entre o registro atual e o registro anterior |
| `num` | Um número de sessão exclusivo, começando em 1, para a chave definida na função `PARTITION BY` da janela. |
| `is_new` | Um booliano usado para identificar se um registro é o primeiro de uma sessão |
| `depth` | Profundidade do registro atual na sessão |

#### Exemplo de Query

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

#### Resultados

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

## Atribuição

Associar ações de clientes ao sucesso é uma parte importante do entendimento dos fatores que influenciam a experiência do cliente. Os ADFs a seguir suportam a primeira e a última atribuição com diferentes configurações de expiração.

Para obter mais informações sobre atribuição no Adobe Analytics, consulte a visão geral [do](https://docs.adobe.com/content/help/pt-BR/analytics/analyze/analysis-workspace/panels/attribution.html) Attribution IQ no Guia de [!DNL Analytics] análise.

### Atribuição de primeiro toque

Retorna o valor da atribuição de primeiro toque e os detalhes de um único canal no conjunto de dados do público alvo [!DNL ExperienceEvent] . O query retorna um `struct` objeto com o valor de primeiro toque, o carimbo de data e hora e a atribuição para cada linha retornada para o canal selecionado.

Esse query é útil se você quiser ver qual interação levou a uma série de ações do cliente. No exemplo mostrado abaixo, o código de rastreamento inicial (`em:946426`) nos [!DNL ExperienceEvent] dados é atribuído a 100% (`1.0`) da responsabilidade pelas ações do cliente, já que foi a primeira interação.

### Especificação

Sintaxe: `ATTRIBUTION_FIRST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])`

| Parâmetro | Descrição |
| --- | --- |
| `timestamp` | Campo de carimbo de data e hora encontrado no conjunto de dados |
| `channelName` | Um nome amigável para usar como rótulo no objeto retornado |
| `channelValue` | A coluna ou o campo que é o canal do público alvo do query |


| Parâmetros de objeto retornados | Descrição |
| ---------------------- | ------------- |
| `name` | A `channelName` entrada como rótulo no ADF |
| `value` | O valor a partir `channelValue` desse é o primeiro toque na [!DNL ExperienceEvent] |
| `timestamp` | O carimbo de data e hora do [!DNL ExperienceEvent] local em que ocorreu o primeiro toque |
| `fraction` | A atribuição do primeiro toque expressa como crédito fracionário |

#### Exemplo de Query

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

#### Resultados

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

### Atribuição de último toque

Retorna o valor da atribuição de último toque e os detalhes de um único canal no conjunto de dados do público alvo [!DNL ExperienceEvent] . O query retorna um `struct` objeto com o último valor de toque, carimbo de data e hora e atribuição para cada linha retornada para o canal selecionado.

Esse query é útil se você quiser ver a interação final em uma série de ações do cliente. No exemplo mostrado abaixo, o código de rastreamento no objeto retornado é a última interação em cada [!DNL ExperienceEvent] registro. A cada código é atribuída uma responsabilidade de 100% (`1.0`) pelas ações do cliente, pois foi a última interação.

### Especificação

Sintaxe: `ATTRIBUTION_LAST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])`

| Parâmetro | Descrição |
| --- | --- |
| `timestamp` | Campo de carimbo de data e hora encontrado no conjunto de dados |
| `channelName` | Um nome amigável para usar como rótulo no objeto retornado |
| `channelValue` | A coluna ou o campo que é o canal do público alvo do query |


| Parâmetros de objeto retornados | Descrição |
| ---------------------- | ------------- |
| `name` | A `channelName` entrada como rótulo no ADF |
| `value` | O valor de `channelValue` que é o último toque na [!DNL ExperienceEvent] |
| `timestamp` | O carimbo de data e hora do [!DNL ExperienceEvent] local em que o `channelValue` foi usado |
| `fraction` | A atribuição do último toque expressa como crédito fracionário |

#### Exemplo de Query

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

#### Resultados

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

### Atribuição de primeiro toque com condição de expiração

Retorna o valor da atribuição de primeiro toque e os detalhes de um único canal no conjunto de dados do público alvo, que expira após ou antes de uma condição. [!DNL ExperienceEvent] O query retorna um `struct` objeto com o valor de primeiro toque, o carimbo de data e hora e a atribuição para cada linha retornada para o canal selecionado.

Esse query é útil se você quiser ver qual interação levou a uma série de ações do cliente dentro de uma parte do [!DNL ExperienceEvent] conjunto de dados determinada por uma condição de escolha. No exemplo mostrado abaixo, uma compra é registrada (`commerce.purchases.value IS NOT NULL`) em cada um dos quatro dias mostrados nos resultados (15, 21, 23 e 29 de julho) e o código de rastreamento inicial em cada dia recebe 100% (`1.0`) de responsabilidade pelas ações do cliente.

#### Especificação

Sintaxe: `ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])`

| Parâmetro | Descrição |
| --- | --- |
| `timestamp` | Campo de carimbo de data e hora encontrado no conjunto de dados |
| `channelName` | Um nome amigável para usar como rótulo no objeto retornado |
| `channelValue` | A coluna ou o campo que é o canal do público alvo do query |
| `expCondition` | A condição que determina o ponto de expiração do canal |
| `expBefore` | O padrão é `false`. Booliano para indicar se o canal expira antes ou depois que a condição especificada é atendida. Ativado principalmente para condições de expiração de sessão (por exemplo, `sess.depth = 1, true`), para garantir que o primeiro toque não seja selecionado de uma sessão anterior. |

| Parâmetros de objeto retornados | Descrição |
| ---------------------- | ------------- |
| `name` | A `channelName` entrada como rótulo no ADF |
| `value` | O valor de `channelValue` que é o primeiro toque no [!DNL ExperienceEvent] anterior ao `expCondition` |
| `timestamp` | O carimbo de data e hora do [!DNL ExperienceEvent] local em que ocorreu o primeiro toque |
| `fraction` | A atribuição do primeiro toque expressa como crédito fracionário |

#### Exemplo de Query

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

#### Resultados

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

### Atribuição de primeiro toque com tempo limite de expiração

Retorna o valor da atribuição de primeiro toque e os detalhes de um único canal no conjunto de dados do público alvo [!DNL ExperienceEvent] por um período de tempo especificado. O query retorna um `struct` objeto com o valor de primeiro toque, o carimbo de data e hora e a atribuição para cada linha retornada para o canal selecionado. Esse query é útil se você quiser ver qual interação, dentro de um intervalo de tempo selecionado, levou a uma ação do cliente. No exemplo mostrado abaixo, o primeiro toque retornado para cada ação do cliente é a primeira interação nos sete dias anteriores (`expTimeout = 86400 * 7`).

#### Especificação

Sintaxe: `ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])`

| Parâmetro | Descrição |
| --- | --- |
| `timestamp` | Campo de carimbo de data e hora encontrado no conjunto de dados |
| `channelName` | Um nome amigável para usar como rótulo no objeto retornado |
| `channelValue` | A coluna ou o campo que é o canal do público alvo do query |
| `expTimeout` | A janela de tempo (em segundos) anterior ao evento do canal que o query procura por um evento de primeiro toque |

| Parâmetros de objeto retornados | Descrição |
| ---------------------- | ------------- |
| `name` | A `channelName` entrada como rótulo no ADF |
| `value` | O valor de `channelValue` que é o primeiro toque dentro do `expTimeout` intervalo especificado |
| `timestamp` | O carimbo de data e hora do [!DNL ExperienceEvent] local em que ocorreu o primeiro toque |
| `fraction` | A atribuição do primeiro toque expressa como crédito fracionário |

#### Exemplo de Query

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

#### Resultados

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

### Atribuição de último toque com condição de expiração

Retorna o valor da atribuição de último toque e os detalhes de um único canal no conjunto de dados do público alvo, que expira após ou antes de uma condição. [!DNL ExperienceEvent] O query retorna um `struct` objeto com o último valor de toque, carimbo de data e hora e atribuição para cada linha retornada para o canal selecionado. Esse query é útil se você quiser ver a última interação em uma série de ações do cliente dentro de uma parte do [!DNL ExperienceEvent] conjunto de dados determinada por uma condição de escolha. No exemplo mostrado abaixo, uma compra é registrada (`commerce.purchases.value IS NOT NULL`) em cada um dos quatro dias mostrados nos resultados (15, 21, 23 e 29 de julho) e o último código de rastreamento em cada dia recebe 100% (`1.0`) de responsabilidade pelas ações do cliente.

#### Especificação

Sintaxe: `ATTRIBUTION_LAST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])`

| Parâmetro | Descrição |
| --- | --- |
| `timestamp` | Campo de carimbo de data e hora encontrado no conjunto de dados |
| `channelName` | Um nome amigável para usar como rótulo no objeto retornado |
| `channelValue` | A coluna ou o campo que é o canal do público alvo do query |
| `expCondition` | A condição que determina o ponto de expiração do canal |
| `expBefore` | O padrão é `false`. Booliano para indicar se o canal expira antes ou depois que a condição especificada é atendida. Ativado principalmente para condições de expiração de sessão (por exemplo, `sess.depth = 1, true`), para garantir que o último toque não seja selecionado de uma sessão anterior. |

| Parâmetros de objeto retornados | Descrição |
| ---------------------- | ------------- |
| `name` | A `channelName` entrada como rótulo no ADF |
| `value` | O valor de `channelValue` que é o último toque no [!DNL ExperienceEvent] anterior ao `expCondition` |
| `timestamp` | O carimbo de data e hora do [!DNL ExperienceEvent] local em que ocorreu o último toque |
| `percentage` | A atribuição do último toque expressa como crédito fracionário |

#### Exemplo de Query

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

#### Resultados

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

### Atribuição de último toque com tempo limite de expiração

Retorna o valor da atribuição de último toque e os detalhes de um único canal no conjunto de dados do público alvo [!DNL ExperienceEvent] por um período de tempo especificado. O query retorna um `struct` objeto com o último valor de toque, carimbo de data e hora e atribuição para cada linha retornada para o canal selecionado. Esse query é útil se você quiser ver a última interação dentro de um intervalo de tempo selecionado. No exemplo mostrado abaixo, o último toque retornado para cada ação do cliente é a interação final dentro dos sete dias seguintes (`expTimeout = 86400 * 7`).

#### Especificação

Sintaxe: `ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])`

| Parâmetro | Descrição |
| --- | --- |
| `timestamp` | Campo de carimbo de data e hora encontrado no conjunto de dados |
| `channelName` | Um nome amigável para usar como rótulo no objeto retornado |
| `channelValue` | A coluna ou o campo que é o canal do público alvo do query |
| `expTimeout` | A janela de tempo (em segundos) após o evento do canal que o query procura por um evento de último toque |

| Parâmetros de objeto retornados | Descrição |
| ---------------------- | ------------- |
| `name` | A `channelName` entrada como rótulo no ADF |
| `value` | O valor de `channelValue` que é o último toque dentro do `expTimeout` intervalo especificado |
| `timestamp` | O carimbo de data e hora do [!DNL ExperienceEvent] local em que ocorreu o último toque |
| `percentage` | A atribuição do último toque expressa como crédito fracionário |

#### Exemplo de Query

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

#### Resultados

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

## Próximo toque/anterior

É importante entender como os clientes navegam em uma experiência. Ele pode ser usado para entender a profundidade de envolvimento do cliente, confirmar as etapas desejadas de uma experiência que estão funcionando conforme projetado e identificar possíveis pontos problemáticos que afetam o cliente. Os seguintes ADFs suportam a criação de visualizações de definição de caminho a partir de seus relacionamentos Anterior e Próximo. Você poderá criar a Página anterior e a Próxima página, ou percorrer vários eventos para criar a Definição de caminho.

### Toque anterior

Determina o valor anterior de um campo específico a um número definido de etapas a partir da janela. Observe no exemplo que a `WINDOW` função está configurada com um quadro de `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` configuração do ADF para observar a linha atual e tudo antes dela.

#### Especificação

Sintaxe: `PREVIOUS(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])`

| Parâmetro | Descrição |
| --- | --- |
| `key` | A coluna ou o campo do evento. |
| `shift` | (opcional) O número de eventos distantes do evento atual. O padrão é 1. |
| `ingnoreNulls` | Booliano para indicar se `key` valores nulos devem ser ignorados. O padrão é `false`. |


| Parâmetros de objeto retornados | Descrição |
| ---------------------- | ------------- |
| `value` | O valor baseado no `key` usado no ADF |

#### Exemplo de Query

```sql
SELECT endUserIds._experience.mcid.id, _experience.analytics.session.num, timestamp, web.webPageDetails.name
    PREVIOUS(web.webPageDetails.name, 3)
      OVER(PARTITION BY endUserIds._experience.mcid.id, _experience.analytics.session.num
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, _experience.analytics.session.num, timestamp ASC
```

#### Resultados

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

### Próximo toque

Determina o próximo valor de um campo específico a um número definido de etapas à distância dentro da janela. Observe no exemplo que a `WINDOW` função está configurada com um quadro de `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` configuração do ADF para observar a linha atual e tudo depois dela.

#### Especificação

Sintaxe: `NEXT(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])`

| Parâmetro | Descrição |
| --- | --- |
| `key` | A coluna ou o campo do evento |
| `shift` | (opcional) O número de eventos distantes do evento atual. O padrão é 1. |
| `ingnoreNulls` | Booliano para indicar se `key` valores nulos devem ser ignorados. O padrão é `false`. |


| Parâmetros de objeto retornados | Descrição |
| ---------------------- | ------------- |
| `value` | O valor baseado no `key` usado no ADF |

#### Exemplo de Query

```sql
SELECT endUserIds._experience.aaid.id, timestamp, web.webPageDetails.name,
    NEXT(web.webPageDetails.name, 1, true)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.aaid.id, timestamp ASC
LIMIT 10
```

#### Resultados

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

## Intervalo de tempo

O intervalo de tempo permite explorar o comportamento latente do cliente em um período anterior ou posterior à ocorrência de um evento. Examine os eventos dentro de 7 dias após uma campanha ou outro tipo de evento em todos os seus clientes.

### Tempo entre correspondência anterior

Fornece uma nova dimensão, que mede o tempo decorrido desde um incidente específico.

#### Especificação

Sintaxe: `TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])`

| Parâmetro | Descrição |
| --- | --- |
| `timestamp` | Campo de carimbo de data e hora encontrado no conjunto de dados preenchido em todos os eventos. |
| `eventDefintion` | Expressão para qualificar o evento anterior. |
| `timeUnit` | Unidade de saída: dias, horas, minutos e segundos. O padrão é segundos. |

Saída: Retorna um número que representa a unidade de tempo desde que o evento correspondente anterior foi visto ou permanece nulo se nenhum evento correspondente foi encontrado.

#### Exemplo de Query

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

#### Resultados

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

### Tempo entre a próxima correspondência

Fornece uma nova dimensão, que mede o tempo antes de um evento específico ocorrer.

#### Especificação

Sintaxe: `TIME_BETWEEN_NEXT_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])`

| Parâmetro | Descrição |
| --- | --- |
| `timestamp` | Campo de carimbo de data e hora encontrado no conjunto de dados preenchido em todos os eventos. |
| `eventDefintion` | Expressão para qualificar o evento seguinte. |
| `timeUnit` | Unidade de saída: dias, horas, minutos e segundos. O padrão é segundos. |

Saída: Retorna um número negativo que representa a unidade de tempo atrás do próximo evento correspondente ou permanece nulo se um evento correspondente não for encontrado.

#### Exemplo de Query

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

#### Resultados

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

## Próximas etapas

Usando as funções descritas aqui, você pode gravar query para acessar seus próprios [!DNL ExperienceEvent] conjuntos de dados usando [!DNL Query Service]. Para obter mais informações sobre como criar query no, consulte [!DNL Query Service]a documentação sobre como [criar query](../creating-queries/creating-queries.md).
