---
title: Análise de atribuição
description: Este documento explica como você pode usar o Serviço de query para criar uma técnica de medição de eficácia de marketing com base no modelo de atribuição de marketing de primeiro e último contato.
source-git-commit: 870626f25b1aabdcb5739bbb1ab85bdad44df195
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 1%

---

# Análise de atribuição

A atribuição é um conceito analítico que ajuda a determinar as táticas de marketing, como canais, ofertas e mensagens, que contribuem para vendas ou conversões comerciais. Esse conceito avalia a jornada do consumidor (o processo pelo qual um cliente interage com uma empresa para atingir uma meta) que resulta em uma compra ou aquisição com base em pontos de contato do cliente (sempre que um consumidor interage com sua marca). Por meio da análise de atribuição, os profissionais de marketing podem avaliar o retorno sobre o investimento dos canais que os conectam a um cliente em potencial.

## Introdução

Os exemplos de SQL neste documento são consultas comumente usadas com dados do Adobe Analytics. Este tutorial requer uma compreensão funcional dos seguintes componentes:

* [O conector de origem do Adobe Analytics para obter a visão geral dos dados do conjunto de relatórios](../../sources/connectors/adobe-applications/mapping/analytics.md).
* [A documentação de mapeamentos de campo do Analytics](../../sources/connectors/adobe-applications/mapping/analytics.md) O fornece mais informações sobre assimilação e mapeamento de dados analíticos para uso com o Serviço de query.
* [A visão geral do Attribution IQ](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html?lang=pt-BR)
* [O guia do painel Atribuição do Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/overview.html?lang=pt-BR).

