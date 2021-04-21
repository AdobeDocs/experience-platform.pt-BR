---
keywords: Experience Platform; publicar um modelo; Data Science Workspace; tópicos populares; api de aprendizado de máquina do sensei
solution: Experience Platform
title: Publicar um modelo como um serviço usando a API de aprendizado de máquina do Sensei
topic-legacy: tutorial
type: Tutorial
description: Este tutorial aborda o processo de publicação de um modelo como um serviço usando a API de aprendizado de máquina do Sensei.
exl-id: f78b1220-0595-492d-9f8b-c3a312f17253
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 1%

---

# Publicar um modelo como um serviço usando o [!DNL Sensei Machine Learning API]

Este tutorial aborda o processo de publicação de um modelo como um serviço usando o [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml).

## Introdução

Este tutorial requer uma compreensão funcional do Adobe Experience Platform Data Science Workspace. Antes de iniciar este tutorial, revise a [Visão geral do Data Science Workspace](../home.md) para obter uma introdução de alto nível ao serviço.

Para acompanhar este tutorial, você deve ter um Mecanismo ML, Instância ML e Experimento existentes. Para obter etapas sobre como criá-las na API, consulte o tutorial em [importar uma receita empacotada](./import-packaged-recipe-api.md).

Finalmente, antes de iniciar este tutorial, reveja a seção [introdução](../api/getting-started.md) do guia do desenvolvedor para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API [!DNL Sensei Machine Learning], incluindo os cabeçalhos necessários usados neste tutorial:

- `{ACCESS_TOKEN}`
- `{IMS_ORG}`
- `{API_KEY}`

Todas as solicitações de POST, PUT e PATCH exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

### Termos principais

A tabela a seguir descreve alguns termos comuns usados neste tutorial:

| Termo | Definição |
--- | ---
| **Instância de Aprendizagem de Máquina (Instância ML)** | Uma instância de um mecanismo [!DNL Sensei] para um locatário específico, contendo dados, parâmetros e código [!DNL Sensei] específicos. |
| **Experimento** | Uma entidade-guarda-chuva para realizar treinamentos Execuções de Experimento, pontuação de Execuções de Experimento, ou ambos. |
| **Experimento agendado** | Um termo para descrever a automação de treinamentos ou pontuação de Execuções de Experimento, regido por um agendamento definido pelo usuário. |
| **Execução do experimento** | Um exemplo específico de treinamento ou experiência de pontuação. Execuções de vários experimentos de um determinado experimento podem diferir nos valores do conjunto de dados usados para treinamento ou pontuação. |
| **Modelo treinado** | Um modelo de aprendizado de máquina criado pelo processo de experimentação e engenharia de recursos antes de chegar a um modelo validado, avaliado e finalizado. |
| **Modelo publicado** | Um modelo finalizado e com versão chegou após treinamento, validação e avaliação. |
| **Serviço de Aprendizagem de Máquina (ML Service)** | Uma Instância ML implantada como um Serviço para oferecer suporte a solicitações sob demanda para treinamento e pontuação usando um endpoint da API. Um Serviço ML também pode ser criado usando Execuções de Experimento treinadas existentes. |

## Criar um Serviço ML com uma Execução de Experiência de Treinamento existente e pontuação agendada

Ao publicar um Experimento de treinamento como um Serviço ML, você pode agendar a pontuação fornecendo detalhes para a pontuação Experimento Execute a carga de uma solicitação de POST. Isso resulta na criação de uma entidade de Experimento agendada para pontuação.

**Formato da API**

```http
POST /mlServices
```

**Solicitação**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'Content-Type: application/json'
  -d '{
        "name": "Service name",
        "description": "Service description",
        "trainingExperimentId": "c4155146-b38f-4a8b-86d8-1de3838c8d87",
        "trainingExperimentRunId": "5c5af39c73fcec153117eed1",
        "scoringDataSetId": "5c5af39c73fcec153117eed1",
        "scoringTimeframe": "20000",
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| Propriedade | Descrição |
--- | ---
| `mlInstanceId` | Identificação de Instância ML existente, a Execução de Experiência de Treinamento usada para criar o Serviço ML deve corresponder a esta Instância ML específica. |
| `trainingExperimentId` | Identificação de experimento correspondente à identificação da Instância ML. |
| `trainingExperimentRunId` | Um Experimento de Treinamento específico a ser usado para publicar o Serviço ML. |
| `scoringDataSetId` | Identificação que se refere ao conjunto de dados específico a ser usado para execuções de experimento de pontuação programadas. |
| `scoringTimeframe` | Um valor Integer representando minutos para filtrar dados a serem usados para pontuar Execuções de Experimento. Por exemplo, um valor `10080` significa que os dados dos últimos 10080 minutos ou 168 horas serão usados para cada execução de experimento de pontuação agendada. Observe que um valor `0` não filtrará dados, todos os dados no conjunto de dados são usados para pontuação. |
| `scoringSchedule` | Contém detalhes sobre a pontuação programada de Execuções de Experimento. |
| `scoringSchedule.startTime` | Data e hora que indica quando iniciar a pontuação. |
| `scoringSchedule.endTime` | Data e hora que indica quando iniciar a pontuação. |
| `scoringSchedule.cron` | Valor Cron indicando o intervalo no qual as Execuções de Experimento devem ser pontuadas. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do Serviço ML recém-criado, incluindo seu `id` exclusivo e `scoringExperimentId` para seu Experimento de pontuação correspondente.


