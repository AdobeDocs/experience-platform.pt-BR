---
keywords: Experience Platform;guia do desenvolvedor;SDK;Criação de modelos;Data Science Workspace;tópicos populares;teste
solution: Experience Platform
title: SDK de criação de modelo
description: O SDK de criação de modelo permite desenvolver receitas e pipelines de recursos de aprendizado de máquina personalizados que podem ser usados no Adobe Experience Platform Data Science Workspace, fornecendo modelos implementáveis no PySpark e no Spark (Scala).
exl-id: c7577f93-a64f-49b7-a76d-71f21d619052
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 1%

---

# SDK de criação de modelo

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

A SDK de Criação de Modelo permite desenvolver Fórmulas de aprendizado de máquina personalizadas e Pipelines de Recursos que podem ser usados no Data Science Workspace [!DNL Adobe Experience Platform], fornecendo modelos implementáveis em [!DNL PySpark] e [!DNL Spark (Scala)].

Este documento fornece informações sobre as várias classes encontradas no SDK de criação de modelo.

## DataLoader {#dataloader}

A classe DataLoader encapsula tudo relacionado à recuperação, filtragem e retorno de dados brutos de entrada. Exemplos de dados de entrada incluem aqueles para treinamento, pontuação ou engenharia de recursos. Os carregadores de dados estendem a classe abstrata `DataLoader` e devem substituir o método abstrato `load`.

**PySpark**

A tabela a seguir descreve os métodos abstratos de uma classe PySpark Data Loader:

<table>
    <thead>
        <tr>
            <th>Método e descrição</th>
            <th>Parâmetros</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>load(self, configProperties, spark)</code></p>
                <p>Carregar e retornar dados do Experience Platform como um DataFrame Pandas</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: autorreferência</li>
                    <li><code>configProperties</code>: mapa de propriedades de configuração</li>
                    <li><code>spark</code>: Sessão do Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

A tabela a seguir descreve os métodos abstratos de uma classe de Carregador de Dados [!DNL Spark]:

<table>
    <thead>
        <tr>
            <th>Método e descrição</th>
            <th>Parâmetros</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>load(configProperties, sparkSession)</code></p>
                <p>Carregar e retornar dados do Experience Platform como um DataFrame</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: mapa de propriedades de configuração</li>
                    <li><code>sparkSession</code>: Sessão do Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### Carregar dados de um conjunto de dados [!DNL Experience Platform] {#load-data-from-a-platform-dataset}

O exemplo a seguir recupera dados de [!DNL Experience Platform] por ID e retorna um DataFrame, no qual a ID do conjunto de dados (`datasetId`) é uma propriedade definida no arquivo de configuração.

