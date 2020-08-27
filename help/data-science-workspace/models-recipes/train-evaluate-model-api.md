---
keywords: Experience Platform;train and evaluate;Data Science Workspace;popular topics;Sensei Machine Learning API
solution: Experience Platform
title: Treinar e avaliar um modelo (API)
topic: Tutorial
description: Este tutorial mostrará como criar, treinar e avaliar um Modelo usando chamadas à API de aprendizado de máquina do Sensei.
translation-type: tm+mt
source-git-commit: 7615476c4b728b451638f51cfaa8e8f3b432d659
workflow-type: tm+mt
source-wordcount: '1210'
ht-degree: 1%

---


# Treinar e avaliar um modelo (API)


Este tutorial mostrará como criar, treinar e avaliar um Modelo usando chamadas de API. Consulte [este documento](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) para obter uma lista detalhada da documentação da API.

## Pré-requisitos

Siga a opção [Importar uma receita empacotada usando a API](./import-packaged-recipe-api.md) para criar um mecanismo, que é necessária para treinar e avaliar um modelo usando a API.

Siga este [tutorial](../../tutorials/authentication.md) para obter autorização para chamadas de API de criação de start.

No tutorial, agora você deve ter os seguintes valores:

- `{ACCESS_TOKEN}`: O valor do token do portador específico fornecido após a autenticação.
- `{IMS_ORG}`: Suas credenciais organizacionais IMS encontradas na sua integração exclusiva ao Adobe Experience Platform.
- `{API_KEY}`: O valor da sua chave de API específica foi encontrado na sua integração exclusiva ao Adobe Experience Platform.

- Link para uma imagem do Docker de um serviço inteligente

## Fluxo de trabalho da API

Estaremos consumindo as APIs para criar uma Execução de Experimento para treinamento. Para este tutorial, estaremos focados nos endpoints **Engines**, **MLInances** e **Experiments** . O gráfico a seguir descreve a relação entre os três e também introduz a ideia de uma Execução e um Modelo.

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE]
>
>Os termos &quot;Mecanismo&quot;, &quot;MLInposition&quot;, &quot;MLService&quot;, &quot;Experimento&quot; e &quot;Modelo&quot; são chamados de termos diferentes na interface do usuário. Se você for da interface do usuário, a tabela a seguir mapeará as diferenças.
> 
> | Termo da interface do usuário | Termo da API |
> --- | ---
> | Receita | Mecanismo |
> | Modelo | Instância MLI |
> | Execuções de treinamento | Experimento |
> | Serviço de | MLService |



### Criar uma instância MLI

A criação de uma instância MLI pode ser feita usando a seguinte solicitação. Você usará o que foi retornado ao criar um Mecanismo a partir do tutorial `{ENGINE_ID}` Importar uma Receita empacotada usando a API [](./import-packaged-recipe-ui.md) .

