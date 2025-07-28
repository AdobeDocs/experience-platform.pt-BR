---
title: Habilitar captura de dados de alteração para conexões de origem na API
description: Saiba como habilitar a captura de dados de alteração para conexões de origem na API
source-git-commit: d8b4557424e1f29dfdd8893932aef914226dd60d
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---

# Habilitar captura de dados de alteração para conexões de origem na API

A captura de dados de alteração nas origens do Adobe Experience Platform é um recurso que você pode usar para manter a sincronização de dados em tempo real entre os sistemas de origem e de destino.

Atualmente, o Experience Platform oferece suporte a **cópia de dados incremental**, o que garante que registros recém-criados ou atualizados no sistema de origem sejam copiados periodicamente para os conjuntos de dados assimilados. Este processo depende do uso da **coluna de carimbo de data/hora**, como `LastModified`, para rastrear alterações e capturar **apenas os dados recém-inseridos ou atualizados**. No entanto, esse método não leva em conta os registros excluídos, o que pode levar a inconsistências de dados ao longo do tempo.

Com a captura de dados de alteração, um determinado fluxo captura e aplica todas as alterações, incluindo inserções, atualizações e exclusões. Da mesma forma, os conjuntos de dados do Experience Platform permanecem totalmente sincronizados com o sistema de origem.

Você pode usar a captura de dados de alteração para as seguintes origens:

## [!DNL Amazon S3]

Verifique se `_change_request_type` está presente no arquivo [!DNL Amazon S3] que você pretende assimilar na Experience Platform. Além disso, verifique se os seguintes valores válidos estão incluídos no arquivo:

* `u`: para inserções e atualizações
* `d`: para exclusões.

Se `_change_request_type` não estiver presente no arquivo, o valor padrão `u` será usado.

Leia a documentação a seguir para obter as etapas sobre como habilitar a captura de dados de alteração para sua conexão de origem do [!DNL Amazon S3]:

* [Criar uma [!DNL Amazon S3] conexão básica](../api/create/cloud-storage/s3.md).
* [Criar uma conexão de origem para um armazenamento na nuvem](../api/collect/cloud-storage.md#create-a-source-connection).

## [!DNL Azure Blob]

Verifique se `_change_request_type` está presente no arquivo [!DNL Azure Blob] que você pretende assimilar na Experience Platform. Além disso, verifique se os seguintes valores válidos estão incluídos no arquivo:

* `u`: para inserções e atualizações
* `d`: para exclusões.

Se `_change_request_type` não estiver presente no arquivo, o valor padrão `u` será usado.

Leia a documentação a seguir para obter as etapas sobre como habilitar a captura de dados de alteração para sua conexão de origem do [!DNL Azure Blob]:

* [Criar uma [!DNL Azure Blob] conexão básica](../api/create/cloud-storage/blob.md).
* [Criar uma conexão de origem para um armazenamento na nuvem](../api/collect/cloud-storage.md#create-a-source-connection).

## [!DNL Azure Databricks]

Você deve habilitar o **feed de dados de alteração** na tabela [!DNL Azure Databricks] para usar a captura de dados de alteração na conexão de origem.

Use os seguintes comandos para habilitar explicitamente a opção de alteração de feed de dados em [!DNL Azure Databricks]

**Nova tabela**

Para aplicar o feed de dados de alteração a uma nova tabela, defina a propriedade de tabela `delta.enableChangeDataFeed` como `TRUE` no comando `CREATE TABLE`.

```sql
CREATE TABLE student (id INT, name STRING, age INT) TBLPROPERTIES (delta.enableChangeDataFeed = true)
```

**Tabela existente**

Para aplicar o feed de dados de alteração a uma tabela existente, defina a propriedade de tabela `delta.enableChangeDataFeed` como `TRUE` no comando `ALTER TABLE`.

```sql
ALTER TABLE myDeltaTable SET TBLPROPERTIES (delta.enableChangeDataFeed = true)
```

**Todas as novas tabelas**

Para aplicar o feed de dados de alteração a todas as novas tabelas, defina suas propriedades padrão como `TRUE`.

```sql
set spark.databricks.delta.properties.defaults.enableChangeDataFeed = true;
```

Para obter mais informações, leia o [[!DNL Azure Databricks] guia sobre como habilitar o feed de dados de alteração](https://docs.databricks.com/aws/en/delta/delta-change-data-feed#enable-change-data-feed).

Leia a documentação a seguir para obter as etapas sobre como habilitar a captura de dados de alteração para sua conexão de origem do [!DNL Azure Databricks]:

* [Criar uma [!DNL Azure Databricks] conexão básica](../api/create/databases/databricks.md).
* [Criar uma conexão de origem para um banco de dados](../api/collect/database-nosql.md#create-a-source-connection).

## [!DNL Data Landing Zone]

Você deve habilitar o **feed de dados de alteração** na tabela [!DNL Data Landing Zone] para usar a captura de dados de alteração na conexão de origem.

Use os comandos a seguir para habilitar explicitamente a opção de alteração de feed de dados em [!DNL Data Landing Zone].

Leia a documentação a seguir para obter as etapas sobre como habilitar a captura de dados de alteração para sua conexão de origem do [!DNL Data Landing Zone]:

* [Criar uma [!DNL Data Landing Zone] conexão básica](../api/create/cloud-storage/data-landing-zone.md).
* [Criar uma conexão de origem para um armazenamento na nuvem](../api/collect/cloud-storage.md#create-a-source-connection).

## [!DNL Google BigQuery]

Para usar a captura de dados de alteração na conexão de origem do [!DNL Google BigQuery]. Navegue até a página [!DNL Google BigQuery] no console [!DNL Google Cloud] e defina `enable_change_history` como `TRUE`. Essa propriedade ativa o histórico de alterações da tabela de dados.

Para obter mais informações, leia o manual sobre [instruções de linguagem de definição de dados em [!DNL GoogleSQL]](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list).

Leia a documentação a seguir para obter as etapas sobre como habilitar a captura de dados de alteração para sua conexão de origem do [!DNL Google BigQuery]:

* [Criar uma [!DNL Google BigQuery] conexão básica](../api/create/databases/bigquery.md).
* [Criar uma conexão de origem para um banco de dados](../api/collect/database-nosql.md#create-a-source-connection).

## [!DNL Google Cloud Storage]

Verifique se `_change_request_type` está presente no arquivo [!DNL Google Cloud Storage] que você pretende assimilar na Experience Platform. Além disso, verifique se os seguintes valores válidos estão incluídos no arquivo:

* `u`: para inserções e atualizações
* `d`: para exclusões.

Se `_change_request_type` não estiver presente no arquivo, o valor padrão `u` será usado.

Leia a documentação a seguir para obter as etapas sobre como habilitar a captura de dados de alteração para sua conexão de origem do [!DNL Google Cloud Storage]:

* [Criar uma [!DNL Google Cloud Storage] conexão básica](../api/create/cloud-storage/google.md).
* [Criar uma conexão de origem para um armazenamento na nuvem](../api/collect/cloud-storage.md#create-a-source-connection).


## [!DNL SFTP]

Verifique se `_change_request_type` está presente no arquivo [!DNL SFTP] que você pretende assimilar na Experience Platform. Além disso, verifique se os seguintes valores válidos estão incluídos no arquivo:

* `u`: para inserções e atualizações
* `d`: para exclusões.

Se `_change_request_type` não estiver presente no arquivo, o valor padrão `u` será usado.

Leia a documentação a seguir para obter as etapas sobre como habilitar a captura de dados de alteração para sua conexão de origem do [!DNL SFTP]:

* [Criar uma [!DNL SFTP] conexão básica](../api/create/cloud-storage/sftp.md).
* [Criar uma conexão de origem para um armazenamento na nuvem](../api/collect/cloud-storage.md#create-a-source-connection).


## [!DNL Snowflake]

Você deve habilitar o **controle de alterações** nas tabelas [!DNL Snowflake] para usar a captura de dados de alterações em suas conexões de origem.

Em [!DNL Snowflake], habilite o controle de alterações usando `ALTER TABLE` e definindo `CHANGE_TRACKING` como `TRUE`.

```sql
ALTER TABLE mytable SET CHANGE_TRACKING = TRUE
```

Para obter mais informações, leia o [[!DNL Snowflake] guia sobre como usar a cláusula de alterações](https://docs.snowflake.com/en/sql-reference/constructs/changes#usage-notes).

Leia a documentação a seguir para obter as etapas sobre como habilitar a captura de dados de alteração para sua conexão de origem do [!DNL Snowflake]:

* [Criar uma [!DNL Snowflake] conexão básica](../api/create/databases/snowflake.md).
* [Criar uma conexão de origem para um banco de dados](../api/collect/database-nosql.md#create-a-source-connection).

