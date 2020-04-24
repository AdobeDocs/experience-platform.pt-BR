---
keywords: Experience Platform;Tutorial;Feature Pipeline;Data Science Workspace;popular topics
solution: Experience Platform
title: Criar um pipeline de recurso
topic: Tutorial
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# Criar um pipeline de recurso

A Adobe Experience Platform permite que você crie e crie Pipelines de Recursos personalizados para executar engenharia de recursos em escala por meio do Sensei Machine Learning Framework Runtime (a seguir denominado &quot;Runtime&quot;).

Este documento descreve as várias classes encontradas em um Recurso Pipeline e fornece um tutorial passo a passo para a criação de um Recurso Pipeline personalizado usando o SDK [de criação de](./sdk.md) modelo no PySpark e no Spark.

## Classes de pipeline de recurso

A tabela a seguir descreve as principais Classes abstratas que devem ser estendidas para criar um Pipeline de recurso:

| Classe abstrata | Descrição |
| -------------- | ----------- |
| DataLoader | Uma classe DataLoader fornece implementação para a recuperação de dados de entrada. |
| DatasetTransformer | Uma classe DatasetTransformer fornece implementações para transformar o conjunto de dados de entrada. Você pode optar por não fornecer uma classe DatasetTransformer e implementar sua lógica de engenharia de recursos na classe FeaturePipelineFactory. |
| FeaturePipelineFactory | Uma classe FeaturePipelineFactory cria um Spark Pipeline que consiste em uma série de Spark Transformers para executar engenharia de recursos. Você pode optar por não fornecer uma classe FeaturePipelineFactory e implementar sua lógica de engenharia de recursos na classe DatasetTransformer. |
| DataSaver | Uma classe DataSaver fornece a lógica para o armazenamento de um conjunto de dados de recurso. |

Quando um trabalho de Pipeline de Recurso é iniciado, o Tempo de Execução primeiro executará o DataLoader para carregar dados de entrada como DataFrame e depois modifica o DataFrame executando DatasetTransformer, FeaturePipelineFactory ou ambos. Por fim, o conjunto de dados de recursos resultante é armazenado por meio do DataSaver.

O diagrama a seguir mostra a ordem de execução do Tempo de execução:

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## Implemente suas classes Feature Pipeline {#implement-your-feature-pipeline-classes}

As seções a seguir fornecem detalhes e exemplos sobre a implementação das classes necessárias para um Recurso Pipeline.

### Definir variáveis no arquivo JSON de configuração {#define-variables-in-the-configuration-json-file}

O arquivo JSON de configuração consiste em pares de valores chave e destina-se a especificar quaisquer variáveis a serem posteriormente definidas durante o tempo de execução. Esses pares de valores chave podem definir propriedades como local do conjunto de dados de entrada, ID do conjunto de dados de saída, ID do locatário, cabeçalhos de coluna e assim por diante.

O exemplo a seguir demonstra pares de valores chave encontrados em um arquivo de configuração. Expanda o exemplo para ver os detalhes:


**exemplo JSON de configuração**

```json
[
    {
        "name": "fp",
        "parameters": [
            {
                "key": "datasetId",
                "value": "000"
            },
            {
                "key": "featureDatasetId",
                "value": "111"
            },
            {
                "key": "tenantId",
                "value": "_tenantid"
            }
        ]
    }
]
```



Você pode acessar o JSON de configuração por meio de qualquer método de classe que defina `configProperties` como parâmetro. Por exemplo:

**PySpark**

```python
input_dataset_id = str(configProperties.get("datasetId"))
```

**Faísca**

```scala
val input_dataset_id: String = configProperties.get("datasetId")
```


### Preparar os dados de entrada com DataLoader {#prepare-the-input-data-with-dataloader}

O DataLoader é responsável pela recuperação e filtragem de dados de entrada. Sua implementação do DataLoader deve estender a classe abstrata `DataLoader` e substituir o método abstrato `load`.

O exemplo a seguir recupera um conjunto de dados da Plataforma por ID e o retorna como um DataFrame, onde a ID do conjunto de dados (`datasetId`) é uma propriedade definida no arquivo de configuração. Expanda cada exemplo para ver os detalhes:


**Exemplo de PySpark**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    def load(self, configProperties, spark):

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
        df = spark.read.format("com.adobe.platform.dataset") \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('orgId', org_id) \
            .option('serviceApiKey', api_key) \
            .load(dataset_id)

        # return as DataFrame
        return df
```




**Exemplo de Spark**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DataLoader
import org.apache.spark.sql.{DataFrame, SparkSession}

class MyDataLoader extends DataLoader {
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



### Transformar um conjunto de dados com DatasetTransformer {#transform-a-dataset-with-datasettransformer}

Um DatasetTransformer fornece a lógica para transformar um DataFrame de entrada e retorna um DataFrame derivado novo. Essa classe pode ser implementada para trabalhar em conjunto com um FeaturePipelineFactory, funcionar como o único componente de engenharia de recursos ou você pode optar por não implementar essa classe.

O exemplo a seguir estende a classe DatasetTransformer. Expanda cada exemplo para ver os detalhes:


**Exemplo de PySpark**

```python
# PySpark