**Solicitação**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/mlInstances \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d `{JSON_PAYLOAD}`
```

`{ACCESS_TOKEN}`: O valor do token do portador específico fornecido após a autenticação.\
`{IMS_ORG}`: Suas credenciais organizacionais IMS encontradas na sua integração exclusiva ao Adobe Experience Platform.\
`{API_KEY}`: O valor da sua chave de API específica foi encontrado na sua integração exclusiva ao Adobe Experience Platform.\
`{JSON_PAYLOAD}`: A configuração da nossa instância MLI. O exemplo que usamos em nosso tutorial é mostrado aqui:

```JSON
{
    "name": "Retail - Instance",
    "description": "Instance for ML Instance",
    "engineId": "{ENGINE_ID}",
    "createdBy": {
        "displayName": "John Doe",
        "userId": "johnd"
    },
    "tags": {
        "purpose": "tutorial"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "numFeatures",
                    "value": "10"
                },
                {
                    "key": "maxIter",
                    "value": "2"
                },
                {
                    "key": "regParam",
                    "value": "0.15"
                },
                {
                    "key": "trainingDataLocation",
                    "value": "sample_training_data.csv"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoringDataLocation",
                    "value": "sample_scoring_data.csv"
                },
                {
                    "key": "scoringResultsLocation",
                    "value": "scoring_results.net"
                }
            ]
        }
    ]
}
```

>[!NOTE]
>
>No `{JSON_PAYLOAD}`, definimos parâmetros usados para treinamento e pontuação no `tasks` array. A ID `{ENGINE_ID}` é o Mecanismo que você deseja usar e o `tag` campo é um parâmetro opcional usado para identificar a Instância.

A resposta conterá o `{INSTANCE_ID}` que representa a instância MLI criada. É possível criar várias MLInentes de modelo com configurações diferentes.

**Resposta**

```JSON
{
    "id": "{INSTANCE_ID}",
    "name": "Retail - Instance",
    "description": "Instance for ML Instance",
    "engineId": "{ENGINE_ID}",
    "created": "2018-21-21T11:11:11.111Z",
    "createdBy": {
        "displayName": "John Doe",
        "userId": "johnd"
    },
    "updated": "2018-21-01T11:11:11.111Z",
    "deleted": false,
    "tags": {
        "purpose": "tutorial"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [...]
        },
        {
            "name": "score",
            "parameters": [...]
        }
    ]
}
```

`{ENGINE_ID}`: Essa ID que representa o mecanismo no qual a MLInposition é criada.\
`{INSTANCE_ID}`: A ID que representa a instância MLI.

### Criar um experimento

Um Experimento é usado por um cientista de dados para chegar a um modelo de alto desempenho durante o treinamento. Vários experimentos incluem alteração de conjuntos de dados, recursos, parâmetros de aprendizado e hardware. A seguir está um exemplo de criação de um Experimento.

**Solicitação**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY' \
  -d `{JSON PAYLOAD}`
```

`{IMS_ORG}`: Suas credenciais organizacionais IMS encontradas na sua integração exclusiva ao Adobe Experience Platform.\
`{ACCESS_TOKEN}`: O valor do token do portador específico fornecido após a autenticação.\
`{API_KEY}`: O valor da sua chave de API específica foi encontrado na sua integração exclusiva ao Adobe Experience Platform.\
`{JSON_PAYLOAD}`: Objeto de experimento criado. O exemplo que usamos em nosso tutorial é mostrado aqui:

```JSON
{
    "name": "Experiment for Retail ",
    "mlInstanceId": "{INSTANCE_ID}",
    "tags": {
        "test": "guide"
    }
}
```

`{INSTANCE_ID}`: A ID que representa a instância MLI.

A resposta da criação do Experimento é assim.

