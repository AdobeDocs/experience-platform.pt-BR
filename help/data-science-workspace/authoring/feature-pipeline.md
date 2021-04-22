---
keywords: Experience Platform, Tutorial, pipeline de recursos, Data Science Workspace, tópicos populares
title: Criar um pipeline de recurso usando o SDK de criação de modelo
topic-legacy: tutorial
type: Tutorial
description: O Adobe Experience Platform permite criar e criar pipelines de recursos personalizados para executar engenharia de recursos em escala por meio da Execução da Estrutura de Aprendizagem de Máquinas do Sensei. Este documento descreve as várias classes encontradas em um pipeline de recursos e fornece um tutorial passo a passo para criar um pipeline de recursos personalizados usando o SDK de criação de modelo no PySpark.
exl-id: c2c821d5-7bfb-4667-ace9-9566e6754f98
translation-type: tm+mt
source-git-commit: 441d7822f287fabf1b06cdf3f6982f9c910387a8
workflow-type: tm+mt
source-wordcount: '1441'
ht-degree: 0%

---

# Criar um pipeline de recursos usando o SDK de criação de modelo

>[!IMPORTANT]
>
> No momento, os Pipelines de recursos estão disponíveis apenas por meio da API.

O Adobe Experience Platform permite criar e criar pipelines de recursos personalizados para executar a engenharia de recursos em escala por meio do Sensei Machine Learning Framework Runtime (a seguir, chamado de &quot;Tempo de execução&quot;).

Este documento descreve as várias classes encontradas em um pipeline de recursos e fornece um tutorial passo a passo para criar um pipeline de recursos personalizados usando o [SDK de criação de modelo](./sdk.md) no PySpark.

O seguinte fluxo de trabalho ocorre quando um pipeline de recursos é executado:

1. A receita carrega o conjunto de dados em um pipeline.
2. A transformação do recurso é feita no conjunto de dados e gravada de volta no Adobe Experience Platform.
3. Os dados transformados são carregados para treinamento.
4. O pipeline de recurso define os estágios com os Regressos de Aumento de Gradiente como o modelo escolhido.
5. O pipeline é usado para se adequar aos dados de treinamento e o modelo treinado é criado.
6. O modelo é transformado com o conjunto de dados de pontuação.
7. Colunas interessantes da saída são então selecionadas e salvas em [!DNL Experience Platform] com os dados associados.

## Introdução

Para executar uma fórmula em qualquer organização, é necessário o seguinte:
- Um conjunto de dados de entrada.
- O esquema do conjunto de dados.
- Um schema transformado e um conjunto de dados vazio com base nesse schema.
- Um schema de saída e um conjunto de dados vazio com base nesse schema.

