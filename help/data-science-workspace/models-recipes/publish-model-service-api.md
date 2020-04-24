---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Publicar um modelo como um serviço (API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# Publicar um modelo como um serviço (API)

## Pré-requisitos

- Siga este [tutorial](../../tutorials/authentication.md) para obter autorização para chamadas de API de criação de start.
No tutorial, agora você deve ter as seguintes informações:
   - `{ACCESS_TOKEN}`: O valor do token do portador específico fornecido após a autenticação.
   - `{IMS_ORG}`: Suas credenciais organizacionais IMS encontradas na integração exclusiva da Adobe Experience Platform.
   - `{API_KEY}`: O valor da chave da API específica encontrado na integração exclusiva da Adobe Experience Platform.
- Este tutorial requer entidades existentes de Mecanismo ML, Instância ML e Experimento. Consulte este [Tutorial](./import-packaged-recipe-api.md) sobre como criar entidades de Mecanismo ML, Instância ML ou Experimento.
- Para obter informações sobre pontos de extremidade de API e solicitações mencionadas neste tutorial, consulte a API [completa de aprendizado de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)máquina do Sensei.

## Termos principais

Alguns termos comuns usados neste tutorial:

| Termo | Definição |
--- | ---
| **Instância de aprendizado de máquina (Instância ML)** | A entidade conceitual que é uma Instância de um Mecanismo Sensei para um locatário específico composta por dados específicos, parâmetros e código do Sensei. |
| **Experimento** | Uma entidade de guarda-chuva para executar execuções de experimento de treinamento, marcar execuções de experimento ou ambos. |
| **Experiência agendada** | Um termo para descrever a automação do treinamento ou a pontuação de Execuções de Experimento, regido por um agendamento definido pelo usuário. |
| **Execução do experimento** | Uma instância específica de treinamento ou experiência de pontuação. Execuções de vários experimentos de um determinado experimento podem diferir nos valores do conjunto de dados usados para treinamento ou pontuação. |
| **Modelo treinado** | Um modelo de aprendizado de máquina criado pelo processo de experimentação e engenharia de recursos antes de chegar a um modelo validado, avaliado e finalizado. |
| **Modelo publicado** | Um modelo finalizado e com versão chegou após treinamento, validação e avaliação. |
| **Serviço de aprendizado de máquina (Serviço ML)** | Uma Instância ML implantada como um Serviço para suportar solicitação sob demanda para treinamento e pontuação por meio de um terminal. Observe que um Serviço ML também pode ser criado usando execuções de experimento treinadas existentes. |


## Fluxo de trabalho da API

Este tutorial irá parar de criar, recuperar e atualizar um Serviço ML.

## Criação de um Serviço ML com uma Execução de Experiência de treinamento existente e pontuação programada

Ao publicar uma Execução de Experiência de treinamento como um Serviço ML, você pode agendar a pontuação fornecendo detalhes para a Execução de Experiência de pontuação em seu {JSON_PAYLOAD}. `scoringSchedule` Isso resulta na criação de uma entidade de Experimento programada para pontuação. Certifique-se de ter os valores `mlInstanceId`, `trainingExperimentId`, `trainingExperimentRunId`, `scoringDataSetId`e de que eles existem e são válidos.

Para start, faça uma `POST` solicitação para `/mlServices`. Um exemplo de comando de ondulação é mostrado abaixo:

**Solicitação**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -d '{JSON_PAYLOAD}'
```

- `{API_KEY}` : O valor da chave da API específica encontrado na integração exclusiva da Adobe Experience Platform.
- `{IMS_ORG}` :  A ID de empresa do IMS pode ser encontrada nos detalhes de integração no console de E/S da Adobe.
- `{ACCESS_TOKEN}` : O valor do token do portador específico fornecido após a autenticação.
- `{JSON_PAYLOAD}` : Um exemplo de formato de carga JSON pode ser visto abaixo:

```JSON
{
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingExperimentRunId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-03-13T00:00",
    "endTime": "2019-03-14T00:00",
    "cron": "30 * * * *"
  }
}
```

- `mlInstanceId` : Identificação de instância ML existente, a execução de teste de treinamento usada para criar o serviço ML deve corresponder a essa instância ML específica.
- `trainingExperimentId` : Identificação do experimento correspondente à identificação da instância ML.
- `trainingExperimentRunId` : Uma Execução de Experimento de treinamento específica a ser usada para publicar o Serviço ML.
- `scoringDataSetId` : Identificação referente ao conjunto de dados específico a ser usado para execuções de experimento de pontuação programada.
- `scoringTimeframe` : Um valor inteiro que representa minutos para filtrar dados a serem usados para pontuar execuções de experimento. Por exemplo, um valor de `"10080"` significa que os dados dos últimos 10080 minutos ou 168 horas serão usados para cada execução de teste de pontuação programada. Observe que um valor de não `"0"` filtrará dados, todos os dados no conjunto de dados são usados para pontuação.
- `scoringSchedule` : Contém detalhes sobre a pontuação programada de Execuções de Experimento.
- `startTime` : definição.
- `endTime` : definição.
- `cron` : definição.

**Resposta**

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

Na resposta JSON, a chave `scoringExperimentId` com o valor correspondente sugere que um novo Experimento de pontuação foi criado, juntamente com o cronograma de Experimento fornecido na `POST` solicitação. A `id` chave na resposta identifica exclusivamente o Serviço ML que foi criado.

## Criando um Serviço ML a partir de uma Instância ML existente

Dependendo do caso de uso e dos requisitos específicos, a criação de um Serviço ML com uma Instância ML é flexível em termos de programação de treinamentos e pontuação de Execuções de Experimento. Este tutorial abordará os casos específicos em que:

- [Você não precisa de treinamento agendado, mas requer pontuação agendada.](#ml-service-with-scheduled-experiment-for-scoring)
- [Você precisa de Execuções de Experimento programadas para treinamento e pontuação.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

Observe que um Serviço ML pode ser criado usando uma Instância ML sem agendar nenhum treinamento ou experiência de pontuação. Esse Serviço ML criará entidades comuns de Experimento e uma única Execução de Experimento para treinamento e pontuação.

### Serviço ML com Experimento programado para pontuação {#ml-service-with-scheduled-experiment-for-scoring}

A criação de um Serviço ML publicando uma Instância ML com Execuções de Experimento programadas para pontuação resultará na criação de uma entidade de Experimento comum para treinamento. A Execução do Experimento de treinamento resultante gerada será usada para todas as Execuções do Experimento de pontuação programadas. Certifique-se de que você tenha os valores `mlInstanceId`, `trainingDataSetId`e `scoringDataSetId` necessários para a criação do Serviço ML, e que eles existem e são valores válidos.

Para start, faça uma `POST` solicitação para `/mlServices`. Um exemplo de comando de ondulação é mostrado abaixo:

**Solicitação**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -d '{JSON_PAYLOAD}'
```

