---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, sintaxe sql, sql, ctas, CTAS, Criar tabela como selecionar
solution: Experience Platform
title: Sintaxe SQL no Serviço de Consulta
topic-legacy: syntax
description: Este documento mostra a sintaxe SQL suportada pelo Adobe Experience Platform Query Service.
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: 2a74d900053a868ce936d957dee008da846d6608
workflow-type: tm+mt
source-wordcount: '2668'
ht-degree: 2%

---

# Sintaxe SQL no Serviço de Consulta

O Adobe Experience Platform Query Service fornece a capacidade de usar o SQL ANSI padrão para `SELECT` instruções e outros comandos limitados. Este documento aborda a sintaxe SQL suportada por [!DNL Query Service].

## SELECIONAR consultas {#select-queries}

A sintaxe a seguir define um `SELECT` query suportada por [!DNL Query Service]:

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

em que `from_item` pode ser uma das seguintes opções:

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

Essa cláusula pode ser usada para ler dados de forma incremental em uma tabela com base nas IDs de snapshot. Uma ID de instantâneo é um marcador de ponto de verificação representado por um número de tipo longo aplicado a uma tabela de lago de dados sempre que os dados são gravados nela. O `SNAPSHOT` anexa-se à relação de tabela à qual é usada ao lado.

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

Observe que uma `SNAPSHOT` A cláusula funciona com um alias de tabela ou tabela, mas não em cima de uma subconsulta ou exibição. A `SNAPSHOT` a cláusula funcionará em qualquer lugar que uma `SELECT` é possível aplicar a query em uma tabela.

Além disso, você pode usar `HEAD` e `TAIL` como valores de deslocamento especiais para cláusulas de instantâneo. Usando `HEAD` refere-se a um deslocamento antes do primeiro instantâneo, enquanto `TAIL` refere-se a um deslocamento após o último instantâneo.

>[!NOTE]
>
>Se você estiver consultando entre duas IDs de instantâneo e o instantâneo de início expirar, os dois cenários a seguir poderão ocorrer, dependendo do sinalizador opcional de comportamento de fallback (`resolve_fallback_snapshot_on_failure`) está definido:
>
>- Se o sinalizador de comportamento de fallback opcional estiver definido, o Serviço de Consulta escolherá o instantâneo mais antigo disponível, definirá-o como o instantâneo inicial e retornará os dados entre o instantâneo mais antigo disponível e o instantâneo final especificado. Esses dados são **inclusivo** do primeiro instantâneo disponível.
>
>- Se o sinalizador de comportamento de fallback opcional não estiver definido, um erro será retornado.


### cláusula WHERE

Por padrão, corresponde produzidas por um `WHERE` cláusula sobre uma `SELECT` As consultas fazem distinção entre maiúsculas e minúsculas. Se quiser que as correspondências não diferenciem maiúsculas de minúsculas, você pode usar a palavra-chave `ILIKE` em vez de `LIKE`.

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

A `SELECT` A consulta que usa associações tem a seguinte sintaxe:

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### UNIÃO, INTERSECT e EXCETO

O `UNION`, `INTERSECT`e `EXCEPT` as cláusulas são usadas para combinar ou excluir como linhas de duas ou mais tabelas:

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### CRIAR TABELA COMO SELECIONADO

A sintaxe a seguir define um `CREATE TABLE AS SELECT` Consulta (CTAS):

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

