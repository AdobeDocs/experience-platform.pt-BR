---
keywords: Experience Platform;home;tópicos populares;serviço de consulta;Serviço de consulta;sintaxe sql;ctas;CTAS;Criar tabela como selecionar
solution: Experience Platform
title: Sintaxe SQL no Serviço de consulta
description: Este documento detalha e explica a sintaxe SQL suportada pelo Adobe Experience Platform Query Service.
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '4686'
ht-degree: 1%

---

# Sintaxe SQL no Serviço de consulta

Você pode usar o ANSI SQL padrão para instruções `SELECT` e outros comandos limitados no Serviço de consulta do Adobe Experience Platform. Este documento aborda a sintaxe SQL suportada por [!DNL Query Service].

## Consultas SELECT {#select-queries}

A sintaxe a seguir define uma consulta `SELECT` com suporte de [!DNL Query Service]:

```sql
[ WITH with_query [, ...] ]
SELECT [ ALL | DISTINCT [( expression [, ...] ) ] ]
    [ * | expression [ [ AS ] output_name ] [, ...] ]
    [ FROM from_item [, ...] ]
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
    [ WHERE condition ]
    [ GROUP BY grouping_element [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT | MINUS } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start ]
```

A seção de guias abaixo fornece as opções disponíveis para as palavras-chave FROM, GROUP e WITH.

>[!BEGINTABS]

>[!TAB `from_item`]

```sql
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
```

```sql
[ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
```

```sql
with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
```

```sql
from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

>[!TAB `grouping_element`]

```sql
( )
```

```sql
expression
```

```sql
( expression [, ...] )
```

```sql
ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
```

```sql
CUBE ( { expression | ( expression [, ...] ) } [, ...] )
```

```sql
GROUPING SETS ( grouping_element [, ...] )
```

>[!TAB `with_query`]

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
```

>[!ENDTABS]

As subseções a seguir fornecem detalhes sobre as cláusulas adicionais que você pode usar em seus queries, desde que elas sigam o formato descrito acima.

### cláusula SNAPSHOT

Esta cláusula pode ser usada para ler incrementalmente os dados em uma tabela com base nas IDs do instantâneo. Uma ID de instantâneo é um marcador de ponto de verificação representado por um número tipo Long que é aplicado a uma tabela de data lake sempre que os dados são gravados nela. A cláusula `SNAPSHOT` anexa a si mesma à relação de tabela à qual é usada ao lado.

```sql
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
```

#### Exemplo

```sql
SELECT * FROM table_to_be_queried SNAPSHOT SINCE start_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT AS OF end_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN start_snapshot_id AND end_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN 'HEAD' AND start_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN end_snapshot_id AND 'TAIL';

SELECT * FROM (SELECT id FROM table_to_be_queried SNAPSHOT BETWEEN start_snapshot_id AND end_snapshot_id) C;

(SELECT * FROM table_to_be_queried SNAPSHOT SINCE start_snapshot_id) a
  INNER JOIN 
(SELECT * from table_to_be_joined SNAPSHOT AS OF your_chosen_snapshot_id) b 
  ON a.id = b.id;
```