- `{API_KEY}` : O valor da chave da API específica encontrado na integração exclusiva da Adobe Experience Platform.
- `{IMS_ORG}` :  A ID de empresa do IMS pode ser encontrada nos detalhes de integração no console de E/S da Adobe.
- `{ACCESS_TOKEN}` : O valor do token do portador específico fornecido após a autenticação.
- `{JSON_PAYLOAD}` : Um exemplo de formato de carga JSON pode ser visto abaixo:

```JSON
{
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
}
```

| Tecla JSON | Descrição |
| --- | --- |
| **`mlInstanceId`** | Identificação da instância ML existente, que representa a instância ML usada para criar o serviço ML. |
| **`trainingDataSetId`** | Identificação referente ao conjunto de dados específico a utilizar para a experiência de formação. |
| **`trainingTimeframe`** | Um valor inteiro que representa minutos para filtrar dados a serem usados para o Experimento de treinamento. Por exemplo, um valor de `"10080"` significa que os dados dos últimos 10080 minutos ou 168 horas serão usados para a Execução do Experimento de treinamento. Observe que um valor de não `"0"` filtrará dados, todos os dados no conjunto de dados são usados para treinamento. |
| **`scoringDataSetId`** | Identificação referente ao conjunto de dados específico a ser usado para execuções de experimento de pontuação programada. |
| **`scoringTimeframe`** | Um valor inteiro que representa minutos para filtrar dados a serem usados para pontuar execuções de experimento. Por exemplo, um valor de `"10080"` significa que os dados dos últimos 10080 minutos ou 168 horas serão usados para cada execução de teste de pontuação programada. Observe que um valor de não `"0"` filtrará dados, todos os dados no conjunto de dados são usados para pontuação. |
| **`scoringSchedule`** | Contém detalhes sobre a pontuação programada de Execuções de Experimento. |

**Resposta**

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

A partir da `JSON` resposta, as teclas `trainingExperimentId` e `scoringExperimentId` sugerem que uma nova entidade de treinamento e pontuação do Experimento foi criada para este Serviço ML. A presença do `scoringSchedule` objeto se refere aos detalhes da pontuação da programação de Execução de Experimento. A `id` chave na resposta refere-se ao Serviço ML que você acabou de criar.

### Serviço ML com Experimentos programados para treinamento e pontuação {#ml-service-with-scheduled-experiments-for-training-and-scoring}

Para publicar uma instância ML existente como um serviço ML com treinamento programado e classificações de execuções de experimento, você deve fornecer agendamentos de treinamento e pontuação. Quando um Serviço ML dessa configuração é criado, entidades de Experimento programadas para treinamento e pontuação também são criadas. Observe que os agendamentos de treinamento e pontuação não precisam ser os mesmos. Durante uma execução de trabalho de pontuação, o modelo treinado mais recente produzido pelas Execuções de Experiência de treinamento programado será buscado e usado para a execução de pontuação programada.

Para criar o Serviço ML, faça uma `POST` solicitação para `/mlServices` que o `{JSON_PAYLOAD}` representante do objeto de Serviço ML seja adicionado. Verifique se os valores `mlInstanceId`, `trainingDataSetId`e `scoringDataSetId` existem e são válidos.

**Solicitação**

```SHELL
curl -X POST "https://platform-int.adobe.io/data/sensei/mlServices" 
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
  -d "{JSON_PAYLOAD}"
```

- `{API_KEY}` : O valor da chave da API específica encontrado na integração exclusiva da Adobe Experience Platform.
- `{IMS_ORG}` :  A ID de empresa do IMS pode ser encontrada nos detalhes de integração no console de E/S da Adobe.
- `{ACCESS_TOKEN}` : O valor do token do portador específico fornecido após a autenticação.
- `{JSON_PAYLOAD}` : Um exemplo de formato de carga JSON pode ser visto abaixo:

```JSON
{
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
}
```

| Tecla JSON | Descrição |
| --- | --- |
| **`mlInstanceId`** | Identificação da instância ML existente, que representa a instância ML usada para criar o serviço ML. |
| **`trainingDataSetId`** | Identificação referente ao conjunto de dados específico a utilizar para a experiência de formação. |
| **`trainingTimeframe`** | Um valor inteiro que representa minutos para filtrar dados a serem usados para o Experimento de treinamento. Por exemplo, um valor de `"10080"` significa que os dados dos últimos 10080 minutos ou 168 horas serão usados para a Execução do Experimento de treinamento. Observe que um valor de não `"0"` filtrará dados, todos os dados no conjunto de dados são usados para treinamento. |
| **`scoringDataSetId`** | Identificação referente ao conjunto de dados específico a ser usado para execuções de experimento de pontuação programada. |
| **`scoringTimeframe`** | Um valor inteiro que representa minutos para filtrar dados a serem usados para pontuar execuções de experimento. Por exemplo, um valor de `"10080"` significa que os dados dos últimos 10080 minutos ou 168 horas serão usados para cada execução de teste de pontuação programada. Observe que um valor de não `"0"` filtrará dados, todos os dados no conjunto de dados são usados para pontuação. |
| **`trainingSchedule`** | Contém detalhes sobre execuções de experimento de treinamento agendado. |
| **`scoringSchedule`** | Contém detalhes sobre a pontuação programada de Execuções de Experimento. |