**Resposta**

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "created": "2018-01-01T11:11:11.111Z",
    "updated": "2018-01-01T11:11:11.111Z",
    "deleted": false,
    "tags": {
        "test": "guide"
    }
}
```

`{EXPERIMENT_ID}`: A ID que representa o Experimento que você acabou de criar.
`{INSTANCE_ID}`: A ID que representa a instância MLI.

### Criar um Experimento programado para treinamento

Experimentos programados são usados para que não seja necessário criar cada Execução de experimento por meio de uma chamada de API. Em vez disso, fornecemos todos os parâmetros necessários durante a criação do Experimento e cada execução será criada periodicamente.

Para indicar a criação de um Experimento programado, é necessário adicionar uma `template` seção no corpo da solicitação. Em `template`, todos os parâmetros necessários para as execuções de programação são incluídos, como `tasks`, que indicam a ação e `schedule`, que indica o tempo das execuções programadas.

**Solicitação**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}`
```

`{IMS_ORG}`: Suas credenciais organizacionais IMS encontradas na sua integração exclusiva ao Adobe Experience Platform.\
`{ACCESS_TOKEN}`: O valor do token do portador específico fornecido após a autenticação.\
`{API_KEY}`: O valor da sua chave de API específica foi encontrado na sua integração exclusiva ao Adobe Experience Platform.\
`{JSON_PAYLOAD}`: Dados a serem publicados. O exemplo que usamos em nosso tutorial é mostrado aqui:

```JSON
{
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "template": {
        "tasks": [{
            "name": "train",
            "parameters": [
                   {
                        "value": "1000",
                        "key": "numFeatures"
                    }
            ],
            "specification": {
                "type": "SparkTaskSpec",
                "executorCores": 5,
                "numExecutors": 5
            }
        }],
        "schedule": {
            "cron": "*/20 * * * *",
            "startTime": "2018-11-11",
            "endTime": "2019-11-11"
        }
    }
}
```

Quando criamos um Experimento, o corpo, `{JSON_PAYLOAD}`, deve conter o parâmetro `mlInstanceId` ou o `mlInstanceQuery` . Neste exemplo, um Experimento programado chamará uma execução a cada 20 minutos, definido no `cron` parâmetro, começando do `startTime` até o `endTime`.

**Resposta**

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "created": "2018-11-11T11:11:11.111Z",
    "updated": "2018-11-11T11:11:11.111Z",
    "deleted": false,
    "workflowId": "endid123_0379bc0b_8f7e_4706_bcd9_1a2s3d4f5g_abcdf",
    "template": {
        "tasks": [
            {
                "name": "train",
                "parameters": [...],
                "specification": {
                    "type": "SparkTaskSpec",
                    "executorCores": 5,
                    "numExecutors": 5
                }
            }
        ],
        "schedule": {
            "cron": "*/20 * * * *",
            "startTime": "2018-07-04",
            "endTime": "2018-07-06"
        }
    }
}
```

`{EXPERIMENT_ID}`: A ID que representa o Experimento.\
`{INSTANCE_ID}`: A ID que representa a instância MLI.


### Criar uma Execução de Experimento para treinamento

Com uma entidade do Experimento criada, uma execução de treinamento pode ser criada e executada usando a chamada abaixo. Você precisará do `{EXPERIMENT_ID}` e indicará o que `mode` deseja acionar no corpo da solicitação.

**Solicitação**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{EXPERIMENT_ID}`: A ID correspondente ao Experimento que você deseja público alvo. Isso pode ser encontrado na resposta ao criar seu Experimento.\
`{IMS_ORG}`: Suas credenciais organizacionais IMS encontradas na sua integração exclusiva ao Adobe Experience Platform.\
`{ACCESS_TOKEN}`: O valor do token do portador específico fornecido após a autenticação.\
`{API_KEY}`: O valor da sua chave de API específica foi encontrado na sua integração exclusiva ao Adobe Experience Platform.\
`{JSON_PAYLOAD}`: Para criar uma execução de treinamento, é necessário incluir o seguinte no corpo:

```JSON
{
    "mode":"Train"
}
```

Você também pode substituir os parâmetros de configuração incluindo uma `tasks` matriz:

```JSON
{
   "mode":"Train",
   "tasks": [
        {
           "name": "train",
           "parameters": [
                {
                   "key": "numFeatures",
                   "value": "2"
                }
            ]
        }
    ]
}
```

Você obterá a seguinte resposta, informando o usuário `{EXPERIMENT_RUN_ID}` e a configuração em `tasks`.

**Resposta**

```JSON
{
    "id": "{EXPERIMENT_RUN_ID}",
    "mode": "train",
    "experimentId": "{EXPERIMENT_ID}",
    "created": "2018-01-01T11:11:11.903Z",
    "updated": "2018-01-01T11:11:11.903Z",
    "deleted": false,
    "tasks": [
        {
            "name": "Train",
            "parameters": [...]
        }
    ]
}
```

`{EXPERIMENT_RUN_ID}`:  A ID que representa a Execução do Experimento.\
`{EXPERIMENT_ID}`: A ID que representa o Experimento em que a Execução de Experimento está.

### Recuperar um status de Execução de Experimento

O status da execução do Experimento pode ser consultado com o `{EXPERIMENT_RUN_ID}`.

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs/{EXPERIMENT_RUN_ID}/status \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}'
```

