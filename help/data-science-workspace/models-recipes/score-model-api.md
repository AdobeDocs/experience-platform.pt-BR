---
keywords: Experience Platform; Pontuar um modelo; Data Science Workspace; tópicos populares; api de aprendizado de máquina do sensei
solution: Experience Platform
title: Pontuar um modelo usando a API de aprendizado de máquina do Sensei
topic-legacy: tutorial
type: Tutorial
description: Este tutorial mostrará como aproveitar as APIs de aprendizado de máquina do Sensei para criar um experimento e uma execução de experimento.
exl-id: 202c63b0-86d8-4a82-8ec8-d144a8911d08
source-git-commit: 6ae6bbb5af0f007e483145dca5d4d505c388cc2c
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 1%

---

# Pontuação de um modelo usando a [!DNL Sensei Machine Learning API]

Este tutorial mostrará como aproveitar as APIs para criar um Experimento e uma Execução de Experimento. Para obter uma lista de todos os endpoints na API do Sensei Machine Learning, consulte [este documento](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/).

## Criar um Experimento agendado para pontuação

Semelhante aos Experimentos programados para treinamento, a criação de um Experimento programado para pontuação também é feita ao incluir um `template` para o parâmetro body . Além disso, a variável `name` campo sob `tasks` no corpo é definido como `score`.

Este é um exemplo de criação de um Experimento que será executado a cada 20 minutos a partir de `startTime` e será executado até `endTime`.

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

`{IMS_ORG}`: Suas credenciais da organização IMS encontradas na integração exclusiva do Adobe Experience Platform.\
`{ACCESS_TOKEN}`: O valor do token portador específico fornecido após a autenticação.\
`{API_KEY}`: Seu valor específico da chave de API encontrado na integração exclusiva do Adobe Experience Platform.\
`{JSON_PAYLOAD}`: Objeto de Execução de Experimento a ser enviado. O exemplo usado em nosso tutorial é mostrado aqui:

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

A resposta a seguir é após criar o Experimento agendado.

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

Agora, com o modelo treinado, podemos criar uma Execução de experiência para pontuação. O valor da variável `modelId` é o parâmetro `id` parâmetro retornado na solicitação do GET Model acima.

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

`{IMS_ORG}`: Suas credenciais da organização IMS encontradas na integração exclusiva do Adobe Experience Platform.\
`{ACCESS_TOKEN}`: O valor do token portador específico fornecido após a autenticação.\
`{API_KEY}`: Seu valor específico da chave de API encontrado na integração exclusiva do Adobe Experience Platform.\
`{EXPERIMENT_ID}`: A ID correspondente ao Experimento que você deseja direcionar. Isso pode ser encontrado na resposta ao criar seu Experimento.\
`{JSON_PAYLOAD}`: Dados a publicar. O exemplo usado em nosso tutorial está aqui:

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

`{EXPERIMENT_ID}`: A ID correspondente ao Experimento em que a execução está.\
`{EXPERIMENT_RUN_ID}`: A ID correspondente à Execução do experimento que você acabou de criar.


### Recuperar um status de Execução de experiência para Execução de experiência agendada

Para obter Execuções de Experimento para Experimentos programados, a consulta é mostrada abaixo:

**Solicitação**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`: A ID correspondente ao Experimento em que a execução está.\
`{ACCESS_TOKEN}`: O valor do token portador específico fornecido após a autenticação.\
`{IMS_ORG}`: Suas credenciais da organização IMS encontradas na integração exclusiva do Adobe Experience Platform.

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

`{EXPERIMENT_RUN_ID}`: A ID correspondente à Execução do experimento.\
`{EXPERIMENT_ID}`: A ID correspondente ao Experimento em que a execução está.

### Parar e excluir um experimento programado

Se você deseja interromper a execução de um Experimento programado antes de seu `endTime`, isso pode ser feito consultando uma solicitação DELETE para a variável `{EXPERIMENT_ID}`

**Solicitação**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`: A ID correspondente ao Experimento.\
`{ACCESS_TOKEN}`: O valor do token portador específico fornecido após a autenticação.\
`{IMS_ORG}`: Suas credenciais da organização IMS encontradas na integração exclusiva do Adobe Experience Platform.

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
