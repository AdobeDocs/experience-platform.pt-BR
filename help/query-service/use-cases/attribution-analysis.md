---
title: Análise de atribuição
description: Este documento explica como você pode usar o Serviço de consulta para criar uma técnica de medição de eficácia de marketing com base no modelo de atribuição de marketing de primeiro e último contato.
exl-id: d62cd349-06fc-4ce6-a5e8-978f11186927
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 0%

---

# Análise de atribuição

Atribuição é um conceito analítico que ajuda a determinar as táticas de marketing, como canais, ofertas e mensagens, que contribuem para as vendas ou conversões dos negócios. Esse conceito avalia a jornada do consumidor (o processo pelo qual um cliente interage com uma empresa para atingir uma meta) que resulta em uma compra ou aquisição com base em pontos de contato do cliente (sempre que um consumidor interage com sua marca). Por meio da análise de atribuição, os profissionais de marketing podem avaliar o retorno sobre o investimento dos canais que os conectam a um cliente potencial.

## Introdução

Os exemplos de SQL neste documento são consultas comumente usadas com dados do Adobe Analytics. Este tutorial requer um entendimento prático dos seguintes componentes:

* [O conector de origem do Adobe Analytics para a visão geral dos dados do conjunto de relatórios](../../sources/connectors/adobe-applications/mapping/analytics.md).
* [A documentação de mapeamentos de campo do Analytics](../../sources/connectors/adobe-applications/mapping/analytics.md) fornece mais informações sobre assimilação e mapeamento de dados de análise para uso com o Serviço de consulta.
* [A visão geral do Attribution IQ](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html?lang=pt-BR)
* [Guia do painel Atribuição do Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html?lang=pt-BR).