`{EXPERIMENT_ID}`: A ID que representa o Experimento.\
`{EXPERIMENT_RUN_ID}`: A ID que representa a Execução do Experimento.\
`{ACCESS_TOKEN}`: O valor do token do portador específico fornecido após a autenticação.\
`{IMS_ORG}`: Suas credenciais organizacionais IMS encontradas na sua integração exclusiva ao Adobe Experience Platform.\
`{API_KEY}`: O valor da sua chave de API específica foi encontrado na sua integração exclusiva ao Adobe Experience Platform.

**Resposta**

A chamada do GET fornecerá o status no `state` parâmetro, como mostrado abaixo:

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "RunStatus for experimentRunId {EXPERIMENT_RUN_ID}",
    "experimentRunId": "{EXPERIMENT_RUN_ID}",
    "deleted": false,
    "status": {
        "tasks": [
            {
                "id": "{MODEL_ID}",
                "state": "DONE",
                "tasklogs": [
                    {
                        "name": "execution",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    },
                    {
                        "name": "stderr",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    },
                    {
                        "name": "stdout",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    }
                ]
            }
        ]
    }
}
```

`{EXPERIMENT_RUN_ID}`:  A ID que representa a Execução do Experimento.\
`{EXPERIMENT_ID}`: A ID que representa o Experimento em que a Execução de Experimento está.

Além do `DONE` estado, outros estados incluem:
- `PENDING`
- `RUNNING`
- `FAILED`

Para obter mais informações, os registros detalhados podem ser encontrados sob o `tasklogs` parâmetro.

### Recuperar o modelo treinado

Para que o Modelo treinado seja criado acima durante o treinamento, fazemos a seguinte solicitação:

**Solicitação**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_RUN_ID}`: A ID correspondente à Execução do experimento que você deseja público alvo. Isso pode ser encontrado na resposta ao criar sua Execução de Experimento.\
`{ACCESS_TOKEN}`: O valor do token do portador específico fornecido após a autenticação.\
`{IMS_ORG}`: Suas credenciais organizacionais IMS encontradas na sua integração exclusiva ao Adobe Experience Platform.

A resposta representa o Modelo treinado que foi criado.

**Resposta**

```JSON
{
    "children": [
        {
            "id": "{MODEL_ID}",
            "name": "Tutorial trained Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "trained model for ID",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/{MODEL_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z",
            "deleted": false
        }
    ],
    "_page": {
        "property": "ExperimentRunId=={EXPERIMENT_RUN_ID},deleted!=true",
        "count": 1
    }
}
```

`{MODEL_ID}`: A ID correspondente ao Modelo.\
`{EXPERIMENT_ID}`:  A ID correspondente ao Experimento em que a Execução do Experimento está localizada.\
`{EXPERIMENT_RUN_ID}`: A ID correspondente à execução do experimento.

### Parar e excluir um Experimento programado

Se você quiser interromper a execução de um Experimento programado antes de seu lançamento, `endTime`isso pode ser feito consultando uma solicitação de DELETE para o `{EXPERIMENT_ID}`

**Solicitação**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`:  A ID correspondente ao Experimento.\
`{ACCESS_TOKEN}`: O valor do token do portador específico fornecido após a autenticação.\
`{IMS_ORG}`: Suas credenciais organizacionais IMS encontradas na sua integração exclusiva ao Adobe Experience Platform.

>[!NOTE]
>
>A chamada da API desativará a criação de novas execuções do Experimento. No entanto, não interromperá a execução de Execuções de Experimento já em execução.

A seguir está a Resposta notificando que o Experimento foi excluído com êxito.

**Resposta**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## Próximas etapas

Este tutorial mostra como consumir as APIs para criar um Mecanismo, um Experimento, Execuções de Experimento programadas e Modelos treinados. No [próximo exercício](./score-model-api.md), você fará previsões marcando um novo conjunto de dados usando o modelo treinado de melhor desempenho.