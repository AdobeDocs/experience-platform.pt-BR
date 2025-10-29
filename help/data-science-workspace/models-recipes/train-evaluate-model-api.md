---
keywords: Experience Platform;treinar e avaliar;Data Science Workspace;tópicos populares;API de aprendizado de máquina do Sensei
solution: Experience Platform
title: Treinar e avaliar um modelo usando a API de aprendizado de máquina do Sensei
type: Tutorial
description: Este tutorial mostrará como criar, treinar e avaliar um Modelo usando chamadas da API do Sensei Machine Learning.
exl-id: 8107221f-184c-426c-a33e-0ef55ed7796e
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 1%

---

# Treinar e avaliar um modelo usando a API [!DNL Sensei Machine Learning]

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

Este tutorial mostrará como criar, treinar e avaliar um Modelo usando chamadas de API. Consulte [este documento](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) para obter uma lista detalhada da documentação da API.

## Pré-requisitos

Siga a [Importar uma fórmula empacotada usando a API](./import-packaged-recipe-api.md) para criar um Mecanismo, necessário para treinar e avaliar um Modelo usando a API.

Siga o [tutorial de autenticação da API do Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) para começar a fazer chamadas de API.

No tutorial, agora você deve ter os seguintes valores:

- `{ACCESS_TOKEN}`: Seu valor de token de portador específico fornecido após a autenticação.
- `{ORG_ID}`: as credenciais da sua organização foram encontradas em sua integração exclusiva com o Adobe Experience Platform.
- `{API_KEY}`: O valor da sua chave de API específica foi encontrado na sua integração exclusiva do Adobe Experience Platform.

- Link para uma imagem do Docker de um serviço inteligente

## Fluxo de trabalho da API

Estaremos consumindo as APIs para criar uma Execução de experimento para treinamento. Neste tutorial, estaremos focados nos endpoints de Mecanismos, Instâncias do MLI e Experimentos. O gráfico a seguir descreve a relação entre os três e também introduz a ideia de uma Execução e um Modelo.

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE]
>
>Os termos &quot;Mecanismo&quot;, &quot;MLInstance&quot;, &quot;MLService&quot;, &quot;Experimento&quot; e &quot;Modelo&quot; são chamados de termos diferentes na interface do usuário. Se você vem da interface do usuário do, a tabela a seguir mapeia as diferenças.

| Termo da interface | Termo da API |
| --- | --- |
| Fórmula | Mecanismo |
| Modelo | MLInstance |
| Execuções de treinamento | Experimento |
| Serviço | MLService |

### Criar uma MLInstance

A criação de uma MLInstance pode ser feita usando a solicitação a seguir. Você usará o `{ENGINE_ID}` que foi retornado ao criar um Mecanismo a partir do [Tutorial de importação de fórmula empacotada usando a API](./import-packaged-recipe-ui.md).

**Solicitação**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/mlInstances \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d `{JSON_PAYLOAD}`
```

`{ACCESS_TOKEN}`: Seu valor de token de portador específico fornecido após a autenticação.\
`{ORG_ID}`: as credenciais da sua organização foram encontradas em sua integração exclusiva com o Adobe Experience Platform.\
`{API_KEY}`: O valor da sua chave de API específica foi encontrado na sua integração exclusiva do Adobe Experience Platform.\
`{JSON_PAYLOAD}`: A configuração de nossa MLInstance. O exemplo que usamos em nosso tutorial é mostrado aqui:

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
>No `{JSON_PAYLOAD}`, definimos parâmetros usados para treinamento e pontuação na matriz `tasks`. `{ENGINE_ID}` é a ID do Mecanismo que você deseja usar e o campo `tag` é um parâmetro opcional usado para identificar a Instância.

A resposta contém o `{INSTANCE_ID}` que representa a MLInstance criada. Várias MLInstances de modelo com configurações diferentes podem ser criadas.

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

`{ENGINE_ID}`: esta ID que representa o Mecanismo no qual a MLInstance é criada.\
`{INSTANCE_ID}`: a ID que representa a MLInstance.

### Criar um experimento

Um experimento é usado por um cientista de dados para chegar a um modelo de alto desempenho durante o treinamento. Vários experimentos incluem a alteração de conjuntos de dados, recursos, parâmetros de aprendizado e hardware. Veja a seguir um exemplo de como criar um experimento.

**Solicitação**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY' \
  -d `{JSON PAYLOAD}`
```

`{ORG_ID}`: as credenciais da sua organização foram encontradas em sua integração exclusiva com o Adobe Experience Platform.\
`{ACCESS_TOKEN}`: Seu valor de token de portador específico fornecido após a autenticação.\
`{API_KEY}`: O valor da sua chave de API específica foi encontrado na sua integração exclusiva do Adobe Experience Platform.\
`{JSON_PAYLOAD}`: objeto de experimento criado. O exemplo que usamos em nosso tutorial é mostrado aqui:

```JSON
{
    "name": "Experiment for Retail ",
    "mlInstanceId": "{INSTANCE_ID}",
    "tags": {
        "test": "guide"
    }
}
```

`{INSTANCE_ID}`: a ID que representa a MLInstance.

A resposta da criação do experimento é semelhante a esta.

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

`{EXPERIMENT_ID}`: a ID que representa o experimento recém-criado.
`{INSTANCE_ID}`: a ID que representa a MLInstance.

### Criar um experimento programado para treinamento

Experimentos agendados são usados para que não seja necessário criar cada uma das execuções de experimento por meio de uma chamada de API. Em vez disso, fornecemos todos os parâmetros necessários durante a criação do Experimento e cada execução será criada periodicamente.

Para indicar a criação de um experimento agendado, devemos adicionar uma seção `template` no corpo da solicitação. Em `template`, todos os parâmetros necessários para execuções de agendamento estão incluídos, como `tasks`, que indica qual ação, e `schedule`, que indica o tempo das execuções agendadas.