>[!NOTE]
>
>Ao usar `HEAD` ou `TAIL` em uma cláusula `SNAPSHOT`, você deve envolvê-los entre aspas simples (por exemplo, &#39;HEAD&#39;, &#39;TAIL&#39;). Usá-los sem aspas resulta em um erro de sintaxe.

A tabela abaixo explica o significado de cada opção de sintaxe na cláusula SNAPSHOT.

| Sintaxe | Significado |
|-------------------------------------------------------------------|------------------------------------------------------------------------------------------|
| `SINCE start_snapshot_id` | Lê dados iniciando da ID de instantâneo especificada (exclusivo). |
| `AS OF end_snapshot_id` | Lê os dados como estavam na ID de instantâneo especificada (inclusive). |
| `BETWEEN start_snapshot_id AND end_snapshot_id` | Lê dados entre as IDs de instantâneo de início e término especificadas. É exclusivo de `start_snapshot_id` e inclui de `end_snapshot_id`. |
| `BETWEEN HEAD AND start_snapshot_id` | Lê dados desde o início (antes do primeiro instantâneo) até a ID de instantâneo inicial especificada (inclusive). Observe que isso retorna somente linhas em `start_snapshot_id`. |
| `BETWEEN end_snapshot_id AND TAIL` | Lê dados logo após o `end_snapshot_id` especificado até o final do conjunto de dados (excluindo a ID do instantâneo). Isso significa que se `end_snapshot_id` for o último instantâneo no conjunto de dados, a consulta retornará zero linhas porque não há instantâneos além do último instantâneo. |
| `SINCE start_snapshot_id INNER JOIN table_to_be_joined AS OF your_chosen_snapshot_id ON table_to_be_queried.id = table_to_be_joined.id` | Lê dados iniciando a partir da ID de instantâneo especificada de `table_to_be_queried` e une-os com os dados de `table_to_be_joined` como estavam em `your_chosen_snapshot_id`. A associação é baseada em IDs correspondentes das colunas ID das duas tabelas que estão sendo unidas. |

Uma cláusula `SNAPSHOT` funciona com um alias de tabela ou tabela, mas não sobre uma subconsulta ou exibição. Uma cláusula `SNAPSHOT` funciona em qualquer lugar que uma consulta `SELECT` em uma tabela possa ser aplicada.

Além disso, você pode usar `HEAD` e `TAIL` como valores de deslocamento especiais para cláusulas de instantâneo. O uso de `HEAD` refere-se a um deslocamento antes do primeiro instantâneo, enquanto `TAIL` refere-se a um deslocamento após o último instantâneo.

>[!NOTE]
>
>Se você estiver consultando entre duas IDs de instantâneo, os dois cenários a seguir poderão ocorrer se o instantâneo de início expirar e o sinalizador de comportamento de fallback opcional (`resolve_fallback_snapshot_on_failure`) estiver definido:
>
>- Se o sinalizador de comportamento de fallback opcional estiver definido, o Serviço de Consulta escolherá o instantâneo disponível mais antigo, o definirá como o instantâneo inicial e retornará os dados entre o instantâneo disponível mais antigo e o instantâneo final especificado. Estes dados são **inclusivos** do instantâneo mais antigo disponível.

### Cláusula WHERE

Por padrão, correspondências produzidas por uma cláusula `WHERE` em uma consulta `SELECT` fazem distinção entre maiúsculas e minúsculas. Se você quiser que as correspondências não diferenciem maiúsculas de minúsculas, poderá usar a palavra-chave `ILIKE` em vez de `LIKE`.

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

A lógica das cláusulas LIKE e ILIKE é explicada na tabela a seguir:

| Cláuso | Operador |
| ------ | -------- |
| `WHERE condition LIKE pattern` | `~~` |
| `WHERE condition NOT LIKE pattern` | `!~~` |
| `WHERE condition ILIKE pattern` | `~~*` |
| `WHERE condition NOT ILIKE pattern` | `!~~*` |

**Exemplo**

```sql
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

Esta consulta retorna clientes com nomes que começam com &quot;A&quot; ou &quot;a&quot;.

### ASSOCIAR-SE

Uma consulta `SELECT` que usa junções tem a seguinte sintaxe:

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### UNIÃO, INTERSEÇÃO e EXCETO

As cláusulas `UNION`, `INTERSECT` e `EXCEPT` são usadas para combinar ou excluir linhas semelhantes de duas ou mais tabelas:

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### CRIAR TABELA COMO SELECIONAR {#create-table-as-select}

Use o comando `CREATE TABLE AS SELECT` (CTAS) para materializar os resultados de uma consulta `SELECT` em uma nova tabela. Isso é útil para criar conjuntos de dados transformados, executar agregações ou visualizar dados com recursos projetados antes de usá-los em um modelo.

Se você estiver pronto para treinar um modelo usando recursos transformados, consulte a [Documentação de modelos](../advanced-statistics/models.md) para obter orientação sobre como usar `CREATE MODEL` com a cláusula `TRANSFORM`.

Opcionalmente, você pode incluir uma cláusula `TRANSFORM` para aplicar uma ou mais funções de engenharia de recursos diretamente na instrução CTAS. Use o `TRANSFORM` para inspecionar os resultados da sua lógica de transformação antes do treinamento do modelo.

Essa sintaxe se aplica às tabelas permanentes e temporárias.

```sql
CREATE TABLE table_name 
  [WITH (schema='target_schema_title', rowvalidation='false', label='PROFILE')] 
  [TRANSFORM (transformFunctionExpression1, transformFunctionExpression2, ...)]
AS (select_query)
```

```sql
CREATE TEMP TABLE table_name 
  [WITH (schema='target_schema_title', rowvalidation='false', label='PROFILE')] 
  [TRANSFORM (transformFunctionExpression1, transformFunctionExpression2, ...)]
AS (select_query)
```

| Parâmetro | Descrição |
| ----- | ----- |
| `schema` | O título do esquema XDM. Use essa cláusula somente se desejar associar a nova tabela a um esquema XDM existente. |
| `rowvalidation` | (Opcional) Permite a validação em nível de linha para cada lote assimilado no conjunto de dados. O padrão é verdadeiro. |
| `label` | (Opcional) Use o valor `PROFILE` para rotular o conjunto de dados como habilitado para assimilação de Perfil. |
| `transform` | (Opcional) Aplica transformações de engenharia de recursos (como indexação de sequência, codificação com um único acesso ou TF-IDF) antes de materializar o conjunto de dados. Essa cláusula é usada para visualizar recursos transformados. Consulte a documentação da cláusula [`TRANSFORM`](#transform) para obter mais detalhes. |
| `select_query` | Uma instrução `SELECT` padrão que define o conjunto de dados. Consulte a [`SELECT` seção de consultas](#select-queries) para obter mais detalhes. |

>[!NOTE]
>
>A instrução `SELECT` deve incluir um alias para funções de agregação como `COUNT`, `SUM` ou `MIN`. Você pode fornecer a consulta `SELECT` com ou sem parênteses. Isso se aplica independentemente da cláusula `TRANSFORM` ser usada ou não.

**Exemplos**

Um exemplo básico usando uma cláusula `TRANSFORM` para visualizar alguns recursos projetados:

```sql
CREATE TABLE ctas_transform_table_vp14 
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments
)
AS SELECT * FROM movie_review_e2e_DND;
```

Um exemplo mais avançado com várias etapas de transformação:

```sql
CREATE TABLE ctas_transform_table 
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments,
  stop_words_remover(token_comments, array('and','very','much')) stp_token,
  ngram(stp_token, 3) ngram_token,
  tf_idf(ngram_token, 20) ngram_idf,
  count_vectorizer(stp_token, 13) cnt_vec_comments,
  tf_idf(token_comments, 10, 1) as cmts_idf
)
AS SELECT * FROM movie_review;
```

Um exemplo de tabela temporária:

```sql
CREATE TEMP TABLE ctas_transform_table 
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments,
  stop_words_remover(token_comments, array('and','very','much')) stp_token,
  ngram(stp_token, 3) ngram_token,
  tf_idf(ngram_token, 20) ngram_idf,
  count_vectorizer(stp_token, 13) cnt_vec_comments,
  tf_idf(token_comments, 10, 1) as cmts_idf
)
AS SELECT * FROM movie_review;
```

#### Limitações e comportamento {#limitations-and-behavior}

Lembre-se das seguintes limitações ao usar a cláusula `TRANSFORM` com `CREATE TABLE` ou `CREATE TEMP TABLE`:

- Se qualquer função de transformação gerar uma saída de vetor, ela será convertida automaticamente em uma matriz.
- Como resultado, tabelas criadas usando `TRANSFORM` não podem ser usadas diretamente em instruções `CREATE MODEL`. Você deve redefinir a lógica de transformação durante a criação do modelo para gerar os vetores de recursos apropriados.
- As transformações são aplicadas somente durante a criação da tabela. Os novos dados inseridos na tabela com `INSERT INTO` são **não transformados automaticamente**. Para aplicar transformações a novos dados, você deve recriar a tabela usando `CREATE TABLE AS SELECT` com a cláusula `TRANSFORM`.
- Esse método se destina à visualização e validação de transformações em um ponto no tempo, não para a criação de pipelines de transformação reutilizáveis.

>[!NOTE]
>
>Para obter mais detalhes sobre as funções de transformação disponíveis e seus tipos de saída, consulte [Tipos de dados de saída de transformação de recurso](../advanced-statistics/feature-transformation.md#available-transformations).


### Cláusula TRANSFORM {#transform}

Use a cláusula `TRANSFORM` para aplicar uma ou mais funções de engenharia de recursos a um conjunto de dados antes do treinamento de modelo ou da criação de tabela. Essa cláusula permite visualizar, validar ou definir a forma exata dos recursos de entrada.

A cláusula `TRANSFORM` pode ser usada nas seguintes instruções:

- `CREATE MODEL`
- `CREATE TABLE`
- `CREATE TEMP TABLE`

Consulte a [Documentação de modelos](../advanced-statistics/models.md) para obter instruções detalhadas sobre como usar CREATE MODEL, incluindo como definir transformações, definir opções de modelo e configurar dados de treinamento.

Para uso com `CREATE TABLE`, consulte a [seção CREATE TABLE AS SELECT](#create-table-as-select).

#### Exemplo de CRIAR MODELO

```sql
CREATE MODEL review_model
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) AS ohe_add_comments,
  tokenizer(comments) AS token_comments,
  stop_words_remover(token_comments, array('and','very','much')) AS stp_token,
  ngram(stp_token, 3) AS ngram_token,
  tf_idf(ngram_token, 20) AS ngram_idf,
  count_vectorizer(stp_token, 13) AS cnt_vec_comments,
  tf_idf(token_comments, 10, 1) AS cmts_idf,
  vector_assembler(array(cmts_idf, viewsgot, ohe_add_comments, ngram_idf, cnt_vec_comments)) AS features
)
OPTIONS(MODEL_TYPE='logistic_reg', LABEL='reviews')
AS SELECT * FROM movie_review_e2e_DND;
```

#### Limitações {#limitations}

As limitações a seguir aplicam-se ao usar `TRANSFORM` com `CREATE TABLE`. Consulte a seção `CREATE TABLE AS SELECT` limitações e comportamento para obter uma explicação detalhada de como os dados transformados são armazenados, como as saídas de vetor são tratadas e por que os resultados não podem ser reutilizados diretamente em fluxos de trabalho de treinamento de modelo.

- Saídas de vetor são convertidas automaticamente em matrizes, que não podem ser usadas diretamente em `CREATE MODEL`.
- A lógica de transformação não é mantida como metadados e não pode ser reutilizada em lotes.

## INSERIR EM

O comando `INSERT INTO` é definido da seguinte maneira:

>[!IMPORTANT]
>
>O Serviço de Consulta oferece suporte a **operações somente acréscimo** usando o mecanismo ITAS. `INSERT INTO` é o único comando de manipulação de dados com suporte; as operações **update** e **delete** não estão disponíveis. Para refletir as alterações em seus dados, insira novos registros que representem o estado desejado.

```sql
INSERT INTO table_name select_query
```

| Parâmetros | Descrição |
| ----- | ----- |
| `table_name` | O nome da tabela na qual você deseja inserir a consulta. |
| `select_query` | Uma instrução `SELECT`. A sintaxe da consulta `SELECT` pode ser encontrada na [seção de consultas SELECT](#select-queries). |

**Exemplo**

>[!NOTE]
>
>Veja a seguir um exemplo planejado e apenas para fins de instrução.

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!INFO]
> 
>**não** coloque a instrução `SELECT` entre parênteses (). Além disso, o esquema do resultado da instrução `SELECT` deve estar em conformidade com o da tabela definida na instrução `INSERT INTO`. Você pode fornecer uma cláusula `SNAPSHOT` para ler deltas incrementais na tabela de destino.

A maioria dos campos em um esquema XDM real não é encontrada no nível raiz e o SQL não permite o uso da notação de pontos. Para obter um resultado realista usando campos aninhados, mapeie cada campo no caminho `INSERT INTO`.

Para `INSERT INTO` caminhos aninhados, use a seguinte sintaxe:

```sql
INSERT INTO [dataset]
SELECT struct([source field1] as [target field in schema],
[source field2] as [target field in schema],
[source field3] as [target field in schema]) [tenant name]
FROM [dataset]
```

**Exemplo**

```sql
INSERT INTO Customers SELECT struct(SupplierName as Supplier, City as SupplierCity, Country as SupplierCountry) _Adobe FROM OnlineCustomers;
```

## SOLTAR TABELA

O comando `DROP TABLE` remove uma tabela existente e exclui o diretório associado à tabela do sistema de arquivos se ela não for uma tabela externa. Se a tabela não existir, ocorrerá uma exceção.

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

| Parâmetros | Descrição |
| ------ | ------ |
| `IF EXISTS` | Se isso for especificado, nenhuma exceção será lançada se a tabela **não** existir. |

## CRIAR BANCO DE DADOS

O comando `CREATE DATABASE` cria um banco de dados do Azure Data Lake Storage (ADLS).

```sql
CREATE DATABASE [IF NOT EXISTS] db_name
```

## SOLTAR BANCO DE DADOS

O comando `DROP DATABASE` exclui o banco de dados de uma instância.

```sql
DROP DATABASE [IF EXISTS] db_name
```

| Parâmetros | Descrição |
| ------ | ------ |
| `IF EXISTS` | Se isso for especificado, nenhuma exceção será lançada se o banco de dados **não** existir. |

## SOLTAR ESQUEMA

O comando `DROP SCHEMA` descarta um esquema existente.

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

| Parâmetros | Descrição |
| ------ | ------ |
| `IF EXISTS` | Se este parâmetro for especificado e o esquema **não** existir, nenhuma exceção será lançada. |
| `RESTRICT` | O valor padrão do modo. Se especificado, o esquema só será descartado se **não** contiver tabelas. |
| `CASCADE` | Se especificado, o esquema é descartado junto com todas as tabelas presentes no esquema. |

## CRIAR VISUALIZAÇÃO {#create-view}

Uma exibição SQL é uma tabela virtual baseada no conjunto de resultados de uma instrução SQL. Crie uma exibição com a instrução `CREATE VIEW` e dê um nome a ela. Você pode usar esse nome para se referir aos resultados da query. Isso facilita a reutilização de consultas complexas.

A sintaxe a seguir define uma consulta `CREATE VIEW` para um conjunto de dados. Esse conjunto de dados pode ser um ADLS ou um conjunto de dados de armazenamento acelerado.

```sql
CREATE VIEW view_name AS select_query
```

| Parâmetros | Descrição |
| ------ | ------ |
| `view_name` | O nome da exibição a ser criada. |
| `select_query` | Uma instrução `SELECT`. A sintaxe da consulta `SELECT` pode ser encontrada na [seção de consultas SELECT](#select-queries). |

**Exemplo**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

A sintaxe a seguir define uma consulta `CREATE VIEW` que cria uma exibição no contexto de um banco de dados e esquema.

**Exemplo**

```sql
CREATE VIEW db_name.schema_name.view_name AS select_query
CREATE OR REPLACE VIEW db_name.schema_name.view_name AS select_query
```

| Parâmetros | Descrição |
| ------ | ------ |
| `db_name` | O nome do banco de dados. |
| `schema_name` | O nome do esquema. |
| `view_name` | O nome da exibição a ser criada. |
| `select_query` | Uma instrução `SELECT`. A sintaxe da consulta `SELECT` pode ser encontrada na [seção de consultas SELECT](#select-queries). |

**Exemplo**

```sql
CREATE VIEW <dbV1 AS SELECT color, type FROM Inventory;

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory;
```

## MOSTRAR EXIBIÇÕES

A consulta a seguir mostra a lista de exibições.

```sql
SHOW VIEWS;
```

```console
 Db Name  | Schema Name | Name  | Id       |  Dataset Dependencies | Views Dependencies | TYPE