from sdk.dataset_transformer import DatasetTransformer

class MyDatasetTransformer(DatasetTransformer):

    def transform(self, configProperties, dataset):
        transformed = dataset

        '''
        Transformations
        '''

        # return new DataFrame
        return transformed
```




**Exemplo de Spark**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DatasetTransformer

class MyDatasetTransformer extends DatasetTransformer {

    override def transform(configProperties: ConfigProperties, dataset: Dataset[_]): Dataset[_] = {
        val transformed = dataset

        /*
        transformations
        */
        
        // return new DataFrame
        transformed
    }
}
```



### Recursos de dados do engenheiro com FeaturePipelineFactory {#engineer-data-features-with-featurepipelinefactory}

Um FeaturePipelineFactory permite implementar sua lógica de engenharia de recursos definindo e encadeando uma série de Transformadores Spark através de um Spark Pipeline. Essa classe pode ser implementada para trabalhar em cooperação com um DatasetTransformer, funcionar como o único componente de engenharia de recursos ou você pode optar por não implementar essa classe.

O exemplo a seguir estende a classe FeaturePipelieFactory e implementa uma série de transformadores Spark como vários estágios em um Spark Pipeline. Expanda cada exemplo para ver os detalhes:


**Exemplo de PySpark**

```python
# PySpark

from pyspark.ml import Pipeline
from pyspark.ml.feature import HashingTF, Tokenizer
from sdk.feature_pipeline_factory import FeaturePipelineFactory

class MyFeaturePipelineFactory(FeaturePipelineFactory):

    def create_pipeline(self, configProperties):

        # Spark Transformers
        tokenizer = Tokenizer(inputCol="lower_text", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")

        # Chain together Spark Transformers as Spark Pipeline Stages
        pipeline = Pipeline(stages=[tokenizer, hashingTF])

        # return a Spark Pipeline
        return pipeline

    def get_param_map(self, configProperties, sparkSession):
        pass
```




**Exemplo de Spark**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.FeaturePipelineFactory
import org.apache.spark.ml.feature.{HashingTF, Tokenizer}
import org.apache.spark.ml.Pipeline
import org.apache.spark.ml.param.ParamMap
import org.apache.spark.sql.SparkSession

class MyFeaturePipelineFactory(uid:String) extends FeaturePipelineFactory(uid) {
    def this() = this("MyFeaturePipeline")

    override def createPipeline(configProperties: ConfigProperties): Pipeline = {
        
        // Spark Transformers
        val tokenizer = new Tokenizer()
            .setInputCol("lower_text")
            .setOutputCol("words")
        val hashingTF = new HashingTF()
            .setInputCol(tokenizer.getOutputCol())
            .setOutputCol("features")

        // Chain together Spark Transformers as Spark Pipeline Stages
        val pipeline = new Pipeline()
            .setStages(Array(tokenizer, hashingTF))
        
        // return a Spark Pipeline
        pipeline
    }

    override def getParamMap(configProperties: ConfigProperties, sparkSession: SparkSession): ParamMap = {
        val map = new ParamMap()
        map
    }
}
```



### Armazenar seu conjunto de dados de recursos com o DataSaver {#store-your-feature-dataset-with-datasaver}

O DataSaver é responsável por armazenar seus conjuntos de dados de recursos resultantes em um local de armazenamento. Sua implementação do DataSaver deve estender a classe abstrata `DataSaver` e substituir o método abstrato `save`.

O exemplo a seguir estende a classe DataSaver que armazena dados para um conjunto de dados da plataforma por ID, onde a ID do conjunto de dados (`featureDatasetId`) e a ID do locatário (`tenantId`) são propriedades definidas no arquivo de configuração. Expanda cada exemplo para ver os detalhes:


**Exemplo de PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct


class MyDataSaver(DataSaver):
    def save(self, configProperties, data_feature):

        # Spark context
        sparkContext = data_features._sc

        # preliminary checks
        if configProperties is None:
            raise ValueError("configProperties parameter is null")
        if data_features is None:
            raise ValueError("data_features parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")

        # prepare variables
        timestamp = "2019-01-01 00:00:00"
        output_dataset_id = str(
            configProperties.get("featureDatasetId"))
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

        # create and prepare DataFrame with valid columns
        output_df = data_features.withColumn("date", col("date").cast(StringType()))
        output_df = output_df.withColumn(tenant_id, struct(col("date"), col("store"), col("features")))
        output_df = output_df.withColumn("timestamp", lit(timestamp).cast(TimestampType()))
        output_df = output_df.withColumn("_id", lit("empty"))
        output_df = output_df.withColumn("eventType", lit("empty"))

        # store data into dataset
        output_df.select(tenant_id, "_id", "eventType", "timestamp") \
            .write.format("com.adobe.platform.dataset") \
            .option('orgId', org_id) \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('serviceApiKey', api_key) \
            .save(output_dataset_id)
```




