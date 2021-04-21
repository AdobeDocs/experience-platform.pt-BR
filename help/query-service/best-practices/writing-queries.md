---
keywords: Experience Platform, home, tópicos populares, serviço de consultas, serviço de consultas, gravação de consultas, gravação de consultas;
solution: Experience Platform
title: Orientações gerais para a execução de query no serviço de query
topic-legacy: queries
type: Tutorial
description: Este documento detalha detalhes importantes a saber ao gravar consultas no Adobe Experience Platform Query Service.
exl-id: a7076c31-8f7c-455e-9083-cbbb029c93bb
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 3%

---

# Orientações gerais para a execução da consulta em [!DNL Query Service]

Este documento detalha detalhes importantes a saber ao gravar consultas no Adobe Experience Platform [!DNL Query Service].

Para obter informações detalhadas sobre a sintaxe SQL usada em [!DNL Query Service], leia a [documentação da sintaxe SQL](../sql/syntax.md).

## Modelos de execução de query

Adobe Experience Platform [!DNL Query Service] tem dois modelos de execução de consulta: interativa e não interativa. A execução interativa é usada para desenvolvimento de consultas e geração de relatórios em ferramentas de business intelligence, enquanto a não interativa é usada para tarefas e consultas operacionais maiores como parte de um fluxo de trabalho de processamento de dados.

### Execução de query interativa

As consultas podem ser executadas interativamente enviando-as por meio da interface do usuário [!DNL Query Service] ou [por meio de um cliente conectado](../clients/overview.md). Ao executar [!DNL Query Service] por meio de um cliente conectado, uma sessão ativa é executada entre o cliente e [!DNL Query Service] até que a consulta enviada retorne ou expire.

A execução de query interativa tem as seguintes limitações:

| Parâmetro | Limitação |
| --------- | ---------- |
| Tempo limite da consulta | 10 minutos |
| Máximo de linhas retornadas | 50.000 |
| Máximo de consultas simultâneas | 5 |

>[!NOTE]
>
>Para substituir a limitação máxima de linhas, inclua `LIMIT 0` em sua query. O tempo limite da consulta de 10 minutos ainda é aplicado.

Por padrão, os resultados de consultas interativas são retornados ao cliente e **not** são persistentes. Para persistir os resultados como um conjunto de dados em [!DNL Experience Platform], a query deve usar a sintaxe `CREATE TABLE AS SELECT`.

### Execução de consulta não interativa

Consultas enviadas por meio da API [!DNL Query Service] são executadas de forma não interativa. Execução não interativa significa que [!DNL Query Service] recebe a chamada da API e executa a consulta na ordem em que é recebida. As consultas não interativas sempre resultam na geração de um novo conjunto de dados em [!DNL Experience Platform] para receber os resultados ou na inserção de novas linhas em um conjunto de dados existente.

## Acesso a um campo específico em um objeto

Para acessar um campo dentro de um objeto em sua query, você pode usar a notação de pontos (`.`) ou a notação de colchetes (`[]`). A instrução SQL a seguir usa a notação de pontos para atravessar o objeto `endUserIds` até o objeto `mcid`.

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | O nome da tabela de análise. |

A instrução SQL a seguir usa a notação de colchete para atravessar o objeto `endUserIds` até o objeto `mcid`.

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | O nome da tabela de análise. |

>[!NOTE]
>
>Como cada tipo de notação retorna os mesmos resultados, o que você escolhe usar é de sua preferência.

Ambas as consultas de exemplo acima retornam um objeto nivelado, em vez de um único valor:

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

O objeto `endUserIds._experience.mcid` retornado contém os valores correspondentes para os seguintes parâmetros:

- `id`
- `namespace`
- `primary`

Quando a coluna é declarada apenas para o objeto, ela retorna o objeto inteiro como uma string. Para exibir somente a ID, use:

```sql
SELECT endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

```console
     endUserIds._experience.mcid.id 
----------------------------------------
 48168239533518554367684086979667672499
(1 row)
```

## Aspas

Aspas simples, aspas duplas e aspas traseiras têm usos diferentes em consultas do Serviço de query.

### Aspas simples

A aspa simples (`'`) é usada para criar cadeias de texto. Por exemplo, ele pode ser usado na instrução `SELECT` para retornar um valor de texto estático no resultado e na cláusula `WHERE` para avaliar o conteúdo de uma coluna.

A consulta a seguir declara um valor de texto estático (`'datasetA'`) para uma coluna:

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

A consulta a seguir usa uma sequência de caracteres de aspas simples (`'homepage'`) em sua cláusula WHERE para retornar eventos de uma página específica.

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
LIMIT 10
```

### Aspas duplas

A aspa dupla (`"`) é usada para declarar um identificador com espaços.

A consulta a seguir usa aspas duplas para retornar valores de colunas especificadas quando uma coluna contém um espaço em seu identificador:

```sql
SELECT
  no_space_column,
  "space column"
FROM
( SELECT 
    'column1' as no_space_column,
    'column2' as "space column"
)
```

