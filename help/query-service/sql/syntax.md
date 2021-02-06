---
keywords: Experience Platform;home;popular topics;query service;Query service;sql syntax;sql;ctas;CTAS;Criar tabela como selecionar
solution: Experience Platform
title: Sintaxe SQL no Query Service
topic: syntax
description: Este documento mostra a sintaxe SQL suportada pelo Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: 97dc0b5fb44f5345fd89f3f56bd7861668da9a6e
workflow-type: tm+mt
source-wordcount: '2221'
ht-degree: 0%

---


# Sintaxe SQL no Query Service

[!DNL Query Service] fornece a capacidade de usar SQL ANSI padrão para  `SELECT` instruções e outros comandos limitados. Este documento mostra a sintaxe SQL suportada por [!DNL Query Service].

## Definir um query SELECT

A sintaxe a seguir define um query `SELECT` suportado por [!DNL Query Service]:

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

em que `from_item` pode ser um dos seguintes:

```sql
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    [ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
    with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

e `grouping_element` pode ser um dos seguintes:

```sql
( )
    expression
    ( expression [, ...] )
    ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
    CUBE ( { expression | ( expression [, ...] ) } [, ...] )
    GROUPING SETS ( grouping_element [, ...] )
```

e `with_query` é:

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
 
TABLE [ ONLY ] table_name [ * ]
```

### Cláusula SNAPSHOT

Essa cláusula pode ser usada para ler dados em uma tabela de forma incremental com base em IDs de snapshot. Uma ID de instantâneo é um marcador de ponto de verificação identificado por um número, do tipo Longo, em uma tabela de datalake sempre que os dados são gravados nela. A cláusula SNAPSHOT se anexa à relação da tabela à qual é usada.

```sql
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
```

#### Exemplo

```sql
SELECT * FROM Customers SNAPSHOT SINCE 123;

SELECT * FROM Customers SNAPSHOT AS OF 345;

SELECT * FROM Customers SNAPSHOT BETWEEN 123 AND 345;

SELECT * FROM (SELECT id FROM CUSTOMERS BETWEEN 123 AND 345) C 

SELECT * FROM Customers SNAPSHOT SINCE 123 INNER JOIN Inventory AS OF 789 ON Customers.id = Inventory.id;
```

Observe que uma cláusula SNAPSHOT funciona com um alias de tabela ou tabela, mas não sobre um subquery ou visualização. Uma cláusula SNAPHOST funcionará em qualquer lugar em que um query SELECT em uma tabela possa ser aplicado.

### Cláusula WHERE ILIKE

A palavra-chave ILIKE pode ser usada em vez de LIKE para fazer correspondências na cláusula WHERE da seção SELECT query não diferencia maiúsculas de minúsculas.

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

A lógica das cláusulas LIKE e ILIKE é a seguinte:
- ```WHERE condition LIKE pattern```,  ```~~``` é equivalente ao padrão
- ```WHERE condition NOT LIKE pattern```,  ```!~~``` é equivalente ao padrão
- ```WHERE condition ILIKE pattern```,  ```~~*``` equivalente ao padrão
- ```WHERE condition NOT ILIKE pattern```,  ```!~~*``` equivalente ao padrão


#### Exemplo

```sql
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

Retorna clientes com nomes que começam em &quot;A&quot; ou &quot;a&quot;.

## JUNTOS

Um query `SELECT` usando joins tem a seguinte sintaxe:

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```


## UNIÃO, INTERSECT e EXCETO

As cláusulas `UNION`, `INTERSECT` e `EXCEPT` são suportadas para combinar ou excluir linhas como linhas de duas ou mais tabelas:

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

## CRIAR TABELA COMO SELECIONAR

A sintaxe a seguir define um query `CREATE TABLE AS SELECT` (CTAS) suportado por [!DNL Query Service]:

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

em que,
`target_schema_title` é o título do schema XDM. Use esta cláusula somente se desejar usar um schema XDM existente para o novo conjunto de dados criado pelo query CTAS
`rowvalidation` especifica se o usuário deseja a validação em nível de linha de todos os novos lotes ingeridos para o novo conjunto de dados criado. O valor padrão é &#39;true&#39;

e `select_query` é uma instrução `SELECT`, cuja sintaxe é definida acima neste documento.


