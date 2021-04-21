---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, sintaxe sql, sql, ctas, CTAS, Criar tabela como selecionar
solution: Experience Platform
title: Sintaxe SQL no Serviço de Consulta
topic-legacy: syntax
description: Este documento mostra a sintaxe SQL suportada pelo Adobe Experience Platform Query Service.
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 1%

---

# Sintaxe SQL no Serviço de Consulta

O Adobe Experience Platform Query Service fornece a capacidade de usar o SQL ANSI padrão para instruções `SELECT` e outros comandos limitados. Este documento cobre a sintaxe SQL suportada por [!DNL Query Service].

## SELECIONAR consultas {#select-queries}

A sintaxe a seguir define uma consulta `SELECT` suportada por [!DNL Query Service]:

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

onde `from_item` pode ser uma das seguintes opções:

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

e `grouping_element` pode ser uma das seguintes opções:

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

e `with_query` é:

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
```

As subseções a seguir fornecem detalhes sobre cláusulas adicionais que podem ser usadas em queries, desde que sigam o formato descrito acima.

### Cláusula SNAPSHOT

Essa cláusula pode ser usada para ler dados de forma incremental em uma tabela com base nas IDs de snapshot. Uma ID de instantâneo é um marcador de ponto de verificação representado por um número de tipo longo aplicado a uma tabela de lago de dados sempre que os dados são gravados nela. A cláusula `SNAPSHOT` se anexa à relação da tabela à qual é usada ao lado.

```sql
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
```

#### Exemplo

```sql
SELECT * FROM Customers SNAPSHOT SINCE 123;

SELECT * FROM Customers SNAPSHOT AS OF 345;

SELECT * FROM Customers SNAPSHOT BETWEEN 123 AND 345;

SELECT * FROM Customers SNAPSHOT BETWEEN HEAD AND 123;

SELECT * FROM Customers SNAPSHOT BETWEEN 345 AND TAIL;

SELECT * FROM (SELECT id FROM CUSTOMERS BETWEEN 123 AND 345) C 

