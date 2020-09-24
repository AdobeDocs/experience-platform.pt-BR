---
keywords: Experience Platform;Score a model;Data Science Workspace;popular topics;sensei machine learning api
solution: Experience Platform
title: Pontuação de um modelo (API)
topic: tutorial
type: Tutorial
description: Este tutorial mostrará como aproveitar as APIs de aprendizado de máquina do Sensei para criar um Experimento e uma Execução de Experimento.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 1%

---


# Pontuação de um modelo (API)

Este tutorial mostrará como aproveitar as APIs para criar um Experimento e uma Execução de Experimento. Para obter uma lista detalhada da documentação da API, consulte [este documento](https://www.adobe.io/apis/cloudplatform/dataservices/api-reference.html).

## Criar um Experimento programado para pontuação

Semelhante aos Experimentos programados para treinamento, a criação de um Experimento programado para pontuação também é feita pela inclusão de uma `template` seção ao parâmetro body. Além disso, o `name` campo `tasks` no corpo é definido como `score`.

A seguir está um exemplo de criação de um Experimento que será executado a cada 20 minutos, começando em `startTime` e sendo executado até `endTime`.

**Solicitação**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{IMS_ORG}`: Suas credenciais organizacionais IMS encontradas na sua integração exclusiva ao Adobe Experience Platform.\
`{ACCESS_TOKEN}`: O valor do token do portador específico fornecido após a autenticação.\
`{API_KEY}`: O valor da sua chave de API específica foi encontrado na sua integração exclusiva ao Adobe Experience Platform.\
`{JSON_PAYLOAD}`: Objeto de Execução de Experimento a ser enviado. O exemplo que usamos em nosso tutorial é mostrado aqui:

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

`{INSTANCE_ID}`: A ID que representa a instância MLI.\
`{MODEL_ID}`: A ID que representa o Modelo treinado.

A seguir está a resposta após a criação do Experimento programado.

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

`{EXPERIMENT_ID}`: A ID que representa o Experimento.\
`{INSTANCE_ID}`: A ID que representa a instância MLI.


### Criar uma execução de experimento para pontuação

Agora com o modelo treinado, podemos criar uma Execução de Experimento para pontuação. O valor do `modelId` parâmetro é o `id` parâmetro retornado na solicitação do Modelo de GET acima.

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

`{IMS_ORG}`: Suas credenciais organizacionais IMS encontradas na sua integração exclusiva ao Adobe Experience Platform.\
`{ACCESS_TOKEN}`: O valor do token do portador específico fornecido após a autenticação.\
`{API_KEY}`: O valor da sua chave de API específica foi encontrado na sua integração exclusiva ao Adobe Experience Platform.\
`{EXPERIMENT_ID}`: A ID correspondente ao Experimento que você deseja público alvo. Isso pode ser encontrado na resposta ao criar seu Experimento.\
`{JSON_PAYLOAD}`: Dados a serem publicados. O exemplo que usamos em nosso tutorial é o seguinte:

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

`{MODEL_ID}`: A ID correspondente ao Modelo.

A resposta da criação da Execução de Experimento é mostrada abaixo:

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

`{EXPERIMENT_ID}`:  A ID correspondente ao Experimento em que a execução está localizada.\
`{EXPERIMENT_RUN_ID}`: A ID correspondente à Execução do experimento que você acabou de criar.


### Recuperar um status de Execução de Experimento para Execução de Experimento programada

Para obter Execuções de Experimento para Experimentos programados, o query é mostrado abaixo:

**Solicitação**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`:  A ID correspondente ao Experimento em que a execução está localizada.\
`{ACCESS_TOKEN}`: O valor do token do portador específico fornecido após a autenticação.\
`{IMS_ORG}`: Suas credenciais organizacionais IMS encontradas na sua integração exclusiva ao Adobe Experience Platform.

Como há várias Execuções de Experimento para um Experimento específico, a resposta retornada terá uma matriz de IDs de Execução.

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

`{EXPERIMENT_RUN_ID}`: A ID correspondente à execução do experimento.\
`{EXPERIMENT_ID}`:  A ID correspondente ao Experimento em que a execução está localizada.

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
