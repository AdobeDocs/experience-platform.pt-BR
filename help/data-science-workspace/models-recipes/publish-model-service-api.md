---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Publicar um modelo como um serviço (API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1478'
ht-degree: 1%

---


# Publicar um modelo como um serviço (API)

Este tutorial aborda o processo de publicação de um modelo como um serviço usando o [!DNL Sensei Machine Learning API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml).

## Introdução

Este tutorial requer uma compreensão do Adobe Experience Platform Data Science Workspace. Antes de iniciar este tutorial, reveja a visão geral [da](../home.md) Data Science Workspace para obter uma introdução de alto nível ao serviço.

Para acompanhar este tutorial, você deve ter um Mecanismo ML, uma Instância ML e um Experimento existentes. Para obter etapas sobre como criá-las na API, consulte o tutorial sobre como [importar uma receita](./import-packaged-recipe-api.md)empacotada.

Por fim, antes de iniciar este tutorial, reveja a seção [Introdução](../api/getting-started.md) [!DNL Sensei Machine Learning] do guia do desenvolvedor para obter informações importantes que você precisa saber para fazer chamadas para a API com êxito, incluindo os cabeçalhos necessários usados neste tutorial:

- `{ACCESS_TOKEN}`
- `{IMS_ORG}`
- `{API_KEY}`

Todas as solicitações de POST, PUT e PATCH exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

### Termos principais

A tabela a seguir descreve alguns termos comuns usados neste tutorial:

| Termo | Definição |
--- | ---
| **Instância de aprendizado de máquina (Instância ML)** | Uma instância de um [!DNL Sensei] Mecanismo para um locatário específico, contendo dados, parâmetros e [!DNL Sensei] código específicos. |
| **Experimento** | Uma entidade de guarda-chuva para executar execuções de experimento de treinamento, marcar execuções de experimento ou ambos. |
| **Experiência agendada** | Um termo para descrever a automação do treinamento ou a pontuação de Execuções de Experimento, regido por um agendamento definido pelo usuário. |
| **Execução do experimento** | Uma instância específica de treinamento ou experiência de pontuação. Execuções de vários experimentos de um determinado experimento podem diferir nos valores do conjunto de dados usados para treinamento ou pontuação. |
| **Modelo treinado** | Um modelo de aprendizado de máquina criado pelo processo de experimentação e engenharia de recursos antes de chegar a um modelo validado, avaliado e finalizado. |
| **Modelo publicado** | Um modelo finalizado e com versão chegou após treinamento, validação e avaliação. |
| **Serviço de aprendizado de máquina (Serviço ML)** | Uma Instância ML implantada como um Serviço para suportar solicitações sob demanda para treinamento e pontuação usando um terminal de API. Um Serviço ML também pode ser criado usando Execuções de Experimento treinadas existentes. |

## Criar um Serviço ML com uma Execução de Experiência de treinamento existente e pontuação programada

Ao publicar uma Execução de Experiência de treinamento como um Serviço ML, você pode agendar a pontuação fornecendo detalhes para a pontuação Experimento Executar a carga de uma solicitação de POST. Isso resulta na criação de uma entidade de Experimento programada para pontuação.

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
| `mlInstanceId` | Identificação de instância ML existente, a execução de teste de treinamento usada para criar o serviço ML deve corresponder a essa instância ML específica. |
| `trainingExperimentId` | Identificação do experimento correspondente à identificação da instância ML. |
| `trainingExperimentRunId` | Uma Execução de Experimento de treinamento específica a ser usada para publicar o Serviço ML. |
| `scoringDataSetId` | Identificação referente ao conjunto de dados específico a ser usado para execuções de experimento de pontuação programada. |
| `scoringTimeframe` | Um valor inteiro que representa minutos para filtrar dados a serem usados para pontuar execuções de experimento. Por exemplo, um valor de `10080` significa que os dados dos últimos 10080 minutos ou 168 horas serão usados para cada execução de teste de pontuação programada. Observe que um valor de não `0` filtrará dados, todos os dados no conjunto de dados são usados para pontuação. |
| `scoringSchedule` | Contém detalhes sobre a pontuação programada de Execuções de Experimento. |
| `scoringSchedule.startTime` | Data e hora que indica quando a pontuação do start deve ser exibida. |
| `scoringSchedule.endTime` | Data e hora que indica quando a pontuação do start deve ser exibida. |
| `scoringSchedule.cron` | Valor Cron que indica o intervalo pelo qual classificar Execuções de Experimento. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do Serviço ML recém-criado, incluindo seu exclusivo `id` e o `scoringExperimentId` correspondente Experimento de pontuação.


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

Dependendo do caso de uso e dos requisitos específicos, a criação de um Serviço ML com uma Instância ML é flexível em termos de programação de treinamentos e pontuação de Execuções de Experimento. Este tutorial abordará os casos específicos em que:

- [Você não precisa de treinamento agendado, mas requer pontuação agendada.](#ml-service-with-scheduled-experiment-for-scoring)
- [Você precisa de Execuções de Experimento programadas para treinamento e pontuação.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

Observe que um Serviço ML pode ser criado usando uma Instância ML sem agendar nenhum treinamento ou experiência de pontuação. Tais Serviços ML criarão entidades comuns de Experimento e uma única Execução de Experimento para treinamento e pontuação.

### Serviço ML com Experimento programado para pontuação {#ml-service-with-scheduled-experiment-for-scoring}

Você pode criar um Serviço ML publicando uma Instância ML com Execuções de Experimento programadas para pontuação, o que criará uma entidade de Experimento comum para treinamento. Uma Execução de Experimento de treinamento é gerada e será usada para todas as Execuções de Experimento de pontuação programadas. Certifique-se de que você tenha os valores `mlInstanceId`, `trainingDataSetId`e `scoringDataSetId` necessários para a criação do Serviço ML, e que eles existem e são valores válidos.

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

| Tecla JSON | Descrição |
| --- | --- |
| `mlInstanceId` | Identificação da instância ML existente, que representa a instância ML usada para criar o serviço ML. |
| `trainingDataSetId` | Identificação referente ao conjunto de dados específico a utilizar para a experiência de formação. |
| `trainingTimeframe` | Um valor inteiro que representa minutos para filtrar dados a serem usados para o Experimento de treinamento. Por exemplo, um valor de `"10080"` significa que os dados dos últimos 10080 minutos ou 168 horas serão usados para a Execução do Experimento de treinamento. Observe que um valor de não `"0"` filtrará dados, todos os dados no conjunto de dados são usados para treinamento. |
| `scoringDataSetId` | Identificação referente ao conjunto de dados específico a ser usado para execuções de experimento de pontuação programada. |
| `scoringTimeframe` | Um valor inteiro que representa minutos para filtrar dados a serem usados para pontuar execuções de experimento. Por exemplo, um valor de `"10080"` significa que os dados dos últimos 10080 minutos ou 168 horas serão usados para cada execução de teste de pontuação programada. Observe que um valor de não `"0"` filtrará dados, todos os dados no conjunto de dados são usados para pontuação. |
| `scoringSchedule` | Contém detalhes sobre a pontuação programada de Execuções de Experimento. |
| `scoringSchedule.startTime` | Data e hora que indica quando a pontuação do start deve ser exibida. |
| `scoringSchedule.endTime` | Data e hora que indica quando a pontuação do start deve ser exibida. |
| `scoringSchedule.cron` | Valor Cron que indica o intervalo pelo qual classificar Execuções de Experimento. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do Serviço ML recém-criado. Isso inclui os Experimentos únicos do serviço `id`, bem como o treinamento `trainingExperimentId` e `scoringExperimentId` os Experimentos de pontuação correspondentes, respectivamente.

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

Para publicar uma instância ML existente como um serviço ML com treinamento programado e classificações de execuções de experimento, você deve fornecer agendamentos de treinamento e pontuação. Quando um Serviço ML dessa configuração é criado, entidades de Experimento programadas para treinamento e pontuação também são criadas. Observe que os agendamentos de treinamento e pontuação não precisam ser os mesmos. Durante uma execução de trabalho de pontuação, o modelo treinado mais recente produzido pelas Execuções de Experiência de treinamento programado será buscado e usado para a execução de pontuação programada.

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

| Tecla JSON | Descrição |
| --- | --- |
| `mlInstanceId` | Identificação da instância ML existente, que representa a instância ML usada para criar o serviço ML. |
| `trainingDataSetId` | Identificação referente ao conjunto de dados específico a utilizar para a experiência de formação. |
| `trainingTimeframe` | Um valor inteiro que representa minutos para filtrar dados a serem usados para o Experimento de treinamento. Por exemplo, um valor de `"10080"` significa que os dados dos últimos 10080 minutos ou 168 horas serão usados para a Execução do Experimento de treinamento. Observe que um valor de não `"0"` filtrará dados, todos os dados no conjunto de dados são usados para treinamento. |
| `scoringDataSetId` | Identificação referente ao conjunto de dados específico a ser usado para execuções de experimento de pontuação programada. |
| `scoringTimeframe` | Um valor inteiro que representa minutos para filtrar dados a serem usados para pontuar execuções de experimento. Por exemplo, um valor de `"10080"` significa que os dados dos últimos 10080 minutos ou 168 horas serão usados para cada execução de teste de pontuação programada. Observe que um valor de não `"0"` filtrará dados, todos os dados no conjunto de dados são usados para pontuação. |
| `trainingSchedule` | Contém detalhes sobre execuções de experimento de treinamento agendado. |
| `scoringSchedule` | Contém detalhes sobre a pontuação programada de Execuções de Experimento. |
| `scoringSchedule.startTime` | Data e hora que indica quando a pontuação do start deve ser exibida. |
| `scoringSchedule.endTime` | Data e hora que indica quando a pontuação do start deve ser exibida. |
| `scoringSchedule.cron` | Valor Cron que indica o intervalo pelo qual classificar Execuções de Experimento. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do Serviço ML recém-criado. Isso inclui os Experimentos únicos do serviço `id`, bem como o treinamento `trainingExperimentId` e `scoringExperimentId` os Experimentos de pontuação correspondentes, respectivamente. Na resposta de exemplo abaixo, a presença de `trainingSchedule` e `scoringSchedule` sugere que as entidades de Experimento para treinamento e pontuação são Experimentos programados.

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

## Procurar um serviço ML {#retrieving-ml-services}

Você pode procurar um Serviço ML existente, fazendo uma `GET` solicitação para `/mlServices` e fornecendo o serviço ML exclusivo `id` no caminho.

**Formato da API**

```http
GET /mlServices/{SERVICE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SERVICE_ID}` | O exclusivo `id` do serviço ML que você está procurando. |

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
>A recuperação de Serviços ML diferentes pode retornar uma resposta com mais ou menos pares de valores chave. A resposta acima é uma representação de um Serviço [ML com treinamento agendado e classificação de Execuções](#ml-service-with-scheduled-experiments-for-training-and-scoring)de Experimento.


## Agendar treinamento ou pontuação

Se desejar programar a pontuação e o treinamento em um Serviço ML que já foi publicado, você poderá fazer isso atualizando o Serviço ML existente com uma `PUT` solicitação em `/mlServices`.

**Formato da API**

```http
PUT /mlServices/{SERVICE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SERVICE_ID}` | O exclusivo `id` do serviço ML que você está atualizando. |

**Solicitação**

A solicitação a seguir agende o treinamento e a pontuação de um Serviço ML existente, adicionando as teclas `trainingSchedule` e `scoringSchedule` com suas respectivas `startTime`, `endTime`e `cron` chaves.

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
>Não tente modificar o `startTime` em treinamentos agendados existentes e trabalhos de pontuação. Se for `startTime` necessário modificar, considere publicar o mesmo Modelo e reprogramar o treinamento e a pontuação de trabalhos.

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