Uma explicação dos parâmetros no `OVER()` pode ser encontrada no [seção funções da janela](../sql/adobe-defined-functions.md#window-functions). O [Glossário de termos de marketing e comércio do Adobe](https://business.adobe.com/glossary/index.html) pode também ser útil.

Para cada um dos seguintes casos de uso, um exemplo de consulta SQL parametrizado é fornecido como um template para você personalizar. Forneça parâmetros onde você visualizar `{ }` nos exemplos de SQL que você está interessado em avaliar.

## Objetivos

Um caso de uso de atribuição usa dados do Adobe Analytics para ajudar a associar ações do cliente a um resultado bem-sucedido. Essa associação é uma parte essencial da compreensão dos fatores que influenciam as experiências dos clientes. Os dados da análise de atribuição podem ser usados para entender a importância do ponto de contato de um cliente durante a jornada do cliente.

Os exemplos de query contidos neste documento são compatíveis com vários casos de uso para atribuição de primeiro e último toque com diferentes configurações de expiração. Este guia ilustra os seguintes conceitos principais:

* Atribuição de primeiro e último toque.
* Atribuição de primeiro e último toque com tempo limite de expiração.
* Atribuição de primeiro e último toque com condição de expiração.

## Parâmetros de consulta de atribuição {#attribution-query-parameters}

A tabela abaixo fornece um detalhamento dos parâmetros e suas descrições usadas em consultas de atribuição de primeiro e último toque:

| Parâmetro | Descrição |
|---|---|
| `{TIMESTAMP}` | O campo de carimbo de data e hora encontrado no conjunto de dados. |
| `{CHANNEL_NAME}` | O rótulo do objeto retornado. |
| `{CHANNEL_VALUE}` | A coluna ou campo que é o canal de destino do query. |
| `{EXP_TIMEOUT}` | A janela de tempo antes do evento do canal, em segundos, que a query pesquisa por um evento de primeiro toque. |
| `{EXP_CONDITION}` | A condição que determina o ponto de expiração do canal. |
| `{EXP_BEFORE}` | Um booleano que indica se o canal expira antes ou depois da condição especificada, `{EXP_CONDITION}`, é atendido. Isso é ativado principalmente para as condições de expiração de uma sessão, para garantir que o primeiro toque não seja selecionado em uma sessão anterior. Por padrão, esse valor é definido como `false`. |

## Componentes da coluna Resultados da consulta {#query-result-column-components}

Os resultados das queries de atribuição são fornecidos na variável `first_touch` ou `last_touch` coluna. Essas colunas são compostas pelos seguintes componentes:

```console
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parâmetros | Descrição |
| ---------- | ----------- |
| `{NAME}` | O `{CHANNEL_NAME}`, inserido como um rótulo no Azure Data Fatory (ADF). |
| `{VALUE}` | O valor de `{CHANNEL_VALUE}` que é o último contato dentro do `{EXP_TIMEOUT}` intervalo |
| `{TIMESTAMP}` | O carimbo de data e hora da variável [!DNL Experience Event] em que ocorreu o último contato |
| `{FRACTION}` | A atribuição do último toque, expressa como uma fração decimal. |

### Atribuição de primeiro toque {#first-touch}

A atribuição de primeiro contato atribui 100% da responsabilidade por um resultado bem-sucedido ao canal inicial que o consumidor encontrou. Este exemplo SQL é usado para destacar a interação que levou a uma série subsequente de ações do cliente.

A query abaixo retorna o valor da atribuição de primeiro toque e os detalhes do canal no target [!DNL Experience Event] conjunto de dados. Também retorna um valor `struct` para o canal selecionado com o valor de primeiro toque, carimbo de data e hora e atribuição para cada linha.

**Sintaxe do query**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

Para obter uma lista completa de parâmetros potencialmente necessários e suas descrições, consulte [seção parâmetros de consulta de atribuição](#attribution-query-parameters).

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

Nos resultados abaixo, o código de rastreamento inicial `em:946426` é retirado do [!DNL Experience Event] conjunto de dados. Esse código de rastreamento é atribuído com 100% (`1.0`) da responsabilidade pelas ações do cliente, pois foi a primeira interação.

```console
                 id                 |       timestamp       | trackingCode |                   first_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
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

Para obter uma análise dos resultados exibidos na `first_touch` , consulte a [seção componentes da coluna](#query-result-column-components).

### Atribuição de último toque {#second-touch}

A atribuição de último contato atribui 100% da responsabilidade por um resultado bem-sucedido ao último canal que o consumidor encontrou. Este exemplo de SQL é usado para destacar a interação final em uma série de ações do cliente.

O query retorna o valor da atribuição de último toque e os detalhes do canal no target [!DNL Experience Event] conjunto de dados. Também retorna um valor `struct` para o canal selecionado com o valor de último toque, carimbo de data e hora e atribuição para cada linha.

**Sintaxe do query**

```sql
ATTRIBUTION_LAST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

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

Nos resultados exibidos abaixo, o código de rastreamento no objeto retornado é a última interação em cada [!DNL Experience Event] gravar. A cada código é atribuído 100% (`1.0`) responsabilidade pelas ações do cliente, já que foi a última interação.

```console
                 id                |       timestamp       | trackingCode |                   last_touch                   
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

Para obter uma análise dos resultados exibidos na `last_touch` , consulte a [seção componentes da coluna](#query-result-column-components).

### Atribuição de primeiro contato com condição de expiração {#first-touch-attribution-with-expiration-condition}

Esse query é usado para ver qual interação levou a uma série de ações do cliente em uma parte do [!DNL Experience Event] conjunto de dados determinado por uma condição de sua escolha.

O query retorna o valor da atribuição de primeiro toque e os detalhes de um único canal no target [!DNL Experience Event] conjunto de dados, que expira após ou antes de uma condição. Também retorna um valor `struct` objeto com valor de primeiro toque, carimbo de data e hora e atribuição para cada linha retornada para o canal selecionado.

**Sintaxe do query**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

Para obter uma lista completa de parâmetros potencialmente necessários e suas descrições, consulte [seção parâmetros de consulta de atribuição](#attribution-query-parameters).

**Exemplo de consulta**

No exemplo mostrado abaixo, uma compra é registrada (`commerce.purchases.value IS NOT NULL`) em cada um dos quatro dias mostrados nos resultados (15 de julho, 21, 23 e 29), e o código de rastreamento inicial em cada dia é atribuído a 100% (`1.0`) responsabilidade pelas ações do cliente.

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
                 id               |       timestamp       | trackingCode |                   first_touch                   
----------------------------------+-----------------------+--------------+-------------------------------------------------
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

Para obter uma análise dos resultados exibidos na `first_touch` , consulte a [seção componentes da coluna](#query-result-column-components).

### Atribuição de primeiro contato com tempo limite de expiração {#first-touch-attribution-with-expiration-timeout}

Esse query é usado para localizar a interação, dentro de um período de tempo selecionado, que levou à ação bem-sucedida do cliente.

A query abaixo retorna o valor da atribuição de primeiro toque e os detalhes de um único canal no target [!DNL Experience Event] conjunto de dados para um período especificado. O query retorna um `struct` objeto com valor de primeiro toque, carimbo de data e hora e atribuição para cada linha retornada para o canal selecionado.

**Sintaxe do query**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

Para obter uma lista completa de parâmetros potencialmente necessários e suas descrições, consulte [seção parâmetros de consulta de atribuição](#attribution-query-parameters).

**Exemplo de consulta**

No exemplo mostrado abaixo, o primeiro contato retornado para cada ação do cliente é a primeira interação nos sete dias anteriores (expTimeout = 86400 * 7).

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
-----------------------------------+-----------------------+--------------+-------------------------------------------------
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

Para obter uma análise dos resultados exibidos na `first_touch` , consulte a [seção componentes da coluna](#query-result-column-components).

### Atribuição de último contato com condição de expiração {#last-touch-attribution-with-expiration-condition}

Esse query é usado para encontrar a última interação em uma série de ações do cliente em uma parte do [!DNL Experience Event] conjunto de dados determinado por uma condição de sua escolha.

A query abaixo retorna o valor da atribuição de último toque e os detalhes de um único canal no target [!DNL Experience Event] conjunto de dados, que expira após ou antes de uma condição. O query retorna um `struct` objeto com valor de último toque, carimbo de data e hora e atribuição para cada linha retornada para o canal selecionado.

**Sintaxe do query**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

Para obter uma lista completa de parâmetros potencialmente necessários e suas descrições, consulte [seção parâmetros de consulta de atribuição](#attribution-query-parameters).

**Exemplo de consulta**

No exemplo mostrado abaixo, uma compra é registrada (`commerce.purchases.value IS NOT NULL`) em cada um dos quatro dias mostrados nos resultados (15 de julho, 21, 23 e 29), e o último código de rastreamento em cada dia é atribuído a 100% (`1.0`) responsabilidade pelas ações do cliente.

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
                id                 |       timestamp       | trackingCode |                   last_touch                   
-----------------------------------+-----------------------+--------------+------------------------------------------------
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

Para obter uma análise dos resultados exibidos na `last_touch` , consulte a [seção componentes da coluna](#query-result-column-components).

### Atribuição de último contato com tempo limite de expiração {#last-touch-attribution-with-expiration-timeout}

Esta consulta é usada para encontrar a última interação em um intervalo de tempo selecionado. O query retorna o valor da atribuição de último toque e os detalhes de um único canal no target [!DNL Experience Event] conjunto de dados para um período especificado. O query retorna um `struct` objeto com valor de último toque, carimbo de data e hora e atribuição para cada linha retornada para o canal selecionado.

**Sintaxe do query**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

Para obter uma lista completa de parâmetros potencialmente necessários e suas descrições, consulte [seção parâmetros de consulta de atribuição](#attribution-query-parameters).

**Exemplo de consulta**

No exemplo mostrado abaixo, o último contato retornado para cada ação do cliente é a interação final dentro dos sete dias seguintes (`expTimeout = 86400 * 7`).

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

Para obter uma análise dos resultados exibidos na `last_touch` , consulte a [seção componentes da coluna](#query-result-column-components).