**PySpark**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    """
    Implementation of DataLoader which loads a DataFrame and prepares data
    """

    def load_dataset(config_properties, spark, task_id):

        PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"
        PLATFORM_SDK_PQS_INTERACTIVE = "interactive"

        # prepare variables
        service_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        dataset_id = str(config_properties.get(task_id))

        # validate variables
        for arg in ['service_token', 'user_token', 'org_id', 'dataset_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # load dataset through Spark session

        query_options = get_query_options(spark.sparkContext)

        pd = spark.read.format(PLATFORM_SDK_PQS_PACKAGE) \
            .option(query_options.userToken(), user_token) \
            .option(query_options.serviceToken(), service_token) \
            .option(query_options.imsOrg(), org_id) \
            .option(query_options.apiKey(), api_key) \
            .option(query_options.mode(), PLATFORM_SDK_PQS_INTERACTIVE) \
            .option(query_options.datasetId(), dataset_id) \
            .load()
        pd.show()

        # return as DataFrame
        return pd
```

**Spark (Scala)**

```scala
// Spark

package com.adobe.platform.ml

import java.time.LocalDateTime

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.query.QSOption
import org.apache.spark.ml.feature.StringIndexer
import org.apache.spark.sql.expressions.Window
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.{StructType, TimestampType}
import org.apache.spark.sql.{DataFrame, SparkSession}
import org.apache.spark.sql.Column

/**
 * Implementation of DataLoader which loads a DataFrame and prepares data
 */
class MyDataLoader extends DataLoader {

    final val PLATFORM_SDK_PQS_PACKAGE: String = "com.adobe.platform.query"
    final val PLATFORM_SDK_PQS_INTERACTIVE: String = "interactive"
    final val PLATFORM_SDK_PQS_BATCH: String = "batch"

    /**
    *
    * @param configProperties - Configuration Properties map
    * @param sparkSession     - SparkSession
    * @return                 - DataFrame which is loaded for training
    */


  def load_dataset(configProperties: ConfigProperties, sparkSession: SparkSession, taskId: String): DataFrame = {

    require(configProperties != null)
    require(sparkSession != null)

    // Read the configs
    val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

    val dataSetId: String = configProperties.get(taskId).getOrElse("")

    // Load the dataset
    var df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, PLATFORM_SDK_PQS_INTERACTIVE)
      .option(QSOption.datasetId, dataSetId)
      .load()
    df.show()
    df
    }
}
```

## DataSaver {#datasaver}

A classe DataSaver encapsula tudo relacionado ao armazenamento de dados de saída, incluindo aqueles da pontuação ou engenharia de recursos. Os salvadores de dados estendem a classe abstrata `DataSaver` e devem substituir o método abstrato `save`.

**PySpark**

A tabela a seguir descreve os métodos abstratos de uma classe de Economizador de Dados [!DNL PySpark]:

<table>
    <thead>
        <tr>
            <th>Método e descrição</th>
            <th>Parâmetros</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>save(self, configProperties, dataframe)</code></p>
                <p>Recebe dados de saída como um DataFrame e os armazena em um conjunto de dados do Experience Platform</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: autorreferência</li>
                    <li><code>configProperties</code>: mapa de propriedades de configuração</li>
                    <li><code>dataframe</code>: dados a serem armazenados no formato de um DataFrame</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

A tabela a seguir descreve os métodos abstratos de uma classe de Economizador de Dados [!DNL Spark]:

<table>
    <thead>
        <tr>
            <th>Método e descrição</th>
            <th>Parâmetros</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>save(configProperties, dataFrame)</code></p>
                <p>Recebe dados de saída como um DataFrame e os armazena em um conjunto de dados do Experience Platform</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: mapa de propriedades de configuração</li>
                    <li><code>dataFrame</code>: dados a serem armazenados no formato de um DataFrame</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### Salvar dados em um conjunto de dados [!DNL Experience Platform] {#save-data-to-a-platform-dataset}

Para armazenar dados em um conjunto de dados [!DNL Experience Platform], as propriedades devem ser fornecidas ou definidas no arquivo de configuração:

- Uma ID de conjunto de dados [!DNL Experience Platform] válida para a qual os dados serão armazenados
- A ID do locatário pertencente à sua organização

Os exemplos a seguir armazenam dados (`prediction`) em um conjunto de dados [!DNL Experience Platform], em que a ID do conjunto de dados (`datasetId`) e a ID do locatário (`tenantId`) são propriedades definidas no arquivo de configuração.


**PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct
from .helper import *


class MyDataSaver(DataSaver):
    """
    Implementation of DataSaver which stores a DataFrame to an Experience Platform dataset
    """

    def save(self, config_properties, prediction):

        # Spark context
        sparkContext = prediction._sc

        # preliminary checks
        if config_properties is None:
            raise ValueError("config_properties parameter is null")
        if prediction is None:
            raise ValueError("prediction parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")
        
        PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"

        # prepare variables
        scored_dataset_id = str(config_properties.get("scoringResultsDataSetId"))
        tenant_id = str(config_properties.get("tenant_id"))
        timestamp = "2019-01-01 00:00:00"

        service_token = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
       for arg in ['service_token', 'user_token', 'org_id', 'scored_dataset_id', 'api_key', 'tenant_id']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)
        
        scored_df = prediction.withColumn("date", col("date").cast(StringType()))
        scored_df = scored_df.withColumn(tenant_id, struct(col("date"), col("store"), col("prediction")))
        scored_df = scored_df.withColumn("timestamp", lit(timestamp).cast(TimestampType()))
        scored_df = scored_df.withColumn("_id", lit("empty"))
        scored_df = scored_df.withColumn("eventType", lit("empty")

        # store data into dataset

        query_options = get_query_options(sparkContext)

        scored_df.select(tenant_id, "_id", "eventType", "timestamp").write.format(PLATFORM_SDK_PQS_PACKAGE) \
            .option(query_options.userToken(), user_token) \
            .option(query_options.serviceToken(), service_token) \
            .option(query_options.imsOrg(), org_id) \
            .option(query_options.apiKey(), api_key) \
            .option(query_options.datasetId(), scored_dataset_id) \
            .save()
```

**Spark (Scala)**

