---
keywords: Experience Platform;publicar um modelo;Data Science Workspace;tópicos populares;api de aprendizado de máquina do sensei
solution: Experience Platform
title: Publish um modelo como um serviço usando a API de aprendizado de máquina do Sensei
type: Tutorial
description: Este tutorial aborda o processo de publicação de um modelo como um serviço usando a API de aprendizado de máquina do Sensei.
exl-id: f78b1220-0595-492d-9f8b-c3a312f17253
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1541'
ht-degree: 2%

---

# Publish um modelo como um serviço usando o [!DNL Sensei Machine Learning API]

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

Este tutorial aborda o processo de publicação de um modelo como um serviço usando o [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml).

## Introdução

Este tutorial requer uma compreensão funcional do Adobe Experience Platform Data Science Workspace. Antes de começar este tutorial, revise a [visão geral do Data Science Workspace](../home.md) para obter uma introdução geral ao serviço.

Para seguir este tutorial, você deve ter um Mecanismo ML, uma Instância ML e um Experimento existentes. Para obter etapas sobre como criá-los na API, consulte o tutorial sobre [importação de uma fórmula em pacote](./import-packaged-recipe-api.md).

Finalmente, antes de iniciar este tutorial, revise a seção [introdução](../api/getting-started.md) do guia do desenvolvedor para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API [!DNL Sensei Machine Learning], incluindo os cabeçalhos necessários usados neste tutorial:

- `{ACCESS_TOKEN}`
- `{ORG_ID}`
- `{API_KEY}`

Todas as solicitações de POST, PUT e PATCH exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

### Termos principais

A tabela a seguir descreve algumas terminologias comuns usadas neste tutorial:

| Termo | Definição |
| --- | --- |
| **Instância do Machine Learning (ML Instance)** | Uma instância de um Mecanismo [!DNL Sensei] para um locatário específico, contendo dados, parâmetros e código [!DNL Sensei] específicos. |
| **Experimento** | Uma entidade abrangente para manter execuções de experimento de treinamento, pontuar execuções de experimento ou ambos. |
| **Experimento agendado** | Um termo para descrever a automação de treinamentos ou execuções de experimento de pontuação, regido por um agendamento definido pelo usuário. |
| **Execução de experimento** | Uma instância específica de experimentos de treinamento ou pontuação. Várias execuções de experimento de um experimento específico podem diferir nos valores do conjunto de dados usados para treinamento ou pontuação. |
| **Modelo Treinado** | Um modelo de aprendizado de máquina criado pelo processo de experimentação e engenharia de recursos antes de chegar a um modelo validado, avaliado e finalizado. |
| **Modelo publicado** | Um modelo finalizado e com controle de versão foi obtido após o treinamento, a validação e a avaliação. |
| **Serviço de Aprendizado de Máquina (ML Service)** | Uma instância de ML implantada como um serviço para oferecer suporte a solicitações sob demanda para treinamento e pontuação usando um endpoint de API. Um serviço de ML também pode ser criado usando execuções de experimento treinadas. |

## Criar um serviço de ML com uma execução de experimento de treinamento existente e pontuação programada

Ao publicar uma Execução de experimento de treinamento como um Serviço ML, você pode agendar a pontuação fornecendo detalhes para a Execução de experimento de pontuação da carga de uma solicitação POST. Isso resulta na criação de uma entidade de Experimento agendada para pontuação.

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
  -H 'x-gw-ims-org-id: {ORG_ID}'
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
| --- | --- |
| `mlInstanceId` | Identificação da instância de ML existente, a execução de experimento de treinamento usada para criar o serviço de ML deve corresponder a essa instância de ML específica. |
| `trainingExperimentId` | Identificação do experimento correspondente à identificação da Instância de ML. |
| `trainingExperimentRunId` | Uma Execução de experimento de treinamento específica a ser usada para publicar o Serviço de ML. |
| `scoringDataSetId` | Identificação que se refere ao conjunto de dados específico a ser usado para execuções de experimento de pontuação programada. |
| `scoringTimeframe` | Um valor inteiro que representa minutos para filtrar dados a serem usados para pontuar Execuções de experimento. Por exemplo, um valor de `10080` significa que dados dos últimos 10.080 minutos ou 168 horas serão usados para cada Execução de experimento de pontuação agendada. Observe que um valor de `0` não filtrará dados, todos os dados no conjunto de dados são usados para pontuação. |
| `scoringSchedule` | Contém detalhes sobre execuções de experimento de pontuação programada. |
| `scoringSchedule.startTime` | Data e hora que indicam quando iniciar a pontuação. |
| `scoringSchedule.endTime` | Data e hora que indicam quando iniciar a pontuação. |
| `scoringSchedule.cron` | Valor de cron que indica o intervalo pelo qual pontuar as execuções de experimento. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do Serviço ML recém-criado, incluindo seu `id` exclusivo e o `scoringExperimentId` para seu Experimento de pontuação correspondente.


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