|----------------------------------------------------------------------------------------------
 qsaccel  | profile_agg | view1 | view_id1 | dwh_dataset1          |                    | DWH
          |             | view2 | view_id2 | adls_dataset          | adls_views         | ADLS
(2 rows)
```

## SOLTAR VISUALIZAÇÃO

A sintaxe a seguir define uma consulta `DROP VIEW`:

```sql
DROP VIEW [IF EXISTS] view_name
```

| Parâmetros | Descrição |
| ------ | ------ |
| `IF EXISTS` | Se isso for especificado, nenhuma exceção será lançada se a exibição **não** existir. |
| `view_name` | O nome da exibição a ser excluída. |

**Exemplo**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## Bloqueio anônimo {#anonymous-block}

Um bloco anônimo consiste em duas seções: executável e seções de manipulação de exceções. Em um bloco anônimo, a seção executável é obrigatória. No entanto, a seção de tratamento de exceções é opcional.

O exemplo a seguir mostra como criar um bloco com uma ou mais instruções a serem executadas juntas:

```sql
$$BEGIN
  statementList
[EXCEPTION exceptionHandler]
$$END

exceptionHandler:
      WHEN OTHER
      THEN statementList

statementList:
    : (statement (';')) +
```

Veja abaixo um exemplo de uso de bloco anônimo.

```sql
$$BEGIN
   SET @v_snapshot_from = select parent_id  from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_snapshot_to = select snapshot_id from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_log_id = select now();
   CREATE TABLE tracking_email_id_incrementally
     AS SELECT _id AS id FROM email_tracking_experience_event_dataset SNAPSHOT BETWEEN @v_snapshot_from AND @v_snapshot_to;

EXCEPTION
  WHEN OTHER THEN
    DROP TABLE IF EXISTS tracking_email_id_incrementally;
    SELECT 'ERROR';
$$END;
```

### Instruções condicionais em um bloco anônimo {#conditional-anonymous-block-statements}

A estrutura de controle IF-THEN-ELSE permite a execução condicional de uma lista de instruções quando uma condição é avaliada como TRUE. Essa estrutura de controle só é aplicável em um bloco anônimo. Se essa estrutura for usada como um comando independente, ela resultará em um erro de sintaxe (&quot;Comando inválido fora do Bloco anônimo&quot;).

O trecho de código abaixo demonstra o formato correto de uma declaração condicional IF-THEN-ELSE em um bloco anônimo.

```javascript
IF booleanExpression THEN
   List of statements;
ELSEIF booleanExpression THEN 
   List of statements;
ELSEIF booleanExpression THEN 
   List of statements;
ELSE
   List of statements;
END IF
```

**Exemplo**

O exemplo abaixo executa `SELECT 200;`.

```sql
$$BEGIN
    SET @V = SELECT 2;
    SELECT @V;
    IF @V = 1 THEN
       SELECT 100;
    ELSEIF @V = 2 THEN
       SELECT 200;
    ELSEIF @V = 3 THEN
       SELECT 300;
    ELSE    
       SELECT 'DEFAULT';
    END IF;   

 END$$;