SELECT * FROM Customers SNAPSHOT SINCE 123 INNER JOIN Inventory AS OF 789 ON Customers.id = Inventory.id;
```

Observe que uma cláusula `SNAPSHOT` funciona com um alias de tabela ou tabela, mas não sobre uma subconsulta ou exibição. Uma cláusula `SNAPSHOT` funcionará em qualquer lugar em que uma consulta `SELECT` em uma tabela possa ser aplicada.

Além disso, você pode usar `HEAD` e `TAIL` como valores de deslocamento especiais para cláusulas de instantâneo. Usar `HEAD` se refere a um deslocamento antes do primeiro instantâneo, enquanto `TAIL` se refere a um deslocamento após o último instantâneo.

### cláusula WHERE

Por padrão, as correspondências produzidas por uma cláusula `WHERE` em uma consulta `SELECT` fazem distinção entre maiúsculas e minúsculas. Se desejar que as correspondências não diferenciem maiúsculas de minúsculas, você pode usar a palavra-chave `ILIKE` em vez de `LIKE`.

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

A lógica das cláusulas LIKE e ILIKE é explicada no quadro seguinte:

| Cláusula | Operador |
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

Esse query retorna clientes com nomes começando em &quot;A&quot; ou &quot;a&quot;.

### JOIN

Uma consulta `SELECT` que usa associações tem a seguinte sintaxe:

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### UNIÃO, INTERSECT e EXCETO

As cláusulas `UNION`, `INTERSECT` e `EXCEPT` são usadas para combinar ou excluir linhas como de duas ou mais tabelas:

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### CRIAR TABELA COMO SELECIONADO

A sintaxe a seguir define uma consulta `CREATE TABLE AS SELECT` (CTAS):

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

**Parâmetros**

- `schema`: O título do esquema XDM. Use esta cláusula somente se desejar usar um esquema XDM existente para o novo conjunto de dados criado pela consulta CTAS.
- `rowvalidation`: (Opcional) Especifica se o usuário deseja a validação em nível de linha de cada novo lote assimilado para o conjunto de dados recém-criado. O valor padrão é `true`.
- `select_query`: Uma  `SELECT` declaração. A sintaxe da consulta `SELECT` pode ser encontrada na seção [SELECT queries](#select-queries).

**Exemplo**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>A instrução `SELECT` deve ter um alias para as funções agregadas, como `COUNT`, `SUM`, `MIN` e assim por diante. Além disso, a declaração `SELECT` pode ser fornecida com ou sem parênteses (). Você pode fornecer uma cláusula `SNAPSHOT` para ler deltas incrementais na tabela de destino.

## INSERIR EM

O comando `INSERT INTO` é definido da seguinte maneira:

```sql
INSERT INTO table_name select_query
```

**Parâmetros**

- `table_name`: O nome da tabela na qual você deseja inserir o query.
- `select_query`: Uma  `SELECT` declaração. A sintaxe da consulta `SELECT` pode ser encontrada na seção [SELECT queries](#select-queries).

**Exemplo**

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!NOTE]
> A instrução `SELECT` **não deve** ser colocada entre parênteses (). Além disso, o schema do resultado da instrução `SELECT` deve estar em conformidade com o da tabela definida na instrução `INSERT INTO`. Você pode fornecer uma cláusula `SNAPSHOT` para ler deltas incrementais na tabela de destino.

## TABELA DE SOLTAÇÕES

O comando `DROP TABLE` solta uma tabela existente e exclui o diretório associado à tabela do sistema de arquivos se não for uma tabela externa. Se a tabela não existir, ocorre uma exceção.

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

**Parâmetros**

- `IF EXISTS`: Se isso for especificado, nenhuma exceção será lançada se a tabela  **** não existir.

## CRIAR EXIBIÇÃO

A sintaxe a seguir define uma consulta `CREATE VIEW`:

```sql
CREATE VIEW view_name AS select_query
```

**Parâmetros**

- `view_name`: O nome da exibição a ser criada.
- `select_query`: Uma  `SELECT` declaração. A sintaxe da consulta `SELECT` pode ser encontrada na seção [SELECT queries](#select-queries).

**Exemplo**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

## EXIBIÇÃO DE SOLTAR

A sintaxe a seguir define uma consulta `DROP VIEW`:

```sql
DROP VIEW [IF EXISTS] view_name
```

**Parâmetro**

- `IF EXISTS`: Se isso for especificado, nenhuma exceção será lançada se a exibição  **** não existir.
- `view_name`: O nome da exibição a ser excluída.

**Exemplo**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## [!DNL Spark] Comandos SQL

A subseção abaixo cobre os comandos SQL Spark suportados pelo Serviço de Consulta.

### DEFINIR

O comando `SET` define uma propriedade e retorna o valor de uma propriedade existente ou lista todas as propriedades existentes. Se um valor for fornecido para uma chave de propriedade existente, o valor antigo será substituído.

```sql
SET property_key = property_value
```

**Parâmetros**

- `property_key`: O nome da propriedade que você deseja listar ou alterar.
- `property_value`: O valor que você deseja que a propriedade seja definida.

Para retornar o valor de qualquer configuração, use `SET [property key]` sem um `property_value`.

## Comandos PostgreSQL

As subseções abaixo abordam os comandos PostgreSQL suportados pelo Serviço de Consulta.

### INÍCIO

O comando `BEGIN` ou, alternativamente, o comando `BEGIN WORK` ou `BEGIN TRANSACTION`, inicia um bloco de transações. Quaisquer instruções inseridas após o comando begin serão executadas em uma única transação até que um comando COMMIT ou ROLLBACK explícito seja fornecido. Esse comando é igual a `START TRANSACTION`.

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### FECHAR

O comando `CLOSE` libera os recursos associados a um cursor aberto. Depois que o cursor é fechado, nenhuma operação subsequente é permitida nele. Um cursor deve ser fechado quando não for mais necessário.

```sql
CLOSE name
CLOSE ALL
```

Se `CLOSE name` for usado, `name` representa o nome de um cursor aberto que precisa ser fechado. Se `CLOSE ALL` for usado, todos os cursores abertos serão fechados.

### DESALOCAR

O comando `DEALLOCATE` permite desalocar uma instrução SQL preparada anteriormente. Se você não desalocar explicitamente uma declaração preparada, ela será desalocada quando a sessão terminar. Mais informações sobre instruções preparadas podem ser encontradas na seção [PREPARE command](#prepare).

```sql
DEALLOCATE name
DEALLOCATE ALL
```

Se `DEALLOCATE name` for usado, `name` representa o nome da instrução preparada que precisa ser desalocada. Se `DEALLOCATE ALL` for usado, todas as instruções preparadas serão desalocadas.

### DECLARAR

O comando `DECLARE` permite que o usuário crie um cursor, que pode ser usado para recuperar um pequeno número de linhas de uma consulta maior. Após a criação do cursor, as linhas são buscadas usando `FETCH`.

```sql
DECLARE name CURSOR FOR query
```

**Parâmetros**

- `name`: O nome do cursor a ser criado.
- `query`: Um  `SELECT` comando  `VALUES` ou que fornece as linhas a serem retornadas pelo cursor.

### EXECUTAR

O comando `EXECUTE` é usado para executar uma instrução preparada anteriormente. Como as instruções preparadas existem apenas para a duração de uma sessão, a instrução preparada deve ter sido criada por uma instrução `PREPARE` executada anteriormente na sessão atual. Mais informações sobre o uso de instruções preparadas podem ser encontradas na seção [`PREPARE` command](#prepare).

Se a instrução `PREPARE` que criou a instrução especificou alguns parâmetros, um conjunto de parâmetros compatível deve ser transmitido à instrução `EXECUTE`. Se esses parâmetros não forem enviados, um erro será gerado.

```sql
EXECUTE name [ ( parameter ) ]
```

**Parâmetros**

- `name`: O nome da instrução preparada a ser executada.
- `parameter`: O valor real de um parâmetro para a instrução preparada. Deve ser uma expressão que produza um valor compatível com o tipo de dados desse parâmetro, conforme determinado quando a instrução preparada foi criada.  Se houver vários parâmetros para a instrução preparada, eles serão separados por vírgulas.

### EXPLICAR

O comando `EXPLAIN` exibe o plano de execução da instrução fornecida. O plano de execução mostra como as tabelas referenciadas pela instrução serão digitalizadas.  Se houver referência a várias tabelas, elas mostrarão quais algoritmos de junção são usados para reunir as linhas necessárias de cada tabela de entrada.

```sql
EXPLAIN option statement
```

Onde `option` pode ser um dos seguintes:

```sql
ANALYZE
FORMAT { TEXT | JSON }
```

**Parâmetros**

- `ANALYZE`: Se o  `option` contiver  `ANALYZE`, os tempos de execução e outras estatísticas serão mostrados.
- `FORMAT`: Se o  `option` contiver  `FORMAT`, ele especificará o formato de saída, que pode ser  `TEXT` ou  `JSON`. A saída não textual contém as mesmas informações que o formato de saída de texto, mas é mais fácil para os programas analisar. Esse parâmetro assume como padrão `TEXT`.
- `statement`: Qualquer  `SELECT`,  `INSERT`,  `UPDATE`,  `DELETE`,  `VALUES`,  `EXECUTE`,  `DECLARE`,  `CREATE TABLE AS` ou  `CREATE MATERIALIZED VIEW AS` instrução, cujo plano de execução você deseja ver.

>[!IMPORTANT]
>
>Lembre-se de que a instrução é realmente executada quando a opção `ANALYZE` é usada. Embora `EXPLAIN` descarte qualquer saída que `SELECT` retorne, outros efeitos colaterais da declaração ocorrem como de costume.

**Exemplo**

O exemplo a seguir mostra o plano de uma consulta simples em uma tabela com uma única coluna `integer` e 10000 linhas:

```sql
EXPLAIN SELECT * FROM foo;
```

```console
                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### BUSCA

