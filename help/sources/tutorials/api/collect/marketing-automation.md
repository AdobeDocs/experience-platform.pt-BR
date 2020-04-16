---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Coletar dados de automação de marketing por meio de conectores de origem e APIs
topic: overview
translation-type: tm+mt
source-git-commit: 2f7961a4ca0bc0fec2ed1f50f5101e4dd734a282

---


# Coletar dados de automação de marketing por meio de conectores de origem e APIs

Este tutorial aborda as etapas para recuperar dados de um sistema de automação de marketing e trazê-los para a Plataforma por meio de conectores de origem e APIs.

## Introdução

Este tutorial requer que você tenha informações sobre o arquivo que deseja trazer para a Plataforma, incluindo o caminho e a estrutura do arquivo. Se você não tiver essas informações, consulte o tutorial sobre como [explorar um aplicativo de automação de marketing usando a API](../../api/create/marketing-automation/hubspot.md) do Serviço de Fluxo antes de tentar este tutorial.

Este tutorial também exige que você tenha uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Sistema](../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual a plataforma Experience organiza os dados da experiência do cliente.
   * [Noções básicas da composição](../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Guia](../../../../xdm/api/getting-started.md)do desenvolvedor do Registro do Schema: Inclui informações importantes que você precisa saber para executar com êxito chamadas para a API do Registro do Schema. Isso inclui seu `{TENANT_ID}`, o conceito de &quot;container&quot; e os cabeçalhos necessários para fazer solicitações (com atenção especial ao cabeçalho Accept e seus possíveis valores).
* [Serviço](../../../../catalog/home.md)de catálogo: Catálogo é o sistema de registro para localização e linhagem de dados na Experience Platform.
* [Ingestão](../../../../ingestion/batch-ingestion/overview.md)em lote: A API de ingestão em lote permite que você ingira dados na Experience Platform como arquivos em lote.
* [Caixas de proteção](../../../../sandboxes/home.md): A plataforma Experience fornece caixas de proteção virtuais que particionam uma única instância da Plataforma em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a um sistema de automação de marketing usando a API de Serviço de Fluxo.

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de solução de problemas da plataforma Experience.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para APIs de plataforma, você deve primeiro concluir o tutorial [de](../../../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas da API da plataforma da experiência, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos na plataforma Experience, incluindo os pertencentes ao Serviço de fluxo, estão isolados para caixas de proteção virtuais específicas. Todas as solicitações para APIs de plataforma exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

## Criar uma classe e um schema XDM ad hoc

Para trazer dados externos para a Plataforma por meio de conectores de origem, é necessário criar uma classe e um schema XDM ad-hoc para os dados de origem brutos.

Para criar uma classe e um schema ad-hoc, siga as etapas descritas no tutorial [do schema](../../../../xdm/tutorials/ad-hoc.md)ad-hoc. Ao criar uma classe ad-hoc, todos os campos encontrados nos dados de origem devem ser descritos no corpo da solicitação.

Continue seguindo as etapas descritas no guia do desenvolvedor até que você tenha criado um schema ad-hoc. Obtenha e armazene o identificador exclusivo (`$id`) do schema ad-hoc e prossiga para a próxima etapa deste tutorial.

## Criar uma conexão de origem {#source}

Com um schema XDM ad-hoc criado, uma conexão de origem agora pode ser criada usando uma solicitação POST para a API de Serviço de Fluxo. Uma conexão de origem consiste em uma conexão básica, um arquivo de dados de origem e uma referência ao schema que descreve os dados de origem.

**Formato da API**

```https
POST /sourceConnections
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Marketing automation source connection",
        "baseConnectionId": "2fce94c1-9a93-4971-8e94-c19a93097129",
        "description": "Marketing automation source connection",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/80a6e931bd5e00190b72daafb4e1e4f7913a114808be9ac0",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "Hubspot.Contacts"
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `baseConnectionId` | A ID de conexão do aplicativo de automação de marketing |
| `data.schema.id` | A `$id` do schema XDM ad-hoc. |
| `params.path` | O caminho do arquivo de origem. |
| `connectionSpec.id` | A ID de especificação de conexão do aplicativo de automação de marketing. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada. Armazene esse valor conforme necessário em etapas posteriores para criar uma conexão de público alvo.

```json
{
    "id": "c315c0ae-a339-44c4-95c0-aea33964c420",
    "etag": "\"67010af9-0000-0200-0000-5e9795c40000\""
}
```

## Criar um schema XDM de público alvo {#target}

Em etapas anteriores, um schema XDM ad-hoc foi criado para estruturar os dados de origem. Para que os dados de origem sejam usados na Plataforma, um schema de público alvo também deve ser criado para estruturar os dados de origem de acordo com suas necessidades. O schema do público alvo é então usado para criar um conjunto de dados da Plataforma no qual os dados de origem estão contidos.

Um schema XDM de público alvo pode ser criado executando-se uma solicitação POST para a API [do Registro de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)Schemas. Se você preferir usar a interface do usuário na Experience Platform, o tutorial [do Editor de](../../../../xdm/tutorials/create-schema-ui.md) Schemas fornece instruções passo a passo para executar ações semelhantes no Editor de Schemas.

**Formato da API**

```https
POST /schemaregistry/tenant/schemas
```

**Solicitação**

A solicitação de exemplo a seguir cria um schema XDM que estende a classe de Perfil Individual XDM.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "type": "object",
        "title": "Target schema for marketing automation",
        "description": "Target schema for marketing automation",
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
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

Uma resposta bem-sucedida retorna detalhes do schema recém-criado, incluindo seu identificador exclusivo (`$id`). Armazene essa ID conforme necessário em etapas posteriores para criar um conjunto de dados de público alvo, mapeamento e fluxo de dados.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/63f2c82fcdcb606c536a62d7716e34acbf63cd4582a1c16b",
    "meta:altId": "_{TENANT_ID}.schemas.63f2c82fcdcb606c536a62d7716e34acbf63cd4582a1c16b",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for marketing automation",
    "type": "object",
    "description": "Target schema for marketing automation",
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
    "imsOrg": "{IMS_ORG}",
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
        "repo:createdDate": 1586992941717,
        "repo:lastModifiedDate": 1586992941717,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CREATED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{CREATED_USER_ID}",
        "eTag": "d11e63a422b84a843cdd58d0ba8a16ce0a2068eda49ab380c1605ddd10efdf23",
        "meta:globalLibVersion": "1.9.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Criar um conjunto de dados de público alvo

É possível criar um conjunto de dados de público alvo executando uma solicitação POST para a API [do serviço de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)catálogo, fornecendo a ID do schema do público alvo dentro da carga.

**Formato da API**

```https
POST /catalog/dataSets
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Target dataset for marketing automation",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/14d89c5bb88e2ff488f23db896be469e7e30bb166bda8722",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `schemaRef.id` | A `$id` do schema XDM do público alvo. |

**Resposta**

Uma resposta bem-sucedida retorna uma matriz que contém a ID do conjunto de dados recém-criado no formato `"@/datasets/{DATASET_ID}"`. A ID do conjunto de dados é uma sequência de caracteres somente leitura, gerada pelo sistema, usada para fazer referência ao conjunto de dados em chamadas de API. Armazene a ID do conjunto de dados do público alvo conforme necessário em etapas posteriores para criar uma conexão de público alvo e um fluxo de dados.

```json
[
    "@/dataSets/5e9797ac6d771118ad8356db"
]
```

## Criar uma conexão básica de conjunto de dados

Para criar uma conexão de público alvo e assimilar dados externos na Plataforma, é necessário adquirir uma conexão básica de conjunto de dados.

Para criar uma conexão base de conjunto de dados, siga as etapas descritas no tutorial [de conexão base de](../create-dataset-base-connection.md)conjunto de dados.

Continue seguindo as etapas descritas no guia do desenvolvedor até que você tenha criado uma conexão base de conjunto de dados. Obtenha e armazene o identificador exclusivo (`$id`) da conexão base e prossiga para a próxima etapa deste tutorial.

## Criar uma conexão de público alvo

Agora você tem os identificadores exclusivos para uma conexão básica de conjunto de dados, um schema de público alvo e um conjunto de dados de público alvo. Usando esses identificadores, é possível criar uma conexão de público alvo usando a API de Serviço de Fluxo para especificar o conjunto de dados que conterá os dados de origem de entrada.

**Formato da API**

```https
POST /targetConnections
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "baseConnectionId": "44b1c1e43-a5ee-4d86-9c1e-43a5eebd8601",
        "name": "Target Connection for marketing automation",
        "description": "Target Connection for marketing automation",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/63f2c82fcdcb606c536a62d7716e34acbf63cd4582a1c16b",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5e9797ac6d771118ad8356db
        },
            "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `baseConnectionId` | A ID da conexão básica do conjunto de dados. |
| `data.schema.id` | A `$id` do schema XDM do público alvo. |
| `params.dataSetId` | A ID do conjunto de dados do público alvo. |
| `connectionSpec.id` | A ID de especificação de conexão para sua automação de marketing. |

>[!IMPORTANT] Ao criar uma conexão de público alvo, certifique-se de usar o valor de conexão base do conjunto de dados para a conexão básica em vez da ID de conexão do conector de origem de terceiros. `id`

```json
{
    "id": "fd82157f-0eea-4c81-8215-7f0eeaec8139",
    "etag": "\"5301d5ac-0000-0200-0000-5e97981a0000\""
}
```

## Criar um mapeamento {#mapping}

Para que os dados de origem sejam ingeridos em um conjunto de dados de público alvo, eles devem primeiro ser mapeados para o schema de público alvo ao qual o conjunto de dados de público alvo adere. Isso é obtido executando uma solicitação POST para a API de serviço de conversão com mapeamentos de dados definidos na carga da solicitação.

**Formato da API**

```https
POST /conversion/mappingSets
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/adobe_mcdp_connectors_stg/schemas/63f2c82fcdcb606c536a62d7716e34acbf63cd4582a1c16b",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "Properties_Firstname_Value",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "Properties_Lastname_Value",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "repositoryCreatedBy",
                "sourceAttribute": "Added_At",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Portal_Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `xdmSchema` | A ID do schema XDM do público alvo. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes do mapeamento recém-criado, incluindo seu identificador exclusivo (`id`). Armazene esse valor conforme necessário na etapa posterior para criar um fluxo de dados.

```json
{
    "id": "280a3cc950894945bf815c5fc60f3803",
    "version": 0,
    "createdDate": 1586993661034,
    "modifiedDate": 1586993661034,
    "createdBy": "28AF22BA5DE6B0B40A494036@AdobeID",
    "modifiedBy": "28AF22BA5DE6B0B40A494036@AdobeID"
}
```

## Pesquisar especificações de fluxo de dados {#specs}

Um dataflow é responsável por coletar dados de fontes e trazê-los para a Plataforma. Para criar um fluxo de dados, você deve primeiro obter as especificações do fluxo de dados responsáveis pela coleta de dados de automação de marketing.

**Formato da API**

```https
GET /flowSpecs?property=name=="CRMToAEP"
```

**Solicitação**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CRMToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da especificação de fluxo de dados responsável por trazer os dados do seu sistema de automação de marketing para a Plataforma. Armazene o valor do `id` campo conforme necessário na próxima etapa para criar um novo fluxo de dados.

```json
{
    "items": [
        {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "name": "CRMToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "transformationSpecs": [
                {
                    "name": "Copy",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "properties": {
                            "deltaColumn": {
                                "type": "object",
                                "properties": {
                                    "name": {
                                        "type": "string"
                                    },
                                    "dateFormat": {
                                        "type": "string"
                                    },
                                    "timezone": {
                                        "type": "string"
                                    }
                                },
                                "required": [
                                    "name"
                                ]
                            }
                        },
                        "required": [
                            "deltaColumn"
                        ]
                    }
                },
                {
                    "name": "Mapping",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines various params required for different mapping from source to target",
                        "properties": {
                            "mappingId": {
                                "type": "string"
                            },
                            "mappingVersion": {
                                "type": "string"
                            }
                        }
                    }
                }
            ],
            "scheduleSpec": {
                "name": "PeriodicSchedule",
                "type": "Periodic",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "startTime": {
                            "description": "epoch time",
                            "type": "integer"
                        },
                        "endTime": {
                            "description": "epoch time",
                            "type": "integer"
                        },
                        "interval": {
                            "type": "integer"
                        },
                        "frequency": {
                            "type": "string",
                            "enum": [
                                "minute",
                                "hour",
                                "day",
                                "week"
                            ]
                        },
                        "backfill": {
                            "type": "boolean",
                            "default": true
                        }
                    },
                    "required": [
                        "startTime",
                        "frequency",
                        "interval"
                    ],
                    "if": {
                        "properties": {
                            "frequency": {
                                "const": "minute"
                            }
                        }
                    },
                    "then": {
                        "properties": {
                            "interval": {
                                "minimum": 15
                            }
                        }
                    },
                    "else": {
                        "properties": {
                            "interval": {
                                "minimum": 1
                            }
                        }
                    }
                }
            }
        }
    ]
}
```

## Criar um fluxo de dados

A última etapa para coletar dados de automação de marketing é criar um fluxo de dados. Agora, você tem os seguintes valores obrigatórios preparados:

* [ID da conexão de origem](#source)
* [ID de conexão do Público alvo](#target)
* [ID de mapeamento](#mapping)
* [ID de especificação do fluxo de dados](#specs)

Um fluxo de dados é responsável por programar e coletar dados de uma fonte. Você pode criar um fluxo de dados executando uma solicitação POST enquanto fornece os valores mencionados anteriormente na carga.

**Formato da API**

```https
POST /flows
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dataflow for marketing automation",
        "description": "Dataflow for marketing automation",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "c315c0ae-a339-44c4-95c0-aea33964c420"
        ],
        "targetConnectionIds": [
            "fd82157f-0eea-4c81-8215-7f0eeaec8139"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "280a3cc950894945bf815c5fc60f3803",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "<START TIME>",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `flowSpec.id` | ID de especificação do Dataflow. |
| `sourceConnectionIds` | ID da conexão de origem. |
| `targetConnectionIds` | ID de conexão do Público alvo. |
| `transformations.params.mappingId` | ID de mapeamento. |

**Resposta**

Uma resposta bem-sucedida retorna a ID (`id`) do fluxo de dados recém-criado.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```

## Próximas etapas

Ao seguir este tutorial, você criou um conector de origem para coletar dados de um sistema de automação de marketing de forma programada. Os dados recebidos agora podem ser usados pelos serviços de plataforma downstream, como o Perfil do cliente em tempo real e a Área de trabalho de análise de dados. Consulte os seguintes documentos para obter mais detalhes:

* [Visão geral do Perfil do cliente em tempo real](../../../../profile/home.md)
* [Visão geral da Análise do espaço de trabalho da Data Science](../../../../data-science-workspace/home.md)