>[!NOTE]
>
>Aspas duplas **não podem** ser usadas com acesso ao campo de notação de pontos.

### Aspas atrás

A aspa traseira `` ` `` é usada para omitir nomes de colunas reservados **somente** ao usar sintaxe de notação de pontos. Por exemplo, como `order` é uma palavra reservada no SQL, você deve usar aspas retroativas para acessar o campo `commerce.order`:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

Aspas antigas também são usadas para acessar um campo que começa com um número. Por exemplo, para acessar o campo `30_day_value`, seria necessário usar a notação de aspas.

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

As aspas traseiras são **não** necessárias se você estiver usando a notação de colchetes.

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 LIMIT 10
```

## Exibindo informações da tabela

Depois de se conectar ao Serviço de query, você pode ver todas as tabelas disponíveis no Platform usando os comandos `\d` ou `SHOW TABLES`.

### Exibição de tabela padrão

O comando `\d` mostra a exibição padrão do PostgreSQL para listar tabelas. Um exemplo da saída deste comando pode ser visto abaixo:

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

### Exibição detalhada da tabela

`SHOW TABLES` é um comando personalizado que fornece informações mais detalhadas sobre as tabelas. Um exemplo da saída deste comando pode ser visto abaixo:

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

### Informações do esquema

Para exibir informações mais detalhadas sobre os schemas na tabela, você pode usar o comando `\d {TABLE_NAME}`, onde `{TABLE_NAME}` é o nome da tabela cujas informações de schema deseja exibir.

O exemplo a seguir mostra as informações do schema para a tabela `luma_midvalues`, que seria vista usando `\d luma_midvalues`:

```sql
                         Table "public.luma_midvalues"
      Column       |             Type            | Collation | Nullable | Default 
-------------------+-----------------------------+-----------+----------+---------
 timestamp         | timestamp                   |           |          | 
 _id               | text                        |           |          | 
 productlistitems  | anyarray                    |           |          | 
 commerce          | luma_midvalues_commerce     |           |          | 
 receivedtimestamp | timestamp                   |           |          | 
 enduserids        | luma_midvalues_enduserids   |           |          | 
 datasource        | datasource                  |           |          | 
 web               | luma_midvalues_web          |           |          | 
 placecontext      | luma_midvalues_placecontext |           |          | 
 identitymap       | anymap                      |           |          | 
 marketing         | marketing                   |           |          | 
 environment       | luma_midvalues_environment  |           |          | 
 _experience       | luma_midvalues__experience  |           |          | 
 device            | device                      |           |          | 
 search            | search                      |           |          | 
```

Além disso, é possível obter mais informações sobre uma coluna específica ao anexar o nome da coluna ao nome da tabela. Isso seria gravado no formato `\d {TABLE_NAME}_{COLUMN}`.

O exemplo a seguir mostra informações adicionais para a coluna `web` e seria chamado usando o seguinte comando: `\d luma_midvalues_web`:

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## Associar conjuntos de dados

É possível unir vários conjuntos de dados para incluir dados de outros conjuntos de dados em sua query.

O exemplo a seguir uniria os dois conjuntos de dados a seguir (`your_analytics_table` e `custom_operating_system_lookup`) e criará uma instrução `SELECT` para os 50 principais sistemas operacionais por número de exibições de página.

**Query**

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE TIMESTAMP >= ('2018-01-01') AND TIMESTAMP <= ('2018-12-31')
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

**Resultados**

| OperatingSystem | PageViews |
| --------------- | --------- |
| Windows 7 | 2781979,0 |
| Windows XP | 1669824,0 |
| Windows 8 | 420024,0 |
| Adobe AIR | 315032,0 |
| Windows Vista | 173566,0 |
| Mobile iOS 6.1.3 | 119069,0 |
| Linux | 56516,0 |
| OSX 10.6.8 | 53652,0 |
| Android 4.0.4 | 46167,0 |
| Android 4.0.3 | 31852,0 |
| Windows Server 2003 e XP x64 Edition | 28883,0 |
| Android 4.1.1 | 24336,0 |
| Android 2.3.6 | 15735,0 |
| OSX 10.6 | 13357,0 |
| Windows Phone 7.5 | 11054,0 |
| Android 4.3 | 9221,0 |

## Desduplicação

O Serviço de query oferece suporte à desduplicação de dados ou à remoção de linhas duplicadas dos dados. Para obter mais informações sobre desduplicação, leia o [Guia de desduplicação do serviço de consulta](./deduplication.md).

## Próximas etapas

Ao ler este documento, você foi apresentado a algumas considerações importantes ao gravar consultas usando [!DNL Query Service]. Para obter mais informações sobre como usar a sintaxe SQL para gravar suas próprias consultas, leia a [documentação da sintaxe SQL](../sql/syntax.md).

Para obter mais amostras de queries que podem ser usadas no Serviço de query, leia os guias em [Adobe Analytics sample queries](./adobe-analytics.md), [Adobe Target sample queries](./adobe-target.md) ou [ExperienceEvent sample queries](./experience-event-queries.md).
