---
keywords: Experience Platform;início;tópicos populares;dados de armazenamento na nuvem;dados de transmissão;transmissão;;home;popular topics;cloud storage data;streaming data;streaming data;streaming
solution: Experience Platform
title: Criar um fluxo de dados de transmissão para dados brutos usando a API do serviço de fluxo
type: Tutorial
description: Este tutorial aborda as etapas para recuperar dados de transmissão e trazê-los para a Platform usando conectores de origem e APIs.
exl-id: 898df7fe-37a9-4495-ac05-30029258a6f4
source-git-commit: 39b5a2b76c28033b9e98dcefc4cdcaa9964f4d2e
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 3%

---

# Crie um fluxo de dados de transmissão para dados brutos usando o [!DNL Flow Service] API

Este tutorial aborda as etapas para recuperar dados brutos de um conector de origem de transmissão e trazê-los para o Experience Platform usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este tutorial requer que você tenha uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   - [Noções básicas da composição do esquema](../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   - [Guia do desenvolvedor do Registro de esquema](../../../../xdm/api/getting-started.md): inclui informações importantes que você precisa saber para executar com êxito chamadas para a API do Registro de esquema. Isso inclui o `{TENANT_ID}`, o conceito de &quot;contêineres&quot; e os cabeçalhos necessários para fazer solicitações (com atenção especial ao cabeçalho Aceitar e seus valores possíveis).
- [[!DNL Catalog Service]](../../../../catalog/home.md): Catálogo é o sistema de registro para localização e linhagem de dados no Experience Platform.
- [[!DNL Streaming ingestion]](../../../../ingestion/streaming-ingestion/overview.md): a assimilação de streaming para o Platform fornece aos usuários um método para enviar dados de dispositivos no lado do cliente e do servidor para o Experience Platform em tempo real.
- [Sandboxes](../../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../../../landing/api-guide.md).

### Criar uma conexão de origem {#source}

Este tutorial também requer que você tenha uma ID de conexão de origem válida para um conector de streaming. Se você não tiver essas informações, consulte os seguintes tutoriais sobre como criar uma conexão de origem de fluxo antes de tentar este tutorial:

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

## Criar um esquema XDM de destino {#target-schema}

Para que os dados de origem sejam usados na Platform, um esquema de destino deve ser criado para estruturar os dados de origem de acordo com suas necessidades. O esquema de destino é usado para criar um conjunto de dados da Platform no qual os dados de origem estão contidos. Esse esquema XDM do Target também estende o XDM [!DNL Individual Profile] classe.

Para criar um esquema XDM de destino, faça uma solicitação POST ao `/schemas` endpoint do [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

**Formato da API**

```http
POST /tenant/schemas
```

**Solicitação**

O exemplo de solicitação a seguir cria um esquema XDM que estende o XDM [!DNL Individual Profile] classe.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "type": "object",
        "title": "Sample schema for a streaming connector",
        "description": "Sample schema for a streaming connector",
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
            }
        ],
        "meta:containerId": "tenant",
        "meta:resourceType": "schemas",
        "meta:xdmType": "object",
        "meta:class": "https://ns.adobe.com/xdm/context/profile"
    }'