**Exemplo de Spark**

```scala
// Spark

import com.adobe.platform.dataset.DataSetOptions
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

class MyDataSaver extends DataSaver {
    override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

        // Spark session
        val sparkSession = dataFrame.sparkSession

        // preliminary checks
        require(configProperties != null)
        require(dataFrame != null)

        // prepare variables
        val timestamp:String = "2019-01-01 00:00:00"
        val output_dataset_id: String = configProperties
            .get("featureDatasetId").getOrElse("")
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

        // create and prepare DataFrame with valid columns
        import sparkSession.implicits._

        var output_df  = dataFrame.withColumn("date", $"date".cast("String"))
        output_df = output_df.withColumn("timestamp", lit(timestamp).cast(TimestampType))
        output_df = output_df.withColumn("_id", lit("empty"))
        output_df = output_df.withColumn("eventType", lit("empty"))

        // store data into dataset
        output_df.select(tenant_id, "_id", "eventType", "timestamp").write.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .save(output_dataset_id)
    }
}
```

### Especifique os nomes de classe implementados no arquivo do aplicativo {#specify-your-implemented-class-names-in-the-application-file}

Agora que as classes do Feature Pipeline estão definidas e implementadas, você deve especificar os nomes das classes no arquivo do aplicativo.

Os exemplos a seguir especificam nomes de classe implementados. Expanda o exemplo para ver os detalhes:


**Exemplo de PySpark**

```yaml
# application.yaml

# Name of the implementation of DataLoader abstract class
feature.dataLoader: MyDataLoader

# Name of the implementation of DatasetTransformer abstract class
feature.dataset.transformer: MyDatasetTransformer

# Name of the implementation of FeaturePipelineFactory abstract class
feature.pipeline.class: MyFeaturePipelineFactory

# Name of the implementation of DataSaver abstract class
feature.dataSaver: MyDataSaver
```




**Exemplo de Spark**

```properties
# application.properties

# Name of the implementation of DataLoader abstract class
feature.pipeline.class=MyDataLoader

# Name of the implementation of DatasetTransformer abstract class
feature.dataset.transformer=MyDatasetTransformer

# Name of the implementation of FeaturePipelineFactory abstract class
feature.dataLoader=MyFeaturePipelineFactory

# Name of the implementation of DataSaver abstract class
feature.dataSaver=MyDataSaver
```



## Criar o artefato binário {#build-the-binary-artifact}

Agora que suas classes Feature Pipeline foram implementadas, você pode criá-las e compilá-las em um artefato binário que pode ser usado para criar um Feature Pipeline por meio de chamadas de API.

**PySpark**

Para criar um Pipeline de recursos do PySpark, execute o script `setup.py` Python localizado no diretório raiz do SDK de criação de modelos.

>[!NOTE] A criação de um Pipeline de recursos do PySpark requer a instalação do Python 3 em sua máquina.

```shell
python3 setup.py bdist_egg
```

A criação bem-sucedida do seu Recurso Pipeline gerará um `.egg` artefato no `/dist` diretório. Esse artefato é usado para criar um Recurso Pipeline.

**Faísca**

Para criar um Pipeline de recursos de faísca, execute o seguinte comando de console no diretório raiz do SDK de criação de modelo:

>[!NOTE] A criação de um Spark Feature Pipeline requer que você tenha o Scala e sbt instalados em sua máquina.

```shell
mvn clean install
```

A criação bem-sucedida do seu Recurso Pipeline gerará um `.jar` artefato no `/dist` diretório. Esse artefato é usado para criar um Recurso Pipeline.

## Criar um mecanismo de pipeline de recurso usando a API {#create-a-feature-pipeline-engine-using-the-api}

Agora que você criou seu Feature Pipeline e construiu o artefato binário, você pode [criar um Feature Pipeline Engine usando a API](../api/engines.md#create-a-feature-pipeline-engine-using-binary-artifacts)Sensei Machine Learning. A criação bem-sucedida de um Mecanismo de pipeline de recurso fornecerá uma ID de mecanismo como parte do corpo da resposta. Certifique-se de salvar esse valor antes de continuar com as próximas etapas.

## Próximas etapas {#next-steps}

[//]: # (Next steps section should refer to tutorials on how to score data using the Feature Pipeline Engine. Update this document once those tutorials are available)

Ao ler este documento, você criou um Recurso Pipeline usando o SDK de criação de modelo, criou um artefato binário e usou o artefato para criar um Recurso Pipeline por meio de uma chamada de API. Agora você está pronto para [criar um Modelo](../api/mlinstances.md#create-an-mlinstance) de pipeline de recurso usando seus conjuntos de dados de transformação de mecanismos e start recém-criados e extraindo recursos de dados em escala.