Uma explicação dos parâmetros dentro da função `OVER()` pode ser encontrada na [seção de funções da janela](../sql/adobe-defined-functions.md#window-functions). O [Glossário de Termos do Adobe Marketing e do Commerce](https://business.adobe.com/glossary/index.html) também pode ser útil.

Para cada um dos seguintes casos de uso, um exemplo de consulta SQL parametrizada é fornecido como um template para você personalizar. Forneça parâmetros sempre que `{ }` for exibido nos exemplos SQL que você estiver interessado em avaliar.

## Objetivos

Um caso de uso de atribuição usa dados do Adobe Analytics para ajudar a associar ações do cliente a um resultado bem-sucedido. Essa associação é uma parte essencial da compreensão dos fatores que influenciam as experiências do cliente. Os dados da análise de atribuição podem ser usados para entender a importância do ponto de contato de um cliente durante a jornada do cliente.

Os exemplos de consulta contidos neste documento oferecem suporte a vários casos de uso para atribuição de primeiro e último contato com diferentes configurações de expiração. Este guia ilustra os seguintes conceitos principais:

* Atribuição de primeiro e último contato.
* Atribuição de primeiro e último contato com tempo limite de expiração.
* Atribuição de primeiro e último contato com condição de expiração.

## Parâmetros de consulta de atribuição {#attribution-query-parameters}

A tabela abaixo fornece um detalhamento dos parâmetros e suas descrições usados em consultas de atribuição de primeiro e último toque:

| Parâmetro | Descrição |
|---|---|
| `{TIMESTAMP}` | O campo de carimbo de data e hora encontrado no conjunto de dados. |
| `{CHANNEL_NAME}` | O rótulo do objeto retornado. |
| `{CHANNEL_VALUE}` | A coluna ou o campo que é o canal de destino da consulta. |
| `{EXP_TIMEOUT}` | A janela de tempo antes do evento de canal, em segundos, que a consulta pesquisa por um evento de primeiro contato. |
| `{EXP_CONDITION}` | A condição que determina o ponto de expiração do canal. |
| `{EXP_BEFORE}` | Um booleano que indica se o canal expira antes ou depois da condição especificada, `{EXP_CONDITION}`, que foi atendida. Isso é ativado principalmente para as condições de expiração de uma sessão, para garantir que o primeiro contato não seja selecionado em uma sessão anterior. Por padrão, esse valor está definido como `false`. |

## Componentes da coluna de resultados da consulta {#query-result-column-components}

Os resultados das consultas de atribuição são fornecidos na coluna `first_touch` ou `last_touch`. Essas colunas são compostas pelos seguintes componentes:

```console
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parâmetros | Descrição |
| ---------- | ----------- |
| `{NAME}` | O `{CHANNEL_NAME}`, inserido como um rótulo no ADF (Azure Data Fatory). |
| `{VALUE}` | O valor de `{CHANNEL_VALUE}` que é o último contato dentro do intervalo `{EXP_TIMEOUT}` especificado |
| `{TIMESTAMP}` | O carimbo de data/hora de [!DNL Experience Event] onde ocorreu o último contato |
| `{FRACTION}` | A atribuição do último contato, expresso como uma fração decimal. |

### Atribuição de primeiro contato {#first-touch}

A atribuição de primeiro contato credita 100% da responsabilidade por um resultado bem-sucedido ao canal inicial que o consumidor encontrou. Este exemplo de SQL é usado para destacar a interação que levou a uma série subsequente de ações do cliente.

A consulta abaixo retorna o valor da atribuição de primeiro contato e os detalhes do canal no conjunto de dados de destino [!DNL Experience Event]. Ele também retorna um objeto `struct` para o canal selecionado com o valor de primeiro contato, carimbo de data e hora e atribuição para cada linha.

>[!NOTE]
>
>A Experience Cloud ID (ECID) também é conhecida como MCID e continua a ser usada em namespaces.

**Sintaxe de consulta**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

Para obter uma lista completa de parâmetros possivelmente necessários e suas descrições, consulte a [seção de parâmetros de consulta de atribuição](#attribution-query-parameters).

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

Nos resultados abaixo, o código de rastreamento inicial `em:946426` é retirado do conjunto de dados [!DNL Experience Event]. Este código de rastreamento é atribuído com 100% (`1.0`) da responsabilidade pelas ações do cliente porque foi a primeira interação.

```console
                 id                 |       timestamp       | trackingCode |                   first_touch                   
|-----------------------------------+-----------------------+--------------+-------------------------------------------------
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

Para obter um detalhamento dos resultados exibidos na coluna `first_touch`, consulte a [seção de componentes da coluna](#query-result-column-components).

### Atribuição de último contato {#second-touch}

A atribuição Último contato credita 100% da responsabilidade por um resultado bem-sucedido ao último canal que o consumidor encontrou. Este exemplo de SQL é usado para destacar a interação final em uma série de ações do cliente.

A consulta retorna o valor da atribuição de último contato e os detalhes do canal no conjunto de dados de destino [!DNL Experience Event]. Ele também retorna um objeto `struct` para o canal selecionado com o valor de último contato, carimbo de data e hora e atribuição para cada linha.

**Sintaxe de consulta**

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

Nos resultados exibidos abaixo, o código de rastreamento no objeto retornado é a última interação em cada registro [!DNL Experience Event]. A cada código é atribuída uma responsabilidade de 100% (`1.0`) pelas ações do cliente, pois foi a última interação.

```console
                 id                |       timestamp       | trackingCode |                   last_touch                   
|-----------------------------------+-----------------------+--------------+-------------------------------------------------
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

Para obter um detalhamento dos resultados exibidos na coluna `last_touch`, consulte a [seção de componentes da coluna](#query-result-column-components).

### Atribuição de primeiro contato com condição de expiração {#first-touch-attribution-with-expiration-condition}

Esta consulta é usada para ver qual interação levou a uma série de ações do cliente em uma parte do conjunto de dados [!DNL Experience Event] determinada por uma condição de sua escolha.

A consulta retorna o valor e os detalhes da atribuição de primeiro contato para um único canal no conjunto de dados de destino [!DNL Experience Event], expirando após ou antes de uma condição. Ele também retorna um objeto `struct` com o valor de primeiro contato, carimbo de data e hora e atribuição para cada linha retornada para o canal selecionado.

**Sintaxe de consulta**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

Para obter uma lista completa de parâmetros possivelmente necessários e suas descrições, consulte a [seção de parâmetros de consulta de atribuição](#attribution-query-parameters).

**Exemplo de consulta**

No exemplo mostrado abaixo, uma compra é registrada (`commerce.purchases.value IS NOT NULL`) em cada um dos quatro dias mostrados nos resultados (15, 21, 23 e 29 de julho), e o código de rastreamento inicial em cada dia recebe 100% (`1.0`) de responsabilidade pelas ações do cliente.

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
|----------------------------------+-----------------------+--------------+-------------------------------------------------
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

Para obter um detalhamento dos resultados exibidos na coluna `first_touch`, consulte a [seção de componentes da coluna](#query-result-column-components).

### Atribuição de primeiro contato com tempo limite de expiração {#first-touch-attribution-with-expiration-timeout}

Essa consulta é usada para encontrar a interação, em um período selecionado, que levou à ação bem-sucedida do cliente.

A consulta abaixo retorna o valor e os detalhes da atribuição de primeiro contato para um único canal no conjunto de dados de destino [!DNL Experience Event] por um período especificado. A consulta retorna um objeto `struct` com o valor de primeiro contato, carimbo de data/hora e atribuição para cada linha retornada para o canal selecionado.

**Sintaxe de consulta**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

Para obter uma lista completa de parâmetros possivelmente necessários e suas descrições, consulte a [seção de parâmetros de consulta de atribuição](#attribution-query-parameters).

**Exemplo de consulta**

No exemplo mostrado abaixo, o primeiro contato retornado para cada ação do cliente é a interação mais antiga nos sete dias anteriores (expTimeout = 86400 * 7).

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
|-----------------------------------+-----------------------+--------------+-------------------------------------------------
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

Para obter um detalhamento dos resultados exibidos na coluna `first_touch`, consulte a [seção de componentes da coluna](#query-result-column-components).

### Atribuição de último contato com condição de expiração {#last-touch-attribution-with-expiration-condition}

Esta consulta é usada para localizar a última interação em uma série de ações do cliente em uma parte do conjunto de dados [!DNL Experience Event] determinada por uma condição de sua escolha.

A consulta abaixo retorna o valor e os detalhes da atribuição de último contato para um único canal no conjunto de dados de destino [!DNL Experience Event], expirando após ou antes de uma condição. A consulta retorna um objeto `struct` com o valor de último contato, carimbo de data/hora e atribuição para cada linha retornada para o canal selecionado.

**Sintaxe de consulta**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

Para obter uma lista completa de parâmetros possivelmente necessários e suas descrições, consulte a [seção de parâmetros de consulta de atribuição](#attribution-query-parameters).

**Exemplo de consulta**

No exemplo mostrado abaixo, uma compra é registrada (`commerce.purchases.value IS NOT NULL`) em cada um dos quatro dias mostrados nos resultados (15, 21, 23 e 29 de julho), e o último código de rastreamento em cada dia recebe 100% (`1.0`) de responsabilidade pelas ações do cliente.

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
|-----------------------------------+-----------------------+--------------+------------------------------------------------
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

Para obter um detalhamento dos resultados exibidos na coluna `last_touch`, consulte a [seção de componentes da coluna](#query-result-column-components).

### Atribuição de último contato com tempo limite de expiração {#last-touch-attribution-with-expiration-timeout}

Esta query é usada para localizar a última interação em um intervalo de tempo selecionado. A consulta retorna o valor e os detalhes da atribuição de último contato para um único canal no conjunto de dados de destino [!DNL Experience Event] por um período especificado. A consulta retorna um objeto `struct` com o valor de último contato, carimbo de data/hora e atribuição para cada linha retornada para o canal selecionado.

**Sintaxe de consulta**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

Para obter uma lista completa de parâmetros possivelmente necessários e suas descrições, consulte a [seção de parâmetros de consulta de atribuição](#attribution-query-parameters).

**Exemplo de consulta**

No exemplo mostrado abaixo, o último contato retornado para cada ação do cliente é a interação final nos sete dias seguintes (`expTimeout = 86400 * 7`).

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
|-----------------------------------+-----------------------+--------------+-------------------------------------------------
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

Para obter um detalhamento dos resultados exibidos na coluna `last_touch`, consulte a [seção de componentes da coluna](#query-result-column-components).
