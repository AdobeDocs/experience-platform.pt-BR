---
title: Práticas recomendadas para a organização de ativos de dados no serviço de consulta
description: Este documento descreve um meio lógico de organizar os dados para facilitar o uso com o Serviço de consulta.
exl-id: 12d6af99-035a-4f80-b7c0-c6413aa50697
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 0%

---

# Organizar ativos de dados no Serviço de consulta

Este documento fornece orientação sobre as práticas recomendadas para organizar ativos de dados, incluindo conjuntos de dados, exibições e tabelas temporárias para uso com o Serviço de consulta da Adobe Experience Platform. Ela aborda como estruturar seus dados, bem como informações sobre como acessar, atualizar e excluir essas informações.

É importante organizar logicamente seus ativos de dados na Experience Platform [!DNL Data Lake] à medida que eles crescem. O Serviço de consulta estende as construções SQL que permitem agrupar logicamente os ativos de dados em uma sandbox. Esse método de organização permite o compartilhamento de ativos de dados entre esquemas sem a necessidade de movê-los fisicamente.

## Introdução

Antes de continuar com este documento, você deve conhecer bem os recursos do [Serviço de Consulta](../home.md) e ter lido o [guia da interface do usuário](../ui/user-guide.md).

## Organização de dados no Serviço de consulta

Os exemplos a seguir demonstram as construções disponíveis por meio do Adobe Experience Platform Query Service para organizar logicamente seus dados usando a sintaxe SQL padrão. Você deve começar criando um banco de dados que atue como um container para seus pontos de dados. Um banco de dados pode conter um ou mais esquemas, e cada esquema pode ter uma ou mais referências a um ativo de dados (conjuntos de dados, visualizações, tabelas temporárias etc.). Essas referências incluem quaisquer relações ou associações entre os conjuntos de dados.

Consulte o [guia do usuário do Editor de Consultas](../ui/user-guide.md) para obter orientações detalhadas sobre como usar a interface do usuário do Serviço de Consulta para criar consultas SQL.

As seguintes construções SQL para organizar logicamente conjuntos de dados em uma sandbox são compatíveis.

```SQL
CREATE DATABASE databaseA;
CREATE SCHEMA databaseA.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

O exemplo (ligeiramente truncado por brevidade) demonstra essa metodologia em que `databaseA` contém o esquema `schema1`.

## Associar ativos de dados a um esquema

Depois que um esquema é criado para atuar como um container dos ativos de dados, cada conjunto de dados pode ser associado a um ou mais esquemas no banco de dados usando a sintaxe SQL ALTER TABLE.

O exemplo a seguir adiciona `dataset1`, `dataset2`, `dataset3` e `v1` ao contêiner `databaseA.schema1` criado no exemplo anterior.

```SQL
ALTER TABLE dataset1 ADD SCHEMA databaseA.schema1;
 
ALTER TABLE dataset2 ADD SCHEMA databaseA.schema1;
 
ALTER TABLE dataset3 ADD SCHEMA databaseA.schema1;
 
ALTER VIEW v1  ADD SCHEMA databaseA.schema1;
```

## Acessar ativos de dados do container de dados

Qualificando adequadamente o nome do banco de dados, qualquer cliente do [!DNL PostgreSQL] pode se conectar a qualquer estrutura de dados criada usando a palavra-chave SHOW. Para obter mais informações sobre a palavra-chave SHOW, consulte a seção [SHOW na documentação da sintaxe SQL](../sql/syntax.md#show).

&quot;all&quot; é o nome de banco de dados padrão que contém cada banco de dados e container de esquema em uma sandbox. Ao fazer uma conexão [!DNL PostgreSQL] usando o `dbname="all"`, você pode acessar qualquer **banco de dados e esquema** criados para organizar logicamente seus dados.

A listagem de todos os bancos de dados em `dbname="all"` exibe três bancos de dados disponíveis.

```sql
SHOW DATABASES;
  
name     
|---------
databaseA
databaseB
databaseC
```

Listar todos os esquemas em `dbname="all"` exibe os três esquemas relacionados a cada banco de dados na sandbox.

```SQL
SHOW SCHEMAS;
  
database       | schema
|----------------------
databaseA      | schema1
databaseA      | schema2
databaseB      | schema3
```

Ao fazer uma conexão [!DNL PostgreSQL] usando `dbname="databaseA"`, você pode acessar qualquer esquema associado a esse banco de dados específico, como mostrado no exemplo abaixo.

```sql
SHOW DATABASES;
  
name     
|---------
databaseA
 

SHOW SCHEMAS;
  
database       | schema
|----------------------
databaseA      | schema1
databaseA      | schema2
```

A notação de pontos permite acessar cada tabela associada a um esquema específico conectado ao banco de dados escolhido. Conectando-se a `DBNAME = databaseA.schema1;`, todas as tabelas associadas a esse esquema específico (`schema1`) são mostradas. Isso fornece informações sobre qual conjunto de dados contém qual tabela.

```sql
SHOW DATABASES;
  
name     
|---------
databaseA


SHOW SCHEMAS;
  
database       | schema
|----------------------
databaseA      | schema1


SHOW tables;
name       | type
|----------------------
dataset1| table
dataset2| table
dataset3| table
```

## Atualizar ou remover ativos de dados de um container de dados

À medida que a quantidade de ativos de dados em sua organização (ou sandbox) aumenta, é necessário atualizar ou remover ativos de dados de um contêiner de dados. Os ativos individuais podem ser removidos do container da organização fazendo referência ao banco de dados e ao nome do esquema apropriados usando a notação de pontos. A tabela e a exibição (`t1` e `v1` respectivamente) adicionadas a `databaseA.schema1` no primeiro exemplo, são removidas usando a sintaxe no exemplo a seguir.

```sql
ALTER TABLE databaseA.schema2.t1 REMOVE SCHEMA databaseA.schema2;
ALTER VIEW databaseA.schema2.v1 REMOVE SCHEMA databaseA.schema2;
```

### Remover ativos de dados

A função [DROP TABLE](../sql/syntax.md#drop-table) remove apenas fisicamente um ativo de dados de [!DNL Data Lake] quando existe uma única referência à tabela em todos os bancos de dados da organização.

```sql
DROP TABLE databaseA.schema2.t1;
```

### Remover um contêiner de ativo de dados

O banco de dados e o schema também podem ser removidos usando funções SQL padrão.

#### Remover um banco de dados

Se houver outras referências a ativos de dados associados ao banco de dados, a função exibirá um erro ao tentar remover o banco de dados.

```sql
DROP DATABASE databaseA;
```

#### Remover um esquema

Há três considerações importantes a serem observadas ao remover um esquema:

- A remoção de um esquema não exclui fisicamente nenhum ativo de dados, como tabelas, exibições ou tabelas temporárias.
- Se houver ativos de dados referenciados no esquema de destino e o modo for RESTRICT, uma exceção será lançada.
- Se houver ativos de dados referenciados no esquema de destino e o modo for CASCADE, o sistema removerá todos os ativos de dados referenciados pelo container do esquema e excluirá o container do esquema.

```sql
DROP SCHEMA databaseA.schema2;
```

## Próximas etapas

Ao ler este documento, agora você tem uma melhor compreensão das práticas recomendadas relacionadas à organização e à estrutura de seus ativos de dados para uso com o Serviço de consulta da Adobe Experience Platform. É recomendável continuar aprendendo sobre as práticas recomendadas do Serviço de Consulta lendo sobre a [documentação de eliminação da duplicação de dados](../key-concepts/deduplication.md).
