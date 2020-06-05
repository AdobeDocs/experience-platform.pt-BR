---
keywords: Experience Platform;developer guide;SDK;Model authoring;Data Science Workspace;popular topics
solution: Experience Platform
title: Guia do desenvolvedor do SDK
topic: Overview
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 1%

---


# Guia do desenvolvedor do SDK

O SDK de criação de modelo permite desenvolver Fórmulas de aprendizado e Pipelines de Recursos personalizados em máquina que podem ser usados na [!DNL Adobe Experience Platform] Data Science Workspace, fornecendo modelos implementáveis no PySpark e no Spark.

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

A tabela a seguir descreve os métodos abstratos de uma classe Spark Data Loader:

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

### Carregar dados de um conjunto de dados de plataforma {#load-data-from-a-platform-dataset}

O exemplo a seguir recupera dados da plataforma por ID e retorna um DataFrame, onde a ID do conjunto de dados (`datasetId`) é uma propriedade definida no arquivo de configuração.

**PySpark**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    """
    Implementation of DataLoader which loads a DataFrame and prepares data
    """

    def load(self, configProperties, spark):
        """
        Load and return dataset

        :param configProperties:    Configuration properties
        :param spark:               Spark session
        :return:                    DataFrame
        """

        # preliminary checks
        if configProperties is None :
            raise ValueError("configProperties parameter is null")
        if spark is None:
            raise ValueError("spark parameter is null")

        # prepare variables
        dataset_id = str(
            configProperties.get("datasetId"))
        service_token = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
        for arg in ['dataset_id', 'service_token', 'user_token', 'org_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # load dataset through Spark session
        pd = spark.read.format("com.adobe.platform.dataset") \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('orgId', org_id) \
            .option('serviceApiKey', api_key) \
            .load(dataset_id)

        # return as DataFrame
        return pd
```

**Faísca**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DataLoader
import org.apache.spark.sql.{DataFrame, SparkSession}

/**
 * Implementation of DataLoader which loads a DataFrame and prepares data
 */
class MyDataLoader extends DataLoader {

    /**
     * @param configProperties  - Configuration properties
     * @param sparkSession      - Spark session
     * @return                  - DataFrame
     */
    override def load(configProperties: ConfigProperties, sparkSession: SparkSession): DataFrame = {

        // preliminary checks
        require(configProperties != null)
        require(sparkSession != null)

        // prepare variables
        val dataSetId: String = configProperties
            .get("datasetId").getOrElse("")
        val serviceToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
        val userToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_TOKEN", "").toString
        val orgId: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
        val apiKey: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

        // validate variables
        List(dataSetId, serviceToken, userToken, orgId, apiKey).foreach(
            value => required(value != "")
        )

        // load dataset through Spark session
        var df = sparkSession.read.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .load(dataSetId)
        
        // return as DataFrame
        df
    }
}
```

## DataSaver {#datasaver}

A classe DataSaver encapsula qualquer coisa relacionada ao armazenamento de dados de saída, incluindo os dados de pontuação ou engenharia de recursos. Os servidores de dados estendem a classe abstrata `DataSaver` e devem substituir o método abstrato `save`.

**PySpark**

A tabela a seguir descreve os métodos abstratos de uma classe PySpark Data Saver:

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

**Faísca**

A tabela a seguir descreve os métodos abstratos de uma classe Spark Data Saver:

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

### Salvar dados em um conjunto de dados da plataforma {#save-data-to-a-platform-dataset}

Para armazenar dados em um conjunto de dados da Plataforma, as propriedades devem ser fornecidas ou definidas no arquivo de configuração:

- Uma ID válida do conjunto de dados da plataforma para a qual os dados serão armazenados
- A ID do locatário pertencente à sua organização

Os exemplos a seguir armazenam dados (`prediction`) em um conjunto de dados da Plataforma, onde a ID do conjunto de dados (`datasetId`) e a ID do locatário (`tenantId`) são propriedades definidas no arquivo de configuração.


**PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType


class MyDataSaver(DataSaver):
    """
    Implementation of DataSaver which stores a DataFrame to a Platform dataset
    """

    def save(self, configProperties, prediction):
        """
        Store DataFrame to a Platform dataset

        :param configProperties:    Configuration properties
        :param prediction:          DataFrame to be stored to a Platform dataset
        """

        # Spark context
        sparkContext = prediction._sc

        # preliminary checks
        if configProperties is None:
            raise ValueError("configProperties parameter is null")
        if prediction is None:
            raise ValueError("prediction parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")

        # prepare variables
        timestamp = "2019-01-01 00:00:00"
        output_dataset_id = str(
            configProperties.get("datasetId"))
        tenant_id = str(
            configProperties.get("tenantId"))
        service_token = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
        for arg in ['output_dataset_id', 'tenant_id', 'service_token', 'user_token', 'org_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # store data into dataset
        prediction.write.format("com.adobe.platform.dataset") \
            .option('orgId', org_id) \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('serviceApiKey', api_key) \
            .save(output_dataset_id)
```




**Faísca**

```scala
// Spark

import com.adobe.platform.dataset.DataSetOptions
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

/**
 * Implementation of DataSaver which stores a DataFrame to a Platform dataset
 */
class ScoringDataSaver extends DataSaver {

    /**
     * @param configProperties  - Configuration properties
     * @param dataFrame         - DataFrame to be stored to a Platform dataset
     */
    override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

        // Spark session
        val sparkSession = dataFrame.sparkSession
        import sparkSession.implicits._

        // preliminary checks
        require(configProperties != null)
        require(dataFrame != null)

        // prepare variables
        val predictionColumn = configProperties.get(Constants.PREDICTION_COL)
            .getOrElse(Constants.DEFAULT_PREDICTION)
        val timestamp:String = "2019-01-01 00:00:00"
        val output_dataset_id: String = configProperties
            .get("datasetId").getOrElse("")
        val tenant_id:String = configProperties
            .get("tenantId").getOrElse("")
        val serviceToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
        val userToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_TOKEN", "").toString
        val orgId: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
        val apiKey: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

        // validate variables
        List(output_dataset_id, tenant_id, serviceToken, userToken, orgId, apiKey).foreach(
            value => require(value != "")
        )

        // store data into dataset
        dataFrame.write.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .save(output_dataset_id)
    }
}
```

## DatasetTransformer {#datasettransformer}

A classe DatasetTransformer modifica e transforma a estrutura de um conjunto de dados. O Tempo de Execução do Sensei Machine Learning não exige que esse componente seja definido e é implementado com base em seus requisitos.

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

**Faísca**

A tabela a seguir descreve os métodos abstratos de uma classe de transformador de conjunto de dados Spark:

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

**Faísca**

A tabela a seguir descreve os métodos de classe de um Spark FeaturePipelineFactory:

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

A classe PipelineFactory encapsula métodos e definições para treinamento e pontuação de modelo, onde lógica e algoritmos de treinamento são definidos na forma de um Spark Pipeline.

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

**Faísca**

A tabela a seguir descreve os métodos de classe de um Spark PipelineFactory:

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

**Faísca**

A tabela a seguir descreve os métodos de classe de um avaliador MLE Spark:

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