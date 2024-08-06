---
keywords: Experience Platform; Marcar um modelo; Área de trabalho de ciência de dados; tópicos populares; api sensei de aprendizado de máquina
solution: Experience Platform
title: Marcar um modelo usando a API de aprendizado de máquina do Sensei
type: Tutorial
description: Esta tutorial mostrará como usar as APIs de aprendizagem de máquina do Sensei para criar um Experimento e uma Execução Experimento.
exl-id: 202c63b0-86d8-4a82-8ec8-d144a8911d08
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 1%

---

# Pontuar um modelo usando a variável [!DNL Sensei Machine Learning API]

>[!NOTE]
>
>O Área de trabalho de ciência de dados não está mais disponível para compra.
>
>Esta documentação destina-se a clientes existentes com direitos anteriores à Data Science Área de trabalho.

Este tutorial mostrará como usar as APIs para criar um Experimento e uma Execução Experimento. Para obter uma lista de todos os endpoints da API de aprendizagem de máquina do Sensei, consulte [esta documento](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/).

## Criar um Experimento agendado para pontuação

Semelhante aos Experimentos programados para treinamento, a criação de um Experimento programado para pontuação também é feita por meio da inclusão de uma `template` seção no parâmetro body. Além disso, o campo `name` em `tasks` no corpo é definido como `score`.

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

`{EXPERIMENT_ID}`: a ID que representa a Experimento.\
`{INSTANCE_ID}`: a ID que representa o MLInstance.


### Criar uma corrida Experimento para pontuação

Agora, com o modelo treinado, podemos criar uma Experimento Corrida para pontuação. O valor do `modelId` parâmetro é o `id` parâmetro retornado no GET Modelo solicitação acima.

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

`{ORG_ID}`: suas credenciais de organização encontradas na integração exclusiva do Adobe Experience Platform.\
`{ACCESS_TOKEN}`: seu valor de token portador específico fornecido após a autenticação.\
`{API_KEY}`: seu valor de chave de API específico encontrado na integração exclusiva do Adobe Experience Platform.\
`{EXPERIMENT_ID}`: a ID correspondente ao Experimento que você deseja Direcionamento. Isso pode ser encontrado na resposta ao criar sua Experimento.\
`{JSON_PAYLOAD}`: dados a serem publicados. O exemplo que usamos em nosso tutorial está aqui:

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
`{ORG_ID}`: suas credenciais de organização encontradas na integração exclusiva do Adobe Experience Platform.

Como há várias Experimento Execuções para um Experimento específico, a resposta retornada terá uma matriz de IDs de execução.

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

`{EXPERIMENT_RUN_ID}`: a ID correspondente ao Experimento Run.\
`{EXPERIMENT_ID}`: a ID correspondente à Experimento em que a Execução está.

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