## Criando um Serviço de ML a partir de uma Instância de ML existente

Dependendo do caso de uso e dos requisitos específicos, a criação de um Serviço de ML com uma Instância de ML é flexível em termos de agendamento de treinamento e pontuação de Execuções de experimento. Este tutorial abordará os casos específicos em que:

- [Você não precisa de treinamento programado, mas precisa de pontuação programada.](#ml-service-with-scheduled-experiment-for-scoring)
- [Você precisa de Execuções de experimento programadas para treinamento e pontuação.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

Observe que um Serviço de ML pode ser criado usando uma Instância de ML sem programar nenhum treinamento ou experimento de pontuação. Esses Serviços de ML criarão entidades de Experimento comuns e uma única Execução de experimento para treinamento e pontuação.

### Serviço de ML com experimento agendado para pontuação {#ml-service-with-scheduled-experiment-for-scoring}

Você pode criar um Serviço de ML publicando uma Instância de ML com Execuções de experimento programadas para pontuação, o que criará uma entidade de experimento comum para treinamento. Uma Execução de experimento de treinamento é gerada e será usada para todas as Execuções de experimento de pontuação programadas. Verifique se você tem os `mlInstanceId`, `trainingDataSetId` e `scoringDataSetId` necessários para a criação do Serviço ML, e se eles existem e são valores válidos.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' 
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
| `mlInstanceId` | Identificação da Instância ML existente, representando a Instância ML usada para criar o Serviço ML. |
| `trainingDataSetId` | Identificação referente ao conjunto de dados específico a ser usado para o experimento de treinamento. |
| `trainingTimeframe` | Um valor inteiro que representa minutos para filtrar dados a serem usados para treinamento do Experimento. Por exemplo, um valor de `"10080"` significa que dados dos últimos 10.080 minutos ou 168 horas serão usados para a Execução de experimento de treinamento. Observe que um valor de `"0"` não filtrará os dados, todos os dados no conjunto de dados são usados para treinamento. |
| `scoringDataSetId` | Identificação que se refere ao conjunto de dados específico a ser usado para execuções de experimento de pontuação programada. |
| `scoringTimeframe` | Um valor inteiro que representa minutos para filtrar dados a serem usados para pontuar Execuções de experimento. Por exemplo, um valor de `"10080"` significa que dados dos últimos 10.080 minutos ou 168 horas serão usados para cada Execução de experimento de pontuação agendada. Observe que um valor de `"0"` não filtrará dados, todos os dados no conjunto de dados são usados para pontuação. |
| `scoringSchedule` | Contém detalhes sobre execuções de experimento de pontuação programada. |
| `scoringSchedule.startTime` | Data e hora que indicam quando iniciar a pontuação. |
| `scoringSchedule.endTime` | Data e hora que indicam quando iniciar a pontuação. |
| `scoringSchedule.cron` | Valor de cron que indica o intervalo pelo qual pontuar as execuções de experimento. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do Serviço ML recém-criado. Isso inclui o `id` exclusivo do serviço, bem como o `trainingExperimentId` e o `scoringExperimentId` para seus Experimentos de treinamento e pontuação correspondentes, respectivamente.

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

### Serviço de ML com experimentos programados para treinamento e pontuação {#ml-service-with-scheduled-experiments-for-training-and-scoring}

Para publicar uma Instância de ML existente como um Serviço de ML com treinamentos programados e execuções de experimento de pontuação, é necessário fornecer programações de treinamento e pontuação. Quando um Serviço de ML dessa configuração é criado, entidades de Experimento programadas para treinamento e pontuação também são criadas. Observe que as programações de treinamento e pontuação não precisam ser iguais. Durante a execução de um trabalho de pontuação, o modelo treinado mais recente produzido pelas Execuções de experimento de treinamento programado será buscado e usado para a execução de pontuação programada.

**Formato da API**

```http
POST /mlServices
```

**Solicitação**

```SHELL
curl -X POST 'https://platform.adobe.io/data/sensei/mlServices' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
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
| `mlInstanceId` | Identificação da Instância ML existente, representando a Instância ML usada para criar o Serviço ML. |
| `trainingDataSetId` | Identificação referente ao conjunto de dados específico a ser usado para o experimento de treinamento. |
| `trainingTimeframe` | Um valor inteiro que representa minutos para filtrar dados a serem usados para treinamento do Experimento. Por exemplo, um valor de `"10080"` significa que dados dos últimos 10.080 minutos ou 168 horas serão usados para a Execução de experimento de treinamento. Observe que um valor de `"0"` não filtrará os dados, todos os dados no conjunto de dados são usados para treinamento. |
| `scoringDataSetId` | Identificação que se refere ao conjunto de dados específico a ser usado para execuções de experimento de pontuação programada. |
| `scoringTimeframe` | Um valor inteiro que representa minutos para filtrar dados a serem usados para pontuar Execuções de experimento. Por exemplo, um valor de `"10080"` significa que dados dos últimos 10.080 minutos ou 168 horas serão usados para cada Execução de experimento de pontuação agendada. Observe que um valor de `"0"` não filtrará dados, todos os dados no conjunto de dados são usados para pontuação. |
| `trainingSchedule` | Contém detalhes sobre execuções de experimento de treinamento programadas. |
| `scoringSchedule` | Contém detalhes sobre execuções de experimento de pontuação programada. |
| `scoringSchedule.startTime` | Data e hora que indicam quando iniciar a pontuação. |
| `scoringSchedule.endTime` | Data e hora que indicam quando iniciar a pontuação. |
| `scoringSchedule.cron` | Valor de cron que indica o intervalo pelo qual pontuar as execuções de experimento. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do Serviço ML recém-criado. Isso inclui o `id` exclusivo do serviço, bem como o `trainingExperimentId` e `scoringExperimentId` de seus Experimentos de treinamento e pontuação correspondentes, respectivamente. Na resposta de exemplo abaixo, a presença de `trainingSchedule` e `scoringSchedule` sugere que as entidades de Experimento para treinamento e pontuação são Experimentos agendados.

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

## Pesquisar um serviço de ML {#retrieving-ml-services}

Você pode pesquisar um Serviço ML existente fazendo uma solicitação `GET` para `/mlServices` e fornecendo o `id` exclusivo do Serviço ML no caminho.

**Formato da API**

```http
GET /mlServices/{SERVICE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SERVICE_ID}` | O `id` exclusivo do Serviço ML que você está pesquisando. |

**Solicitação**

```SHELL
curl -X GET 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
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
>A recuperação de diferentes serviços de ML pode retornar uma resposta com mais ou menos pares de valores-chave. A resposta acima é uma representação de um [Serviço ML com treinamento agendado e pontuações de Execuções de Experimento](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## Agendar treinamento ou pontuação

Se você quiser agendar a pontuação e o treinamento em um Serviço ML que já foi publicado, atualize o Serviço ML existente com uma solicitação `PUT` em `/mlServices`.

**Formato da API**

```http
PUT /mlServices/{SERVICE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SERVICE_ID}` | O `id` exclusivo do Serviço ML que você está atualizando. |

**Solicitação**

A solicitação a seguir agenda o treinamento e a pontuação para um Serviço ML existente adicionando as chaves `trainingSchedule` e `scoringSchedule` com suas respectivas chaves `startTime`, `endTime` e `cron`.

```SHELL
curl -X PUT 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
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
>Não tente modificar o `startTime` em treinamentos e trabalhos de pontuação programados existentes. Se o `startTime` deve ser modificado, considere publicar o mesmo Modelo e reagendar trabalhos de treinamento e pontuação.

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