O comando `FETCH` recupera linhas usando um cursor criado anteriormente.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

**Parâmetros**

- `num_of_rows`: O número de linhas a serem buscadas.
- `cursor_name`: O nome do cursor do qual você está recuperando informações.

### PREPARAR {#prepare}

O comando `PREPARE` permite criar uma instrução preparada. Uma instrução preparada é um objeto do lado do servidor que pode ser usado para modelar instruções SQL semelhantes.

As instruções preparadas podem receber parâmetros, que são valores substituídos na instrução quando é executada. Os parâmetros são referenciados por posição, usando $1, $2, etc., ao usar instruções preparadas.

Como opção, você pode especificar uma lista de tipos de dados de parâmetro. Se o tipo de dados de um parâmetro não estiver listado, ele poderá ser inferido do contexto.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

**Parâmetros**

- `name`: O nome da instrução preparada.
- `data_type`: Os tipos de dados dos parâmetros da instrução preparada. Se o tipo de dados de um parâmetro não estiver listado, ele poderá ser inferido do contexto. Se precisar adicionar vários tipos de dados, é possível adicioná-los em uma lista separada por vírgulas.

### ROLLBACK

O comando `ROLLBACK` desfaz a transação atual e descarta todas as atualizações feitas pela transação.

```sql
ROLLBACK
ROLLBACK WORK
```

### SELECIONAR EM

O comando `SELECT INTO` cria uma nova tabela e a preenche com dados calculados por uma query. Os dados não são retornados ao cliente, pois estão com um comando normal `SELECT`. As colunas da nova tabela têm os nomes e os tipos de dados associados às colunas de saída do comando `SELECT`.

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

**Parâmetros**