### Exemplo

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
```

Observe que para um determinado query CTAS:

1. A instrução `SELECT` deve ter um alias para as funções de agregação, como `COUNT`, `SUM`, `MIN` e assim por diante.
2. A instrução `SELECT` pode ser fornecida com ou sem parênteses ().
3. A instrução `SELECT` pode ser fornecida com uma cláusula SNAPSHOT para ler deltas incrementais na tabela de públicos alvos.

```sql
CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

## INSERIR EM

A sintaxe a seguir define um query `INSERT INTO` suportado por [!DNL Query Service]:

```sql
INSERT INTO table_name select_query
```

em que `select_query` é uma instrução `SELECT`, cuja sintaxe é definida acima neste documento.

### Exemplo

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;
```

Observe que para um determinado query INSERIR EM:

1. A instrução `SELECT` NÃO DEVE estar entre parênteses ().
2. O schema do resultado da instrução `SELECT` deve estar em conformidade com o da tabela definida na instrução `INSERT INTO`.
3. A instrução `SELECT` pode ser fornecida com uma cláusula SNAPSHOT para ler deltas incrementais na tabela de públicos alvos.

```sql
INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

### TABELA DE SOLTA

Solte uma tabela e exclua o diretório associado à tabela do sistema de arquivos se esta não for uma tabela EXTERNA. Se a tabela a ser solta não existir, uma exceção ocorrerá.

```sql
DROP [TEMP] TABLE [IF EXISTS] [db_name.]table_name
```

### Parâmetros

- `IF EXISTS`: Se a tabela não existir, nada acontece
- `TEMP`: Tabela temporária

## CRIAR VISUALIZAÇÃO

A sintaxe a seguir define um query `CREATE VIEW` suportado por [!DNL Query Service]:

```sql
CREATE [ OR REPLACE ] VIEW view_name AS select_query
```

Onde `view_name` é o nome da visualização a ser criada
e `select_query` é uma instrução `SELECT`, cuja sintaxe é definida acima neste documento.

Exemplo:

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory
CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

### Visualização DE SOLTE

A sintaxe a seguir define um query `DROP VIEW` suportado por [!DNL Query Service]:

```sql
DROP VIEW [IF EXISTS] view_name
```

Em que `view_name` é o nome da visualização a ser excluída

Exemplo:

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## [!DNL Spark] Comandos SQL

### CONJUNTO

Defina uma propriedade, retorne o valor de uma propriedade existente ou lista todas as propriedades existentes. Se um valor for fornecido para uma chave de propriedade existente, o valor antigo será substituído.

```sql
SET property_key [ To | =] property_value
```

Para retornar o valor de qualquer configuração, use `SHOW [setting name]`.

## Comandos PostgreSQL

### INÍCIO

Este comando é analisado e o comando concluído é enviado de volta para o cliente. É o mesmo que o comando `START TRANSACTION`.

```sql
BEGIN [ TRANSACTION ]
```

#### Parâmetros

- `TRANSACTION`: Palavras-chave opcionais. Escuta, não se toma nenhuma medida a este respeito.

### FECHAR

`CLOSE` libera os recursos associados a um cursor aberto. Depois que o cursor é fechado, nenhuma operação subsequente é permitida nele. Um cursor deve ser fechado quando não for mais necessário.

```sql
CLOSE { name }
```

#### Parâmetros

- `name`: o nome de um cursor aberto a ser fechado.

### CONFIRMAR

Nenhuma ação é executada em [!DNL Query Service] como resposta à declaração de transação de confirmação.

```sql
COMMIT [ WORK | TRANSACTION ]
```

#### Parâmetros

- `WORK`
- `TRANSACTION`: Palavras-chave opcionais. Eles não têm efeito.

### DESALOCAR

Use `DEALLOCATE` para desalocar uma instrução SQL preparada anteriormente. Se você não desalocar explicitamente uma declaração preparada, ela será desalocada quando a sessão terminar.

```sql
DEALLOCATE [ PREPARE ] { name | ALL }
```

#### Parâmetros

- `Prepare`: Esta palavra-chave é ignorada.
- `name`: O nome da instrução preparada a ser desalocada.
- `ALL`: Desalocar todas as declarações preparadas.

### DECLARAR