```

**Resposta**

Uma resposta bem-sucedida retorna detalhes do esquema recém-criado, incluindo seu identificador exclusivo (`$id`). Essa ID é necessária nas etapas posteriores para criar um conjunto de dados, um mapeamento e um fluxo de dados de destino.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
    "meta:altId": "_{TENANT_ID}.schemas.e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Sample schema for a streaming connector",
    "type": "object",
    "description": "Sample schema for a streaming connector",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1604960074752,
        "repo:lastModifiedDate": 1604960074752,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{MODIFIED_USER_ID}",
        "eTag": "8522a151effd974429518ed90c3eaf6efc9bf6ffb6644087a85c6d4455dcd045",
        "meta:globalLibVersion": "1.16.1"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "{SANDBOX_ID}",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Criar um conjunto de dados de destino

Com um esquema XDM de destino criado e seu esquema exclusivo `$id` agora você pode criar um conjunto de dados de destino para conter seus dados de origem. Para criar um conjunto de dados de destino, faça uma solicitação POST ao `dataSets` endpoint do [API do serviço de catálogo](https://www.adobe.io/experience-platform-apis/references/catalog/), ao fornecer a ID do schema de público-alvo na carga.

**Formato da API**

```http
POST /catalog/dataSets
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test streaming dataset",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags": {
            "identity": [
            "enabled:true"
            ],
            "profile": [
            "enabled:true"
            ]
        }
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome do conjunto de dados a ser criado. |
| `schemaRef.id` | O URI `$id` para o esquema XDM, o conjunto de dados será baseado em. |
| `schemaRef.contentType` | A versão do esquema. Esse valor deve ser definido como `application/vnd.adobe.xed-full-notext+json;version=1`, que retorna a versão secundária mais recente do esquema. Consulte a seção sobre [controle de versão do esquema](../../../../xdm/api/getting-started.md#versioning) no guia API XDM para obter mais informações. |

**Resposta**

Uma resposta bem-sucedida retorna uma matriz que contém a ID do conjunto de dados recém-criado no formato `"@/datasets/{DATASET_ID}"`. A ID do conjunto de dados é uma cadeia de caracteres gerada pelo sistema e somente leitura usada para fazer referência ao conjunto de dados em chamadas de API. A ID do conjunto de dados de destino é necessária nas etapas posteriores para criar uma conexão de destino e um fluxo de dados.

```json
[
    "@/dataSets/5f7187bac6d00f194fb937c0"
]
```

## Criar uma conexão de destino {#target-connection}

As conexões do Target criam e gerenciam uma conexão de destino com a Platform ou qualquer local onde os dados transferidos sejam direcionados. As conexões de destino contêm informações sobre o destino de dados, o formato de dados e a ID de conexão de destino necessária para criar um fluxo de dados. As instâncias de conexão de destino são específicas para um locatário e uma organização.

Para criar uma conexão de target, faça uma solicitação POST ao `/targetConnections` endpoint do [!DNL Flow Service] API. Como parte da solicitação, você deve fornecer o formato de dados, a variável `dataSetId` recuperado na etapa anterior e a ID de especificação de conexão fixa vinculada ao [!DNL Data Lake]. Essa ID é `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

**Formato da API**

```http
POST /targetConnections
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Streaming target connection",
        "description": "Streaming target connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5f7187bac6d00f194fb937c0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `data.format` | O formato especificado dos dados que você está trazendo para o data lake. |
| `params.dataSetId` | A ID do conjunto de dados de destino gerado na etapa anterior. **Nota**: você deve fornecer uma ID de conjunto de dados válida ao criar uma conexão de destino. Uma ID de conjunto de dados inválida resultará em um erro. |
| `connectionSpec.id` | A ID de especificação da conexão usada para se conectar ao data lake. Essa ID é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo da nova conexão de destino (`id`). Essa ID é necessária nas etapas posteriores.

```json
{
    "id": "d9300194-6a82-4163-b001-946a821163b8",
    "etag": "\"4006d3e4-0000-0200-0000-5f7189220000\""
}
```

## Criar um mapeamento {#mapping}

Para que os dados de origem sejam assimilados em um conjunto de dados de destino, eles devem primeiro ser mapeados para o esquema de destino ao qual o conjunto de dados de destino adere.

Para criar um conjunto de mapeamento, faça uma solicitação POST ao `mappingSets` endpoint do [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) ao fornecer o esquema XDM do público-alvo `$id` e os detalhes dos conjuntos de mapeamento que deseja criar.

**Formato da API**

```http
POST /mappingSets
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "_{TENANT_ID}.schemas.e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
        "xdmVersion": "1.0",
        "mappings": [
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "firstName",
                "identity": false,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "lastName",
                "identity": false,
                "version": 0
            }
        ]
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `xdmSchema` | A variável `$id` do esquema XDM do público-alvo. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes do mapeamento recém-criado, incluindo seu identificador exclusivo (`id`). Essa ID é necessária em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "380b032b445a46008e77585e046efe5e",
    "version": 0,
    "createdDate": 1604960750613,
    "modifiedDate": 1604960750613,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Recuperar uma lista de especificações de fluxo de dados {#specs}

Um fluxo de dados é responsável por coletar dados de fontes e trazê-los para a Platform. Para criar um fluxo de dados, primeiro obtenha as especificações do fluxo de dados executando uma solicitação GET para o [!DNL Flow Service] API.

**Formato da API**

```http
GET /flowSpecs
```

**Solicitação**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de especificações de fluxo de dados. A ID de especificação do fluxo de dados que você precisa recuperar para criar um fluxo de dados usando qualquer um dos [!DNL Amazon Kinesis], [!DNL Azure Event Hubs]ou  [!DNL Google PubSub], é `d69717ba-71b4-4313-b654-49f9cf126d7a`.

```json
{
    "items": [
        {
            "id": "d69717ba-71b4-4313-b654-49f9cf126d7a",
            "name": "Stream data with optional transformation",
            "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
                "86043421-563b-46ec-8e6c-e23184711bf6",
                "70116022-a743-464a-bbfe-e226a7f8210c"
            ],
            "targetConnectionSpecIds": [
                "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                "db4fe783-ef79-4a12-bda9-32b2b1bc3b2c"
            ],
            "transformationSpecs": [
                {
                    "name": "Mapping",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines various params required for different mapping from source to target",
                        "properties": {
                            "mappingId": {
                                "type": "string"
                            }
                        }
                    }
                }
            ],
            "attributes": {
                "uiAttributes": {
                    "apiFeatures": {
                        "flowRunsSupported": false
                    }
                }
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "StreamingSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "StreamingSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        },
    ]
}
```

## Criar um fluxo de dados

A última etapa para coletar dados de transmissão é criar um fluxo de dados. Até agora, você tem os seguintes valores necessários preparados:

- [ID da conexão de origem](#source)
- [ID da conexão de destino](#target)
- [ID de mapeamento](#mapping)
- [ID da especificação do fluxo de dados](#specs)

Um fluxo de dados é responsável por agendar e coletar dados de uma origem. Você pode criar um fluxo de dados executando uma solicitação POST enquanto fornece os valores mencionados anteriormente na carga.

**Formato da API**

```http
POST /flows
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Streaming dataflow",
        "description": "Streaming dataflow",
        "flowSpec": {
            "id": "d69717ba-71b4-4313-b654-49f9cf126d7a",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "e96d6135-4b50-446e-922c-6dd66672b6b2"
        ],
        "targetConnectionIds": [
            "723222e2-6ab9-4b0b-b222-e26ab9bb0bc2"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "380b032b445a46008e77585e046efe5e",
                    "mappingVersion": 0
                }
            }
        ]
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `flowSpec.id` | A variável [ID de especificação de fluxo](#specs) recuperado na etapa anterior. |
| `sourceConnectionIds` | A variável [ID da conexão de origem](#source) recuperado em uma etapa anterior. |
| `targetConnectionIds` | A variável [ID da conexão de destino](#target-connection) recuperado em uma etapa anterior. |
| `transformations.params.mappingId` | A variável [ID do mapeamento](#mapping) recuperado em uma etapa anterior. |

**Resposta**

Uma resposta bem-sucedida retorna a ID (`id`) do fluxo de dados recém-criado.

```json
{
    "id": "1f086c23-2ea8-4d06-886c-232ea8bd061d",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Publicar dados para assimilação

Veja abaixo a carga de amostra para obter exemplos de json bruto ou compatível com XDM que você pode enviar para assimilação.

>[!NOTE]
>
>Você deve adicionar um atraso de pelo menos ~5 minutos entre a criação do fluxo de dados e a assimilação de quaisquer dados de transmissão. Isso permite que o fluxo de dados seja totalmente ativado, antes que quaisquer dados sejam assimilados.

Os exemplos a seguir se aplicam a todos os de:

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

>[!BEGINTABS]

>[!TAB Dados brutos]

```json
'{
      "name": "Johnson Smith",
      "location": {
          "city": "Seattle",
          "country": "United State of America",
          "address": "3692 Main Street"
      },
      "gender": "Male",
      "birthday": {
          "year": 1984,
          "month": 6,
          "day": 9
      }
  }'
```

>[!TAB Dados XDM]

```json
{
  "header": {
    "schemaRef": {
      "id": "https://ns.adobe.com/aepstreamingservicesint/schemas/73cae7e6db06ebca535cd973e3ece85e66253962f504e7d8",
      "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
    }
  },
  "body": {
    "xdmMeta": {
      "schemaRef": {
        "id": "https://ns.adobe.com/aepstreamingservicesint/schemas/73cae7e6db06ebca535cd973e3ece85e66253962f504e7d8",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
      }
    },
    "xdmEntity": {
      "_id": "acme",
      "workEmail": {
        "address": "mike@acme.com",
        "primary": true,
        "type": "work",
        "status": "active"
      },
      "person": {
        "gender": "male",
        "name": {
          "firstName": "Mike",
          "lastName": "Wazowski"
        },
        "birthDate": "1985-01-01"
      },
      "identityMap": {
        "ecid": [
          {
            "id": "01262118050522051420082102000000000000"
          }
        ]
      }
    }
  }
}
```

>[!ENDTABS]

## Próximas etapas

Ao seguir este tutorial, você criou um fluxo de dados para coletar dados de transmissão do seu conector de transmissão. Os dados de entrada agora podem ser usados por serviços downstream da plataforma, como [!DNL Real-Time Customer Profile] e [!DNL Data Science Workspace]. Consulte os seguintes documentos para obter mais detalhes:

- [Visão geral do Perfil do cliente em tempo real](../../../../profile/home.md)
- [Visão geral do Espaço de trabalho de ciência de dados](../../../../data-science-workspace/home.md)
