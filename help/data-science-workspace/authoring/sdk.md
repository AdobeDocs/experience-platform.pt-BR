---
keywords: Experience Platform;developer guide;SDK;Model authoring;Data Science Workspace;popular topics;testing
solution: Experience Platform
title: Guia do desenvolvedor do SDK
topic: Overview
description: O SDK de criação de modelo permite desenvolver Fórmulas de aprendizado e Pipelines de Recursos personalizados de máquina que podem ser usados no Adobe Experience Platform Data Science Workspace, fornecendo modelos implementáveis no PySpark e no Spark (Scala).
translation-type: tm+mt
source-git-commit: 2a528c705a7aa610f57047be39be1ce9886ce44c
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 1%

---


# Guia do desenvolvedor do SDK

O SDK de criação de modelo permite desenvolver Fórmulas de aprendizado e Pipelines de Recursos personalizados de máquina que podem ser usados na [!DNL Adobe Experience Platform] Data Science Workspace, fornecendo modelos implementáveis em [!DNL PySpark] e [!DNL Spark (Scala)].

Este documento fornece informações sobre as várias classes encontradas no SDK de criação de modelo.

## DataLoader {#dataloader}

A classe DataLoader encapsula qualquer coisa relacionada à recuperação, filtragem e devolução de dados de entrada brutos. Exemplos de dados de entrada incluem aqueles para treinamento, pontuação ou engenharia de recursos. Os carregadores de dados estendem a classe abstrata `DataLoader` e devem substituir o método abstrato `load`.

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
                <p><code class=" language-undefined">load(self, configProperties, spark)</code></p>
                <p>Carregar e retornar dados da plataforma como um DataFrame dos painéis</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Referência automática</li>
                    <li><code class=" language-undefined">configProperties</code>: Mapa de propriedades de configuração</li>
                    <li><code class=" language-undefined">spark</code>: Sessão Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Faísca**

A tabela a seguir descreve os métodos abstratos de uma classe de [!DNL Spark] Carregador de dados:

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
                <p><code class=" language-undefined">load(configProperties, sparkSession)</code></p>
                <p>Carregar e retornar dados da plataforma como um DataFrame</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Mapa de propriedades de configuração</li>
                    <li><code class=" language-undefined">sparkSession</code>: Sessão Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### Carregar dados de um [!DNL Platform] conjunto de dados {#load-data-from-a-platform-dataset}

O exemplo a seguir recupera [!DNL Platform] dados por ID e retorna um DataFrame, onde a ID do conjunto de dados (`datasetId`) é uma propriedade definida no arquivo de configuração.

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

A classe DataSaver encapsula qualquer coisa relacionada ao armazenamento de dados de saída, incluindo os dados de pontuação ou engenharia de recursos. Os servidores de dados estendem a classe abstrata `DataSaver` e devem substituir o método abstrato `save`.

**PySpark**

A tabela a seguir descreve os métodos abstratos de uma classe do [!DNL PySpark] Data Saver:

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
                <p><code class=" language-undefined">save(self, configProperties, dataframe)</code></p>
                <p>Receber dados de saída como um DataFrame e armazená-los em um conjunto de dados da plataforma</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Referência automática</li>
                    <li><code class=" language-undefined">configProperties</code>: Mapa de propriedades de configuração</li>
                    <li><code class=" language-undefined">dataframe</code>: Dados a serem armazenados na forma de um DataFrame</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

A tabela a seguir descreve os métodos abstratos de uma classe do [!DNL Spark] Data Saver:

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
                <p><code class=" language-undefined">save(configProperties, dataFrame)</code></p>
                <p>Receber dados de saída como um DataFrame e armazená-los em um conjunto de dados da plataforma</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Mapa de propriedades de configuração</li>
                    <li><code class=" language-undefined">dataFrame</code>: Dados a serem armazenados na forma de um DataFrame</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### Salvar dados em um [!DNL Platform] conjunto de dados {#save-data-to-a-platform-dataset}

Para armazenar dados em um [!DNL Platform] conjunto de dados, as propriedades devem ser fornecidas ou definidas no arquivo de configuração:

- Uma ID válida do [!DNL Platform] conjunto de dados para a qual os dados serão armazenados
- A ID do locatário pertencente à sua organização

