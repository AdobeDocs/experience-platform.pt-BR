---
keywords: Experience Platform, treinamento e avaliação, Data Science Workspace, tópicos populares, API de aprendizado de máquina Sensei
solution: Experience Platform
title: Treine e avalie um modelo usando a API Sensei Machine Learning
topic-legacy: tutorial
type: Tutorial
description: Este tutorial mostrará como criar, treinar e avaliar um modelo usando chamadas da API de aprendizado de máquina do Sensei.
exl-id: 8107221f-184c-426c-a33e-0ef55ed7796e
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 1%

---

# Comboio e avaliação de um modelo utilizando [!DNL Sensei Machine Learning] API


Este tutorial mostrará como criar, treinar e avaliar um Modelo usando chamadas de API. Consulte [este documento](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) para obter uma lista detalhada da documentação da API.

## Pré-requisitos

Siga as [Importar uma Receita empacotada usando a API](./import-packaged-recipe-api.md) para criar um mecanismo, que é necessário para treinar e avaliar um modelo usando a API.

Siga as [Tutorial de autenticação da API do Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) para começar a fazer chamadas de API.

No tutorial, agora você deve ter os seguintes valores:

- `{ACCESS_TOKEN}`: O valor do token portador específico fornecido após a autenticação.
- `{ORG_ID}`: Suas credenciais da organização IMS encontradas na integração exclusiva do Adobe Experience Platform.
- `{API_KEY}`: Seu valor específico da chave de API encontrado na integração exclusiva do Adobe Experience Platform.

- Vincular a uma imagem do Docker de um serviço inteligente

## Fluxo de trabalho da API

Estaremos consumindo as APIs para criar uma Execução de experiência para treinamento. Neste tutorial, o foco será nos endpoints Mecanismos, MLInances e Experimentos. O gráfico a seguir descreve a relação entre os três e também introduz a ideia de uma Execução e um Modelo.

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE]
>
>Os termos &quot;Mecanismo&quot;, &quot;Instância MLI&quot;, &quot;Serviço MLS&quot;, &quot;Experimento&quot; e &quot;Modelo&quot; são chamados de termos diferentes na interface do usuário. Se você vem da interface do usuário, a tabela a seguir mapeia as diferenças.

| Termo da interface do usuário | Termo da API |
| --- | --- |
| Receita | Mecanismo |
| Modelo | InstânciaMLI |
| Execuções de treinamento | Experimento |
| Serviço de | MLService |

### Criar uma instância MLI

A criação de uma instância MLI pode ser feita usando a seguinte solicitação. Você usará o `{ENGINE_ID}` que foi retornado ao criar um Mecanismo no [Importar uma Receita empacotada usando a API](./import-packaged-recipe-ui.md) tutorial.

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

`{ACCESS_TOKEN}`: O valor do token portador específico fornecido após a autenticação.\
`{ORG_ID}`: Suas credenciais da organização IMS encontradas na integração exclusiva do Adobe Experience Platform.\
`{API_KEY}`: Seu valor específico da chave de API encontrado na integração exclusiva do Adobe Experience Platform.\
`{JSON_PAYLOAD}`: A configuração da nossa instância MLI. O exemplo usado em nosso tutorial é mostrado aqui:

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
>No `{JSON_PAYLOAD}`, definimos parâmetros usados para treinamento e pontuação no `tasks` matriz. O `{ENGINE_ID}` é a ID do mecanismo que você deseja usar e a variável `tag` é um parâmetro opcional usado para identificar a Instância.

A resposta contém a variável `{INSTANCE_ID}` que representa a instância MLI criada. É possível criar várias MLInstâncias de modelo com configurações diferentes.

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

`{ENGINE_ID}`: Essa ID que representa o mecanismo no qual a instância MLI é criada.\
`{INSTANCE_ID}`: A ID que representa a instância MLI.

### Criar um experimento

Um Experimento é usado por um cientista de dados para chegar a um modelo de alto desempenho durante o treinamento. Vários experimentos incluem a alteração de conjuntos de dados, recursos, parâmetros de aprendizagem e hardware. Este é um exemplo de criação de um Experimento.

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

`{ORG_ID}`: Suas credenciais da organização IMS encontradas na integração exclusiva do Adobe Experience Platform.\
`{ACCESS_TOKEN}`: O valor do token portador específico fornecido após a autenticação.\
`{API_KEY}`: Seu valor específico da chave de API encontrado na integração exclusiva do Adobe Experience Platform.\
`{JSON_PAYLOAD}`: Objeto de experimento criado. O exemplo usado em nosso tutorial é mostrado aqui:

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

Os Experimentos programados são usados para que não seja necessário criar cada Execução de experiência por meio de uma chamada de API. Em vez disso, fornecemos todos os parâmetros necessários durante a criação do Experimento e cada execução será criada periodicamente.

Para indicar a criação de um Experimento agendado, é necessário adicionar um `template` no corpo da solicitação. Em `template`, todos os parâmetros necessários para as execuções de agendamento são incluídos, como `tasks`, que indicam que ação, e `schedule`, que indica o tempo das execuções agendadas.

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

`{ORG_ID}`: Suas credenciais da organização IMS encontradas na integração exclusiva do Adobe Experience Platform.\
`{ACCESS_TOKEN}`: O valor do token portador específico fornecido após a autenticação.\
`{API_KEY}`: Seu valor específico da chave de API encontrado na integração exclusiva do Adobe Experience Platform.\
`{JSON_PAYLOAD}`: Conjunto de dados a serem publicados. O exemplo usado em nosso tutorial é mostrado aqui:

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

Quando criamos um Experimento, o corpo, `{JSON_PAYLOAD}`, deve conter a variável `mlInstanceId` ou `mlInstanceQuery` parâmetro. Neste exemplo, um Experimento programado chamará uma execução a cada 20 minutos, definido na variável `cron` , a partir do `startTime` até que o `endTime`.

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


### Criar um Experimento Executar para treinamento

Com uma entidade de Experimento criada, uma execução de treinamento pode ser criada e executada usando a chamada abaixo. Você precisará do `{EXPERIMENT_ID}` e indicar o que `mode` você deseja acionar no corpo da solicitação.

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

`{EXPERIMENT_ID}`: A ID correspondente ao Experimento que você deseja direcionar. Isso pode ser encontrado na resposta ao criar seu Experimento.\
`{ORG_ID}`: Suas credenciais da organização IMS encontradas na integração exclusiva do Adobe Experience Platform.\
`{ACCESS_TOKEN}`: O valor do token portador específico fornecido após a autenticação.\
`{API_KEY}`: Seu valor específico da chave de API encontrado na integração exclusiva do Adobe Experience Platform.\
`{JSON_PAYLOAD}`: Para criar uma execução de treinamento, é necessário incluir o seguinte no corpo:

```JSON
{
    "mode":"Train"
}
```

Você também pode substituir os parâmetros de configuração incluindo um `tasks` array:

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

Você receberá a seguinte resposta, que informará o `{EXPERIMENT_RUN_ID}` e a configuração em `tasks`.

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

`{EXPERIMENT_RUN_ID}`: A ID que representa a Execução do experimento.\
`{EXPERIMENT_ID}`: A ID que representa o Experimento no qual a Execução do Experimento está.

### Recuperar um status de Execução de Experimento

O status da execução do Experimento pode ser consultado com a variável `{EXPERIMENT_RUN_ID}`.

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs/{EXPERIMENT_RUN_ID}/status \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}'
```

`{EXPERIMENT_ID}`: A ID que representa o Experimento.\
`{EXPERIMENT_RUN_ID}`: A ID que representa a Execução do experimento.\
`{ACCESS_TOKEN}`: O valor do token portador específico fornecido após a autenticação.\
`{ORG_ID}`: Suas credenciais da organização IMS encontradas na integração exclusiva do Adobe Experience Platform.\
`{API_KEY}`: Seu valor específico da chave de API encontrado na integração exclusiva do Adobe Experience Platform.

**Resposta**

A chamada do GET fornecerá o status na variável `state` como mostrado abaixo:

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

`{EXPERIMENT_RUN_ID}`: A ID que representa a Execução do experimento.\
`{EXPERIMENT_ID}`: A ID que representa o Experimento no qual a Execução do Experimento está.

Além do `DONE` , outros estados incluem:
- `PENDING`
- `RUNNING`
- `FAILED`

Para obter mais informações, os logs detalhados podem ser encontrados na seção `tasklogs` parâmetro.

### Recuperar o modelo treinado

Para obter o modelo treinado criado acima durante o treinamento, fazemos o seguinte pedido:

**Solicitação**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_RUN_ID}`: A ID correspondente à Execução do experimento que você deseja direcionar. Isso pode ser encontrado na resposta ao criar sua Execução de experiência.\
`{ACCESS_TOKEN}`: O valor do token portador específico fornecido após a autenticação.\
`{ORG_ID}`: Suas credenciais da organização IMS encontradas na integração exclusiva do Adobe Experience Platform.

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
`{EXPERIMENT_ID}`: A ID correspondente ao Experimento em que a Execução do experimento está localizada.\
`{EXPERIMENT_RUN_ID}`: A ID correspondente à Execução do experimento.

### Parar e excluir um experimento programado

Se você deseja interromper a execução de um Experimento programado antes de seu `endTime`, isso pode ser feito consultando uma solicitação DELETE para a variável `{EXPERIMENT_ID}`

**Solicitação**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`: A ID correspondente ao Experimento.\
`{ACCESS_TOKEN}`: O valor do token portador específico fornecido após a autenticação.\
`{ORG_ID}`: Suas credenciais da organização IMS encontradas na integração exclusiva do Adobe Experience Platform.

>[!NOTE]
>
>A chamada da API desativará a criação de novas execuções de Experimento. No entanto, não interromperá a execução de Execuções de Experimento já em execução.

Veja a seguir a Resposta notificando que o Experimento foi excluído com êxito.

**Resposta**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## Próximas etapas

Este tutorial aborda como consumir as APIs para criar um Mecanismo, um Experimento, Execuções de Experimento Programadas e Modelos Treinados. No [próximo exercício](./score-model-api.md), você fará previsões marcando um novo conjunto de dados usando o modelo treinado de melhor desempenho.