Todos os conjuntos de dados acima precisam ser carregados na interface do usuário [!DNL Platform]. Para configurar isso, use o [script bootstrap](https://github.com/adobe/experience-platform-dsw-reference/tree/master/bootstrap) fornecido pelo Adobe.

## Classes de pipeline de recursos

A tabela a seguir descreve as principais classes abstratas que devem ser estendidas para criar um pipeline de recursos:

| Classe abstrata | Descrição |
| -------------- | ----------- |
| DataLoader | Uma classe DataLoader fornece implementação para a recuperação de dados de entrada. |
| DatasetTransformer | Uma classe DatasetTransformer fornece implementações para transformar o conjunto de dados de entrada. Você pode optar por não fornecer uma classe DatasetTransformer e implementar sua lógica de engenharia de recursos na classe FeaturePipelineFactory . |
| FeaturePipelineFactory | Uma classe FeaturePipelineFactory cria um Pipeline de Spark que consiste em uma série de Transformadores de Spark para executar a engenharia de recursos. Você pode optar por não fornecer uma classe FeaturePipelineFactory e implementar sua lógica de engenharia de recursos na classe DatasetTransformer. |
| DataSaver | Uma classe DataSaver fornece a lógica para o armazenamento de um conjunto de dados de recurso. |

Quando um trabalho de Pipeline de recurso é iniciado, o Tempo de execução primeiro executa o DataLoader para carregar dados de entrada como um DataFrame e, em seguida, modifica o DataFrame executando o DataFrame, o DataTransformer, o FeaturePipelineFactory ou ambos. Por fim, o conjunto de dados do recurso resultante é armazenado por meio do DataSaver.

O fluxograma a seguir mostra a ordem de execução do Runtime:

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## Implemente suas classes de pipeline de recursos {#implement-your-feature-pipeline-classes}

As seções a seguir fornecem detalhes e exemplos sobre a implementação das classes necessárias para um Pipeline de recurso.

### Definir variáveis no arquivo JSON de configuração {#define-variables-in-the-configuration-json-file}

O arquivo JSON de configuração consiste em pares de valores chave e destina-se a especificar quaisquer variáveis a serem posteriormente definidas durante o tempo de execução. Esses pares de valores chave podem definir propriedades, como local do conjunto de dados de entrada, ID do conjunto de dados de saída, ID do locatário, cabeçalhos de coluna e assim por diante.

O exemplo a seguir demonstra os pares de valores chave encontrados em um arquivo de configuração:

**Exemplo de JSON de configuração**

```json
[
    {
        "name": "fp",
        "parameters": [
            {
                "key": "dataset_id",
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

Você pode acessar o JSON de configuração por meio de qualquer método de classe que defina `config_properties` como um parâmetro. Por exemplo:

**PySpark**

```python
dataset_id = str(config_properties.get(dataset_id))
```

Consulte o arquivo [pipeline.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/feature_pipeline_recipes/pyspark/pipeline.json) fornecido pelo Data Science Workspace para obter um exemplo de configuração mais detalhado.

### Prepare os dados de entrada com DataLoader {#prepare-the-input-data-with-dataloader}

O DataLoader é responsável pela recuperação e filtragem de dados de entrada. Sua implementação do DataLoader deve estender a classe abstrata `DataLoader` e substituir o método abstrato `load`.

O exemplo a seguir recupera um conjunto de dados [!DNL Platform] por ID e o retorna como um DataFrame, onde a ID do conjunto de dados (`dataset_id`) é uma propriedade definida no arquivo de configuração.

**Exemplo de PySpark**

```python
# PySpark

from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct
import logging

class MyDataLoader(DataLoader):
    def load_dataset(config_properties, spark, tenant_id, dataset_id):
    PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"
    PLATFORM_SDK_PQS_INTERACTIVE = "interactive"

    service_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
    user_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
    org_id = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
    api_key = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

    dataset_id = str(config_properties.get(dataset_id))

    for arg in ['service_token', 'user_token', 'org_id', 'dataset_id', 'api_key']:
        if eval(arg) == 'None':
            raise ValueError("%s is empty" % arg)

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

    # Get the distinct values of the dataframe
    pd = pd.distinct()

    # Flatten the data
    if tenant_id in pd.columns:
        pd = pd.select(col(tenant_id + ".*"))

    return pd
```

### Transformar um conjunto de dados com DatasetTransformer {#transform-a-dataset-with-datasettransformer}

Um DatasetTransformer fornece a lógica para transformar um DataFrame de entrada e retorna um DataFrame derivado novo. Essa classe pode ser implementada para funcionar em conjunto com um FeaturePipelineFactory, funcionar como o único componente de engenharia de recursos ou você pode optar por não implementar essa classe.

O exemplo a seguir estende a classe DatasetTransformer :

**Exemplo de PySpark**

```python
# PySpark

from sdk.dataset_transformer import DatasetTransformer
from pyspark.ml.feature import StringIndexer
from pyspark.sql.types import IntegerType
from pyspark.sql.functions import unix_timestamp, from_unixtime, to_date, lit, lag, udf, date_format, lower, col, split, explode
from pyspark.sql import Window
from .helper import setupLogger

class MyDatasetTransformer(DatasetTransformer):
    logger = setupLogger(__name__)

    def transform(self, config_properties, dataset):
        tenant_id = str(config_properties.get("tenantId"))

        # Flatten the data
        if tenant_id in dataset.columns:
            self.logger.info("Flatten the data before transformation")
            dataset = dataset.select(col(tenant_id + ".*"))
            dataset.show()

        # Convert isHoliday boolean value to Int
        # Rename the column to holiday and drop isHoliday
        pd = dataset.withColumn("holiday", col("isHoliday").cast(IntegerType())).drop("isHoliday")
        pd.show()

        # Get the week and year from date
        pd = pd.withColumn("week", date_format(to_date("date", "MM/dd/yy"), "w").cast(IntegerType()))
        pd = pd.withColumn("year", date_format(to_date("date", "MM/dd/yy"), "Y").cast(IntegerType()))

        # Convert the date to TimestampType
        pd = pd.withColumn("date", to_date(unix_timestamp(pd["date"], "MM/dd/yy").cast("timestamp")))

        # Convert categorical data
        indexer = StringIndexer(inputCol="storeType", outputCol="storeTypeIndex")
        pd = indexer.fit(pd).transform(pd)

        # Get the WeeklySalesAhead and WeeklySalesLag column values
        window = Window.orderBy("date").partitionBy("store")
        pd = pd.withColumn("weeklySalesLag", lag("weeklySales", 1).over(window)).na.drop(subset=["weeklySalesLag"])
        pd = pd.withColumn("weeklySalesAhead", lag("weeklySales", -1).over(window)).na.drop(subset=["weeklySalesAhead"])
        pd = pd.withColumn("weeklySalesScaled", lag("weeklySalesAhead", -1).over(window)).na.drop(subset=["weeklySalesScaled"])
        pd = pd.withColumn("weeklySalesDiff", (pd['weeklySales'] - pd['weeklySalesLag'])/pd['weeklySalesLag'])

        pd = pd.na.drop()
        self.logger.debug("Transformed dataset count is %s " % pd.count())

        # return transformed dataframe
        return pd
```

### Engenharia de recursos de dados com o FeaturePipelineFactory {#engineer-data-features-with-featurepipelinefactory}

Um FeaturePipelineFactory permite implementar sua lógica de engenharia de recursos definindo e encadeando uma série de Transformadores Spark por meio de um Pipeline Spark. Essa classe pode ser implementada para trabalhar em cooperação com um DatasetTransformer, funcionar como o único componente de engenharia de recursos ou você pode optar por não implementar essa classe.

O exemplo a seguir estende a classe FeaturePipelineFactory :

**Exemplo de PySpark**

```python
# PySpark

from pyspark.ml import Pipeline
from pyspark.ml.regression import GBTRegressor
from pyspark.ml.feature import VectorAssembler

import numpy as np

from sdk.pipeline_factory import PipelineFactory

class MyFeaturePipelineFactory(FeaturePipelineFactory):

    def apply(self, config_properties):
        if config_properties is None:
            raise ValueError("config_properties parameter is null")

        tenant_id = str(config_properties.get("tenantId"))
        input_features = str(config_properties.get("ACP_DSW_INPUT_FEATURES"))

        if input_features is None:
            raise ValueError("input_features parameter is null")
        if input_features.startswith(tenant_id):
            input_features = input_features.replace(tenant_id + ".", "")

        learning_rate = float(config_properties.get("learning_rate"))
        n_estimators = int(config_properties.get("n_estimators"))
        max_depth = int(config_properties.get("max_depth"))

        feature_list = list(input_features.split(","))
        feature_list.remove("date")
        feature_list.remove("storeType")

        cols = np.array(feature_list)

        # Gradient-boosted tree estimator
        gbt = GBTRegressor(featuresCol='features', labelCol='weeklySalesAhead', predictionCol='prediction',
                       maxDepth=max_depth, maxBins=n_estimators, stepSize=learning_rate)

        # Assemble the fields to a vector
        assembler = VectorAssembler(inputCols=cols, outputCol="features")

        # Construct the pipeline
        pipeline = Pipeline(stages=[assembler, gbt])

        return pipeline

    def train(self, config_properties, dataframe):
        pass

    def score(self, config_properties, dataframe, model):
        pass

    def getParamMap(self, config_properties, sparkSession):
        return None
```

### Armazene seu conjunto de dados de recursos com o DataSaver {#store-your-feature-dataset-with-datasaver}

O DataSaver é responsável por armazenar seus conjuntos de dados de recursos resultantes em um local de armazenamento. Sua implementação do DataSaver deve estender a classe abstrata `DataSaver` e substituir o método abstrato `save`.

O exemplo a seguir estende a classe DataSaver, que armazena dados em um conjunto de dados [!DNL Platform] por ID, onde a ID do conjunto de dados (`featureDatasetId`) e a ID do locatário (`tenantId`) são propriedades definidas na configuração.

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


### Especifique os nomes de classe implementados no arquivo de aplicativo {#specify-your-implemented-class-names-in-the-application-file}

Agora que suas classes de pipeline de recursos estão definidas e implementadas, você deve especificar os nomes de suas classes no arquivo YAML do aplicativo.

Os exemplos a seguir especificam nomes de classe implementados:

**Exemplo de PySpark**

```yaml
#Name of the class which contains implementation to get the input data.
feature.dataLoader: InputDataLoaderForFeaturePipeline

#Name of the class which contains implementation to get the transformed data.
feature.dataset.transformer: MyDatasetTransformer

#Name of the class which contains implementation to save the transformed data.
feature.dataSaver: DatasetSaverForTransformedData

#Name of the class which contains implementation to get the training data
training.dataLoader: TrainingDataLoader

#Name of the class which contains pipeline. It should implement PipelineFactory.scala
pipeline.class: TrainPipeline

#Name of the class which contains implementation for evaluation metrics.
evaluator: Evaluator
evaluateModel: True

#Name of the class which contains implementation to get the scoring data.
scoring.dataLoader: ScoringDataLoader

#Name of the class which contains implementation to save the scoring data.
scoring.dataSaver: MyDatasetSaver
```

## Crie o mecanismo de pipeline de recursos usando a API {#create-feature-pipeline-engine-api}

Agora que você criou o pipeline de recursos, é necessário criar uma imagem do Docker para fazer uma chamada para os endpoints do pipeline de recursos na API [!DNL Sensei Machine Learning]. Você precisa de um URL de imagem do Docker para fazer uma chamada para os endpoints do pipeline de recursos.

>[!TIP]
>
>Se você não tiver um URL Docker, visite o [Tutorial Package source em uma fórmula](../models-recipes/package-source-files-recipe.md) para obter uma apresentação passo a passo sobre como criar um URL de host Docker.

Como opção, você também pode usar a seguinte coleção Postman para ajudar a concluir o fluxo de trabalho da API do pipeline de recursos:

https://www.postman.com/collections/c5fc0d1d5805a5ddd41a

### Criar um mecanismo de pipeline de recursos {#create-engine-api}

Depois de ter a localização da imagem do Docker, você pode [criar um mecanismo de pipeline de recursos](../api/engines.md#feature-pipeline-docker) usando a API [!DNL Sensei Machine Learning] executando um POST para `/engines`. A criação bem-sucedida de um mecanismo de pipeline de recursos fornece um identificador exclusivo do Mecanismo (`id`). Salve esse valor antes de continuar.

### Criar uma instância MLI {#create-mlinstance}

Usando seu `engineID` recém-criado, é necessário [criar um MLIposition](../api/mlinstances.md#create-an-mlinstance) fazendo uma solicitação de POST para o endpoint `/mlInstance`. Uma resposta bem-sucedida retorna uma carga contendo os detalhes da instância MLI recém-criada, incluindo seu identificador exclusivo (`id`) usado na próxima chamada da API.

### Criar um experimento {#create-experiment}

Em seguida, você precisa [criar um Experimento](../api/experiments.md#create-an-experiment). Para criar um Experimento, você precisa ter seu identificador exclusivo de MLIposition (`id`) e fazer uma solicitação de POST ao endpoint `/experiment`. Uma resposta bem-sucedida retorna uma carga contendo os detalhes do Experimento recém-criado, incluindo seu identificador exclusivo (`id`) usado na próxima chamada da API.

### Especifique a tarefa do pipeline de recursos de Execução de experiência {#specify-feature-pipeline-task}

Depois de criar um Experimento, você precisa alterar o modo do Experimento para `featurePipeline`. Para alterar o modo, faça um POST adicional para [`experiments/{EXPERIMENT_ID}/runs`](../api/experiments.md#experiment-training-scoring) com seu `EXPERIMENT_ID` e, no corpo, envie `{ "mode":"featurePipeline"}` para especificar uma execução de Experimento do pipeline de recursos.

Depois de concluir, faça uma solicitação GET para `/experiments/{EXPERIMENT_ID}` para [recuperar o status da experiência](../api/experiments.md#retrieve-specific) e aguarde a atualização do status do Experimento para ser concluída.

### Especificar a tarefa de treinamento Experimento executado {#training}

Em seguida, você precisa [especificar a tarefa de execução de treinamento](../api/experiments.md#experiment-training-scoring). Faça um POST para `experiments/{EXPERIMENT_ID}/runs` e, no corpo, defina o modo como `train` e envie uma matriz de tarefas que contêm seus parâmetros de treinamento. Uma resposta bem-sucedida retorna uma carga contendo os detalhes do Experimento solicitado.

Depois de concluir, faça uma solicitação GET para `/experiments/{EXPERIMENT_ID}` para [recuperar o status da experiência](../api/experiments.md#retrieve-specific) e aguarde a atualização do status do Experimento para ser concluída.

### Especifique a tarefa de pontuação de execução de Experimento {#scoring}

>[!NOTE]
>
> Para concluir esta etapa você precisa ter pelo menos uma execução de treinamento bem-sucedida associada ao seu Experimento.

Após uma execução de treinamento bem-sucedida, é necessário [especificar a tarefa de execução de pontuação](../api/experiments.md#experiment-training-scoring). Faça um POST para `experiments/{EXPERIMENT_ID}/runs` e, no corpo, defina o atributo `mode` como &quot;pontuação&quot;. Isso inicia a execução do Experimento de pontuação.

Depois de concluir, faça uma solicitação GET para `/experiments/{EXPERIMENT_ID}` para [recuperar o status da experiência](../api/experiments.md#retrieve-specific) e aguarde a atualização do status do Experimento para ser concluída.

Depois que a pontuação for concluída, o pipeline de recursos deverá estar operacional.

## Próximas etapas {#next-steps}

[//]: # (Next steps section should refer to tutorials on how to score data using the feature pipeline Engine. Update this document once those tutorials are available)

Ao ler este documento, você criou um pipeline de recursos usando o SDK de Criação de Modelo, criou uma imagem do Docker e usou o URL da imagem do Docker para criar um Modelo de pipeline de recursos usando a API [!DNL Sensei Machine Learning]. Agora você está pronto para continuar a transformar conjuntos de dados e extrair recursos de dados em escala usando o [[!DNL Sensei Machine Learning API]](../api/getting-started.md).