Os exemplos a seguir armazenam dados (`prediction`) em um [!DNL Platform] conjunto de dados, onde a ID do conjunto de dados (`datasetId`) e a ID do locatário (`tenantId`) são propriedades definidas no arquivo de configuração.


**PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct
from .helper import *


class MyDataSaver(DataSaver):
    """
    Implementation of DataSaver which stores a DataFrame to a Platform dataset
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
 * Implementation of DataSaver which stores a DataFrame to a Platform dataset
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

A classe DatasetTransformer modifica e transforma a estrutura de um conjunto de dados. O componente não [!DNL Sensei Machine Learning Runtime] exige que esse componente seja definido e é implementado com base em seus requisitos.

No que diz respeito a um pipeline de recursos, os transformadores de conjuntos de dados podem ser usados em conjunto com uma fábrica de pipeline de recursos para preparar dados para a engenharia de recursos.

**PySpark**

A tabela a seguir descreve os métodos de classe de uma classe de transformador de conjunto de dados PySpark:

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
                <p><i>resumo</i><br/><code class=" language-undefined">transform(self, configProperties, dataset)</code></p>
                <p>Utiliza um conjunto de dados como entrada e saída de um novo conjunto de dados derivado</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Referência automática</li>
                    <li><code class=" language-undefined">configProperties</code>: Mapa de propriedades de configuração</li>
                    <li><code class=" language-undefined">dataset</code>: O conjunto de dados de entrada para transformação</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

A tabela a seguir descreve os métodos abstratos de uma classe de transformador de conjunto de [!DNL Spark] dados:

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
                <p><code class=" language-undefined">transform(configProperties, dataset)</code></p>
                <p>Utiliza um conjunto de dados como entrada e saída de um novo conjunto de dados derivado</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Mapa de propriedades de configuração</li>
                    <li><code class=" language-undefined">dataset</code>: O conjunto de dados de entrada para transformação</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## FeaturePipelineFactory {#featurepipelinefactory}

A classe FeaturePipelineFactory contém algoritmos de extração de recursos e define os estágios de um Recurso Pipeline de start a fim.

**PySpark**

A tabela a seguir descreve os métodos de classe de um FeaturePipelineFactory do PySpark:

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
                <p><i>resumo</i><br/><code class=" language-undefined">create_pipeline(self, configProperties)</code></p>
                <p>Criar e retornar um pipeline Spark que contenha uma série de Transformadores Spark</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Referência automática</li>
                    <li><code class=" language-undefined">configProperties</code>: Mapa de propriedades de configuração</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>resumo</i><br/><code class=" language-undefined">get_param_map(self, configProperties, sparkSession)</code></p>
                <p>Recuperar e retornar mapa de parâmetros das propriedades de configuração</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Referência automática</li>
                    <li><code class=" language-undefined">configProperties</code>: Propriedades de configuração</li>
                    <li><code class=" language-undefined">sparkSession</code>: Sessão Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

A tabela a seguir descreve os métodos de classe de um [!DNL Spark] FeaturePipelineFactory:

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
                <p><i>resumo</i><br/><code class=" language-undefined">createPipeline(configProperties)</code></p>
                <p>Criar e retornar um Pipeline que contenha uma série de Transformers</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Mapa de propriedades de configuração</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>resumo</i><br/><code class=" language-undefined">getParamMap(configProperties, sparkSession)</code></p>
                <p>Recuperar e retornar mapa de parâmetros das propriedades de configuração</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Propriedades de configuração</li>
                    <li><code class=" language-undefined">sparkSession</code>: Sessão Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## PipelineFactory {#pipelinefactory}

A classe PipelineFactory encapsula métodos e definições para treinamento e pontuação de modelo, onde lógica e algoritmos de treinamento são definidos na forma de um [!DNL Spark] Pipeline.

**PySpark**

A tabela a seguir descreve os métodos de classe de um PySpark PipelineFactory:

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
                <p><i>resumo</i><br/><code class=" language-undefined">apply(self, configProperties)</code></p>
                <p>Criar e Retornar um pipeline de Faísca que contém a lógica e o algoritmo para treinamento e pontuação de modelo</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Referência automática</li>
                    <li><code class=" language-undefined">configProperties</code>: Propriedades de configuração</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>resumo</i><br/><code class=" language-undefined">train(self, configProperties, dataframe)</code></p>
                <p>Retorna um Pipeline personalizado que contém a lógica e o algoritmo para treinar um modelo. Este método não é necessário se for usado um Spark Pipeline</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Referência automática</li>
                    <li><code class=" language-undefined">configProperties</code>: Propriedades de configuração</li>
                    <li><code class=" language-undefined">dataframe</code>: Conjunto de dados de recursos para entrada de treinamento</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>resumo</i><br/><code class=" language-undefined">score(self, configProperties, dataframe, model)</code></p>
                <p>Pontuação usando o modelo treinado e retornando os resultados</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Referência automática</li>
                    <li><code class=" language-undefined">configProperties</code>: Propriedades de configuração</li>
                    <li><code class=" language-undefined">dataframe</code>: Conjunto de dados de entrada para pontuação</li>
                    <li><code class=" language-undefined">model</code>: Um modelo treinado usado para pontuação</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>resumo</i><br/><code class=" language-undefined">get_param_map(self, configProperties, sparkSession)</code></p>
                <p>Recuperar e retornar mapa de parâmetros das propriedades de configuração</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Referência automática</li>
                    <li><code class=" language-undefined">configProperties</code>: Propriedades de configuração</li>
                    <li><code class=" language-undefined">sparkSession</code>: Sessão Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

A tabela a seguir descreve os métodos de classe de um [!DNL Spark] PipelineFactory:

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
                <p><i>resumo</i><br/><code class=" language-undefined">apply(configProperties)</code></p>
                <p>Criar e Retornar um Pipeline que contém a lógica e o algoritmo para treinamento e pontuação do modelo</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Propriedades de configuração</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>resumo</i><br/><code class=" language-undefined">getParamMap(configProperties, sparkSession)</code></p>
                <p>Recuperar e retornar mapa de parâmetros das propriedades de configuração</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Propriedades de configuração</li>
                    <li><code class=" language-undefined">sparkSession</code>: Sessão Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## MLEvaluator {#mlevaluator}

A classe MLEvaluator fornece métodos para definir métricas de avaliação e determinar conjuntos de dados de treinamento e teste.

**PySpark**

A tabela a seguir descreve os métodos de classe de um PySpark MLEvaluator:

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
                <p><i>resumo</i><br/><code class=" language-undefined">split(self, configProperties, dataframe)</code></p>
                <p>Divide o conjunto de dados de entrada em subconjuntos de treinamento e teste</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Referência automática</li>
                    <li><code class=" language-undefined">configProperties</code>: Propriedades de configuração</li>
                    <li><code class=" language-undefined">dataframe</code>: Conjunto de dados de entrada a ser dividido</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>resumo</i><br/><code class=" language-undefined">evaluate(self, dataframe, model, configProperties)</code></p>
                <p>Avalia um modelo treinado e retorna os resultados da avaliação</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Referência automática</li>
                    <li><code class=" language-undefined">dataframe</code>: Um DataFrame que consiste em dados de treinamento e teste</li>
                    <li><code class=" language-undefined">model</code>: Um modelo treinado</li>
                    <li><code class=" language-undefined">configProperties</code>: Propriedades de configuração</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

A tabela a seguir descreve os métodos de classe de um [!DNL Spark] MLEvaluator:

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
                <p><i>resumo</i><br/><code class=" language-undefined">split(configProperties, data)</code></p>
                <p>Divide o conjunto de dados de entrada em subconjuntos de treinamento e teste</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Propriedades de configuração</li>
                    <li><code class=" language-undefined">data</code>: Conjunto de dados de entrada a ser dividido</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>resumo</i><br/><code class=" language-undefined">evaluate(configProperties, model, data)</code></p>
                <p>Avalia um modelo treinado e retorna os resultados da avaliação</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Propriedades de configuração</li>
                    <li><code class=" language-undefined">model</code>: Um modelo treinado</li>
                    <li><code class=" language-undefined">data</code>: Um DataFrame que consiste em dados de treinamento e teste</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>