`DECLARE` permite que um usuário crie cursores, que podem ser usados para recuperar um pequeno número de linhas por vez fora de um query maior. Depois que o cursor é criado, as linhas são extraídas dele usando `FETCH`.

```sql
DECLARE name CURSOR [ WITH  HOLD ] FOR query
```

#### Parâmetros

- `name`: O nome do cursor a ser criado.
- `WITH HOLD`: Especifica que o cursor pode continuar a ser usado depois que a transação que o criou for confirmada com êxito.
- `query`: Um  `SELECT` ou  `VALUES` comando que fornece as linhas a serem retornadas pelo cursor.

### EXECUTE

`EXECUTE` é usada para executar uma instrução preparada anteriormente. Como as instruções preparadas existem apenas para a duração de uma sessão, a instrução preparada deve ter sido criada por uma instrução `PREPARE` executada anteriormente na sessão atual.

Se a instrução `PREPARE` que criou a instrução especificou alguns parâmetros, um conjunto de parâmetros compatível deve ser passado para a instrução `EXECUTE`, caso contrário, um erro será gerado. Observe que as instruções preparadas (diferentes das funções) não são sobrecarregadas com base no tipo ou número de seus parâmetros. O nome de uma instrução preparada deve ser exclusivo em uma sessão do banco de dados.

```sql
EXECUTE name [ ( parameter [, ...] ) ]
```

#### Parâmetros

- `name`: O nome da instrução preparada a ser executada.
- `parameter`: O valor real de um parâmetro para a instrução preparada. Essa deve ser uma expressão que produz um valor compatível com o tipo de dados desse parâmetro, conforme determinado quando a instrução preparada foi criada.

### EXPLICAÇÃO

Esse comando exibe o plano de execução gerado pelo planejador PostgreSQL para a instrução fornecida. O plano de execução mostra como as tabelas referenciadas pela instrução serão digitalizadas. por varredura sequencial simples, varredura de índice e assim por diante... e se várias tabelas forem referenciadas, quais algoritmos de junção serão usados para reunir as linhas necessárias de cada tabela de entrada.

A parte mais crítica da exibição é o custo estimado de execução do demonstrativo, que é a estimativa do planejador quanto tempo levará para executar o demonstrativo (medido em unidades de custo que são arbitrárias, mas convencionalmente são buscas de página em disco). Na verdade, dois números são mostrados: o custo de start antes da primeira linha pode ser retornado e o custo total para retornar todas as linhas. Para a maioria dos query, o custo total é o que importa, mas em contextos como uma subconsulta em EXISTS, o planejador escolhe o menor custo de start em vez do menor custo total (porque o executor para depois de obter uma linha, de qualquer forma). Além disso, se você limitar o número de linhas a retornar com uma cláusula `LIMIT`, o planejador fará uma interpolação apropriada entre os custos do ponto de extremidade para estimar qual plano é realmente o mais barato.

A opção `ANALYZE` faz com que a instrução seja executada, não apenas planejada. Em seguida, as estatísticas do tempo de execução real são adicionadas à exibição, incluindo o tempo total gasto em cada nó do plano (em milissegundos) e o número total de linhas retornadas. Isso é útil para ver se as estimativas do planejador estão próximas da realidade.

```sql
EXPLAIN [ ( option [, ...] ) ] statement
EXPLAIN [ ANALYZE ] statement

where option can be one of:
    ANALYZE [ boolean ]
    TYPE VALIDATE
    FORMAT { TEXT | JSON }
```

#### Parâmetros

- `ANALYZE`: Execute o comando e mostre os tempos de execução reais e outras estatísticas. Esse parâmetro assume `FALSE` como padrão.
- `FORMAT`: Especifique o formato de saída, que pode ser TEXT, XML, JSON ou YAML. A saída não textual contém as mesmas informações que o formato de saída de texto, mas é mais fácil para os programas analisarem. Esse parâmetro assume `TEXT` como padrão.
- `statement`: Qualquer  `SELECT`,  `INSERT`,  `UPDATE` `DELETE`,  `VALUES`,  `EXECUTE`,  `DECLARE`,  `CREATE TABLE AS`ou  `CREATE MATERIALIZED VIEW AS` instrução, cujo plano de execução você deseja ver.

>[!IMPORTANT]
>
>Lembre-se de que a instrução é executada quando a opção `ANALYZE` é usada. Embora `EXPLAIN` descarte qualquer saída retornada por `SELECT`, outros efeitos colaterais da declaração ocorrem como de costume.

#### Exemplo

Para mostrar o plano de um query simples em uma tabela com uma única coluna `integer` e 10000 linhas:

```sql
EXPLAIN SELECT * FROM foo;

                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### BUSCA

`FETCH` recupera linhas usando um cursor criado anteriormente.

Um cursor tem uma posição associada, que é usada por `FETCH`. A posição do cursor pode ser anterior à primeira linha do resultado do query, em qualquer linha específica do resultado ou após a última linha do resultado. Quando criado, um cursor é posicionado antes da primeira linha. Depois de buscar algumas linhas, o cursor é posicionado na linha recuperada mais recentemente. Se `FETCH` for executado fora do final das linhas disponíveis, o cursor será posicionado à esquerda após a última linha. Se essa linha não existir, um resultado vazio será retornado e os cursores serão posicionados antes da primeira linha ou depois da última linha, conforme apropriado.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

#### Parâmetros

- `num_of_rows`: Uma constante inteira possivelmente assinada, determinando o local ou o número de linhas a serem buscadas.
- `cursor_name`: Um nome de cursor aberto.

### PREPARAR

`PREPARE` cria uma declaração preparada. Uma instrução preparada é um objeto do lado do servidor que pode ser usado para otimizar o desempenho. Quando a instrução `PREPARE` é executada, a instrução especificada é analisada, analisada e regravada. Quando um comando `EXECUTE` é emitido posteriormente, a instrução preparada é planejada e executada. Esta divisão de trabalho evita o trabalho repetitivo de análise de análise, permitindo ao mesmo tempo que o plano de execução dependa dos valores de parâmetro específicos fornecidos.

As instruções preparadas podem usar parâmetros, valores que são substituídos na instrução quando ela é executada. Ao criar a declaração preparada, consulte os parâmetros por posição, usando $1, $2 e assim por diante. Como opção, é possível especificar uma lista correspondente de tipos de dados de parâmetro. Quando o tipo de dados de um parâmetro não é especificado ou é declarado como desconhecido, o tipo é inferido do contexto no qual o parâmetro é referenciado pela primeira vez, se possível. Ao executar a instrução, especifique os valores reais para esses parâmetros na instrução `EXECUTE`.

As instruções preparadas duram apenas pela duração da sessão atual do banco de dados. Quando a sessão terminar, a declaração preparada será esquecida, portanto, ela deve ser recriada antes de ser usada novamente. Isso também significa que uma única instrução preparada não pode ser usada por vários clientes simultâneos do banco de dados. No entanto, cada cliente pode criar sua própria declaração preparada para usar. As instruções preparadas podem ser limpas manualmente usando o comando `DEALLOCATE`.

As instruções preparadas têm potencialmente a maior vantagem de desempenho quando uma única sessão está sendo usada para executar um grande número de instruções semelhantes. A diferença de desempenho é particularmente significativa se as declarações forem complexas de planejar ou regravar, por exemplo, se o query envolver uma junção de muitas tabelas ou exigir a aplicação de várias regras. Se a instrução for relativamente simples de planejar e regravar, mas relativamente dispendiosa de executar, a vantagem de desempenho das instruções preparadas é menos perceptível.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

#### Parâmetros

- `name`: Um nome arbitrário dado a esta declaração preparada em particular. Ela deve ser exclusiva em uma única sessão e é subsequentemente usada para executar ou desalocar uma instrução preparada anteriormente.
- `data-type`: O tipo de dados de um parâmetro para a instrução preparada. Se o tipo de dados de um determinado parâmetro não for especificado ou for especificado como desconhecido, ele será inferido do contexto no qual o parâmetro é referenciado pela primeira vez. Para se referir aos parâmetros na própria declaração preparada, use $1, $2 e assim por diante.


### ROLLBACK

`ROLLBACK` reverte a transação atual e faz com que todas as atualizações feitas pela transação sejam descartadas.

```sql
ROLLBACK [ WORK ]
```

#### Parâmetros

- `WORK`

### SELECIONAR EM

`SELECT INTO` cria uma nova tabela e a preenche com dados calculados por um query. Os dados não são retornados para o cliente, como acontece com um `SELECT` normal. As colunas da nova tabela têm os nomes e os tipos de dados associados às colunas de saída de `SELECT`.

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

#### Parâmetros

- `TEMPORARAY` ou  `TEMP`: Se especificada, a tabela é criada como uma tabela temporária.
- `UNLOGGED:` se especificada, a tabela é criada como uma tabela desconectada.
- `new_table` O nome (opcionalmente qualificado para schema) da tabela a ser criada.

#### Exemplo

Crie uma nova tabela `films_recent` que consiste apenas em entradas recentes da tabela `films`:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### MOSTRAR

`SHOW` exibe a configuração atual dos parâmetros de tempo de execução. Essas variáveis podem ser definidas usando a instrução `SET`, editando o arquivo de configuração postgresql.conf, por meio da variável ambiental `PGOPTIONS` (ao usar libpq ou um aplicativo baseado em libpq) ou por meio de sinalizadores de linha de comando ao iniciar o servidor de pôsteres.

```sql
SHOW name
```

#### Parâmetros

- `name`
   - `SERVER_VERSION`: Mostra o número de versão do servidor.
   - `SERVER_ENCODING`: Mostra a codificação do conjunto de caracteres do lado do servidor. Atualmente, esse parâmetro pode ser exibido, mas não definido, pois a codificação é determinada no momento da criação do banco de dados.
   - `LC_COLLATE`: Mostra a configuração de local do banco de dados para agrupamento (ordenação de texto). Atualmente, esse parâmetro pode ser exibido, mas não definido, pois a configuração é determinada no momento da criação do banco de dados.
   - `LC_CTYPE`: Mostra a configuração de localidade do banco de dados para a classificação de caracteres. Atualmente, esse parâmetro pode ser exibido, mas não definido, pois a configuração é determinada no momento da criação do banco de dados.
      `IS_SUPERUSER`: True se a função atual tiver privilégios de superusuário.
- `ALL`: Mostre os valores de todos os parâmetros de configuração com descrições.

#### Exemplo

Mostrar a configuração atual do parâmetro `DateStyle`

```sql
SHOW DateStyle;
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### TRANSAÇÃO DE start

