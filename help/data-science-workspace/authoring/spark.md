---
keywords: Experience Platform;página inicial;tópicos populares;acesso a dados;spark sdk;api de acesso a dados;spark revenue;read spark;write spark
solution: Experience Platform
title: Acesso a dados usando o Spark no Espaço de trabalho de ciência de dados
type: Tutorial
description: O documento a seguir contém exemplos de como acessar dados usando o Spark para uso no Data Science Workspace.
exl-id: 9bffb52d-1c16-4899-b455-ce570d76d3b4
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Acesso a dados usando o Spark no Espaço de trabalho de ciência de dados

O documento a seguir contém exemplos de como acessar dados usando o Spark para uso no Data Science Workspace. Para obter informações sobre como acessar dados usando notebooks JupyterLab, visite o [Acesso aos dados de notebooks JupyterLab](../jupyterlab/access-notebook-data.md) documentação.

## Introdução

Usar [!DNL Spark] O requer otimizações de desempenho que precisam ser adicionadas ao `SparkSession`. Além disso, você também pode configurar `configProperties` para ler e gravar posteriormente em conjuntos de dados.

```scala
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.query.QSOption
import org.apache.spark.sql.{DataFrame, SparkSession}

Class Helper {

 /**
   *
   * @param configProperties - Configuration Properties map
   * @param sparkSession     - SparkSession
   * @return                 - DataFrame which is loaded for training
   */

   def load_dataset(configProperties: ConfigProperties, sparkSession: SparkSession, taskId: String): DataFrame = {
            // Read the configs
            val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
            val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
            val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
            val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

   }
}
```

## Ler um conjunto de dados

Ao usar o Spark, você tem acesso a dois modos de leitura: interativo e em lote.

O modo interativo cria uma conexão Java Database Connectivity (JDBC) para [!DNL Query Service] e obtém resultados por meio de um JDBC comum `ResultSet` que é traduzido automaticamente para um `DataFrame`. Esse modo funciona de forma semelhante ao modo incorporado [!DNL Spark] método `spark.read.jdbc()`. Esse modo destina-se somente a conjuntos de dados pequenos. Se o conjunto de dados exceder 5 milhões de linhas, é recomendável alternar para o modo de lote.

Usos do modo de lote [!DNL Query Service]O comando COPY do para gerar conjuntos de resultados do Parquet em um local compartilhado. Esses arquivos do Parquet podem ser processados posteriormente.

Um exemplo de leitura de um conjunto de dados no modo interativo pode ser visto abaixo:

```scala
  // Read the configs
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
    val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

 val dataSetId: String = configProperties.get(taskId).getOrElse("")

    // Load the dataset
    var df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, "interactive")
      .option(QSOption.datasetId, dataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .load()
    df.show()
    df
  }
```

Da mesma forma, um exemplo de leitura de um conjunto de dados em modo de lote pode ser visto abaixo:

```scala
val df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, "batch")
      .option(QSOption.datasetId, dataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .load()
    df.show()
    df
```

### SELECIONAR colunas do conjunto de dados

```scala
df = df.select("column-a", "column-b").show()
```

### Cláusula DISTINCT

A cláusula DISTINCT permite buscar todos os valores distintos em nível de linha/coluna, removendo todos os valores duplicados da resposta.

Um exemplo de uso da variável `distinct()` pode ser vista abaixo:

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### Cláusula WHERE

A variável [!DNL Spark] O SDK permite dois métodos de filtragem: usando uma expressão SQL ou filtrando por meio de condições.

Um exemplo do uso dessas funções de filtragem pode ser visto abaixo:

#### Expressão SQL

```scala
df.where("age > 15")
```

#### Condições de filtragem

```scala
df.where("age" > 15 || "name" = "Steve")
```

### Cláusula ORDER BY

A cláusula ORDER BY permite que os resultados recebidos sejam classificados por uma coluna especificada em uma ordem específica (crescente ou decrescente). No [!DNL Spark] SDK, isso é feito usando o `sort()` função.

Um exemplo de uso da variável `sort()` pode ser vista abaixo:

```scala
df = df.sort($"column1", $"column2".desc)
```

### Cláusula LIMIT

A cláusula LIMIT permite limitar o número de registros recebidos do conjunto de dados.

Um exemplo de uso da variável `limit()` pode ser vista abaixo:

```scala
df = df.limit(100)
```

## Gravação em um conjunto de dados

Usar seu `configProperties` mapeamento, é possível gravar em um conjunto de dados no Experience Platform usando `QSOption`.

```scala
val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString 

    df.write.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.datasetId, scoringResultsDataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .save()
```


## Próximas etapas

O Espaço de trabalho de ciência de dados da Adobe Experience Platform fornece uma amostra de fórmula do Scala (Spark) que usa as amostras de código acima para ler e gravar dados. Se quiser saber mais sobre como usar o Spark para acessar seus dados, reveja o [Repositório GitHub da Escala do Data Science Workspace](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala).