Mais informações sobre os parâmetros de consulta SELECT padrão podem ser encontradas na seção [SELECT query](#select-queries). Esta seção listará apenas parâmetros exclusivos ao comando `SELECT INTO`.

- `TEMPORARY` ou  `TEMP`: Um parâmetro opcional. Se especificado, a tabela criada será uma tabela temporária.
- `UNLOGGED`: Um parâmetro opcional. Se especificado, a tabela criada como será uma tabela desconectada. Mais informações sobre tabelas desconectadas podem ser encontradas na documentação [PostgreSQL](https://www.postgresql.org/docs/current/sql-createtable.html).
- `new_table`: O nome da tabela a ser criada.

**Exemplo**

A consulta a seguir cria uma nova tabela `films_recent` que consiste apenas em entradas recentes da tabela `films`:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### MOSTRAR

O comando `SHOW` exibe a configuração atual dos parâmetros de tempo de execução. Essas variáveis podem ser definidas usando a instrução `SET`, editando o arquivo de configuração `postgresql.conf` por meio da variável ambiental `PGOPTIONS` (ao usar libpq ou um aplicativo baseado em libpq) ou por meio de sinalizadores de linha de comando ao iniciar o servidor Postgres.

```sql
SHOW name
SHOW ALL
```

**Parâmetros**

- `name`: O nome do parâmetro de tempo de execução sobre o qual você deseja obter informações. Os valores possíveis para o parâmetro de tempo de execução incluem os seguintes valores:
   - `SERVER_VERSION`: Este parâmetro mostra o número da versão do servidor.
   - `SERVER_ENCODING`: Esse parâmetro mostra a codificação do conjunto de caracteres do lado do servidor.
   - `LC_COLLATE`: Esse parâmetro mostra a configuração de local do banco de dados para agrupamento (ordenação de texto).
   - `LC_CTYPE`: Esse parâmetro mostra a configuração de local do banco de dados para a classificação de caracteres.
      `IS_SUPERUSER`: Esse parâmetro mostra se a função atual tem privilégios de superusuário.
- `ALL`: Mostre os valores de todos os parâmetros de configuração com descrições.

**Exemplo**

A consulta a seguir mostra a configuração atual do parâmetro `DateStyle`.

```sql
SHOW DateStyle;
```

```console
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### COPIAR

O comando `COPY` despeja a saída de qualquer consulta `SELECT` para um local especificado. O usuário deve ter acesso a esse local para que esse comando seja bem-sucedido.

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

**Parâmetros**

- `query`: A consulta que você deseja copiar.
- `format_name`: O formato no qual você deseja copiar a consulta. O `format_name` pode ser um dos `parquet`, `csv` ou `json`. Por padrão, o valor é `parquet`.

>[!NOTE]
>
>O caminho de saída completo será `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### ALTERAR TABELA

O comando `ALTER TABLE` permite adicionar ou soltar restrições de chave primária ou estrangeira, bem como adicionar colunas à tabela.

#### ADICIONAR OU SOLTAR RESTRIÇÃO

As seguintes consultas SQL mostram exemplos de adição ou remoção de restrições a uma tabela.

```sql
ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY column_name NAMESPACE namespace

ALTER TABLE table_name DROP CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT constraint_name FOREIGN KEY ( column_name )
```

**Parâmetros**

- `table_name`: O nome da tabela que você está editando.
- `constraint_name`: O nome da restrição que você deseja adicionar ou excluir.
- `column_name`: O nome da coluna à qual você está adicionando uma restrição.
- `referenced_table_name`: O nome da tabela referenciada pela chave externa.
- `primary_column_name`: O nome da coluna referenciada pela chave externa.

>[!NOTE]
>
>O schema da tabela deve ser exclusivo e não compartilhado entre várias tabelas. Além disso, o namespace é obrigatório para restrições de chave primária.

#### ADICIONAR COLUNA

As seguintes consultas SQL mostram exemplos de adição de colunas a uma tabela.

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

**Parâmetros**

- `table_name`: O nome da tabela que você está editando.
- `column_name`: O nome da coluna que deseja adicionar.
- `data_type`: O tipo de dados da coluna que você deseja adicionar. Os tipos de dados compatíveis incluem: bigint, char, string, data, datetime, duplo, precisão dupla, inteiro, smallint, tinyint, varchar.

### MOSTRAR CHAVES PRIMÁRIAS

O comando `SHOW PRIMARY KEYS` lista todas as restrições de chave primária para o banco de dados especificado.

```sql
SHOW PRIMARY KEYS
```

```console
    tableName | columnName    | datatype | namespace
------------------+----------------------+----------+-----------
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
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```