```

Esta estrutura pode ser usada com `raise_error();` para retornar uma mensagem de erro personalizada. O bloco de código visto abaixo encerra o bloco anônimo com &quot;mensagem de erro personalizada&quot;.

**Exemplo**

```sql
$$BEGIN
    SET @V = SELECT 5;
    SELECT @V;
    IF @V = 1 THEN
       SELECT 100;
    ELSEIF @V = 2 THEN
       SELECT 200;
    ELSEIF @V = 3 THEN
       SELECT 300;
    ELSE    
       SELECT raise_error('custom error message');
    END IF;   

 END$$;
```

#### Instruções IF aninhadas

Instruções IF aninhadas são suportadas em blocos anônimos.

**Exemplo**

```sql
$$BEGIN
    SET @V = SELECT 1;
    IF @V = 1 THEN
       SELECT 100;
       IF @V > 0 THEN
         SELECT 1000;
       END IF;   
    END IF;   

 END$$; 
```

#### Blocos de exceção

Blocos de exceção são suportados em blocos anônimos.

**Exemplo**

```sql
$$BEGIN
    SET @V = SELECT 2;
    IF @V = 1 THEN
       SELECT 100;
    ELSEIF @V = 2 THEN
       SELECT raise_error(concat('custom-error for v= ', '@V' ));

    ELSEIF @V = 3 THEN
       SELECT 300;
    ELSE    
       SELECT 'DEFAULT';
    END IF;  
EXCEPTION WHEN OTHER THEN 
  SELECT 'THERE WAS AN ERROR';    
 END$$;
```

### Auto para JSON {#auto-to-json}

O Serviço de consulta oferece suporte a uma configuração opcional no nível da sessão para retornar campos complexos de nível superior de consultas SELECT interativas como cadeias de caracteres JSON. A configuração `auto_to_json` permite que dados de campos complexos sejam retornados como JSON e depois analisados em objetos JSON usando bibliotecas padrão.

DEFINA o sinalizador de recurso `auto_to_json` como true antes de executar a consulta SELECT que contém campos complexos.

```sql
set auto_to_json=true; 
```

#### Antes de definir o sinalizador `auto_to_json`

A tabela a seguir fornece um exemplo de resultado de consulta antes da aplicação da configuração `auto_to_json`. A mesma consulta SELECT (como visto abaixo) que segmenta uma tabela com campos complexos foi usada em ambos os cenários.

```sql
SELECT * FROM TABLE_WITH_COMPLEX_FIELDS LIMIT 2;
```

Os resultados são os seguintes:

```console
                _id                |                                _experience                                 | application  |                   commerce                   | dataSource |                               device                               |                       endUserIDs                       |                                                                                                environment                                                                                                |                     identityMap                     |                              placeContext                               |   receivedTimestamp   |       timestamp       | userActivityRegion |                                         web                                          | _adcstageforpqs
|-----------------------------------+----------------------------------------------------------------------------+--------------+----------------------------------------------+------------+--------------------------------------------------------------------+--------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------+-------------------------------------------------------------------------+-----------------------+-----------------------+--------------------+--------------------------------------------------------------------------------------+-----------------
 31892EE15DE00000-401D52664FF48A52 | ("("("(1,1)","(1,1)")","(-209479095,4085488201,-2105158467,2189808829)")") | (background) | (NULL,"(USD,NULL)",NULL,NULL,NULL,NULL,NULL) | (475341)   | (32,768,1024,205202,https://ns.adobe.com/xdm/external/deviceatlas) | ("("(31892EE080007B35-E6CE00000000000,"(AAID)",t)")")  | ("(en-US,f,f,t,1.6,"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7",490,1125)",xo.net,64.3.235.13)     | [AAID -> "{(31892EE080007B35-E6CE00000000000,t)}"]  | ("("(34.01,-84.0)",lawrenceville,US,524,30043,ga)",600)                 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | (UT1)              | ("(f,Search Results,"(1.0)")","(http://www.google.com/search?ie=UTF-8&q=,internal)") |
 31892EE15DE00000-401B92664FF48AE8 | ("("("(1,1)","(1,1)")","(-209479095,4085488201,-2105158467,2189808829)")") | (background) | (NULL,"(USD,NULL)",NULL,NULL,NULL,NULL,NULL) | (475341)   | (32,768,1024,205202,https://ns.adobe.com/xdm/external/deviceatlas) | ("("(31892EE100007BF3-215FE00000000001,"(AAID)",t)")") | ("(en-US,f,f,t,1.5,"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7",768,556)",ntt.net,219.165.108.145) | [AAID -> "{(31892EE100007BF3-215FE00000000001,t)}"] | ("("(34.989999999999995,138.42)",shizuoka,JP,392005,420-0812,22)",-240) | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | (UT1)              | ("(f,Home - JJEsquire,"(1.0)")","(NULL,typed_bookmarked)")                           |
(2 rows)  
```

#### Depois de definir o sinalizador `auto_to_json`

A tabela a seguir demonstra a diferença nos resultados que a configuração `auto_to_json` tem no conjunto de dados resultante. A mesma consulta SELECT foi usada em ambos os cenários.

```console
                _id                |   receivedTimestamp   |       timestamp       |                                                                                                                   _experience                                                                                                                   |           application            |             commerce             |    dataSource    |                                                                  device                                                                   |                                                   endUserIDs                                                   |                                                                                                                                                                                           environment                                                                                                                                                                                            |                             identityMap                              |                                                                                            placeContext                                                                                            |      userActivityRegion      |                                                                                     web                                                                                      | _adcstageforpqs
|-----------------------------------+-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+----------------------------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------
 31892EE15DE00000-401D52664FF48A52 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE080007B35-E6CE00000000000","namespace":{"code":"AAID"},"primary":true}}}  | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.6","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":490,"viewportWidth":1125},"domain":"xo.net","ipV4":"64.3.235.13"}     | {"AAID":[{"id":"31892EE080007B35-E6CE00000000000","primary":true}]}  | {"geo":{"_schema":{"latitude":34.01,"longitude":-84.0},"city":"lawrenceville","countryCode":"US","dmaID":524,"postalCode":"30043","stateProvince":"ga"},"localTimezoneOffset":600}                 | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Search Results","pageViews":{"value":1.0}},"webReferrer":{"URL":"http://www.google.com/search?ie=UTF-8&q=","type":"internal"}} |
 31892EE15DE00000-401B92664FF48AE8 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE100007BF3-215FE00000000001","namespace":{"code":"AAID"},"primary":true}}} | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.5","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":768,"viewportWidth":556},"domain":"ntt.net","ipV4":"219.165.108.145"} | {"AAID":[{"id":"31892EE100007BF3-215FE00000000001","primary":true}]} | {"geo":{"_schema":{"latitude":34.989999999999995,"longitude":138.42},"city":"shizuoka","countryCode":"JP","dmaID":392005,"postalCode":"420-0812","stateProvince":"22"},"localTimezoneOffset":-240} | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Home - JJEsquire","pageViews":{"value":1.0}},"webReferrer":{"type":"typed_bookmarked"}}                                        |
(2 rows)
```

### Resolver instantâneo de fallback em caso de falha {#resolve-fallback-snapshot-on-failure}

A opção `resolve_fallback_snapshot_on_failure` é usada para resolver o problema de uma ID de instantâneo expirada.

Defina a opção `resolve_fallback_snapshot_on_failure` como true para substituir um instantâneo por uma ID de instantâneo anterior.

```sql
SET resolve_fallback_snapshot_on_failure=true;
```

A linha de código a seguir substitui o `@from_snapshot_id` pelo `snapshot_id` mais antigo disponível nos metadados.

```sql
$$ BEGIN
    SET resolve_fallback_snapshot_on_failure=true;
    SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                            (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                on a.process_timestamp=b.process_timestamp;
    SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
    SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
    INSERT INTO DIM_TABLE_ABC_Incremental
     SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);

