---
keywords: Experience Platform;perfil;perfil de cliente em tempo real;solução de problemas;API
title: Ponto de extremidade da API de trabalhos de exportação de perfil
type: Documentation
description: O Perfil do cliente em tempo real permite criar uma única visualização de clientes individuais no Adobe Experience Platform, reunindo dados de várias fontes, incluindo dados de atributos e dados comportamentais. Os dados do perfil podem ser exportados para um conjunto de dados para processamento adicional.
role: Developer
exl-id: d51b1d1c-ae17-4945-b045-4001e4942b67
source-git-commit: fd5042bee9b09182ac643bcc69482a0a2b3f8faa
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 2%

---

# Ponto de extremidade de trabalhos de exportação de perfil

O [!DNL Real-Time Customer Profile] permite que você crie uma visão única de clientes individuais reunindo dados de várias fontes, incluindo dados de atributos e dados comportamentais. Os dados do perfil podem ser exportados para um conjunto de dados para processamento adicional. Por exemplo, os dados do [!DNL Profile] podem ser exportados para ativação criando públicos-alvo, e os atributos do perfil podem ser exportados para relatórios.

Este documento fornece instruções passo a passo para criar e gerenciar trabalhos de exportação usando a [API de perfil](https://www.adobe.com/go/profile-apis-en).

>[!NOTE]
>
>Este guia aborda o uso de trabalhos de exportação no [!DNL Profile API]. Para obter informações sobre como gerenciar trabalhos de exportação para o Serviço de Segmentação do Adobe Experience Platform, consulte o manual sobre [trabalhos de exportação na API de Segmentação](../../profile/api/export-jobs.md).

Além de criar um trabalho de exportação, você também pode acessar dados do [!DNL Profile] usando o ponto de extremidade `/entities`, também conhecido como &quot;[!DNL Profile Access]&quot;. Consulte o [manual de ponto de extremidade de entidades](./entities.md) para obter mais informações. Para obter etapas sobre como acessar dados do [!DNL Profile] usando a interface, consulte o [guia do usuário](../ui/user-guide.md).

## Introdução

Os pontos de extremidade de API usados neste guia fazem parte da API [!DNL Real-Time Customer Profile]. Antes de continuar, consulte o [guia de introdução](getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do [!DNL Experience Platform].

## Criar um trabalho de exportação

A exportação de dados [!DNL Profile] requer primeiro a criação de um conjunto de dados para o qual os dados serão exportados e, em seguida, o início de um novo trabalho de exportação. Ambas as etapas podem ser realizadas usando APIs de Experience Platform, sendo que a primeira usa a API de Serviço de catálogo e a última usa a API de perfil do cliente em tempo real. As instruções detalhadas para concluir cada etapa estão descritas nas seções a seguir.

### Criar um conjunto de dados de destino

Ao exportar dados do [!DNL Profile], um conjunto de dados de destino deve ser criado primeiro. É importante que o conjunto de dados seja configurado corretamente para garantir que a exportação seja bem-sucedida.

Uma das principais considerações é o esquema no qual o conjunto de dados se baseia (`schemaRef.id` na solicitação de amostra de API abaixo). Para exportar dados do perfil, o conjunto de dados deve ser baseado no [!DNL XDM Individual Profile] Esquema de união (`https://ns.adobe.com/xdm/context/profile__union`). Um esquema de união é um esquema somente leitura gerado pelo sistema que agrega os campos de esquemas que compartilham a mesma classe. Nesse caso, essa é a classe [!DNL XDM Individual Profile]. Para obter mais informações sobre esquemas de exibição de união, consulte a [seção de união no guia de composição de esquemas](../../xdm/schema/composition.md#union).

As etapas deste tutorial descrevem como criar um conjunto de dados que faz referência ao Esquema de união [!DNL XDM Individual Profile] usando a API [!DNL Catalog]. Você também pode usar a interface de usuário [!DNL Platform] para criar um conjunto de dados que faça referência ao esquema de união. As etapas para usar a interface do usuário estão descritas em [este tutorial de interface do usuário para exportar públicos](../../segmentation/tutorials/create-dataset-export-segment.md), mas também se aplicam aqui. Depois de concluído, você pode retornar a este tutorial para prosseguir com as etapas para [iniciar um novo trabalho de exportação](#initiate).

Se você já tiver um conjunto de dados compatível e souber sua ID, poderá prosseguir diretamente para a etapa para [iniciar um novo trabalho de exportação](#initiate).

**Formato da API**

```http
POST /dataSets
```

**Solicitação**

A solicitação a seguir cria um novo conjunto de dados, fornecendo parâmetros de configuração na carga.

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `schemaRef.id` | A ID da visualização de união (esquema) à qual o conjunto de dados será associado. |

**Resposta**

Uma resposta bem-sucedida retorna uma matriz que contém a ID exclusiva gerada pelo sistema somente leitura do conjunto de dados recém-criado. É necessária uma ID de conjunto de dados configurada corretamente para exportar os dados do perfil com êxito.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Iniciar trabalho de exportação {#initiate}

Depois de ter um conjunto de dados persistente na união, você pode criar um trabalho de exportação para persistir os dados do Perfil para o conjunto de dados fazendo uma solicitação POST para o ponto de extremidade `/export/jobs` na API de Perfil do cliente em tempo real e fornecendo os detalhes dos dados que deseja exportar no corpo da solicitação.

**Formato da API**

```http
POST /export/jobs
```

**Solicitação**

A solicitação a seguir cria um novo trabalho de exportação, fornecendo parâmetros de configuração na carga.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields": {
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
  }' 
```

| Propriedade | Descrição |
| -------- | ----------- |
| `fields` | *(Opcional)* Limita os campos de dados a serem incluídos na exportação apenas àqueles fornecidos neste parâmetro. A omissão desse valor resultará na inclusão de todos os campos nos dados exportados. |
| `mergePolicy` | *(Opcional)* Especifica a política de mesclagem para controlar os dados exportados. Inclua esse parâmetro quando houver vários públicos-alvo sendo exportados. |
| `mergePolicy.id` | A ID da política de mesclagem. |
| `mergePolicy.version` | A versão específica da política de mesclagem a ser usada. A omissão desse valor assumirá como padrão a versão mais recente. |
| `additionalFields.eventList` | *(Opcional)* Controla os campos de eventos de série temporal exportados para objetos filho ou associados fornecendo uma ou mais das seguintes configurações:<ul><li>`eventList.fields`: Controle os campos a serem exportados.</li><li>`eventList.filter`: especifica os critérios que limitam os resultados incluídos de objetos associados. Espera um valor mínimo necessário para a exportação, normalmente uma data.</li><li>`eventList.filter.fromIngestTimestamp`: Filtra os eventos de série temporal para aqueles que foram assimilados após o carimbo de data/hora fornecido. Esse não é o tempo do evento em si, mas o tempo de assimilação dos eventos.</li></ul> |
| `destination` | **(Obrigatório)** Informações de destino dos dados exportados:<ul><li>`destination.datasetId`: **(Obrigatório)** A ID do conjunto de dados para o qual os dados devem ser exportados.</li><li>`destination.segmentPerBatch`: *(Opcional)* Um valor booliano que, se não for fornecido, assumirá `false` como padrão. Um valor de `false` exporta todas as IDs de definição de segmento em uma única ID de lote. Um valor de `true` exporta uma ID de definição de segmento para uma ID de lote. Observe que definir o valor como `true` pode afetar o desempenho da exportação de lotes.</li></ul> |
| `schema.name` | **(Obrigatório)** O nome do esquema associado ao conjunto de dados para o qual os dados devem ser exportados. |

>[!NOTE]
>
>Para exportar apenas dados de Perfil e não incluir dados de série temporal relacionados, remova o objeto &quot;additionalFields&quot; da solicitação.

**Resposta**

Uma resposta bem-sucedida retorna um conjunto de dados preenchido com dados do Perfil, conforme especificado na solicitação.

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
      "dataSetId": "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{ORG_ID}",
    "creationTime": 1559674261657
}
```

## Listar todos os trabalhos de exportação

Você pode retornar uma lista de todos os trabalhos de exportação para uma organização específica executando uma solicitação GET para o ponto de extremidade `export/jobs`. A solicitação também oferece suporte aos parâmetros de consulta `limit` e `offset`, conforme mostrado abaixo.

**Formato da API**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `start` | Deslocar a página de resultados retornados de acordo com o tempo de criação da solicitação. Exemplo: `start=4` |
| `limit` | Limitar o número de resultados retornados. Exemplo: `limit=10` |
| `page` | Retornar uma página específica de resultados, de acordo com o horário de criação da solicitação. Exemplo: `page=2` |
| `sort` | Classifique os resultados por um campo específico em ordem crescente ( **`asc`** ) ou decrescente ( **`desc`** ). O parâmetro de classificação não funciona ao retornar várias páginas de resultados. Exemplo: `sort=updateTime:asc` |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Resposta**

A resposta inclui um objeto `records` que contém os trabalhos de exportação criados por sua organização.

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
      "imsOrgId": "{ORG_ID}",
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
      "imsOrgId": "{ORG_ID}",
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

## Monitorar o progresso da exportação

Para exibir os detalhes de um trabalho de exportação específico ou monitorar seu status enquanto ele é processado, você pode fazer uma solicitação GET para o ponto de extremidade `/export/jobs` e incluir o `id` do trabalho de exportação no caminho. O trabalho de exportação é concluído assim que o campo `status` retorna o valor &quot;SUCCEEDED&quot;.

**Formato da API**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | O `id` do trabalho de exportação que você deseja acessar. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
      "dataSetId": "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{ORG_ID}",
    "creationTime": 1559674261657
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `batchId` | O identificador dos lotes criados a partir de uma exportação bem-sucedida, para ser usado para fins de pesquisa ao ler dados do perfil. |

## Cancelar um trabalho de exportação

o Experience Platform permite cancelar um trabalho de exportação existente, que pode ser útil por vários motivos, incluindo se o trabalho de exportação não foi concluído ou ficou preso no estágio de processamento. Para cancelar um trabalho de exportação, você pode executar uma solicitação DELETE para o ponto de extremidade `/export/jobs` e incluir o `id` do trabalho de exportação que deseja cancelar no caminho da solicitação.

**Formato da API**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | O `id` do trabalho de exportação que você deseja acessar. |

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs/726 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma solicitação de exclusão bem-sucedida retorna o Status HTTP 204 (Sem conteúdo) e um corpo de resposta vazio, indicando que a operação de cancelamento foi bem-sucedida.

## Próximas etapas

Depois que a exportação for concluída com sucesso, seus dados estarão disponíveis no Data Lake no Experience Platform. Você pode usar a [API de acesso a dados](https://www.adobe.io/experience-platform-apis/references/data-access/) para acessar os dados usando a `batchId` associada à exportação. Dependendo do tamanho da exportação, os dados podem estar em partes e o lote pode consistir em vários arquivos.

Para obter instruções passo a passo sobre como usar a API de acesso a dados para acessar e baixar arquivos em lotes, siga o [tutorial sobre acesso a dados](../../data-access/tutorials/dataset-data.md).

Você também pode acessar com êxito os dados exportados do Perfil do cliente em tempo real usando o serviço de consulta da Adobe Experience Platform. Usando a interface ou a API RESTful, o Serviço de consulta permite gravar, validar e executar consultas em dados no Data Lake.

Para obter mais informações sobre como consultar dados de público, consulte a [documentação do Serviço de consulta](../../query-service/home.md).

## Apêndice

A seção a seguir contém informações adicionais sobre trabalhos de exportação na API do perfil.

### Exemplos adicionais de carga útil de exportação

A chamada de API de exemplo mostrada na seção [iniciando um trabalho de exportação](#initiate) cria um trabalho que contém dados de perfil (registro) e de evento (série temporal). Esta seção fornece exemplos adicionais de carga da solicitação para limitar a exportação para conter um tipo de dados ou o outro.

A carga a seguir cria um trabalho de exportação que contém apenas dados de perfil (nenhum evento):

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
    "additionalFields": {
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

### Exportação de públicos

Você também pode usar o ponto de extremidade de trabalhos de exportação para exportar públicos em vez de [!DNL Profile] dados. Consulte o guia sobre [trabalhos de exportação na API de segmentação](../../segmentation/api/export-jobs.md) para obter mais informações.
