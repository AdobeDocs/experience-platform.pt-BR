---
title: Habilitar captura de dados de alteração para conexões de origem na API
description: Saiba como habilitar a captura de dados de alteração para conexões de origem na API
exl-id: 362f3811-7d1e-4f16-b45f-ce04f03798aa
source-git-commit: 2ad0ffba128e8c51f173d24d4dd2404b9cbbb59a
workflow-type: tm+mt
source-wordcount: '1261'
ht-degree: 0%

---

# Habilitar captura de dados de alteração para conexões de origem na API

Use a captura de dados de alteração em origens do Adobe Experience Platform para manter seus sistemas de origem e destino sincronizados em tempo quase real.

Atualmente, o Experience Platform oferece suporte a **cópia de dados incremental**, que transfere periodicamente registros recém-criados ou atualizados do sistema de origem para os conjuntos de dados assimilados. Este método depende de uma **coluna de carimbo de data/hora** para rastrear as alterações, mas não detecta exclusões, o que pode levar a inconsistências de dados ao longo do tempo.

Por outro lado, a captura de dados de alteração captura e aplica inserções, atualizações e exclusões em tempo quase real. Esse controle abrangente de alterações garante que os conjuntos de dados permaneçam totalmente alinhados ao sistema de origem e fornece um histórico completo de alterações, além do que a cópia incremental suporta. No entanto, as operações de exclusão exigem consideração especial, pois afetam todos os aplicativos que usam os conjuntos de dados de destino.

A alteração da captura de dados no Experience Platform requer o **[Data Mirror](../../../xdm/data-mirror/overview.md)** com [esquemas relacionais](../../../xdm/schema/relational.md). Você pode fornecer dados de alteração ao Data Mirror de duas maneiras:

* **[Controle manual de alterações](#file-based-sources)**: inclua uma coluna `_change_request_type` em seu conjunto de dados para fontes que não geram nativamente registros de captura de dados de alteração
* **[Exportações de captura de dados de alteração nativa](#database-sources)**: usar registros de captura de dados de alteração exportados diretamente do sistema de origem

Ambas as abordagens exigem o Data Mirror com esquemas relacionais para preservar relacionamentos e impor exclusividade.

## Data Mirror com esquemas relacionais

>[!AVAILABILITY]
>
>O Data Mirror e esquemas relacionais estão disponíveis para os **titulares de licença de campanhas orquestradas** da Adobe Journey Optimizer. Eles também estão disponíveis como uma **versão limitada** para usuários do Customer Journey Analytics, dependendo da sua licença e da ativação de recursos. Entre em contato com o representante da Adobe para obter acesso.

>[!NOTE]
>
>Esquemas relacionais eram anteriormente chamados de esquemas baseados em modelo em versões anteriores da documentação do Adobe Experience Platform. A funcionalidade e os recursos de captura de dados de alteração permanecem inalterados.

>[!NOTE]
>
>**Usuários de campanhas orquestradas**: use os recursos do Data Mirror descritos neste documento para trabalhar com dados do cliente que mantenham integridade referencial. Mesmo que a origem não use a formatação de captura de dados de alteração, o Data Mirror oferece suporte a recursos relacionais, como imposição de chave primária, upserts em nível de registro e relacionamentos de esquema. Esses recursos garantem uma modelagem de dados consistente e confiável em todos os conjuntos de dados conectados.

O Data Mirror usa esquemas relacionais para estender a captura de dados de alteração e habilitar recursos avançados de sincronização de banco de dados. Para obter uma visão geral do Data Mirror, consulte [visão geral do Data Mirror](../../../xdm/data-mirror/overview.md).

Os esquemas relacionais estendem o Experience Platform para impor a exclusividade da chave primária, rastrear alterações no nível da linha e definir relações no nível do esquema. Com a captura de dados de alteração, eles aplicam inserções, atualizações e exclusões diretamente no data lake, reduzindo a necessidade de extrair, transformar, carregar (ETL) ou reconciliação manual.

Consulte [Visão geral de esquemas relacionais](../../../xdm/schema/relational.md) para obter mais informações.

### Requisitos de esquema relacional para captura de dados de alteração

Antes de usar um esquema relacional com captura de dados de alteração, configure os seguintes identificadores:

* Identifique exclusivamente cada registro com uma chave primária.
* Aplique atualizações em sequência usando um identificador de versão.
* Para esquemas de série temporal, adicione um identificador de carimbo de data e hora.

### Controlar manuseio de coluna {#control-column-handling}

Use a coluna `_change_request_type` para especificar como cada linha deve ser processada:

* `u` — substituir (padrão se a coluna estiver ausente)
* `d` — excluir

Essa coluna é avaliada somente durante a assimilação e não é armazenada ou mapeada para campos XDM.

### Fluxo de trabalho {#workflow}

Para habilitar a captura de dados de alteração com um esquema relacional:

1. Criar um esquema relacional.
2. Adicione os descritores necessários:
   * [Descritor de chave primária](../../../xdm/api/descriptors.md#primary-key-descriptor)
   * [Descritor de versão](../../../xdm/api/descriptors.md#version-descriptor)
   * [Descritor de carimbo de data/hora](../../../xdm/api/descriptors.md#timestamp-descriptor) (somente série temporal)
3. Crie um conjunto de dados a partir do esquema e ative a captura de dados de alteração.
4. Somente para assimilação baseada em arquivo: adicione a coluna `_change_request_type` aos arquivos de origem se precisar especificar explicitamente operações de exclusão. As configurações de exportação do CDC lidam com isso automaticamente para fontes de banco de dados.
5. Conclua a configuração da conexão de origem para habilitar a assimilação.

>[!NOTE]
>
>A coluna `_change_request_type` só é necessária para fontes baseadas em arquivo (Amazon S3, Azure Blob, Armazenamento da Google Cloud, SFTP) quando você deseja controlar explicitamente o comportamento de alteração no nível da linha. Para fontes de banco de dados com recursos nativos do CDC, as operações de alteração são tratadas automaticamente por meio de configurações de exportação do CDC. A assimilação baseada em arquivo presume operações de substituição por padrão. Você só precisará adicionar essa coluna se quiser especificar operações de exclusão nos uploads de arquivo.

>[!IMPORTANT]
>
>**O planejamento de exclusão de dados é necessário**. Todos os aplicativos que usam esquemas relacionais devem entender as implicações de exclusão antes de implementar a captura de dados de alteração. Planeje como as exclusões afetarão os conjuntos de dados relacionados, os requisitos de conformidade e os processos de downstream. Consulte [considerações sobre higiene de dados](../../../hygiene/ui/record-delete.md#relational-record-delete) para obter orientação.

## Fornecendo dados de alteração para fontes baseadas em arquivo {#file-based-sources}

>[!IMPORTANT]
>
>A captura de dados de alteração baseada em arquivo requer o Data Mirror com esquemas relacionais. Antes de seguir as etapas de formatação de arquivo abaixo, verifique se você concluiu o [fluxo de trabalho de instalação do Data Mirror](#workflow) descrito anteriormente neste documento. As etapas abaixo descrevem como formatar seus arquivos de dados para incluir informações de controle de alterações que serão processadas pelo Data Mirror.

Para fontes baseadas em arquivo ([!DNL Amazon S3], [!DNL Azure Blob], [!DNL Google Cloud Storage] e [!DNL SFTP]), inclua uma coluna `_change_request_type` em seus arquivos.

Use os valores `_change_request_type` definidos na seção [Manuseio de coluna de controle](#control-column-handling) acima.

>[!IMPORTANT]
>
>Somente para **fontes baseadas em arquivo**, alguns aplicativos podem exigir uma coluna `_change_request_type` com `u` (substituição) ou `d` (exclusão) para validar os recursos de controle de alterações. Por exemplo, o recurso **Campanhas orquestradas** da Adobe Journey Optimizer exige essa coluna para habilitar a opção &quot;Campanha orquestrada&quot; e permitir a seleção de conjuntos de dados para direcionamento. Os requisitos de validação específicos do aplicativo podem variar.

Siga as etapas específicas da origem abaixo.

### Fontes de armazenamento na nuvem {#cloud-storage-sources}

Habilite a captura de dados de alteração para fontes de armazenamento na nuvem seguindo estas etapas:

1. Crie uma conexão básica para sua origem:

   | Fonte | Guia de conexão básica |
   |---|---|
   | [!DNL Amazon S3] | [Criar uma [!DNL Amazon S3] conexão básica](../api/create/cloud-storage/s3.md) |
   | [!DNL Azure Blob] | [Criar uma [!DNL Azure Blob] conexão básica](../api/create/cloud-storage/blob.md) |
   | [!DNL Google Cloud Storage] | [Criar uma [!DNL Google Cloud Storage] conexão básica](../api/create/cloud-storage/google.md) |
   | [!DNL SFTP] | [Criar uma [!DNL SFTP] conexão básica](../api/create/cloud-storage/sftp.md) |

2. [Criar uma conexão de origem para um armazenamento na nuvem](../api/collect/cloud-storage.md#create-a-source-connection).

Todas as fontes de armazenamento na nuvem usam o mesmo formato de coluna `_change_request_type` descrito na seção [Fontes baseadas em arquivo](#file-based-sources) acima.

## Origens de Banco de Dados {#database-sources}

### [!DNL Azure Databricks]

Para usar a captura de dados de alteração com o [!DNL Azure Databricks], você deve habilitar o **feed de dados de alteração** nas tabelas de origem e configurar o Data Mirror com esquemas relacionais no Experience Platform.

Use os seguintes comandos para habilitar a alteração do feed de dados nas tabelas:

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

### [!DNL Data Landing Zone]

Para usar a captura de dados de alteração com o [!DNL Data Landing Zone], você deve habilitar o **feed de dados de alteração** nas tabelas de origem e configurar o Data Mirror com esquemas relacionais no Experience Platform.

Leia a documentação a seguir para obter as etapas sobre como habilitar a captura de dados de alteração para sua conexão de origem do [!DNL Data Landing Zone]:

* [Criar uma [!DNL Data Landing Zone] conexão básica](../api/create/cloud-storage/data-landing-zone.md).
* [Criar uma conexão de origem para um armazenamento na nuvem](../api/collect/cloud-storage.md#create-a-source-connection).

### [!DNL Google BigQuery]

Para usar a captura de dados de alteração com o [!DNL Google BigQuery], você deve habilitar o histórico de alterações nas tabelas de origem e configurar o Data Mirror com esquemas relacionais no Experience Platform.

Para habilitar o histórico de alterações na conexão de origem do [!DNL Google BigQuery], navegue até a página [!DNL Google BigQuery] no console [!DNL Google Cloud] e defina `enable_change_history` como `TRUE`. Essa propriedade ativa o histórico de alterações da tabela de dados.

Para obter mais informações, leia o manual sobre [instruções de linguagem de definição de dados em [!DNL GoogleSQL]](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list).

Leia a documentação a seguir para obter as etapas sobre como habilitar a captura de dados de alteração para sua conexão de origem do [!DNL Google BigQuery]:

* [Criar uma [!DNL Google BigQuery] conexão básica](../api/create/databases/bigquery.md).
* [Criar uma conexão de origem para um banco de dados](../api/collect/database-nosql.md#create-a-source-connection).

### [!DNL Snowflake]

Para usar a captura de dados de alteração com [!DNL Snowflake], você deve habilitar o **controle de alterações** nas tabelas de origem e configurar o Data Mirror com esquemas relacionais no Experience Platform.

Em [!DNL Snowflake], habilite o controle de alterações usando `ALTER TABLE` e definindo `CHANGE_TRACKING` como `TRUE`.

```sql
ALTER TABLE mytable SET CHANGE_TRACKING = TRUE
```

Para obter mais informações, leia o [[!DNL Snowflake] guia sobre como usar a cláusula de alterações](https://docs.snowflake.com/en/sql-reference/constructs/changes#usage-notes).

Leia a documentação a seguir para obter as etapas sobre como habilitar a captura de dados de alteração para sua conexão de origem do [!DNL Snowflake]:

* [Criar uma [!DNL Snowflake] conexão básica](../api/create/databases/snowflake.md).
* [Criar uma conexão de origem para um banco de dados](../api/collect/database-nosql.md#create-a-source-connection).