Insert Into
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
      cast( @to_snapshot_id AS string) last_snapshot_id,
      cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
EXCEPTION
  WHEN OTHER THEN
    SELECT 'ERROR';
END
$$;
```


## Organização do ativo de dados

É importante organizar logicamente seus ativos de dados no data lake da Adobe Experience Platform à medida que eles crescem. O Serviço de consulta estende as construções SQL que permitem agrupar logicamente os ativos de dados em uma sandbox. Esse método de organização permite o compartilhamento de ativos de dados entre esquemas sem a necessidade de movê-los fisicamente.

As seguintes construções SQL usando sintaxe SQL padrão são compatíveis para que você organize logicamente seus dados.

```SQL
CREATE DATABASE dg1;
CREATE SCHEMA dg1.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

Consulte o guia [organização lógica de ativos de dados](../best-practices/organize-data-assets.md) para obter uma explicação mais detalhada sobre as práticas recomendadas do Serviço de consulta.

## A tabela existe

O comando SQL `table_exists` é usado para confirmar se uma tabela existe atualmente no sistema. O comando retorna um valor booleano: `true` se a tabela **existir**, e `false` se a tabela existir **não**.

Ao validar se uma tabela existe antes de executar as instruções, o recurso `table_exists` simplifica o processo de gravação de um bloco anônimo para abranger os casos de uso `CREATE` e `INSERT INTO`.

A sintaxe a seguir define o comando `table_exists`:

```SQL
$$
BEGIN

#Set mytableexist to true if the table already exists.
SET @mytableexist = SELECT table_exists('target_table_name');

#Create the table if it does not already exist (this is a one time operation).
CREATE TABLE IF NOT EXISTS target_table_name AS
  SELECT *
  FROM   profile_dim_date limit 10;

#Insert data only if the table already exists. Check if @mytableexist = 'true'
 INSERT INTO target_table_name           (
                     select *
                     from   profile_dim_date
                     WHERE  @mytableexist = 'true' limit 20
              ) ;
EXCEPTION
WHEN other THEN SELECT 'ERROR';

END $$; 
```

## Em linha {#inline}

A função `inline` separa os elementos de uma matriz de structs e gera os valores em uma tabela. Ele só pode ser colocado na lista `SELECT` ou em um `LATERAL VIEW`.

A função `inline` **não pode** ser colocada em uma lista de seleção onde há outras funções geradoras.

Por padrão, as colunas produzidas são nomeadas como &quot;col1&quot;, &quot;col2&quot; e assim por diante. Se a expressão for `NULL`, nenhuma linha será produzida.

>[!TIP]
>
>Nomes de colunas podem ser renomeados usando o comando `RENAME`.

**Exemplo**

```sql
> SELECT inline(array(struct(1, 'a'), struct(2, 'b'))), 'Spark SQL';
```

O exemplo retorna o seguinte:

```text
1  a Spark SQL
2  b Spark SQL
```

Este segundo exemplo demonstra ainda mais o conceito e a aplicação da função `inline`. O modelo de dados para o exemplo está ilustrado na imagem abaixo.

![Um diagrama de esquema para productListItems.](../images/sql/productListItems.png)

**Exemplo**

```sql
select inline(productListItems) from source_dataset limit 10;
```

Os valores obtidos de `source_dataset` são usados para preencher a tabela de destino.