```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingExperimentRunId": "string",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-03-13T00:00",
    "endTime": "2019-03-14T00:00",
    "cron": "30 * * * *"
  },
  "created": "2019-04-08T14:45:25.981Z",
  "updated": "2019-04-08T14:45:25.981Z"
}
```

## Criando um Serviço ML a partir de uma Instância ML existente

Dependendo do caso de uso e dos requisitos específicos, a criação de um Serviço ML com uma Instância ML é flexível em termos de agendamento de treinamento e pontuação de Execuções de Experimento. Este tutorial abordará os casos específicos em que:

- [Você não precisa de treinamento programado, mas requer pontuação programada.](#ml-service-with-scheduled-experiment-for-scoring)
- [Você precisa de Execuções de Experimento programadas para treinamento e pontuação.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

Observe que um Serviço ML pode ser criado usando uma Instância ML sem agendar nenhum treinamento ou experiência de pontuação. Esses Serviços ML criarão entidades de Experimento comuns e uma única Execução de Experimento para treinamento e pontuação.

### Serviço ML com Experimento agendado para pontuação {#ml-service-with-scheduled-experiment-for-scoring}

Você pode criar um Serviço ML publicando uma Instância ML com Execuções de Experimento Agendadas para pontuação, o que criará uma entidade de Experimento comum para treinamento. Uma Execução de Experimento de Treinamento é gerada e será usada para todas as Execuções de Experimento de Pontuação programadas. Certifique-se de que você tenha os `mlInstanceId`, `trainingDataSetId` e `scoringDataSetId` necessários para a criação do Serviço ML, e que eles existam e sejam valores válidos.

**Formato da API**

```http
POST /mlServices
```

**Solicitação**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "Service name",
        "description": "Service description",
        "mlInstanceId": "c4155146-b38f-4a8b-86d8-1de3838c8d87",
        "trainingDataSetId": "5c5af39c73fcec153117eed1",
        "trainingTimeframe": "10000",
        "scoringDataSetId": "5c5af39c73fcec153117eed1",
        "scoringTimeframe": "20000",
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| Chave JSON | Descrição |
| --- | --- |
| `mlInstanceId` | Identificação de Instância ML Existente, representando a Instância ML usada para criar o Serviço ML. |
| `trainingDataSetId` | Identificação relativa ao conjunto de dados específico a utilizar para o Experimento de Formação. |
| `trainingTimeframe` | Um valor Integer que representa minutos para filtrar dados a serem usados para treinamento de Experimento. Por exemplo, um valor `"10080"` significa que os dados dos últimos 10080 minutos ou 168 horas serão usados para a Execução do Experimento de treinamento. Observe que um valor `"0"` não filtrará dados, todos os dados no conjunto de dados são usados para treinamento. |
| `scoringDataSetId` | Identificação que se refere ao conjunto de dados específico a ser usado para execuções de experimento de pontuação programadas. |
| `scoringTimeframe` | Um valor Integer representando minutos para filtrar dados a serem usados para pontuar Execuções de Experimento. Por exemplo, um valor `"10080"` significa que os dados dos últimos 10080 minutos ou 168 horas serão usados para cada execução de experimento de pontuação agendada. Observe que um valor `"0"` não filtrará dados, todos os dados no conjunto de dados são usados para pontuação. |
| `scoringSchedule` | Contém detalhes sobre a pontuação programada de Execuções de Experimento. |
| `scoringSchedule.startTime` | Data e hora que indica quando iniciar a pontuação. |
| `scoringSchedule.endTime` | Data e hora que indica quando iniciar a pontuação. |
| `scoringSchedule.cron` | Valor Cron indicando o intervalo no qual as Execuções de Experimento devem ser pontuadas. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do Serviço ML recém-criado. Isso inclui o `id` exclusivo do serviço, bem como `trainingExperimentId` e `scoringExperimentId` para seus Experimentos de treinamento e pontuação correspondentes, respectivamente.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T08:58:10.956Z"
}
```

### Serviço ML com Experimentos programados para treinamento e pontuação {#ml-service-with-scheduled-experiments-for-training-and-scoring}

Para publicar uma Instância ML como um Serviço ML com treinamento agendado e pontuação de Execuções de Experimento, você deve fornecer agendamentos de treinamento e pontuação. Quando um Serviço ML dessa configuração é criado, entidades de Experimento agendadas para treinamento e pontuação também são criadas. Observe que os horários de treinamento e pontuação não precisam ser os mesmos. Durante uma execução de trabalho de pontuação, o modelo treinado mais recente produzido por Execuções de Experimento de Treinamento programadas será buscado e usado para a execução de pontuação programada.

**Formato da API**

```http
POST /mlServices
```

**Solicitação**

```SHELL
curl -X POST 'https://platform-int.adobe.io/data/sensei/mlServices' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "string",
        "description": "string",
        "mlInstanceId": "string",
        "trainingDataSetId": "string",
        "trainingTimeframe": "string",
        "scoringDataSetId": "string",
        "scoringTimeframe": "string",
        "trainingSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        },
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| Chave JSON | Descrição |
| --- | --- |
| `mlInstanceId` | Identificação de Instância ML Existente, representando a Instância ML usada para criar o Serviço ML. |
| `trainingDataSetId` | Identificação relativa ao conjunto de dados específico a utilizar para o Experimento de Formação. |
| `trainingTimeframe` | Um valor Integer que representa minutos para filtrar dados a serem usados para treinamento de Experimento. Por exemplo, um valor `"10080"` significa que os dados dos últimos 10080 minutos ou 168 horas serão usados para a Execução do Experimento de treinamento. Observe que um valor `"0"` não filtrará dados, todos os dados no conjunto de dados são usados para treinamento. |
| `scoringDataSetId` | Identificação que se refere ao conjunto de dados específico a ser usado para execuções de experimento de pontuação programadas. |
| `scoringTimeframe` | Um valor Integer representando minutos para filtrar dados a serem usados para pontuar Execuções de Experimento. Por exemplo, um valor `"10080"` significa que os dados dos últimos 10080 minutos ou 168 horas serão usados para cada execução de experimento de pontuação agendada. Observe que um valor `"0"` não filtrará dados, todos os dados no conjunto de dados são usados para pontuação. |
| `trainingSchedule` | Contém detalhes sobre execuções de experiência de treinamento programadas. |
| `scoringSchedule` | Contém detalhes sobre a pontuação programada de Execuções de Experimento. |
| `scoringSchedule.startTime` | Data e hora que indica quando iniciar a pontuação. |
| `scoringSchedule.endTime` | Data e hora que indica quando iniciar a pontuação. |
| `scoringSchedule.cron` | Valor Cron indicando o intervalo no qual as Execuções de Experimento devem ser pontuadas. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do Serviço ML recém-criado. Isso inclui o `id` exclusivo do serviço, bem como os `trainingExperimentId` e `scoringExperimentId` de seus Experimentos de treinamento e pontuação correspondentes, respectivamente. No exemplo de resposta abaixo, a presença de `trainingSchedule` e `scoringSchedule` sugere que as entidades de Experimento para treinamento e pontuação são Experimentos programados.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",,
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T08:58:10.956Z"
}
```

## Procurar um Serviço ML {#retrieving-ml-services}

Você pode procurar um Serviço ML existente fazendo uma solicitação `GET` para `/mlServices` e fornecendo o `id` exclusivo do Serviço ML no caminho.

**Formato da API**

```http
GET /mlServices/{SERVICE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SERVICE_ID}` | O `id` exclusivo do Serviço ML que está a procurar. |

**Solicitação**

```SHELL
curl -X GET 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do Serviço ML.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-05-13T23:46:03.478Z",
  "updated": "2019-05-13T23:46:03.478Z"
}
```

>[!NOTE]
>
>A recuperação de diferentes serviços ML pode retornar uma resposta com mais ou menos pares de valores chave. A resposta acima é uma representação de um [ML Service com treinamento agendado e pontuação de Execuções de Experimento](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## Agendar treinamento ou pontuação

Se quiser agendar pontuação e treinamento em um Serviço ML já publicado, atualize o Serviço ML existente com uma solicitação `PUT` em `/mlServices`.

**Formato da API**

```http
PUT /mlServices/{SERVICE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SERVICE_ID}` | O `id` exclusivo do Serviço ML que está a atualizar. |

**Solicitação**

A solicitação a seguir agenda o treinamento e a pontuação de um Serviço ML existente, adicionando as chaves `trainingSchedule` e `scoringSchedule` com suas respectivas chaves `startTime`, `endTime` e `cron`.

```SHELL
curl -X PUT 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "string",
        "description": "string",
        "mlInstanceId": "string",
        "trainingExperimentId": "string",
        "trainingDataSetId": "string",
        "trainingTimeframe": "integer",
        "scoringExperimentId": "string",
        "scoringDataSetId": "string",
        "scoringTimeframe": "integer",
        "trainingSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-11T00:00",
          "cron": "20 * * * *"
        },
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-11T00:00",
          "cron": "20 * * * *"
        }
      }'
```

>[!WARNING]
>
>Não tente modificar o `startTime` em treinamentos programados e tarefas de pontuação existentes. Se `startTime` precisar ser modificado, considere publicar o mesmo Modelo e reagendar o treinamento e as tarefas de pontuação.

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do Serviço ML atualizado.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-11T00:00",
    "cron": "20 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-11T00:00",
    "cron": "20 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T09:43:55.563Z"
}
```
