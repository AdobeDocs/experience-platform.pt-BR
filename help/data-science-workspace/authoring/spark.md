---
keywords: Experience Platform;home;popular topics;acesso aos dados;spark sdk;acesso aos dados api;receita de faísca;ler faísca;faísca de gravação
solution: Experience Platform
title: Acessar dados usando o Spark na Data Science Workspace
topic: tutorial
type: Tutorial
description: O documento a seguir contém exemplos de como acessar dados usando o Spark para uso na Data Science Workspace.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---


# Acessar dados usando o Spark na Data Science Workspace

O documento a seguir contém exemplos de como acessar dados usando o Spark para uso na Data Science Workspace. Para obter informações sobre como acessar dados usando notebooks JupyterLab, visite a documentação [Acesso aos notebooks JupyterLab](../jupyterlab/access-notebook-data.md).

## Introdução

O uso de [!DNL Spark] requer otimizações de desempenho que precisam ser adicionadas a `SparkSession`. Além disso, você também pode configurar `configProperties` para, posteriormente, ler e gravar em conjuntos de dados.

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

## Lendo um conjunto de dados

Ao usar o Spark, você tem acesso a dois modos de leitura: interativo e em lote.

O modo interativo cria uma conexão JDBC (Java Database Connectivity) com [!DNL Query Service] e obtém resultados por meio de um JDBC regular `ResultSet` que é automaticamente traduzido para um `DataFrame`. Esse modo funciona de forma semelhante ao método [!DNL Spark] incorporado `spark.read.jdbc()`. Este modo destina-se apenas a pequenos conjuntos de dados. Se o conjunto de dados exceder 5 milhões de linhas, recomendamos que você troque para o modo lote.

O modo de lote usa o comando COPY de [!DNL Query Service] para gerar conjuntos de resultados do Parquet em um local compartilhado. Esses arquivos Parquet podem ser processados posteriormente.

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

Da mesma forma, um exemplo de leitura de um conjunto de dados no modo de lote pode ser visto abaixo:

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

A cláusula DISTINCT permite buscar todos os valores distintos em um nível de linha/coluna, removendo todos os valores de duplicado da resposta.

Um exemplo de uso da função `distinct()` pode ser visto abaixo:

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### cláusula WHERE

O SDK [!DNL Spark] permite dois métodos de filtragem: Usando uma expressão SQL ou filtrando por meio de condições.

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

A cláusula ORDER BY permite que os resultados recebidos sejam classificados por uma coluna especificada em uma ordem específica (crescente ou decrescente). No SDK [!DNL Spark], isso é feito usando a função `sort()`.

Um exemplo de uso da função `sort()` pode ser visto abaixo:

```scala
df = df.sort($"column1", $"column2".desc)
```

### Cláusula LIMIT

A cláusula LIMIT permite limitar o número de registros recebidos do conjunto de dados.

Um exemplo de uso da função `limit()` pode ser visto abaixo:

```scala
df = df.limit(100)
```

## Gravação em um conjunto de dados

Usando o mapeamento `configProperties`, você pode gravar em um conjunto de dados no Experience Platform usando `QSOption`.

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

A Adobe Experience Platform Data Science Workspace fornece uma amostra de fórmula Scala (Spark) que usa as amostras de código acima para ler e gravar dados. Se quiser saber mais sobre como usar o Spark para acessar seus dados, consulte [Repositório Scala GitHub da Data Science](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala).