---
keywords: Experience Platform;Pontuar um modelo;Data Science Workspace;tópicos populares;api de aprendizado de máquina do sensei
solution: Experience Platform
title: Pontuar um modelo usando a API de aprendizado de máquina do Sensei
type: Tutorial
description: Este tutorial mostrará como aproveitar as APIs do Sensei Machine Learning para criar um experimento e uma execução de experimento.
exl-id: 202c63b0-86d8-4a82-8ec8-d144a8911d08
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---

# Pontuar um modelo usando o [!DNL Sensei Machine Learning API]

Este tutorial mostrará como aproveitar as APIs para criar um experimento e uma execução de experimento. Para obter uma lista de todos os endpoints na API do Sensei Machine Learning, consulte [este documento](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/).

## Criar um experimento agendado para pontuação

Semelhante aos Experimentos agendados para treinamento, a criação de um Experimento agendado para pontuação também é feita incluindo uma seção `template` no parâmetro do corpo. Além disso, o campo `name` em `tasks` no corpo é definido como `score`.

Este é um exemplo de criação de um Experimento que será executado a cada 20 minutos a partir de `startTime` e será executado até `endTime`.

**Solicitação**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{ORG_ID}`: as credenciais da sua organização foram encontradas em sua integração exclusiva com o Adobe Experience Platform.\
`{ACCESS_TOKEN}`: Seu valor de token de portador específico fornecido após a autenticação.\
`{API_KEY}`: O valor da sua chave de API específica foi encontrado na sua integração exclusiva do Adobe Experience Platform.\
`{JSON_PAYLOAD}`: objeto de Execução de Experimento a ser enviado. O exemplo que usamos em nosso tutorial é mostrado aqui:

```JSON
{
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "template": {
        "tasks": [{
            "name": "score",
            "parameters": [
                {
                    "key": "modelId",
                    "value": "{MODEL_ID}"
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
            "startTime": "2018-07-04",
            "endTime": "2018-07-06"
        }
    }
}
```

`{INSTANCE_ID}`: a ID que representa a MLInstance.\
`{MODEL_ID}`: a ID que representa o Modelo treinado.

Veja a seguir a resposta após criar o experimento agendado.

**Resposta**

```JSON
{
  "id": "{EXPERIMENT_ID}",
  "name": "Experiment for Retail",
  "mlInstanceId": "{INSTANCE_ID}",
  "created": "2018-11-11T11:11:11.111Z",
  "updated": "2018-11-11T11:11:11.111Z",
  "template": {
    "tasks": [
      {
        "name": "score",
        "parameters": [...],
        "specification": {
          "type": "SparkTaskSpec",
          "executorCores": 5,
          "numExecutors": 5
        }
      }
    ],
    "schedule": {
      "cron": "*\/20 * * * *",
      "startTime": "2018-07-04",
      "endTime": "2018-07-06"
    }
  }
}
```

`{EXPERIMENT_ID}`: a ID que representa o Experimento.\
`{INSTANCE_ID}`: a ID que representa a MLInstance.


### Criar uma execução de experimento para pontuação

Agora, com o modelo treinado, podemos criar uma Execução de experimento para pontuação. O valor do parâmetro `modelId` é o parâmetro `id` retornado na solicitação do Modelo GET acima.

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

`{ORG_ID}`: as credenciais da sua organização foram encontradas em sua integração exclusiva com o Adobe Experience Platform.\
`{ACCESS_TOKEN}`: Seu valor de token de portador específico fornecido após a autenticação.\
`{API_KEY}`: O valor da sua chave de API específica foi encontrado na sua integração exclusiva do Adobe Experience Platform.\
`{EXPERIMENT_ID}`: a ID correspondente ao Experimento que você deseja direcionar. Isso pode ser encontrado na resposta ao criar o experimento.\
`{JSON_PAYLOAD}`: Dados a serem postados. O exemplo que usamos em nosso tutorial está aqui:

```JSON
{
   "mode":"score",
    "tasks": [
        {
            "name": "score",
            "parameters": [
                {
                    "key": "modelId",
                    "value": "{MODEL_ID}"
                }
            ]
        }
    ]
}
```

`{MODEL_ID}`: a ID correspondente ao Modelo.

A resposta da criação da execução do experimento é mostrada abaixo:

**Resposta**

```JSON
{
    "id": "{EXPERIMENT_RUN_ID}",
    "mode": "score",
    "experimentId": "{EXPERIMENT_ID}",
    "created": "2018-01-01T11:11:11.011Z",
    "updated": "2018-01-01T11:11:11.011Z",
    "deleted": false,
    "tasks": [
        {
            "name": "score",
            "parameters": [...]
        }
    ]
}
```

`{EXPERIMENT_ID}`: a ID correspondente ao experimento em que a execução está.\
`{EXPERIMENT_RUN_ID}`: a identificação correspondente à execução do experimento que você acabou de criar.


### Recuperar um status de Execução de experimento para a Execução de experimento programada

Para obter Execuções de experimento para Experimentos programados, a consulta é mostrada abaixo:

**Solicitação**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`: a ID correspondente ao experimento em que a execução está.\
`{ACCESS_TOKEN}`: Seu valor de token de portador específico fornecido após a autenticação.\
`{ORG_ID}`: as credenciais da sua organização foram encontradas em sua integração exclusiva com o Adobe Experience Platform.

Como há várias execuções de experimento para um experimento específico, a resposta retornada terá uma matriz de IDs de execução.

**Resposta**

```JSON
{
    "children": [
        {
            "id": "{EXPERIMENT_RUN_ID}",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z"
        },
        {
            "id": "{EXPERIMENT_RUN_ID}",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z"
        }
    ]
}
```

`{EXPERIMENT_RUN_ID}`: a identificação correspondente à execução do experimento.\
`{EXPERIMENT_ID}`: a ID correspondente ao experimento em que a execução está.

### Parar e excluir um experimento agendado

Se você quiser parar a execução de um Experimento agendado antes de seu `endTime`, isso pode ser feito consultando uma solicitação DELETE para o `{EXPERIMENT_ID}`

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
