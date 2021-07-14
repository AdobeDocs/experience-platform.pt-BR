---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API
title: Exporte o Ponto de Extremidade da API de Tarefas
topic-legacy: guide
type: Documentation
description: O Perfil do cliente em tempo real permite criar uma única visualização de clientes individuais no Adobe Experience Platform, reunindo dados de várias fontes, incluindo dados de atributos e dados comportamentais. Os dados do perfil podem ser exportados para um conjunto de dados para processamento adicional.
exl-id: d51b1d1c-ae17-4945-b045-4001e4942b67
source-git-commit: 453e120fa20232533289ee5ff34821ce8c0c310b
workflow-type: tm+mt
source-wordcount: '1526'
ht-degree: 2%

---

# Ponto de extremidade de tarefas de exportação

[!DNL Real-time Customer Profile] O permite criar uma única visualização de clientes individuais ao reunir dados de várias fontes, incluindo dados de atributos e dados comportamentais. Os dados do perfil podem ser exportados para um conjunto de dados para processamento adicional. Por exemplo, os segmentos de público-alvo dos dados [!DNL Profile] podem ser exportados para ativação e os atributos de perfil podem ser exportados para relatórios.

Este documento fornece instruções passo a passo para criar e gerenciar tarefas de exportação usando a [API de perfil](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

>[!NOTE]
>
>Este guia aborda o uso de tarefas de exportação no [!DNL Profile API]. Para obter informações sobre como gerenciar trabalhos de exportação para o Adobe Experience Platform Segmentation Service, consulte o guia sobre [exportar trabalhos na API de segmentação](../../profile/api/export-jobs.md).

Além de criar um trabalho de exportação, você também pode acessar dados [!DNL Profile] usando o terminal `/entities`, também conhecido como &quot;[!DNL Profile Access]&quot;. Consulte o [guia de ponto de extremidade de entidades](./entities.md) para obter mais informações. Para obter etapas sobre como acessar dados [!DNL Profile] usando a interface do usuário, consulte o [guia do usuário](../ui/user-guide.md).

## Introdução

Os endpoints de API usados neste guia fazem parte da API [!DNL Real-time Customer Profile]. Antes de continuar, consulte o [guia de introdução](getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API [!DNL Experience Platform].

## Criar um trabalho de exportação

A exportação de dados [!DNL Profile] requer primeiro a criação de um conjunto de dados no qual os dados serão exportados e, em seguida, o início de um novo trabalho de exportação. Ambas as etapas podem ser realizadas usando APIs do Experience Platform, com a primeira usando a API do Serviço de catálogo e a segunda usando a API do perfil do cliente em tempo real. As instruções detalhadas para concluir cada etapa são descritas nas seções a seguir.

### Criar um conjunto de dados de destino

Ao exportar [!DNL Profile] dados, um conjunto de dados de destino deve ser criado primeiro. É importante que o conjunto de dados seja configurado corretamente para garantir que a exportação seja bem-sucedida.

Uma das principais considerações é o esquema no qual o conjunto de dados é baseado (`schemaRef.id` na solicitação de amostra de API abaixo). Para exportar dados de perfil, o conjunto de dados deve ser baseado no [!DNL XDM Individual Profile] Esquema de União (`https://ns.adobe.com/xdm/context/profile__union`). Um schema de união é um schema somente leitura gerado pelo sistema que agrega os campos de esquemas que compartilham a mesma classe. Nesse caso, essa é a classe [!DNL XDM Individual Profile]. Para obter mais informações sobre schemas de exibição de união, consulte a seção [união nas noções básicas do guia de composição de schema](../../xdm/schema/composition.md#union).

As etapas a seguir neste tutorial descrevem como criar um conjunto de dados que faça referência ao [!DNL XDM Individual Profile] Esquema de união usando a API [!DNL Catalog]. Você também pode usar a interface do usuário [!DNL Platform] para criar um conjunto de dados que faça referência ao esquema de união. As etapas para usar a interface do usuário são descritas em [este tutorial da interface do usuário para exportar segmentos](../../segmentation/tutorials/create-dataset-export-segment.md), mas também são aplicáveis aqui. Depois de concluído, você pode retornar a este tutorial para prosseguir com as etapas para [iniciar um novo trabalho de exportação](#initiate).

Se você já tiver um conjunto de dados compatível e souber sua ID, poderá prosseguir diretamente para a etapa para [iniciar um novo trabalho de exportação](#initiate).

**Formato da API**

```http
POST /dataSets
```

**Solicitação**

A solicitação a seguir cria um novo conjunto de dados, fornecendo parâmetros de configuração no payload.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Profile Data Export",
        "schemaRef": {
          "id": "https://ns.adobe.com/xdm/context/profile__union",
          "contentType": "application/vnd.adobe.xed+json;version=1"
        }
      }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `name` | Um nome descritivo para o conjunto de dados. |
| `schemaRef.id` | A ID da exibição de união (schema) à qual o conjunto de dados será associado. |

**Resposta**

Uma resposta bem-sucedida retorna uma matriz contendo a ID exclusiva, gerada pelo sistema e somente leitura do conjunto de dados recém-criado. É necessária uma ID de conjunto de dados corretamente configurada para exportar com êxito os dados do perfil.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Iniciar trabalho de exportação {#initiate}

Depois de ter um conjunto de dados que persiste em união, você pode criar um trabalho de exportação para manter os dados do Perfil no conjunto de dados, fazendo uma solicitação POST para o endpoint `/export/jobs` na API do Perfil do cliente em tempo real e fornecendo os detalhes dos dados que deseja exportar no corpo da solicitação.

**Formato da API**

```http
POST /export/jobs
```

**Solicitação**

A solicitação a seguir cria um novo trabalho de exportação, fornecendo parâmetros de configuração no payload.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields" : {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    }
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }' 
```

| Propriedade | Descrição |
| -------- | ----------- |
| `fields` | *(Opcional)* Limita os campos de dados a serem incluídos na exportação somente para aqueles fornecidos neste parâmetro. A omissão desse valor resultará na inclusão de todos os campos nos dados exportados. |
| `mergePolicy` | *(Opcional)* Especifica a política de mesclagem para reger os dados exportados. Inclua esse parâmetro quando houver vários segmentos sendo exportados. |
| `mergePolicy.id` | A ID da política de mesclagem. |
| `mergePolicy.version` | A versão específica da política de mesclagem a ser usada. A omissão desse valor assumirá como padrão a versão mais recente. |
| `additionalFields.eventList` | *(Opcional)* Controla os campos de evento da série de tempo exportados para objetos filhos ou associados, fornecendo uma ou mais das seguintes configurações:<ul><li>`eventList.fields`: Controle os campos a serem exportados.</li><li>`eventList.filter`: Especifica critérios que limitam os resultados incluídos dos objetos associados. Espera um valor mínimo necessário para a exportação, normalmente uma data.</li><li>`eventList.filter.fromIngestTimestamp`: Filtra eventos de séries de tempo para aqueles que foram assimilados após o carimbo de data e hora fornecido. Esse não é o momento do evento em si, mas o tempo de assimilação dos eventos.</li></ul> |
| `destination` | **(Obrigatório)** Informações de destino dos dados exportados:<ul><li>`destination.datasetId`:  **(Obrigatório)** A ID do conjunto de dados em que os dados devem ser exportados.</li><li>`destination.segmentPerBatch`:  *(Opcional)* Um valor booleano que, se não for fornecido, assumirá como padrão  `false`. Um valor `false` exporta todas as IDs de segmento para uma única ID de lote. Um valor `true` exporta uma ID de segmento para uma ID de lote. Observe que definir o valor para ser `true` pode afetar o desempenho da exportação de lote.</li></ul> |
| `schema.name` | **(Obrigatório)** O nome do schema associado ao conjunto de dados em que os dados devem ser exportados. |

>[!NOTE]
>
>Para exportar apenas os dados do Perfil e não incluir os dados de séries de tempo relacionados, remova o objeto &quot;additionalFields&quot; da solicitação.

**Resposta**

Uma resposta bem-sucedida retorna um conjunto de dados preenchido com dados de Perfil, conforme especificado na solicitação.

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "NEW",
    "requestId": "IwkVcD4RupdSmX376OBVORvcvTdA4ypN",
    "computeGatewayJobId": {},
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1559674261657
        }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

## Listar todos os trabalhos de exportação

Você pode retornar uma lista de todos os trabalhos de exportação para uma Organização IMS específica executando uma solicitação de GET para o endpoint `export/jobs`. A solicitação também oferece suporte aos parâmetros de consulta `limit` e `offset`, conforme mostrado abaixo.

**Formato da API**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `start` | Deslocar a página de resultados retornados, de acordo com a hora de criação da solicitação. Exemplo: `start=4` |
| `limit` | Limite o número de resultados retornados. Exemplo: `limit=10` |
| `page` | Retorne uma página específica de resultados, de acordo com o horário de criação da solicitação. Exemplo: `page=2` |
| `sort` | Classifique os resultados por um campo específico em ordem crescente ( **`asc`** ) ou decrescente ( **`desc`** ). O parâmetro de classificação não funciona ao retornar várias páginas de resultados. Exemplo: `sort=updateTime:asc` |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Resposta**

A resposta inclui um objeto `records` contendo os trabalhos de exportação criados pela Organização IMS.

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
      "id": 726,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "timestampOrdered-none-mp",
          "version": 1
      },
      "status": "SUCCEEDED",
      "requestId": "d995479c-8a08-4240-903b-af469c67be1f",
      "computeGatewayJobId": {
          "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
          "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538615973895,
              "endTimeInMs": 1538616233239,
              "totalTimeInMs": 259344
          },
          "profileExportTime": {
              "startTimeInMs": 1538616067445,
              "endTimeInMs": 1538616139576,
              "totalTimeInMs": 72131
          },
          "aCPDatasetWriteTime": {
              "startTimeInMs": 1538616195172,
              "endTimeInMs": 1538616195715,
              "totalTimeInMs": 543
          }
      },
      "destination": {
          "datasetId": "5b7c86968f7b6501e21ba9df",
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
      },
      "updateTime": 1538616233239,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538615973895
    },
    {
      "profileInstanceId": "test_xdm_latest_profile_20_e2e_1538573005395",
      "errors": [
        {
          "code": "0090000009",
          "msg": "Error writing profiles to output path 'adl://va7devprofilesnapshot.azuredatalakestore.net/snapshot/722'",
          "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger" 
        },
        {
          "code": "unknown",
          "msg": "Job aborted.",
          "callStack": "org.apache.spark.SparkException: Job aborted."
        }
      ],
      "jobType": "BATCH",
      "filter": {
        "segments": [
            {
                "segmentId": "7a93d2ff-a220-4bae-9a4e-5f3c35032be3"
            }
        ]
      },
      "id": 722,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "7972e3d6-96ea-4ece-9627-cbfd62709c5d",
          "version": 1
      },
      "status": "FAILED",
      "requestId": "KbOAsV7HXmdg262lc4yZZhoml27UWXPZ",
      "computeGatewayJobId": {
          "exportJob": "15971e0f-317c-4390-9038-1a0498eb356f"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538573416687,
              "endTimeInMs": 1538573922551,
              "totalTimeInMs": 505864
          },
          "profileExportTime": {
              "startTimeInMs": 1538573872211,
              "endTimeInMs": 1538573918809,
              "totalTimeInMs": 46598
          }
      },
      "destination": {
          "datasetId": "5bb4c46757920712f924a3eb",
          "batchId": ""
      },
      "updateTime": 1538573922551,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538573416687
    }
  ],
  "page": {
      "sortField": "createdTime",
      "sort": "desc",
      "pageOffset": "1538573416687_722",
      "pageSize": 2
  },
  "link": {
      "next": "/export/jobs/?limit=2&offset=1538573416687_722"
  }
}
```

## Monitorar progresso da exportação

Para exibir os detalhes de um trabalho de exportação específico ou monitorar seu status enquanto ele é processado, é possível fazer uma solicitação de GET para o endpoint `/export/jobs` e incluir o `id` do trabalho de exportação no caminho. O trabalho de exportação é concluído assim que o campo `status` retorna o valor &quot;SUCCEEDED&quot;.

**Formato da API**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | O `id` do trabalho de exportação que você deseja acessar. |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "SUCCEEDED",
    "requestId": "YwMt1H8QbVlGT2pzyxgwFHTwzpMbHrTq",
    "computeGatewayJobId": {
      "exportJob": "305a2e5c-2cf3-4746-9b3d-3c5af0437754",
      "pushJob": "963f275e-91a3-4fa1-8417-d2ca00b16a8a"
    },
    "metrics": {
      "totalTime": {
        "startTimeInMs": 1547053539564,
        "endTimeInMs": 1547054743929,
        "totalTimeInMs": 1204365
      },
      "profileExportTime": {
        "startTimeInMs": 1547053667591,
        "endTimeInMs": 1547053778195,
        "totalTimeInMs": 110604
      },
      "aCPDatasetWriteTime": {
        "startTimeInMs": 1547054660416,
        "endTimeInMs": 1547054698918,
        "totalTimeInMs": 38502
      }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `batchId` | O identificador dos lotes criados a partir de uma exportação bem-sucedida, que será usado para fins de pesquisa ao ler os dados do perfil. |

## Cancelar um trabalho de exportação

O Experience Platform permite cancelar um trabalho de exportação existente, que pode ser útil por vários motivos, incluindo se o trabalho de exportação não foi concluído ou se tornou preso no estágio de processamento. Para cancelar um trabalho de exportação, você pode executar uma solicitação de DELETE para o endpoint `/export/jobs` e incluir o `id` do trabalho de exportação que deseja cancelar para o caminho da solicitação.

**Formato da API**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | O `id` do trabalho de exportação que você deseja acessar. |

**Solicitação**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs/726 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma solicitação de exclusão bem-sucedida retorna o Status HTTP 204 (Sem conteúdo) e um corpo de resposta vazio, indicando que a operação de cancelamento foi bem-sucedida.

## Próximas etapas

Depois que a exportação for concluída com sucesso, seus dados estarão disponíveis no Data Lake, no Experience Platform. Em seguida, você pode usar a [Data Access API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) para acessar os dados usando o `batchId` associado à exportação. Dependendo do tamanho da exportação, os dados podem estar em partes e o lote pode consistir em vários arquivos.

Para obter instruções passo a passo sobre como usar a API de acesso a dados para acessar e baixar arquivos em lote, siga o [tutorial de acesso a dados](../../data-access/tutorials/dataset-data.md).

Você também pode acessar dados exportados com êxito do Perfil do cliente em tempo real usando o Serviço de query da Adobe Experience Platform. Usando a interface do usuário ou a RESTful API, o Serviço de query permite gravar, validar e executar consultas em dados no Data Lake.

Para obter mais informações sobre como consultar dados do público-alvo, consulte a [documentação do Serviço de query](../../query-service/home.md).

## Apêndice

A seção a seguir contém informações adicionais sobre trabalhos de exportação na API de perfil.

### Exemplos adicionais de carga de exportação

A chamada de API de exemplo mostrada na seção em [iniciar um trabalho de exportação](#initiate) cria um trabalho que contém dados de perfil (registro) e evento (série de tempo). Esta seção fornece exemplos adicionais de carga de solicitação para limitar sua exportação a conter um tipo de dados ou outro.

A carga a seguir cria um trabalho de exportação que contém apenas os dados do perfil (sem eventos):

```json
{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }
```

Para criar um trabalho de exportação que contenha apenas dados do evento (sem atributos de perfil), a carga pode ser semelhante ao seguinte:

```json
{
    "fields": "identityMap",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields" : {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }
```

### Exportar segmentos

Você também pode usar o endpoint exportar trabalhos para exportar segmentos de público-alvo em vez de dados [!DNL Profile]. Consulte o guia em [exportar trabalhos na API de segmentação](../../segmentation/api/export-jobs.md) para obter mais informações.