**Solicitação**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}`
```

`{ORG_ID}`: as credenciais da sua organização foram encontradas em sua integração exclusiva com o Adobe Experience Platform.\
`{ACCESS_TOKEN}`: Seu valor de token de portador específico fornecido após a autenticação.\
`{API_KEY}`: O valor da sua chave de API específica foi encontrado na sua integração exclusiva do Adobe Experience Platform.\
`{JSON_PAYLOAD}`: Conjunto de dados a ser postado. O exemplo que usamos em nosso tutorial é mostrado aqui:

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

Quando criamos um Experimento, o corpo, `{JSON_PAYLOAD}`, deve conter o parâmetro `mlInstanceId` ou `mlInstanceQuery`. Neste exemplo, um Experimento agendado chamará uma execução a cada 20 minutos, definido no parâmetro `cron`, começando em `startTime` até `endTime`.

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

`{EXPERIMENT_ID}`: a ID que representa o Experimento.\
`{INSTANCE_ID}`: a ID que representa a MLInstance.


### Criar uma execução de experimento para treinamento

Com uma entidade de experimento criada, uma execução de treinamento pode ser criada e executada usando a chamada abaixo. Você precisará do `{EXPERIMENT_ID}` e indicará qual `mode` deseja acionar no corpo da solicitação.

**Solicitação**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{EXPERIMENT_ID}`: a ID correspondente ao Experimento que você deseja direcionar. Isso pode ser encontrado na resposta ao criar o experimento.\
`{ORG_ID}`: as credenciais da sua organização foram encontradas em sua integração exclusiva com o Adobe Experience Platform.\
`{ACCESS_TOKEN}`: Seu valor de token de portador específico fornecido após a autenticação.\
`{API_KEY}`: O valor da sua chave de API específica foi encontrado na sua integração exclusiva do Adobe Experience Platform.\
`{JSON_PAYLOAD}`: Para criar uma execução de treinamento, você terá que incluir o seguinte no corpo:

```JSON
{
    "mode":"Train"
}
```

Você também pode substituir os parâmetros de configuração incluindo uma matriz `tasks`:

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

Você receberá a seguinte resposta, que permitirá que você saiba o `{EXPERIMENT_RUN_ID}` e a configuração em `tasks`.

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

`{EXPERIMENT_RUN_ID}`: a identificação que representa a execução do experimento.\
`{EXPERIMENT_ID}`: a identificação que representa o experimento sob o qual a execução do experimento está.

### Recuperar um status de Execução de experimento

O status da execução do experimento pode ser consultado com o `{EXPERIMENT_RUN_ID}`.

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs/{EXPERIMENT_RUN_ID}/status \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}'
```

`{EXPERIMENT_ID}`: a ID que representa o Experimento.\
`{EXPERIMENT_RUN_ID}`: a identificação que representa a execução do experimento.\
`{ACCESS_TOKEN}`: Seu valor de token de portador específico fornecido após a autenticação.\
`{ORG_ID}`: as credenciais da sua organização foram encontradas em sua integração exclusiva com o Adobe Experience Platform.\
`{API_KEY}`: O valor da sua chave de API específica foi encontrado na sua integração exclusiva do Adobe Experience Platform.

**Resposta**

A chamada GET fornecerá o status no parâmetro `state`, conforme mostrado abaixo:

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

`{EXPERIMENT_RUN_ID}`: a identificação que representa a execução do experimento.\
`{EXPERIMENT_ID}`: a identificação que representa o experimento sob o qual a execução do experimento está.

Além do estado `DONE`, outros estados incluem:

- `PENDING`
- `RUNNING`
- `FAILED`

Para obter mais informações, os logs detalhados podem ser encontrados sob o parâmetro `tasklogs`.

### Recuperar o modelo treinado

Para obter o modelo treinado criado acima durante o treinamento, fazemos a seguinte solicitação:

**Solicitação**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_RUN_ID}`: a ID correspondente à Execução do experimento que você deseja direcionar. Isso pode ser encontrado na resposta ao criar a Execução de experimento.\
`{ACCESS_TOKEN}`: Seu valor de token de portador específico fornecido após a autenticação.\
`{ORG_ID}`: as credenciais da sua organização foram encontradas em sua integração exclusiva com o Adobe Experience Platform.

A resposta representa o modelo treinado que foi criado.

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

`{MODEL_ID}`: a ID correspondente ao Modelo.\
`{EXPERIMENT_ID}`: a ID correspondente ao experimento em que a execução do experimento está.\
`{EXPERIMENT_RUN_ID}`: a identificação correspondente à execução do experimento.

### Parar e excluir um experimento agendado

Se você deseja parar a execução de um Experimento agendado antes de seu `endTime`, isso pode ser feito consultando uma solicitação DELETE para o `{EXPERIMENT_ID}`

**Solicitação**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`: a ID correspondente ao experimento.\
`{ACCESS_TOKEN}`: Seu valor de token de portador específico fornecido após a autenticação.\
`{ORG_ID}`: as credenciais da sua organização foram encontradas em sua integração exclusiva com o Adobe Experience Platform.

>[!NOTE]
>
>A chamada de API desativará a criação de novas execuções de Experimento. No entanto, ela não interromperá a execução de execuções de experimentos já em execução.

Esta é a resposta que notifica que o experimento foi excluído com sucesso.

**Resposta**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## Próximas etapas

Este tutorial abordou como consumir as APIs para criar um mecanismo, um experimento, execuções de experimentos programadas e modelos treinados. No [próximo exercício](./score-model-api.md), você fará previsões pontuando um novo conjunto de dados usando o modelo treinado de melhor desempenho.