| Parâmetros | Descrição |
| ----- | ----- |
| `schema` | O título do esquema XDM. Use esta cláusula somente se desejar usar um esquema XDM existente para o novo conjunto de dados criado pela consulta CTAS. |
| `rowvalidation` | (Opcional) Especifica se o usuário deseja a validação em nível de linha de cada novo lote assimilado para o conjunto de dados recém-criado. O valor padrão é `true`. |
| `select_query` | A `SELECT` instrução. A sintaxe da variável `SELECT` pode ser encontrada no [Seção SELECT queries](#select-queries). |

**Exemplo**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>O `SELECT` deve ter um alias para as funções agregadas, como `COUNT`, `SUM`, `MIN`e assim por diante. Além disso, a variável `SELECT` pode ser fornecida com ou sem parênteses (). Você pode fornecer uma `SNAPSHOT` cláusula para ler deltas incrementais na tabela de destino.

## INSERIR EM

O `INSERT INTO` O comando é definido da seguinte maneira:

```sql
INSERT INTO table_name select_query
```

| Parâmetros | Descrição |
| ----- | ----- |
| `table_name` | O nome da tabela na qual você deseja inserir o query. |
| `select_query` | A `SELECT` instrução. A sintaxe da variável `SELECT` pode ser encontrada no [Seção SELECT queries](#select-queries). |

**Exemplo**

>[!NOTE]
>
>Veja a seguir um exemplo bem-sucedido e simplesmente para fins instrutivos.

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!INFO]
> 
> O `SELECT` declaração **não deve** entre parênteses (). Além disso, o schema do resultado da variável `SELECT` deve estar em conformidade com o da tabela definida no `INSERT INTO` instrução. Você pode fornecer uma `SNAPSHOT` cláusula para ler deltas incrementais na tabela de destino.

A maioria dos campos em um esquema XDM real não é encontrada no nível raiz e o SQL não permite o uso de notação de pontos. Para obter um resultado realista usando campos aninhados, mapeie cada campo no `INSERT INTO` caminho.

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

## TABELA DE SOLTAÇÕES

O `DROP TABLE` solta uma tabela existente e exclui o diretório associado à tabela do sistema de arquivos se não for uma tabela externa. Se a tabela não existir, ocorre uma exceção.

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

| Parâmetros | Descrição |
| ------ | ------ |
| `IF EXISTS` | Se isso for especificado, nenhuma exceção será lançada se a tabela fizer **not** existe. |

## CRIAR BANCO DE DADOS

O `CREATE DATABASE` cria um banco de dados ADLS.

```sql
CREATE DATABASE [IF NOT EXISTS] db_name
```

## SOLTAR BANCO DE DADOS

O `DROP DATABASE` exclui o banco de dados de uma instância.

```sql
DROP DATABASE [IF EXISTS] db_name
```

| Parâmetros | Descrição |
| ------ | ------ |
| `IF EXISTS` | Se isso for especificado, nenhuma exceção será lançada se o banco de dados fizer **not** existe. |

## ESQUEMA DE SOLTAR

O `DROP SCHEMA` solta um esquema existente.

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

| Parâmetros | Descrição |
| ------ | ------ |
| `IF EXISTS` | Se isso for especificado, nenhuma exceção será lançada se o schema fizer **not** existe. |
| `RESTRICT` | Valor padrão para o modo . Se isso for especificado, o schema só será descartado se ele for especificado **does not** contém qualquer tabela. |
| `CASCADE` | Se isso for especificado, o schema será descartado junto com todas as tabelas presentes no schema. |

## CRIAR EXIBIÇÃO

A sintaxe a seguir define um `CREATE VIEW` query:

```sql
CREATE VIEW view_name AS select_query
```

| Parâmetros | Descrição |
| ------ | ------ |
| `view_name` | O nome da exibição a ser criada. |
| `select_query` | A `SELECT` instrução. A sintaxe da variável `SELECT` pode ser encontrada no [Seção SELECT queries](#select-queries). |

**Exemplo**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

## EXIBIÇÃO DE SOLTAR

A sintaxe a seguir define um `DROP VIEW` query:

```sql
DROP VIEW [IF EXISTS] view_name
```

| Parâmetros | Descrição |
| ------ | ------ |
| `IF EXISTS` | Se isso for especificado, nenhuma exceção será lançada se a exibição **not** existe. |
| `view_name` | O nome da exibição a ser excluída. |

**Exemplo**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## Bloco anônimo

Um bloco anônimo consiste em duas seções: seções executáveis e de tratamento de exceções. Em um bloco anônimo, a seção executável é obrigatória. No entanto, a seção de tratamento de exceções é opcional.

O exemplo a seguir mostra como criar um bloco com uma ou mais instruções a serem executadas juntas:

```sql
BEGIN
  statementList
[EXCEPTION exceptionHandler]
END

exceptionHandler:
      WHEN OTHER
      THEN statementList

statementList:
    : (statement (';')) +
```

Abaixo está um exemplo de uso de bloco anônimo.

```sql
BEGIN
   SET @v_snapshot_from = select parent_id  from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_snapshot_to = select snapshot_id from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_log_id = select now();
   CREATE TABLE tracking_email_id_incrementally
     AS SELECT _id AS id FROM email_tracking_experience_event_dataset SNAPSHOT BETWEEN @v_snapshot_from AND @v_snapshot_to;

EXCEPTION
  WHEN OTHER THEN
    DROP TABLE IF EXISTS tracking_email_id_incrementally;
    SELECT 'ERROR';
END;
```

## Organização do ativo de dados

É importante organizar logicamente seus ativos de dados no lago de dados do Adobe Experience Platform à medida que crescem. O Serviço de Consulta estende construções SQL que permitem agrupar logicamente ativos de dados em uma sandbox. Esse método de organização permite o compartilhamento de ativos de dados entre esquemas sem a necessidade de movê-los fisicamente.

As construções SQL a seguir que usam a sintaxe SQL padrão são suportadas para que você organize seus dados logicamente.

```SQL
CREATE DATABASE dg1;
CREATE SCHEMA dg1.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

Consulte o guia sobre [organização lógica de ativos de dados](../best-practices/organize-data-assets.md) para obter mais explicações detalhadas sobre as práticas recomendadas do Serviço de query.

## Tabela existe

O `table_exists` O comando SQL é usado para confirmar se uma tabela existe ou não no sistema. O comando retorna um valor booleano: `true` se a tabela **does** existir e `false` se a tabela **not** existe.

Ao validar se uma tabela existe antes de executar as instruções, a variável `table_exists` O recurso simplifica o processo de gravação de um bloco anônimo para abranger ambos os `CREATE` e `INSERT INTO` casos de uso.

A sintaxe a seguir define a variável `table_exists` comando:

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

## Inline {#inline}

A função em linha separa os elementos de uma matriz de estruturas e gera os valores em uma tabela. Ela só pode ser colocada no `SELECT` ou uma `LATERAL VIEW`.

A função em linha **cannot** ser colocada numa lista selecionada, onde existam outras funções de gerador.

Por padrão, as colunas produzidas são nomeadas como &quot;col1&quot;, &quot;col2&quot; e assim por diante. Se a expressão for `NULL` em seguida, nenhuma linha é produzida.

**Exemplo**

```sql
> SELECT inline(array(struct(1, 'a'), struct(2, 'b'))), 'Spark SQL';
```

O exemplo retorna o seguinte:

```text
1  a Spark SQL
2  b Spark SQL
```

## [!DNL Spark] Comandos SQL

A subseção abaixo cobre os comandos SQL Spark suportados pelo Serviço de Consulta.

### DEFINIR

O `SET` O comando define uma propriedade e retorna o valor de uma propriedade existente ou lista todas as propriedades existentes. Se um valor for fornecido para uma chave de propriedade existente, o valor antigo será substituído.

```sql
SET property_key = property_value
```

| Parâmetros | Descrição |
| ------ | ------ |
| `property_key` | O nome da propriedade que você deseja listar ou alterar. |
| `property_value` | O valor que você deseja que a propriedade seja definida. |

Para retornar o valor de qualquer configuração, use `SET [property key]` sem um `property_value`.

## Comandos PostgreSQL

As subseções abaixo abordam os comandos PostgreSQL suportados pelo Serviço de Consulta.

### INÍCIO

O `BEGIN` ou, em alternativa, `BEGIN WORK` ou `BEGIN TRANSACTION` inicia um bloco de transação. Quaisquer instruções inseridas após o comando begin serão executadas em uma única transação até que um comando COMMIT ou ROLLBACK explícito seja fornecido. Este comando é igual ao `START TRANSACTION`.

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### FECHAR

O `CLOSE` libera os recursos associados a um cursor aberto. Depois que o cursor é fechado, nenhuma operação subsequente é permitida nele. Um cursor deve ser fechado quando não for mais necessário.

```sql
CLOSE name
CLOSE ALL
```

If `CLOSE name` é utilizada, `name` representa o nome de um cursor aberto que precisa ser fechado. If `CLOSE ALL` for usado, todos os cursores abertos serão fechados.

### DESALOCAR

O `DEALLOCATE` permite desalocar uma instrução SQL preparada anteriormente. Se você não desalocar explicitamente uma declaração preparada, ela será desalocada quando a sessão terminar. Mais informações sobre instruções preparadas podem ser encontradas na seção [comando PREPARAR](#prepare) seção.

```sql
DEALLOCATE name
DEALLOCATE ALL
```

If `DEALLOCATE name` é utilizada, `name` representa o nome da declaração preparada que precisa ser desalocada. If `DEALLOCATE ALL` for usada, todas as instruções preparadas serão desalocadas.

### DECLARAR

O `DECLARE` permite que um usuário crie um cursor, que pode ser usado para recuperar um pequeno número de linhas de uma consulta maior. Após a criação do cursor, as linhas são buscadas com ele `FETCH`.

```sql
DECLARE name CURSOR FOR query
```

| Parâmetros | Descrição |
| ------ | ------ |
| `name` | O nome do cursor a ser criado. |
| `query` | A `SELECT` ou `VALUES` comando que fornece as linhas a serem retornadas pelo cursor. |

### EXECUTAR

O `EXECUTE` é usado para executar uma instrução preparada anteriormente. Como as instruções preparadas existem apenas para a duração de uma sessão, a instrução preparada deve ter sido criada por um `PREPARE` executada anteriormente na sessão atual. Mais informações sobre o uso de instruções preparadas podem ser encontradas no [`PREPARE` comando](#prepare) seção.

Se a variável `PREPARE` uma instrução que criou a instrução especificou alguns parâmetros, um conjunto de parâmetros compatível deve ser transmitido para a `EXECUTE` instrução. Se esses parâmetros não forem enviados, um erro será gerado.

```sql
EXECUTE name [ ( parameter ) ]
```

| Parâmetros | Descrição |
| ------ | ------ |
| `name` | O nome da instrução preparada a ser executada. |
| `parameter` | O valor real de um parâmetro para a instrução preparada. Deve ser uma expressão que produza um valor compatível com o tipo de dados desse parâmetro, conforme determinado quando a instrução preparada foi criada.  Se houver vários parâmetros para a instrução preparada, eles serão separados por vírgulas. |

### EXPLICAR

O `EXPLAIN` exibe o plano de execução da instrução fornecida. O plano de execução mostra como as tabelas referenciadas pela instrução serão digitalizadas.  Se houver referência a várias tabelas, elas mostrarão quais algoritmos de junção são usados para reunir as linhas necessárias de cada tabela de entrada.

```sql
EXPLAIN option statement
```

Onde `option` pode ser um dos seguintes:

```sql
ANALYZE
FORMAT { TEXT | JSON }
```

| Parâmetros | Descrição |
| ------ | ------ |
| `ANALYZE` | Se a variável `option` contém `ANALYZE`, os tempos de execução e outras estatísticas são mostrados. |
| `FORMAT` | Se a variável `option` contém `FORMAT`, ele especifica o formato de saída, que pode ser `TEXT` ou `JSON`. A saída não textual contém as mesmas informações que o formato de saída de texto, mas é mais fácil para os programas analisar. Esse parâmetro assume como padrão `TEXT`. |
| `statement` | Qualquer `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `VALUES`, `EXECUTE`, `DECLARE`, `CREATE TABLE AS`ou `CREATE MATERIALIZED VIEW AS` , cujo plano de execução você deseja ver. |

>[!IMPORTANT]
>
>Lembre-se de que a instrução é executada quando a variável `ANALYZE` é usada. Embora `EXPLAIN` descarta qualquer saída que uma `SELECT` retorna, outros efeitos colaterais da declaração ocorrem como de costume.

**Exemplo**

O exemplo a seguir mostra o plano de uma consulta simples em uma tabela com um único `integer` coluna e 10000 linhas:

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

O `FETCH` recupera linhas usando um cursor criado anteriormente.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

| Parâmetros | Descrição |
| ------ | ------ |
| `num_of_rows` | O número de linhas a serem buscadas. |
| `cursor_name` | O nome do cursor do qual você está recuperando informações. |

### PREPARAR {#prepare}

O `PREPARE` permite criar uma instrução preparada. Uma instrução preparada é um objeto do lado do servidor que pode ser usado para modelar instruções SQL semelhantes.

As instruções preparadas podem receber parâmetros, que são valores substituídos na instrução quando é executada. Os parâmetros são referenciados por posição, usando $1, $2, etc., ao usar instruções preparadas.

Como opção, você pode especificar uma lista de tipos de dados de parâmetro. Se o tipo de dados de um parâmetro não estiver listado, ele poderá ser inferido do contexto.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

| Parâmetros | Descrição |
| ------ | ------ |
| `name` | O nome da instrução preparada. |
| `data_type` | Os tipos de dados dos parâmetros da instrução preparada. Se o tipo de dados de um parâmetro não estiver listado, ele poderá ser inferido do contexto. Se precisar adicionar vários tipos de dados, é possível adicioná-los em uma lista separada por vírgulas. |

### ROLLBACK

O `ROLLBACK` desfaz a transação atual e descarta todas as atualizações feitas pela transação.

```sql
ROLLBACK
ROLLBACK WORK
```

### SELECIONAR EM

O `SELECT INTO` cria uma nova tabela e a preenche com dados calculados por um query. Os dados não são retornados ao cliente, pois estão em um `SELECT` comando. As colunas da nova tabela têm os nomes e os tipos de dados associados às colunas de saída do `SELECT` comando.

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

Mais informações sobre os parâmetros de consulta SELECT padrão podem ser encontradas no [Seção SELECIONAR query](#select-queries). Esta seção listará apenas os parâmetros exclusivos ao `SELECT INTO` comando.

| Parâmetros | Descrição |
| ------ | ------ |
| `TEMPORARY` ou `TEMP` | Um parâmetro opcional. Se especificado, a tabela criada será uma tabela temporária. |
| `UNLOGGED` | Um parâmetro opcional. Se especificado, a tabela criada como será uma tabela desconectada. Mais informações sobre tabelas desconectadas podem ser encontradas no [Documentação PostgreSQL](https://www.postgresql.org/docs/current/sql-createtable.html). |
| `new_table` | O nome da tabela a ser criada. |

**Exemplo**

A consulta a seguir cria uma nova tabela `films_recent` que consiste apenas em entradas recentes do quadro `films`:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### MOSTRAR

O `SHOW` exibe a configuração atual dos parâmetros de tempo de execução. Essas variáveis podem ser definidas usando a variável `SET` , editando o `postgresql.conf` arquivo de configuração, por meio do `PGOPTIONS` variável ambiental (ao usar libpq ou um aplicativo baseado em libpq) ou por meio de sinalizadores de linha de comando ao iniciar o servidor Postgres.

```sql
SHOW name
SHOW ALL
```

| Parâmetros | Descrição |
| ------ | ------ |
| `name` | O nome do parâmetro de tempo de execução sobre o qual você deseja obter informações. Os valores possíveis para o parâmetro de tempo de execução incluem os seguintes valores:<br>`SERVER_VERSION`: Este parâmetro mostra o número da versão do servidor.<br>`SERVER_ENCODING`: Esse parâmetro mostra a codificação do conjunto de caracteres do lado do servidor.<br>`LC_COLLATE`: Esse parâmetro mostra a configuração de local do banco de dados para agrupamento (ordenação de texto).<br>`LC_CTYPE`: Esse parâmetro mostra a configuração de local do banco de dados para a classificação de caracteres.<br>`IS_SUPERUSER`: Esse parâmetro mostra se a função atual tem privilégios de superusuário. |
| `ALL` | Mostre os valores de todos os parâmetros de configuração com descrições. |

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

O `COPY` comando duplica a saída de qualquer `SELECT` consulta a um local especificado. O usuário deve ter acesso a esse local para que esse comando seja bem-sucedido.

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

| Parâmetros | Descrição |
| ------ | ------ |
| `query` | A consulta que você deseja copiar. |
| `format_name` | O formato no qual você deseja copiar a consulta. O `format_name` pode ser um dos `parquet`, `csv`ou `json`. Por padrão, o valor é `parquet`. |

>[!NOTE]
>
>O caminho de saída completo será `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### ALTERAR TABELA

O `ALTER TABLE` permite adicionar ou soltar restrições de chave primária ou estrangeira, bem como adicionar colunas à tabela.


#### ADICIONAR OU SOLTAR RESTRIÇÃO

As seguintes consultas SQL mostram exemplos de adição ou remoção de restrições a uma tabela.

```sql
ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY column_name NAMESPACE namespace

ALTER TABLE table_name DROP CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT constraint_name FOREIGN KEY ( column_name )
```

| Parâmetros | Descrição |
| ------ | ------ |
| `table_name` | O nome da tabela que você está editando. |
| `constraint_name` | O nome da restrição que você deseja adicionar ou excluir. |
| `column_name` | O nome da coluna à qual você está adicionando uma restrição. |
| `referenced_table_name` | O nome da tabela referenciada pela chave externa. |
| `primary_column_name` | O nome da coluna referenciada pela chave externa. |

>[!NOTE]
>
>O schema da tabela deve ser exclusivo e não compartilhado entre várias tabelas. Além disso, o namespace é obrigatório para restrições de chave primária.

#### ADICIONAR COLUNA

As seguintes consultas SQL mostram exemplos de adição de colunas a uma tabela.

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

#### ADICIONAR ESQUEMA

A consulta SQL a seguir mostra um exemplo de adição de uma tabela a um banco de dados/schema.

```sql
ALTER TABLE table_name ADD SCHEMA database_name.schema_name
```

>[!NOTE]
>
> Tabelas e visualizações ADLS não podem ser adicionadas a bancos de dados/esquemas DWH.


#### REMOVER ESQUEMA

A consulta SQL a seguir mostra um exemplo de remoção de uma tabela de um banco de dados / schema.

```sql
ALTER TABLE table_name REMOVE SCHEMA database_name.schema_name
```

>[!NOTE]
>
> As tabelas e visualizações DWH não podem ser removidas de bancos de dados/esquemas DWH vinculados fisicamente.


**Parâmetros**

| Parâmetros | Descrição |
| ------ | ------ |
| `table_name` | O nome da tabela que você está editando. |
| `column_name` | O nome da coluna que deseja adicionar. |
| `data_type` | O tipo de dados da coluna que você deseja adicionar. Os tipos de dados compatíveis incluem: bigint, char, string, data, datetime, duplo, precisão dupla, inteiro, smallint, tinyint, varchar. |

### MOSTRAR CHAVES PRIMÁRIAS

O `SHOW PRIMARY KEYS` lista todas as restrições de chave primária para o banco de dados em questão.

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

O `SHOW FOREIGN KEYS` lista todas as restrições de chave estrangeira para o banco de dados em questão.

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```


### MOSTRAR DATAGROUPS

O `SHOW DATAGROUPS` retorna uma tabela de todos os bancos de dados associados. Para cada banco de dados, a tabela inclui esquema, tipo de grupo, tipo filho, nome filho e ID filho.

```sql
SHOW DATAGROUPS
```

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                       |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   adls_db     | adls_scheema      | ADLS      | Data Lake Table      | adls_table1                                        | 6149ff6e45cfa318a76ba6d3
   adls_db     | adls_scheema      | ADLS      | Data Warehouse Table | _table_demo1                                       | 22df56cf-0790-4034-bd54-d26d55ca6b21
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view1                                         | c2e7ddac-d41c-40c5-a7dd-acd41c80c5e9
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view4                                         | b280c564-df7e-405f-80c5-64df7ea05fc3
```


### MOSTRAR DATAGROUPS PARA tabela

O `SHOW DATAGROUPS FOR` O comando &#39;table_name&#39; retorna uma tabela de todos os bancos de dados associados que contêm o parâmetro como filho. Para cada banco de dados, a tabela inclui esquema, tipo de grupo, tipo filho, nome filho e ID filho.

```sql
SHOW DATAGROUPS FOR 'table_name'
```

**Parâmetros**

- `table_name`: O nome da tabela para a qual você deseja encontrar bancos de dados associados.

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                      |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   dwh_db_demo | schema2           | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   dwh_db_demo | schema1           | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   qsaccel     | profile_aggs      | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
```
