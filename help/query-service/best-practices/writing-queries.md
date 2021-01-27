---
keywords: Experience Platform;home;popular topics;query service;Query service;writing queries;writing query;
solution: Experience Platform
title: Gravando query
topic: queries
type: Tutorial
description: Este documento detalha detalhes importantes a serem conhecidos ao escrever query no Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: e2c648829bb3268ab319da934f5cc6cc811290b3
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 3%

---


# Orientações gerais para a execução de query em [!DNL Query Service]

Este documento detalha detalhes importantes a serem conhecidos ao gravar query no Adobe Experience Platform [!DNL Query Service].

Para obter informações detalhadas sobre a sintaxe SQL usada em [!DNL Query Service], leia a [documentação da sintaxe SQL](../sql/syntax.md).

## Modelos de execução de query

O Adobe Experience Platform [!DNL Query Service] tem dois modelos de execução de query: interativo e não interativo. A execução interativa é usada para desenvolvimento de query e geração de relatórios em ferramentas de inteligência empresarial, enquanto a não interativa é usada para trabalhos maiores e query operacionais como parte de um fluxo de trabalho de processamento de dados.

### Execução interativa de query

Os query podem ser executados interativamente enviando-os por meio da interface de usuário [!DNL Query Service] ou [por meio de um cliente conectado](../clients/overview.md). Ao executar [!DNL Query Service] por meio de um cliente conectado, uma sessão ativa é executada entre o cliente e [!DNL Query Service] até que o query enviado retorne ou atinja o tempo limite.

A execução de query interativos tem as seguintes limitações:

| Parâmetro | Limitação |
| --------- | ---------- |
| Tempo limite do query | 10 minutos |
| Máximo de linhas retornadas | 50 000 |
| Máximo de query simultâneos | 5 |

>[!NOTE]
>
>Para substituir a limitação máxima de linhas, inclua `LIMIT 0` no seu query. O tempo limite de 10 minutos do query ainda se aplica.

Por padrão, os resultados de query interativos são retornados para o cliente e **não** são persistentes. Para persistir nos resultados como um conjunto de dados em [!DNL Experience Platform], o query deve usar a sintaxe `CREATE TABLE AS SELECT`.

### Execução de query não interativos

Query enviados pela API [!DNL Query Service] são executados de forma não interativa. Execução não interativa significa que [!DNL Query Service] recebe a chamada da API e executa o query na ordem em que é recebido. Query não interativos sempre resultam na geração de um novo conjunto de dados em [!DNL Experience Platform] para receber os resultados, ou na inserção de novas linhas em um conjunto de dados existente.

## Acessar um campo específico em um objeto

Para acessar um campo dentro de um objeto em seu query, você pode usar a notação de pontos (`.`) ou a notação de colchetes (`[]`). A instrução SQL a seguir usa notação de pontos para atravessar o objeto `endUserIds` até o objeto `mcid`.

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | O nome da sua tabela de análise. |

A instrução SQL a seguir usa a notação de colchetes para atravessar o objeto `endUserIds` até o objeto `mcid`.

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | O nome da sua tabela de análise. |

>[!NOTE]
>
>Como cada tipo de notação retorna os mesmos resultados, o que você escolhe usar é de sua preferência.

Ambos os query de exemplo acima retornam um objeto nivelado, em vez de um único valor:

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

Quando a coluna é declarada somente para baixo no objeto, ela retorna o objeto inteiro como uma string. Para visualização somente da ID, use:

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

Aspas simples, aspas de duplo e aspas traseiras têm usos diferentes nos query de serviço do Query.

### Aspas únicas

A aspa única (`'`) é usada para criar strings de texto. Por exemplo, ele pode ser usado na instrução `SELECT` para retornar um valor de texto estático no resultado e na cláusula `WHERE` para avaliar o conteúdo de uma coluna.

O query a seguir declara um valor de texto estático (`'datasetA'`) para uma coluna:

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

O query a seguir usa uma string entre aspas simples (`'homepage'`) em sua cláusula WHERE para retornar eventos para uma página específica.

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
LIMIT 10
```

### citações de duplo

A citação do duplo (`"`) é usada para declarar um identificador com espaços.

O query a seguir usa aspas de duplo para retornar valores de colunas especificadas quando uma coluna contém um espaço em seu identificador:

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
>As aspas de duplo **não podem** ser usadas com acesso ao campo de notação de pontos.

### Aspas anteriores

A citação retroativa `` ` `` é usada para escapar de nomes de colunas reservados **somente** ao usar a sintaxe de notação de pontos. Por exemplo, como `order` é uma palavra reservada no SQL, você deve usar aspas retroativas para acessar o campo `commerce.order`:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

As aspas anteriores também são usadas para acessar um campo que start com um número. Por exemplo, para acessar o campo `30_day_value`, é necessário usar a notação de aspas.

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

As aspas traseiras são **não** necessárias se você estiver usando a notação entre colchetes.

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 LIMIT 10
```

## Exibição de informações da tabela

Depois de se conectar ao Query Service, você pode ver todas as tabelas disponíveis na Plataforma usando os comandos `\d` ou `SHOW TABLES`.

### Visualização de mesa padrão

O comando `\d` mostra a visualização PostgreSQL padrão para listar tabelas. Um exemplo da saída deste comando pode ser visto abaixo:

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

### Visualização detalhada da tabela

`SHOW TABLES` é um comando personalizado que fornece informações mais detalhadas sobre as tabelas. Um exemplo da saída deste comando pode ser visto abaixo:

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

### Informações sobre o schema

Para visualização de informações mais detalhadas sobre os schemas dentro da tabela, você pode usar o comando `\d {TABLE_NAME}`, onde `{TABLE_NAME}` é o nome da tabela cujas informações de schema você deseja visualização.

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

Além disso, você pode obter mais informações sobre uma coluna específica ao anexar o nome da coluna ao nome da tabela. Isso seria escrito no formato `\d {TABLE_NAME}_{COLUMN}`.

O exemplo a seguir mostra informações adicionais para a coluna `web` e seria chamado usando o seguinte comando: `\d luma_midvalues_web`:

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## Como participar de conjuntos de dados

É possível unir vários conjuntos de dados para incluir dados de outros conjuntos de dados no query.

O exemplo a seguir uniria os dois conjuntos de dados a seguir (`your_analytics_table` e `custom_operating_system_lookup`) e cria uma instrução `SELECT` para os 50 principais sistemas operacionais por número de visualizações de página.

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
| Windows Server 2003 e XP x64 Edition | 2883,0 |
| Android 4.1.1 | 24336,0 |
| Android 2.3.6 | 15735,0 |
| OSX 10.6 | 13357,0 |
| Windows Phone 7.5 | 11054,0 |
| Android 4.3 | 9221,0 |

## Desduplicação

O Serviço de query oferece suporte a dados desduplicação-duplicados ou à remoção de linhas de duplicado dos dados. Para obter mais informações sobre o desduplicação-duplicado, leia o [Guia desduplicação-duplicado do Serviço de Query](./deduplication.md).

## Próximas etapas

Ao ler este documento, você recebeu algumas considerações importantes ao escrever query usando [!DNL Query Service]. Para obter mais informações sobre como usar a sintaxe SQL para gravar seus próprios query, leia a [documentação da sintaxe SQL](../sql/syntax.md).

Para obter mais exemplos de query que podem ser usados no Query Service, leia os guias em [query de amostra Adobe Analytics](./adobe-analytics.md), [query de amostra Adobe Target](./adobe-target.md) ou [query de amostra ExperienceEvent](./experience-event-queries.md).