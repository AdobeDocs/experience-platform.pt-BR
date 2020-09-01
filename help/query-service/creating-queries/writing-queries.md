---
keywords: Experience Platform;home;popular topics;query service;Query service;writing queries;writing query;
solution: Experience Platform
title: Gravando query
topic: queries
translation-type: tm+mt
source-git-commit: c5d3be4706ca6d6a30e203067db6ddc894b9bfb4
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 1%

---


# Orientações gerais para a execução de query em [!DNL Query Service]

Este documento detalha detalhes importantes a serem conhecidos ao escrever query no Adobe Experience Platform [!DNL Query Service].

Para obter informações detalhadas sobre a sintaxe SQL usada em [!DNL Query Service], leia a documentação [da sintaxe](../sql/syntax.md)SQL.

## Modelos de execução de query

A Adobe Experience Platform [!DNL Query Service] tem dois modelos de execução de query: interativo e não interativo. A execução interativa é usada para desenvolvimento de query e geração de relatórios em ferramentas de inteligência empresarial, enquanto a não interativa é usada para trabalhos maiores e query operacionais como parte de um fluxo de trabalho de processamento de dados.

### Execução interativa de query

Os query podem ser executados interativamente enviando-os por meio da [!DNL Query Service] interface do usuário ou [por meio de um cliente](../clients/overview.md)conectado. Ao executar [!DNL Query Service] por meio de um cliente conectado, uma sessão ativa é executada entre o cliente e [!DNL Query Service] até o query enviado retornar ou expirar.

A execução de query interativos tem as seguintes limitações:

| Parâmetro | Limitação |
| --------- | ---------- |
| Tempo limite do query | 10 minutos |
| Máximo de linhas retornadas | 50,000 |
| Máximo de query simultâneos | 5 |

>[!NOTE]
>
>Para substituir a limitação máxima de linhas, inclua `LIMIT 0` o query. O tempo limite de 10 minutos do query ainda se aplica.

Por padrão, os resultados de query interativos são retornados ao cliente e **não** são persistentes. Para persistir nos resultados como um conjunto de dados no, [!DNL Experience Platform]o query deve usar a `CREATE TABLE AS SELECT` sintaxe.

### Execução de query não interativos

Query enviados por meio da [!DNL Query Service] API são executados de forma não interativa. Execução não interativa significa que [!DNL Query Service] recebe a chamada da API e executa o query na ordem em que é recebido. Query não interativos sempre resultam na geração de um novo conjunto de dados para receber os resultados, ou na inserção de novas linhas em um conjunto de dados existente. [!DNL Experience Platform]

## Acessar um campo específico em um objeto

Para acessar um campo dentro de um objeto em seu query, é possível usar a notação de pontos (`.`) ou a notação de colchetes (`[]`). A instrução SQL a seguir usa a notação ponto para atravessar o `endUserIds` objeto até o `mcid` objeto.

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | O nome da sua tabela de análise. |

A instrução SQL a seguir usa a notação entre colchetes para atravessar o `endUserIds` objeto até o `mcid` objeto.

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

O `endUserIds._experience.mcid` objeto retornado contém os valores correspondentes para os seguintes parâmetros:

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

## Quando usar aspas simples, aspas de duplo e aspas traseiras

Esta seção explica quando usar aspas simples, aspas de duplo e aspas traseiras em query.

### Aspas únicas

A aspa única (`'`) é usada para criar strings de texto. Por exemplo, ele pode ser usado na `SELECT` declaração para retornar um valor de texto estático no resultado e na `WHERE` cláusula para avaliar o conteúdo de uma coluna.

O query a seguir declara um valor de texto estático (`'datasetA'`) para uma coluna:

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

O query a seguir usa uma sequência de caracteres com aspas simples (`'homepage'`) em sua cláusula WHERE para retornar eventos para uma página específica.

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
>As aspas de duplo **não podem** ser usadas com acesso ao campo de notação de ponto.

### Aspas anteriores

A citação anterior `` ` `` é usada para escapar de nomes de colunas reservados **somente** ao usar a sintaxe de notação de pontos. Por exemplo, como `order` é uma palavra reservada no SQL, você deve usar aspas para acessar o campo `commerce.order`:

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

Aspas traseiras **não** são necessárias se você estiver usando a notação entre colchetes.

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 LIMIT 10
```

## Próximas etapas

Ao ler este documento, você foi apresentado a algumas considerações importantes ao escrever query usando [!DNL Query Service]. Para obter mais informações sobre como usar a sintaxe SQL para gravar seus próprios query, leia a documentação [da sintaxe](../sql/syntax.md)SQL.