| SKU | _experience | quantidade | priceTotal |
|---------------------|-----------------------------------|----------|--------------|
| product-id-1 | (&quot;(&quot;(&quot;(A,pass,B,NULL)&quot;)&quot;)&quot; | 5 | 10,5 |
| product-id-5 | (&quot;(&quot;(&quot;(A, pass, B,NULL)&quot;)&quot;)&quot; |          |              |
| product-id-2 | (&quot;(&quot;(&quot;(AF, C, D,NULL)&quot;)&quot;) | 6 | 40 |
| product-id-4 | (&quot;(&quot;(&quot;(BM, pass, NA,NULL)&quot;)&quot;)&quot; | 3 | 12 |

## DEFINIR

O comando `SET` define uma propriedade e retorna o valor de uma propriedade existente ou lista todas as propriedades existentes. Se um valor for fornecido para uma chave de propriedade existente, o valor antigo será substituído.

```sql
SET property_key = property_value
```

| Parâmetros | Descrição |
| ------ | ------ |
| `property_key` | O nome da propriedade que você deseja listar ou alterar. |
| `property_value` | O valor com o qual você deseja que a propriedade seja definida. |

Para retornar o valor de qualquer configuração, use `SET [property key]` sem um `property_value`.

## [!DNL PostgreSQL] comandos

As subseções abaixo abrangem os comandos [!DNL PostgreSQL] com suporte pelo Serviço de Consulta.

### ANALISAR TABELA {#analyze-table}

O comando `ANALYZE TABLE` executa uma análise de distribuição e cálculos estatísticos para a tabela ou tabelas nomeadas. O uso de `ANALYZE TABLE` varia dependendo se os conjuntos de dados estão armazenados no [repositório acelerado](#compute-statistics-accelerated-store) ou no [data lake](#compute-statistics-data-lake). Consulte as respectivas seções para obter mais informações sobre o uso.

#### CALCULAR ESTATÍSTICAS no armazenamento acelerado {#compute-statistics-accelerated-store}

O comando `ANALYZE TABLE` calcula estatísticas para uma tabela no repositório acelerado. As estatísticas são calculadas sobre consultas CTAS ou ITAS executadas para uma determinada tabela no armazenamento acelerado.

**Exemplo**

```sql
ANALYZE TABLE <original_table_name>
```

Esta é uma lista de cálculos estatísticos que estão disponíveis após o uso do comando `ANALYZE TABLE` :-

| Valores calculados | Descrição |
|---|---|
| `field` | O nome da coluna em uma tabela. |
| `data-type` | O tipo aceitável de dados para cada coluna. |
| `count` | O número de linhas que contêm um valor não nulo para este campo. |
| `distinct-count` | O número de valores exclusivos ou distintos para esse campo. |
| `missing` | O número de linhas que têm um valor nulo para este campo. |
| `max` | O valor máximo da tabela analisada. |
| `min` | O valor mínimo da tabela analisada. |
| `mean` | O valor médio da tabela analisada. |
| `stdev` | O desvio padrão da tabela analisada. |

#### CALCULAR ESTATÍSTICAS no data lake {#compute-statistics-data-lake}

Agora você pode calcular estatísticas em nível de coluna em [!DNL Azure Data Lake Storage] conjuntos de dados (ADLS) com o comando SQL `COMPUTE STATISTICS`. Calcular estatísticas de coluna em todo o conjunto de dados, um subconjunto de um conjunto de dados, todas as colunas ou um subconjunto de colunas.

`COMPUTE STATISTICS` estende o comando `ANALYZE TABLE`. No entanto, os comandos `COMPUTE STATISTICS`, `FILTERCONTEXT` e `FOR COLUMNS` não têm suporte em tabelas de armazenamento aceleradas. No momento, essas extensões para o comando `ANALYZE TABLE` só têm suporte para tabelas ADLS.

**Exemplo**

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS  FOR COLUMNS (commerce, id, timestamp);
```

O comando `FILTER CONTEXT` calcula estatísticas em um subconjunto do conjunto de dados com base na condição de filtro fornecida. O comando `FOR COLUMNS` é direcionado a colunas específicas para análise.

>[!NOTE]
>
>O `Statistics ID` e as estatísticas geradas são válidos apenas para cada sessão e não podem ser acessados em sessões PSQL diferentes.<br><br>Limitações:<ul><li>A geração de estatísticas não é suportada para tipos de dados de matriz ou mapa</li><li>As estatísticas computadas são **não** persistentes entre sessões.</li></ul><br><br>Opções:<br><ul><li>`skip_stats_for_complex_datatypes`</li></ul><br>Por padrão, o sinalizador é definido como verdadeiro. Como resultado, quando as estatísticas são solicitadas em um tipo de dados incompatível, não ocorre o erro, mas os campos são ignorados silenciosamente com os tipos de dados incompatíveis.<br>Para habilitar notificações de erros quando forem solicitadas estatísticas em tipos de dados sem suporte, use: `SET skip_stats_for_complex_datatypes = false`.

A saída do console é exibida conforme visto abaixo.

```console
|     Statistics ID      | 
| ---------------------- |
| adc_geometric_stats_1  |
(1 row)
```

Você pode consultar as estatísticas computadas diretamente fazendo referência a `Statistics ID`. Use o `Statistics ID` ou o nome do alias conforme mostrado na instrução de exemplo abaixo, para exibir a saída por completo. Para saber mais sobre este recurso, consulte a [documentação sobre o nome do alias](../key-concepts/dataset-statistics.md#alias-name).

```sql
-- This statement gets the statistics generated for `alias adc_geometric_stats_1`.
SELECT * FROM adc_geometric_stats_1;
```

Use o comando `SHOW STATISTICS` para exibir os metadados de todas as estatísticas temporárias geradas na sessão. Este comando pode ajudá-lo a refinar o escopo da análise estatística.

```sql
SHOW STATISTICS;
```

Um exemplo de saída de SHOW STATISTICS é visto abaixo.

```console
      statsId         |   tableName   | columnSet |         filterContext       |      timestamp
|----------------------+---------------+-----------+-----------------------------+--------------------
adc_geometric_stats_1 | adc_geometric |   (age)   |                             | 25/06/2023 09:22:26
demo_table_stats_1    |  demo_table   |    (*)    |       ((age > 25))          | 25/06/2023 12:50:26
age_stats             | castedtitanic |   (age)   | ((age > 25) AND (age < 40)) | 25/06/2023 09:22:26
```

Consulte a [documentação de estatísticas do conjunto de dados](../key-concepts/dataset-statistics.md) para obter mais informações.

#### TABLESAMPLE {#tablesample}

O Serviço de consulta da Adobe Experience Platform fornece conjuntos de dados de amostra como parte de seus recursos aproximados de processamento de consulta.

As amostras de conjuntos de dados são usadas melhor quando você não precisa de uma resposta exata para uma operação de agregação em um conjunto de dados. Para realizar consultas exploratórias mais eficientes em grandes conjuntos de dados, emitindo uma consulta aproximada para retornar uma resposta aproximada, use o recurso `TABLESAMPLE`.

Os conjuntos de dados de exemplo são criados com amostras aleatórias uniformes de conjuntos de dados [!DNL Azure Data Lake Storage] (ADLS) existentes, usando apenas uma porcentagem dos registros do original. O recurso de exemplo de conjunto de dados estende o comando `ANALYZE TABLE` com os comandos SQL `TABLESAMPLE` e `SAMPLERATE`.

No exemplo abaixo, a linha um demonstra como calcular uma amostra de 5% da tabela. A linha dois demonstra como calcular uma amostra de 5% a partir de uma exibição filtrada dos dados na tabela.

**Exemplo**

```sql {line-numbers="true"}
ANALYZE TABLE tableName TABLESAMPLE SAMPLERATE 5;
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-01-01')) TABLESAMPLE SAMPLERATE 5:
```

Consulte a [documentação de amostras do conjunto de dados](../key-concepts/dataset-samples.md) para obter mais informações.

### INICIAR

O comando `BEGIN` ou, alternativamente, o comando `BEGIN WORK` ou `BEGIN TRANSACTION`, inicia um bloco de transação. Quaisquer instruções inseridas após o comando begin serão executadas em uma única transação até que um comando COMMIT ou ROLLBACK explícito seja fornecido. Este comando é igual a `START TRANSACTION`.

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### FECHAR

O comando `CLOSE` libera os recursos associados a um cursor aberto. Depois que o cursor for fechado, nenhuma operação subsequente será permitida nele. Um cursor deve ser fechado quando não for mais necessário.

```sql
CLOSE name
CLOSE ALL
```

Se `CLOSE name` for usado, `name` representa o nome de um cursor aberto que deve ser fechado. Se `CLOSE ALL` for usado, todos os cursores abertos serão fechados.

### DESALOCAR

Para desalocar uma instrução SQL preparada anteriormente, use o comando `DEALLOCATE`. Se você não desalocou explicitamente uma instrução preparada, ela será desalocada quando a sessão terminar. Mais informações sobre instruções preparadas podem ser encontradas na seção [comando PREPARE](#prepare).

```sql
DEALLOCATE name
DEALLOCATE ALL
```

Se `DEALLOCATE name` for usado, `name` representa o nome da instrução preparada que deve ser desalocada. Se `DEALLOCATE ALL` for usado, todas as instruções preparadas serão desalocadas.

### DECLARAR

O comando `DECLARE` permite que um usuário crie um cursor, que pode ser usado para recuperar um pequeno número de linhas de uma consulta maior. Após a criação do cursor, as linhas serão buscadas usando `FETCH`.

```sql
DECLARE name CURSOR FOR query
```

| Parâmetros | Descrição |
| ------ | ------ |
| `name` | O nome do cursor a ser criado. |
| `query` | Um comando `SELECT` ou `VALUES` que fornece as linhas a serem retornadas pelo cursor. |

### EXECUTAR

O comando `EXECUTE` é usado para executar uma instrução preparada anteriormente. Como as instruções preparadas só existem durante uma sessão, a instrução preparada deve ter sido criada por uma instrução `PREPARE` executada anteriormente na sessão atual. Mais informações sobre o uso de instruções preparadas podem ser encontradas na seção [`PREPARE` comando](#prepare).

Se a instrução `PREPARE` que criou a instrução especificou alguns parâmetros, um conjunto compatível de parâmetros deve ser passado para a instrução `EXECUTE`. Se esses parâmetros não forem transmitidos, um erro será gerado.

```sql
EXECUTE name [ ( parameter ) ]
```

| Parâmetros | Descrição |
| ------ | ------ |
| `name` | O nome da instrução preparada a ser executada. |
| `parameter` | O valor real de um parâmetro para a instrução preparada. Deve ser uma expressão que produz um valor compatível com o tipo de dados desse parâmetro, conforme determinado quando a instrução preparada foi criada. Se houver vários parâmetros para a instrução preparada, eles serão separados por vírgulas. |

### EXPLICAR

O comando `EXPLAIN` exibe o plano de execução da instrução fornecida. O plano de execução mostra como as tabelas referenciadas pela instrução serão verificadas. Se várias tabelas forem referenciadas, ela mostrará quais algoritmos de junção são usados para reunir as linhas necessárias de cada tabela de entrada.

```sql
EXPLAIN statement
```

Para definir o formato da resposta, use a palavra-chave `FORMAT` com o comando `EXPLAIN`.

```sql
EXPLAIN FORMAT { TEXT | JSON } statement
```

| Parâmetros | Descrição |
| ------ | ------ |
| `FORMAT` | Use o comando `FORMAT` para especificar o formato de saída. As opções disponíveis são `TEXT` ou `JSON`. A saída não textual contém as mesmas informações que o formato de saída de texto, mas é mais fácil para os programas analisarem. O padrão deste parâmetro é `TEXT`. |
| `statement` | Qualquer instrução `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `VALUES`, `EXECUTE`, `DECLARE`, `CREATE TABLE AS` ou `CREATE MATERIALIZED VIEW AS` cujo plano de execução você deseja ver. |

>[!IMPORTANT]
>
>Qualquer saída que uma instrução `SELECT` possa retornar é descartada quando executada com a palavra-chave `EXPLAIN`. Outros efeitos colaterais da declaração acontecem como de costume.

**Exemplo**

O exemplo a seguir mostra o plano para uma consulta simples em uma tabela com uma única coluna `integer` e 10000 linhas:

```sql
EXPLAIN SELECT * FROM foo;
```

```console
                       QUERY PLAN
|---------------------------------------------------------
 Seq Scan on foo (dataSetId = "6307eb92f90c501e072f8457", dataSetName = "foo") [0,1000000242,6973776840203d3d,6e616c58206c6153,6c6c6f430a3d4d20,74696d674c746365]
(1 row)
```

### BUSCAR

O comando `FETCH` recupera linhas usando um cursor criado anteriormente.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

| Parâmetros | Descrição |
| ------ | ------ |
| `num_of_rows` | O número de linhas a serem buscadas. |
| `cursor_name` | O nome do cursor do qual você está recuperando informações. |

### PREPARAR {#prepare}

O comando `PREPARE` permite criar uma instrução preparada. Uma instrução preparada é um objeto do lado do servidor que pode ser usado para modelar instruções SQL semelhantes.

As instruções preparadas podem usar parâmetros, que são valores substituídos na instrução quando ela é executada. Os parâmetros são referenciados por posição, usando $1, $2 e assim por diante, ao usar instruções preparadas.

Como opção, você pode especificar uma lista de tipos de dados de parâmetro. Se o tipo de dados de um parâmetro não estiver listado, o tipo poderá ser inferido do contexto.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

| Parâmetros | Descrição |
| ------ | ------ |
| `name` | O nome da instrução preparada. |
| `data_type` | Os tipos de dados dos parâmetros da instrução preparada. Se o tipo de dados de um parâmetro não estiver listado, o tipo poderá ser inferido do contexto. Se precisar adicionar vários tipos de dados, você poderá adicioná-los em uma lista separada por vírgulas. |

### REVERSÃO

O comando `ROLLBACK` desfaz a transação atual e descarta todas as atualizações feitas pela transação.

```sql
ROLLBACK
ROLLBACK WORK
```

### SELECIONAR EM

O comando `SELECT INTO` cria uma nova tabela e a preenche com dados computados por uma consulta. Os dados não são retornados ao cliente, como acontece com um comando `SELECT` normal. As novas colunas da tabela têm os nomes e tipos de dados associados às colunas de saída do comando `SELECT`.

```sql
[ WITH [ RECURSIVE ] with_query [, ...] ]
SELECT [ ALL | DISTINCT [ ON ( expression [, ...] ) ] ]
    * | expression [ [ AS ] output_name ] [, ...]
    INTO [ TEMPORARY | TEMP | UNLOGGED ] [ TABLE ] new_table
    [ FROM from_item [, ...] ]
    [ WHERE condition ]
    [ GROUP BY expression [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start [ ROW | ROWS ] ]
    [ FETCH { FIRST | NEXT } [ count ] { ROW | ROWS } ONLY ]
    [ FOR { UPDATE | SHARE } [ OF table_name [, ...] ] [ NOWAIT ] [...] ]
```

Mais informações sobre os parâmetros de consulta SELECT padrão podem ser encontradas na [seção de consulta SELECT](#select-queries). Esta seção lista apenas parâmetros exclusivos para o comando `SELECT INTO`.

| Parâmetros | Descrição |
| ------ | ------ |
| `TEMPORARY` ou `TEMP` | Um parâmetro opcional. Se o parâmetro for especificado, a tabela criada será uma tabela temporária. |
| `UNLOGGED` | Um parâmetro opcional. Se o parâmetro for especificado, a tabela criada será uma tabela não registrada. Mais informações sobre tabelas não registradas podem ser encontradas na [[!DNL PostgreSQL] documentação](https://www.postgresql.org/docs/current/sql-createtable.html). |
| `new_table` | O nome da tabela a ser criada. |

**Exemplo**

A consulta a seguir cria uma nova tabela `films_recent` que consiste em apenas entradas recentes da tabela `films`:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### MOSTRAR

O comando `SHOW` exibe a configuração atual dos parâmetros de tempo de execução. Essas variáveis podem ser definidas usando a instrução `SET`, editando o arquivo de configuração `postgresql.conf`, através da variável de ambiente `PGOPTIONS` (ao usar libpq ou um aplicativo baseado em libpq) ou através de sinalizadores de linha de comando ao iniciar o servidor Postgres.

```sql
SHOW name
SHOW ALL
```

| Parâmetros | Descrição |
| ------ | ------ |
| `name` | O nome do parâmetro de tempo de execução sobre o qual você deseja obter informações. Os valores possíveis para o parâmetro de tempo de execução incluem os seguintes valores:<br>`SERVER_VERSION`: esse parâmetro mostra o número de versão do servidor.<br>`SERVER_ENCODING`: este parâmetro mostra a codificação do conjunto de caracteres do lado do servidor.<br>`LC_COLLATE`: Esse parâmetro mostra a configuração de localidade do banco de dados para agrupamento (ordenação de texto).<br>`LC_CTYPE`: Esse parâmetro mostra a configuração de localidade do banco de dados para classificação de caracteres.<br>`IS_SUPERUSER`: Este parâmetro mostra se a função atual tem privilégios de superusuário. |
| `ALL` | Mostrar os valores de todos os parâmetros de configuração com descrições. |

**Exemplo**

A consulta a seguir mostra a configuração atual do parâmetro `DateStyle`.

```sql
SHOW DateStyle;
```

```console
 DateStyle
|-----------
 ISO, MDY
(1 row)
```

### COPIAR

O comando `COPY` duplica a saída de qualquer consulta `SELECT` para um local especificado. O usuário deve ter acesso a esse local para que esse comando tenha êxito.

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

| Parâmetros | Descrição |
| ------ | ------ |
| `query` | A consulta que você deseja copiar. |
| `format_name` | O formato no qual você deseja copiar a consulta. O `format_name` pode ser `parquet`, `csv` ou `json`. O valor padrão é `parquet`. |

>[!NOTE]
>
>O caminho de saída completo é `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### ALTERAR TABELA {#alter-table}

O comando `ALTER TABLE` permite adicionar ou remover restrições de chave primária ou estrangeira e adicionar colunas à tabela.

#### ADICIONAR OU SOLTAR RESTRIÇÃO

As consultas SQL a seguir mostram exemplos de adição ou eliminação de restrições em uma tabela. As restrições de chave primária e chave estrangeira podem ser adicionadas a várias colunas com valores separados por vírgula. Você pode criar chaves compostas transmitindo dois ou mais valores de nome de coluna, como visto nos exemplos abaixo.

**Definir chaves primárias ou compostas**

```sql
ALTER TABLE table_name ADD CONSTRAINT PRIMARY KEY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT PRIMARY KEY ( column_name1, column_name2 ) NAMESPACE namespace
```

**Definir uma relação entre tabelas com base em uma ou mais chaves**

```sql
ALTER TABLE table_name ADD CONSTRAINT FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT FOREIGN KEY ( column_name1, column_name2 ) REFERENCES referenced_table_name ( primary_column_name1, primary_column_name2 )
```

**Definir uma coluna de identidade**

```sql
ALTER TABLE table_name ADD CONSTRAINT PRIMARY IDENTITY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT IDENTITY ( column_name ) NAMESPACE namespace
```

**Remover uma restrição/relação/identidade**

```sql
ALTER TABLE table_name DROP CONSTRAINT PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT PRIMARY KEY ( column_name1, column_name2 )

ALTER TABLE table_name DROP CONSTRAINT FOREIGN KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT FOREIGN KEY ( column_name1, column_name2 )

ALTER TABLE table_name DROP CONSTRAINT PRIMARY IDENTITY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT IDENTITY ( column_name )
```

| Parâmetros | Descrição |
| ------ | ------ |
| `table_name` | O nome da tabela que você está editando. |
| `column_name` | O nome da coluna à qual você está adicionando uma restrição. |
| `referenced_table_name` | O nome da tabela referenciada pela chave estrangeira. |
| `primary_column_name` | O nome da coluna referenciada pela chave estrangeira. |

>[!NOTE]
>
>O schema da tabela deve ser exclusivo e não compartilhado entre várias tabelas. Além disso, o namespace é obrigatório para restrições de chave primária, identidade primária e identidade.

#### Adicionar ou remover identidades primária e secundária

Para adicionar ou excluir restrições para colunas da tabela de identidade primária e secundária, use o comando `ALTER TABLE`.

Os exemplos a seguir adicionam uma identidade primária e uma identidade secundária adicionando restrições.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

As identidades também podem ser removidas removendo restrições, como visto no exemplo abaixo.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

Para obter informações mais detalhadas, consulte o documento sobre [configuração de identidades em conjuntos de dados ad hoc](../data-governance/ad-hoc-schema-identities.md).

#### ADICIONAR COLUNA

As consultas SQL a seguir mostram exemplos de adição de colunas a uma tabela.

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

##### Tipos de dados compatíveis

A tabela a seguir lista os tipos de dados aceitos para adicionar colunas a uma tabela com [!DNL Postgres SQL], XDM e o [!DNL Accelerated Database Recovery] (ADR) no Azure SQL.

| — | Cliente PSQL | XDM | ADR | Descrição |
|---|---|---|---|---|
| 1 | `bigint` | `int8` | `bigint` | Um tipo de dados numéricos usado para armazenar números inteiros grandes variando de -9,223,372,036,854,775,807 a 9,223,372,036,854,775,807 em 8 bytes. |
| 2 | `integer` | `int4` | `integer` | Um tipo de dados numéricos usado para armazenar números inteiros que variam de -2.147.483.648 a 2.147.483.647 em 4 bytes. |
| 3 | `smallint` | `int2` | `smallint` | Um tipo de dados numéricos usado para armazenar números inteiros que variam de -32.768 a 215-1 32.767 em 2 bytes. |
| 4 | `tinyint` | `int1` | `tinyint` | Um tipo de dados numéricos usado para armazenar números inteiros que variam de 0 a 255 em 1 byte. |
| 5 | `varchar(len)` | `string` | `varchar(len)` | Um tipo de dados character de tamanho variável. `varchar` é melhor usado quando os tamanhos das entradas de dados da coluna variam consideravelmente. |
| 6 | `double` | `float8` | `double precision` | `FLOAT8` e `FLOAT` são sinônimos válidos para `DOUBLE PRECISION`. `double precision` é um tipo de dados de ponto flutuante. Os valores de ponto flutuante são armazenados em 8 bytes. |
| 7 | `double precision` | `float8` | `double precision` | `FLOAT8` é um sinônimo válido para `double precision`.`double precision` é um tipo de dados de ponto flutuante. Os valores de ponto flutuante são armazenados em 8 bytes. |
| 8 | `date` | `date` | `date` | Os tipos de dados `date` são valores de data do calendário armazenados de 4 bytes sem nenhuma informação de carimbo de data/hora. O intervalo de datas válidas é de 01-01-0001 a 12-31-9999. |
| 9 | `datetime` | `datetime` | `datetime` | Um tipo de dados usado para armazenar um instante de tempo expresso como data e hora do calendário. `datetime` inclui os qualificadores de: ano, mês, dia, hora, segundo e fração. Uma declaração `datetime` pode incluir qualquer subconjunto dessas unidades de tempo unidas nessa sequência, ou até mesmo incluir apenas uma única unidade de tempo. |
| 10 | `char(len)` | `string` | `char(len)` | A palavra-chave `char(len)` é usada para indicar que o item tem um caractere de comprimento fixo. |

#### ADICIONAR ESQUEMA

A consulta SQL a seguir mostra um exemplo de adição de uma tabela a um banco de dados/esquema.

```sql
ALTER TABLE table_name ADD SCHEMA database_name.schema_name
```

>[!NOTE]
>
> Tabelas e visualizações do ADLS não podem ser adicionadas a bancos de dados/esquemas DWH.


#### REMOVER ESQUEMA

A consulta SQL a seguir mostra um exemplo de remoção de uma tabela de um banco de dados/esquema.

```sql
ALTER TABLE table_name REMOVE SCHEMA database_name.schema_name
```

>[!NOTE]
>
> As tabelas e visualizações DWH não podem ser removidas dos bancos de dados/esquemas DWH vinculados fisicamente.


**Parâmetros**

| Parâmetros | Descrição |
| ------ | ------ |
| `table_name` | O nome da tabela que você está editando. |
| `column_name` | O nome da coluna que você deseja adicionar. |
| `data_type` | O tipo de dados da coluna que você deseja adicionar. Os tipos de dados compatíveis incluem o seguinte: bigint, char, string, date, datetime, double, double precision, integer, smallint, tinyint, varchar. |

### MOSTRAR CHAVES PRIMÁRIAS

O comando `SHOW PRIMARY KEYS` lista todas as restrições de chave primária para o banco de dados especificado.

```sql
SHOW PRIMARY KEYS
```

```console
    tableName | columnName    | datatype | namespace
|------------------+----------------------+----------+-----------
 table_name_1 | column_name1  | text     | "ECID"
 table_name_2 | column_name2  | text     | "AAID"
```

### MOSTRAR CHAVES ESTRANGEIRAS

O comando `SHOW FOREIGN KEYS` lista todas as restrições de chave estrangeira para o banco de dados especificado.

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
|------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```


### MOSTRAR GRUPOS DE DADOS

O comando `SHOW DATAGROUPS` retorna uma tabela de todos os bancos de dados associados. Para cada banco de dados, a tabela inclui esquema, tipo de grupo, tipo filho, nome filho e ID filho.

```sql
SHOW DATAGROUPS
```

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                       |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   adls_db     | adls_scheema      | ADLS      | Data Lake Table      | adls_table1                                        | 6149ff6e45cfa318a76ba6d3
   adls_db     | adls_scheema      | ADLS      | Accelerated Store | _table_demo1                                       | 22df56cf-0790-4034-bd54-d26d55ca6b21
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view1                                         | c2e7ddac-d41c-40c5-a7dd-acd41c80c5e9
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view4                                         | b280c564-df7e-405f-80c5-64df7ea05fc3
```


### MOSTRAR DATAGROUPS PARA tabela

O comando `SHOW DATAGROUPS FOR 'table_name'` retorna uma tabela de todos os bancos de dados associados que contêm o parâmetro como filho. Para cada banco de dados, a tabela inclui esquema, tipo de grupo, tipo filho, nome filho e ID filho.

```sql
SHOW DATAGROUPS FOR 'table_name'
```

**Parâmetros**

- `table_name`: O nome da tabela para a qual você deseja encontrar bancos de dados associados.

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                      |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   dwh_db_demo | schema2           | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   dwh_db_demo | schema1           | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   qsaccel     | profile_aggs      | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
```
