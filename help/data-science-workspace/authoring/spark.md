---
keywords: Experience Platform;home;popular topics;data access;spark sdk;data access api;spark recipe;read spark;write spark
solution: Experience Platform
title: Acessar dados usando o Spark
topic: tutorial
type: Tutorial
description: O documento a seguir contém exemplos de como acessar dados usando o Spark para uso na Data Science Workspace.
translation-type: tm+mt
source-git-commit: fcb4088ecac76d10b0cb69b04ad55167f5cdac3e
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---


# Acessar dados usando o Spark

O documento a seguir contém exemplos de como acessar dados usando o Spark para uso na Data Science Workspace. Para obter informações sobre como acessar dados usando notebooks JupyterLab, visite a documentação de acesso [aos dados dos notebooks](../jupyterlab/access-notebook-data.md) JupyterLab.

## Introdução

O uso [!DNL Spark] requer otimizações de desempenho que precisam ser adicionadas ao `SparkSession`. Além disso, também é possível configurar `configProperties` para que posteriormente seja possível ler e gravar em conjuntos de dados.

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
            val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
            val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
            val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
            val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
            val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

   }
}
```

## Lendo um conjunto de dados

Ao usar o Spark, você tem acesso a dois modos de leitura: interativo e em lote.

O modo interativo cria uma conexão JDBC (Java Database Connectivity) para [!DNL Query Service] e obtém resultados por meio de um JDBC comum `ResultSet` que é automaticamente traduzido para um `DataFrame`. Esse modo funciona de forma semelhante ao [!DNL Spark] método incorporado `spark.read.jdbc()`. Este modo destina-se apenas a pequenos conjuntos de dados. Se o conjunto de dados exceder 5 milhões de linhas, recomendamos que você troque para o modo lote.

O modo Lote usa o comando COPY [!DNL Query Service]do para gerar conjuntos de resultados Parquet em um local compartilhado. Esses arquivos Parquet podem ser processados posteriormente.

Um exemplo de leitura de um conjunto de dados no modo interativo pode ser visto abaixo:

```scala
  // Read the configs
    val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
    val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

 val dataSetId: String = configProperties.get(taskId).getOrElse("")

    // Load the dataset
    var df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
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

Da mesma forma, um exemplo de leitura de um conjunto de dados no modo de lote pode ser visto abaixo:

```scala
val df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
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

A cláusula DISTINCT permite buscar todos os valores distintos em um nível de linha/coluna, removendo todos os valores de duplicado da resposta.

Um exemplo de uso da `distinct()` função pode ser visto abaixo:

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### cláusula WHERE

O [!DNL Spark] SDK permite dois métodos de filtragem: Usando uma expressão SQL ou filtrando por meio de condições.

Um exemplo do uso dessas funções de filtragem pode ser visto abaixo:

#### EXPRESSÃO SQL

```scala
df.where("age > 15")
```

#### Condições de filtragem

```scala
df.where("age" > 15 || "name" = "Steve")
```

### Cláusula ORDER BY

A cláusula ORDER BY permite que os resultados recebidos sejam classificados por uma coluna especificada em uma ordem específica (crescente ou decrescente). No [!DNL Spark] SDK, isso é feito usando a `sort()` função.

Um exemplo de uso da `sort()` função pode ser visto abaixo:

```scala
df = df.sort($"column1", $"column2".desc)
```

### Cláusula LIMIT

A cláusula LIMIT permite limitar o número de registros recebidos do conjunto de dados.

Um exemplo de uso da `limit()` função pode ser visto abaixo:

```scala
df = df.limit(100)
```

## Gravação em um conjunto de dados

Usando seu `configProperties` mapeamento, você pode gravar em um conjunto de dados no Experience Platform usando `QSOption`.

```scala
val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString 

    df.write.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.datasetId, scoringResultsDataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .save()
```


## Próximas etapas

A Adobe Experience Platform Data Science Workspace fornece uma amostra de fórmula Scala (Spark) que usa as amostras de código acima para ler e gravar dados. Se quiser saber mais sobre como usar o Spark para acessar seus dados, consulte o Repositório [Scala GitHub da](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala)Data Science.