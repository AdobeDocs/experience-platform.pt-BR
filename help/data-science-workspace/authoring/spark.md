---
keywords: Experience Platform; Casa; tópicos populares; acesso a dados; spark sdk; api de acesso a dados; fórmula de faísca; ler faísca; gravar faísca
solution: Experience Platform
title: Acesso a dados usando o Spark em Área de trabalho de ciência de dados
type: Tutorial
description: A documento a seguir contém exemplos sobre como acessar dados usando o Spark para uso em Área de trabalho de ciência de dados.
exl-id: 9bffb52d-1c16-4899-b455-ce570d76d3b4
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Acesso a dados usando o Spark no Data Science Área de trabalho

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

O documento a seguir contém exemplos de como acessar dados usando o Spark para uso no Data Science Workspace. Para obter informações sobre como acessar dados usando notebooks JupyterLab, visite a documentação do [JupyterLab notebooks data access](../jupyterlab/access-notebook-data.md).

## Introdução

O uso de [!DNL Spark] requer otimizações de desempenho que precisam ser adicionadas ao `SparkSession`. Além disso, você também pode configurar o `configProperties` para mais tarde, para ler e gravar em conjuntos de dados.

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

O modo interativo cria uma conexão [!DNL Query Service] de Conectividade de banco de dados Java (JDBC) e obtém resultados através de um JDBC `ResultSet` regular que é traduzido automaticamente para um `DataFrame`. Esse modo funciona de forma semelhante ao método `spark.read.jdbc()`integrado[!DNL Spark]. Esse modo destina-se somente a pequenos conjuntos de dados. Se sua conjunto de dados exceder 5 milhões de linhas, sugere-se que você troque para o modo em lote.

O modo de lote usa o comando COPY de [!DNL Query Service] para gerar conjuntos de resultados do Parquet em um local compartilhado. Esses arquivos do Parquet podem ser processados posteriormente.

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

Um exemplo de uso da função `distinct()` pode ser visto abaixo:

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### CLÁUSULA ONDE

O [!DNL Spark] SDK permite dois métodos de filtragem: usar um expressão SQL ou filtrar por meio de condições.

Um exemplo do uso dessas funções de filtragem pode ser visto abaixo:

#### expressão SQL

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

## Escrever em um conjunto de dados

Usando o `configProperties` mapeamento, você pode escrever em um conjunto de dados em Experience Platform usando `QSOption`.

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

O Adobe Experience Platform Data Science Workspace fornece uma amostra de fórmula do Scala (Spark) que usa as amostras de código acima para ler e gravar dados. Se quiser saber mais sobre como usar o Spark para acessar seus dados, reveja o [Repositório GitHub do Data Science Workspace Scala](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala).