**Resposta**

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

A adição de `trainingExperimentId` e `scoringExperimentId` no corpo da resposta sugere a criação de entidades de Experimento para treinamento e pontuação. A presença de `trainingSchedule` e `scoringSchedule` sugere que as entidades de Experimento mencionadas acima para treinamento e pontuação são Experimentos programados. A `id` chave na resposta refere-se ao Serviço ML que você acabou de criar.

## Recuperando Serviços ML {#retrieving-ml-services}

Recuperar um Serviço ML existente é tão simples quanto fazer uma `GET` solicitação para o `/mlServices` terminal. Certifique-se de ter a identificação do Serviço ML específico que está a tentar obter.

**Solicitação**

```SHELL
curl -X GET "https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}" 
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
```

- `{API_KEY}` : O valor da chave da API específica encontrado na integração exclusiva da Adobe Experience Platform.
- `{IMS_ORG}` :  A ID de empresa do IMS pode ser encontrada nos detalhes de integração no console de E/S da Adobe.
- `{ACCESS_TOKEN}` : O valor do token do portador específico fornecido após a autenticação.

**Resposta**

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

A resposta JSON representa o objeto de Serviço ML. Esse objeto equivale à resposta para quando o Serviço ML é criado. Observe que recuperar serviços ML diferentes pode retornar uma resposta com mais ou menos pares de valores chave. A resposta acima é uma representação de um Serviço [ML com treinamento agendado e classificação de Execuções](#ml-service-with-scheduled-experiments-for-training-and-scoring)de Experimento.


## Agendar treinamento ou pontuação

Suponha que você queira agendar a pontuação e o treinamento em um Serviço ML que já tenha sido publicado, atualize o Serviço ML existente com uma `PUT` solicitação em `/mlServices`. Certifique-se de ter a identificação do Serviço ML que deseja atualizar. Para sua referência, [recuperar o Serviço](#retrieving-ml-services) ML que deseja atualizar pode ser uma primeira etapa útil.

**Solicitação**

```SHELL
curl -X PUT "https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}" 
  -H "Authorization: {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
  -d "{JSON_PAYLOAD}"
```

- `{SERVICE_ID}` : Identificação exclusiva referente ao Serviço ML que você deseja atualizar.
- `{API_KEY}` : O valor da chave da API específica encontrado na integração exclusiva da Adobe Experience Platform.
- `{IMS_ORG}` :  A ID de empresa do IMS pode ser encontrada nos detalhes de integração no console de E/S da Adobe.
- `{ACCESS_TOKEN}` : O valor do token do portador específico fornecido após a autenticação.
- `{JSON_PAYLOAD}` : Um exemplo de formato de carga JSON pode ser visto abaixo:

```JSON
{
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
}
```

O treinamento de agendamento e a pontuação podem ser feitos adicionando as teclas `trainingSchedule` e `scoringSchedule` com suas respectivas `startTime`, `endTime`e `cron` teclas.

>[!NOTE] essa `PUT` solicitação em `mlServices` permite modificar Serviços com execuções de experimento programadas existentes. Não **** tente modificar o `startTime` em treinamentos agendados e trabalhos de pontuação existentes. Se for `startTime` necessário modificar, considere publicar o mesmo Modelo e reprogramar o treinamento e a pontuação de trabalhos.

**Resposta**

A resposta será a `{JSON_PAYLOAD}` , mas com `id`chaves extras `created`e `updated` no objeto.

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