```scala
// Spark

package com.adobe.platform.ml

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import com.adobe.platform.query.QSOption
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

/**
 * Implementation of DataSaver which stores a DataFrame to an Experience Platform dataset
 */

class ScoringDataSaver extends DataSaver {

  final val PLATFORM_SDK_PQS_PACKAGE: String = "com.adobe.platform.query"
  final val PLATFORM_SDK_PQS_BATCH: String = "batch"

  /**
    * Method that saves the scoring data into a dataframe
    * @param configProperties  - Configuration Properties map
    * @param dataFrame         - Dataframe with the scoring results
    */
    
  override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

    require(configProperties != null)
    require(dataFrame != null)

    val predictionColumn = configProperties.get(Constants.PREDICTION_COL).getOrElse(Constants.DEFAULT_PREDICTION)
    val sparkSession = dataFrame.sparkSession

    val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
    val tenantId:String = configProperties.get("tenantId").getOrElse("")
    val timestamp:String = "2019-01-01 00:00:00"

    val scoringResultsDataSetId: String = configProperties.get("scoringResultsDataSetId").getOrElse("")
    import sparkSession.implicits._

    var df = dataFrame.withColumn("date", $"date".cast("String"))

    var scored_df  = df.withColumn(tenantId, struct(df("date"), df("store"), df(predictionColumn)))
    scored_df = scored_df.withColumn("timestamp", lit(timestamp).cast(TimestampType))
    scored_df = scored_df.withColumn("_id", lit("empty"))
    scored_df = scored_df.withColumn("eventType", lit("empty"))

    scored_df.select(tenantId, "_id", "eventType", "timestamp").write.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.datasetId, scoringResultsDataSetId)
      .save()
    }
}
```

## DatasetTransformer {#datasettransformer}

A classe DatasetTransformer modifica e transforma a estrutura de um conjunto de dados. O [!DNL Sensei Machine Learning Runtime] não requer que esse componente seja definido e é implementado com base em seus requisitos.

No que diz respeito a um pipeline de recursos, os transformadores de conjunto de dados podem ser usados em conjunto com uma fábrica de pipelines de recursos para preparar dados para a engenharia de recursos.

**PySpark**

A tabela a seguir descreve os métodos de classe de uma classe de transformador do conjunto de dados do PySpark:

<table>
    <thead>
        <tr>
            <th>Método e descrição</th>
            <th>Parâmetros</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>transform(self, configProperties, dataset)</code></p>
                <p>Usa um conjunto de dados como entrada e saída para um novo conjunto de dados derivado</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: autorreferência</li>
                    <li><code>configProperties</code>: mapa de propriedades de configuração</li>
                    <li><code>dataset</code>: o conjunto de dados de entrada para transformação</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

A tabela a seguir descreve os métodos abstratos de uma classe de transformador do conjunto de dados [!DNL Spark]:

<table>
    <thead>
        <tr>
            <th>Método e descrição</th>
            <th>Parâmetros</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>transform(configProperties, dataset)</code></p>
                <p>Usa um conjunto de dados como entrada e saída para um novo conjunto de dados derivado</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: mapa de propriedades de configuração</li>
                    <li><code>dataset</code>: o conjunto de dados de entrada para transformação</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## FeaturePipelineFactory {#featurepipelinefactory}

A classe FeaturePipelineFactory contém algoritmos de extração de recursos e define os estágios de um Pipeline de recursos do início ao fim.

**PySpark**

A tabela a seguir descreve os métodos de classe de um FeaturePipelineFactory PySpark:

<table>
    <thead>
        <tr>
            <th>Método e descrição</th>
            <th>Parâmetros</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>create_pipeline(self, configProperties)</code></p>
                <p>Criar e retornar um Spark Pipeline que contenha uma série de Spark Transformers</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: autorreferência</li>
                    <li><code>configProperties</code>: mapa de propriedades de configuração</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>get_param_map(self, configProperties, sparkSession)</code></p>
                <p>Recuperar e retornar o mapa de parâmetros das propriedades de configuração</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: autorreferência</li>
                    <li><code>configProperties</code>: propriedades de configuração</li>
                    <li><code>sparkSession</code>: Sessão do Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

A tabela a seguir descreve os métodos de classe de uma FeaturePipelineFactory [!DNL Spark]:

<table>
    <thead>
        <tr>
            <th>Método e descrição</th>
            <th>Parâmetros</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>createPipeline(configProperties)</code></p>
                <p>Criar e retornar um pipeline que contenha uma série de transformadores</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: mapa de propriedades de configuração</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>getParamMap(configProperties, sparkSession)</code></p>
                <p>Recuperar e retornar o mapa de parâmetros das propriedades de configuração</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: propriedades de configuração</li>
                    <li><code>sparkSession</code>: Sessão do Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## PipelineFactory {#pipelinefactory}

A classe PipelineFactory encapsula métodos e definições para treinamento e pontuação de modelos, em que a lógica e os algoritmos de treinamento são definidos no formato de um Pipeline [!DNL Spark].

**PySpark**

A tabela a seguir descreve os métodos de classe de um PipelineFactory PySpark:

<table>
    <thead>
        <tr>
            <th>Método e descrição</th>
            <th>Parâmetros</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>apply(self, configProperties)</code></p>
                <p>Criar e retornar um Spark Pipeline que contenha a lógica e o algoritmo para treinamento e pontuação do modelo</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: autorreferência</li>
                    <li><code>configProperties</code>: propriedades de configuração</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>train(self, configProperties, dataframe)</code></p>
                <p>Retorne um Pipeline personalizado que contenha a lógica e o algoritmo para treinar um modelo. Este método não é necessário se um pipeline Spark for usado</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: autorreferência</li>
                    <li><code>configProperties</code>: propriedades de configuração</li>
                    <li><code>dataframe</code>: conjunto de dados de recurso para entrada de treinamento</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>score(self, configProperties, dataframe, model)</code></p>
                <p>Pontuar usando o modelo treinado e retornar os resultados</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: autorreferência</li>
                    <li><code>configProperties</code>: propriedades de configuração</li>
                    <li><code>dataframe</code>: Conjunto de dados de entrada para pontuação</li>
                    <li><code>model</code>: um modelo treinado usado para pontuação</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>get_param_map(self, configProperties, sparkSession)</code></p>
                <p>Recuperar e retornar o mapa de parâmetros das propriedades de configuração</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: autorreferência</li>
                    <li><code>configProperties</code>: propriedades de configuração</li>
                    <li><code>sparkSession</code>: Sessão do Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

A tabela a seguir descreve os métodos de classe de um PipelineFactory [!DNL Spark]:

<table>
    <thead>
        <tr>
            <th>Método e descrição</th>
            <th>Parâmetros</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>apply(configProperties)</code></p>
                <p>Criar e retornar um pipeline que contenha a lógica e o algoritmo para treinamento e pontuação do modelo</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: propriedades de configuração</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>getParamMap(configProperties, sparkSession)</code></p>
                <p>Recuperar e retornar o mapa de parâmetros das propriedades de configuração</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: propriedades de configuração</li>
                    <li><code>sparkSession</code>: Sessão do Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## MLEvaluator {#mlevaluator}

A classe MLEvaluator fornece métodos para definir métricas de avaliação e determinar conjuntos de dados de treinamento e teste.

**PySpark**

A tabela a seguir descreve os métodos de classe de um MLEvaluator PySpark:

<table>
    <thead>
        <tr>
            <th>Método e descrição</th>
            <th>Parâmetros</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>split(self, configProperties, dataframe)</code></p>
                <p>Divide o conjunto de dados de entrada em subconjuntos de treinamento e teste</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: autorreferência</li>
                    <li><code>configProperties</code>: propriedades de configuração</li>
                    <li><code>dataframe</code>: Conjunto de dados de entrada a ser dividido</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>evaluate(self, dataframe, model, configProperties)</code></p>
                <p>Avalia um modelo treinado e retorna os resultados da avaliação</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: autorreferência</li>
                    <li><code>dataframe</code>: um DataFrame que consiste em dados de treinamento e teste</li>
                    <li><code>model</code>: um modelo treinado</li>
                    <li><code>configProperties</code>: propriedades de configuração</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

A tabela a seguir descreve os métodos de classe de um MLEvaluator [!DNL Spark]:

<table>
    <thead>
        <tr>
            <th>Método e descrição</th>
            <th>Parâmetros</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>split(configProperties, data)</code></p>
                <p>Divide o conjunto de dados de entrada em subconjuntos de treinamento e teste</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: propriedades de configuração</li>
                    <li><code>data</code>: Conjunto de dados de entrada a ser dividido</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>evaluate(configProperties, model, data)</code></p>
                <p>Avalia um modelo treinado e retorna os resultados da avaliação</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: propriedades de configuração</li>
                    <li><code>model</code>: um modelo treinado</li>
                    <li><code>data</code>: um DataFrame que consiste em dados de treinamento e teste</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>
