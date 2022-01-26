---
title: Práticas recomendadas para a organização de ativos de dados no serviço de query
description: Este documento descreve um meio lógico de organizar dados para facilitar o uso com o Serviço de query.
source-git-commit: ed9fa7b83f9e1c974bc74e9dde018a87823954ee
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# Organizar ativos de dados no Serviço de query

Este documento fornece orientação sobre as práticas recomendadas para organizar ativos de dados, incluindo conjuntos de dados, exibições e tabelas temporárias para usar com o Serviço de query da Adobe Experience Platform. Ela aborda como estruturar seus dados, bem como informações sobre como acessar, atualizar e excluir essas informações.

É importante organizar logicamente seus ativos de dados na plataforma [!DNL Data Lake] à medida que crescem. O Serviço de Consulta estende construções SQL que permitem agrupar logicamente ativos de dados em uma sandbox. Esse método de organização permite o compartilhamento de ativos de dados entre esquemas sem a necessidade de movê-los fisicamente.

## Introdução

Antes de continuar com este documento, você deve ter uma boa compreensão de [Serviço de query](../home.md) e ler o [guia da interface do usuário](../ui/user-guide.md).

## Organização de dados no Serviço de Consulta

Os exemplos a seguir demonstram as construções disponíveis por meio do Adobe Experience Platform Query Service para organizar logicamente seus dados usando a sintaxe SQL padrão. Você deve começar criando um banco de dados para agir como um container dos pontos de dados. Um banco de dados pode conter um ou mais schemas e cada schema pode ter uma ou mais referências a um ativo de dados (conjuntos de dados, exibições, tabelas temporárias etc). Essas referências incluem qualquer relacionamento ou associação entre os conjuntos de dados.

Consulte a [Guia do usuário do Editor de consultas](../ui/user-guide.md) para obter orientações detalhadas sobre como usar a interface do usuário do serviço de query para criar consultas SQL.

As seguintes construções SQL para organizar logicamente conjuntos de dados em uma sandbox são compatíveis.

```SQL
CREATE DATABASE databaseA;
CREATE SCHEMA databaseA.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

O exemplo (ligeiramente truncado por brevidade) demonstra essa metodologia, em que `databaseA` contém schema `schema1`.

## Associar ativos de dados a um schema

Depois que um schema é criado para atuar como um container dos ativos de dados, cada conjunto de dados pode ser associado a um ou mais schemas no banco de dados usando a sintaxe padrão SQL ALTER TABLE.

O exemplo a seguir adiciona `dataset1`, `dataset2`, `dataset3` e `v1` para `databaseA.schema1` container criado no exemplo anterior.

```SQL
ALTER TABLE dataset1 SET SCHEMA databaseA.schema1;
 
ALTER TABLE dataset2 SET SCHEMA databaseA.schema1;
 
ALTER TABLE dataset3 SET SCHEMA databaseA.schema1;
 
ALTER VIEW v1  SET SCHEMA databaseA.schema1;
```

## Acessar ativos de dados do contêiner de dados

Ao qualificar apropriadamente o nome do banco de dados, qualquer [!DNL PostgreSQL] O cliente pode se conectar a qualquer uma das estruturas de dados criadas usando a palavra-chave SHOW. Para obter mais informações sobre a palavra-chave SHOW, consulte o [seção MOSTRAR na documentação da sintaxe SQL](../sql/syntax.md#show).

&quot;all&quot; é o nome padrão do banco de dados que contém cada banco de dados e contêiner de esquema em uma sandbox. Quando você faz uma [!DNL PostgreSQL] conexão usando `dbname="all"`, você pode acessar **any** banco de dados e esquema criados para organizar logicamente seus dados.

Listar todos os bancos de dados em `dbname="all"` O exibe três bancos de dados disponíveis.

```sql
SHOW DATABASES;
  
name     
---------
databaseA
databaseB
databaseC
```

Listar todos os esquemas em `dbname="all"` exibe os três esquemas relacionados a cada banco de dados na sandbox.

```SQL
SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
databaseB      | schema3
```

Quando você faz uma [!DNL PostgreSQL] conexão usando `dbname="databaseA"`, você pode acessar qualquer esquema associado ao banco de dados específico, conforme mostrado no exemplo abaixo.

```sql
SHOW DATABASES;
  
name     
---------
databaseA
 

SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
```

A notação de pontos permite acessar todas as tabelas associadas a um schema específico conectado ao banco de dados escolhido. Ao conectar-se a `DBNAME = databaseA.schema1;`, todas as tabelas associadas a esse schema específico (`schema1`) são mostradas. Isso fornece informações sobre qual conjunto de dados contém qual tabela.

```sql
SHOW DATABASES;
  
name     
---------
databaseA


SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1


SHOW tables;
name       | type
----------------------
dataset1| table
dataset2| table
dataset3| table
```

## Atualizar ou remover ativos de dados de um contêiner de dados

À medida que a quantidade de ativos de dados na organização IMS (ou sandbox) aumenta, torna-se necessário atualizar ou remover ativos de dados de um contêiner de dados. Os ativos individuais podem ser removidos do container da organização fazendo referência ao banco de dados e ao nome do schema apropriados usando a notação de pontos. A tabela e a exibição (`t1` e `v1` , respectivamente) `databaseA.schema1` no primeiro exemplo, são removidos usando a sintaxe no exemplo a seguir.

```sql
ALTER TABLE databaseA.schema2.t1 REMOVE SCHEMA databaseA.schema2;
ALTER VIEW databaseA.schema2.v1 REMOVE SCHEMA databaseA.schema2;
```

### Remover ativos de dados

O [TABELA DE SOLTAÇÕES](../sql/syntax.md#drop-table) remove fisicamente apenas um ativo de dados do [!DNL Data Lake] quando existe uma única referência à tabela em todos os bancos de dados na organização IMS.

```sql
DROP TABLE databaseA.schema2.t1;
```

### Remover um contêiner de ativo de dados

O banco de dados e o schema também podem ser removidos usando funções SQL padrão.

#### Remover um banco de dados

Se houver outras referências aos ativos de dados associados ao banco de dados, a função emitirá um erro ao tentar remover o banco de dados.

```sql
DROP DATABASE databaseA;
```

#### Remover um esquema

Há três considerações importantes a serem observadas ao remover um schema:

- A remoção de um schema não exclui fisicamente quaisquer ativos de dados, como tabelas, exibições ou tabelas temporárias.
- Se houver algum ativo de dados referenciado no schema de destino e o modo for RESTRICT, uma exceção será lançada.
- Se houver ativos de dados referenciados no schema de destino e o modo for CASCADE, o sistema removerá todos os ativos de dados referenciados pelo contêiner de esquema e excluirá o contêiner de esquema.

```sql
DROP SCHEMA databaseA.schema2;
```

## Próximas etapas

Ao ler este documento, você agora tem uma melhor compreensão das práticas recomendadas relacionadas à organização e estrutura dos ativos de dados para usar com o Serviço de query da Adobe Experience Platform. É recomendável continuar aprendendo sobre as práticas recomendadas do Serviço de query lendo sobre [documentação de desduplicação de dados](./deduplication.md).