Esse comando é analisado e envia o comando concluído de volta para o cliente. É o mesmo que o comando `BEGIN`.

```sql
START TRANSACTION [ transaction_mode [, ...] ]

where transaction_mode is one of:

    ISOLATION LEVEL { SERIALIZABLE | REPEATABLE READ | READ COMMITTED | READ UNCOMMITTED }
    READ WRITE | READ ONLY
```

### COPIAR

Este comando descarrega a saída de qualquer query SELECT para um local especificado. O usuário deve ter acesso a esse local para que esse comando seja bem-sucedido.

```sql
COPY  query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']

where 'format_name' is be one of:
    'parquet', 'csv', 'json'

'parquet' is the default format.
```

>[!NOTE]
>
>O caminho de saída completo será `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`


### ALTERAR

Esse comando ajuda a adicionar ou soltar restrições de chave primária ou estrangeira na tabela.

```sql
Alter TABLE table_name ADD CONSTRAINT Primary key ( column_name )

Alter TABLE table_name ADD CONSTRAINT Foreign key ( column_name ) references referenced_table_name ( primary_column_name )

Alter TABLE table_name ADD CONSTRAINT Foreign key ( column_name ) references referenced_table_name Namespace 'namespace'

Alter TABLE table_name DROP CONSTRAINT Primary key ( column_name )

Alter TABLE table_name DROP CONSTRAINT  Foreign key ( column_name )
```

>[!NOTE]
>O schema de tabela deve ser exclusivo e não compartilhado entre várias tabelas. Além disso, a namespace é obrigatória.


### MOSTRAR CHAVES PRIMÁRIAS

Esse comando lista todas as restrições de chave primária para o banco de dados especificado.

```sql
SHOW PRIMARY KEYS
    tableName | columnName    | datatype | namespace
------------------+----------------------+----------+-----------
 table_name_1 | column_name1  | text     | "ECID"
 table_name_2 | column_name2  | text     | "AAID"
```


### MOSTRAR CHAVES ESTRANGEIRAS

Esse comando lista todas as restrições de chave estrangeira para o banco de dados especificado.

```sql
SHOW FOREIGN KEYS
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```
