---
keywords: Experience Platform, home, tópicos populares, coletar o sucesso do cliente, sucesso do cliente
solution: Experience Platform
title: Criar um fluxo de dados para fontes de sucesso do cliente usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Este tutorial aborda as etapas para recuperar dados de um sistema bem-sucedido do cliente e assimilá-los na plataforma usando conectores de origem e APIs.
exl-id: 0fae04d0-164b-4113-a274-09677f4bbde5
source-git-commit: 93061c84639ca1fdd3f7abb1bbd050eb6eebbdd6
workflow-type: tm+mt
source-wordcount: '1327'
ht-degree: 2%

---

# Crie um fluxo de dados para fontes de sucesso do cliente usando o [!DNL Flow Service] API

Este tutorial aborda as etapas para recuperar dados de uma fonte de sucesso do cliente e trazê-los para a Platform usando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>Para criar um fluxo de dados, você já deve ter uma ID de conexão base válida com uma fonte de sucesso do cliente. Se você não tiver essa ID, consulte a [visão geral das fontes](../../../home.md#customer-success) para obter uma lista de fontes de sucesso do cliente com as quais você pode criar uma conexão básica.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Guia do desenvolvedor do Registro de Schema](../../../../xdm/api/getting-started.md): Inclui informações importantes que você precisa saber para executar com sucesso chamadas para a API do Registro de Esquema. Isso inclui as `{TENANT_ID}`, o conceito de &quot;contêineres&quot; e os cabeçalhos necessários para fazer solicitações (com especial atenção ao cabeçalho Accept e seus possíveis valores).
* [[!DNL Catalog Service]](../../../../catalog/home.md): Catálogo é o sistema de registro para localização de dados e linhagem dentro [!DNL Experience Platform].
* [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md): A API de assimilação em lote permite assimilar dados no [!DNL Experience Platform] como arquivos em lote.
* [Sandboxes](../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../../landing/api-guide.md).

## Criar uma conexão de origem {#source}

Você pode criar uma conexão de origem fazendo uma solicitação de POST para o [!DNL Flow Service] API. Uma conexão de origem consiste em uma ID de conexão, um caminho para o arquivo de dados de origem e uma ID de especificação de conexão.

Para criar uma conexão de origem, você também deve definir um valor enum para o atributo de formato de dados.

Use os seguintes valores enum para conectores baseados em arquivo:

| Formato dos dados | Valor de enumeração |
| ----------- | ---------- |
| Delimitado | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Para todos os conectores baseados em tabela, defina o valor `tabular`.

**Formato da API**

```http
POST /sourceConnections
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Source connection for Customer Success",
        "baseConnectionId": "f1da3694-38a9-403d-9a36-9438a9203d42",
        "description": "Source connection for a Customer Success connector",
        "data": {
            "format": "tabular",
        },
        "params": {
            "tableName": "Account",
            "columns": [
                {
                    "name": "Id",
                    "type": "string",
                    "xdm": {
                        "type": "string"
                    }
                },
                {
                    "name": "Name",
                    "type": "string",
                    "xdm": {
                        "type": "string"
                    }
                },
                {
                    "name": "Phone",
                    "type": "string",
                    "xdm": {
                        "type": "string"
                    }
                },
                {
                    "name": "CreatedDate",
                    "type": "string",
                    "meta:xdmType": "date-time",
                    "xdm": {
                        "type": "string",
                        "format": "date-time"
                    }
                }
            ]
        },
        "connectionSpec": {
            "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `baseConnectionId` | A ID de conexão exclusiva do sistema bem-sucedido do cliente de terceiros que você está acessando. |
| `params.path` | O caminho do arquivo de origem. |
| `connectionSpec.id` | A ID de especificação de conexão associada ao sistema de sucesso específico de clientes de terceiros. Consulte a [apêndice](#appendix) para obter uma lista de IDs de especificação de conexão. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada. Essa ID é necessária em etapas posteriores para criar uma conexão de destino.

```json
{
    "id": "17faf955-2cf8-4b15-baf9-552cf88b1540",
    "etag": "\"2900a761-0000-0200-0000-5ed18cea0000\""
}
```

## Criar um esquema XDM de destino {#target-schema}

Para que os dados de origem sejam usados na Platform, um schema de target deve ser criado para estruturar os dados de origem de acordo com suas necessidades. O schema de destino é usado para criar um conjunto de dados da plataforma no qual os dados de origem estão contidos.

Um esquema XDM de destino pode ser criado executando-se uma solicitação de POST para a [API do Registro de Schema](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Para obter etapas detalhadas sobre como criar um esquema XDM de destino, consulte o tutorial em [criação de um schema usando a API](../../../../xdm/api/schemas.md).

## Criar um conjunto de dados de destino {#target-dataset}

Um conjunto de dados de destino pode ser criado executando uma solicitação de POST para a [API do Serviço de catálogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), fornecendo a ID do schema do target no payload.

Para obter etapas detalhadas sobre como criar um conjunto de dados de destino, consulte o tutorial em [criação de um conjunto de dados usando a API](../../../../catalog/api/create-dataset.md).

## Criar uma conexão de destino {#target-connection}

Uma conexão target representa a conexão com o destino onde os dados assimilados chegam. Para criar uma conexão de destino, você deve fornecer a ID de especificação de conexão fixa associada ao Data Lake. Essa ID de especificação de conexão é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Agora você tem os identificadores exclusivos em um esquema de destino em um conjunto de dados de destino e a ID de especificação de conexão em um lago de dados. Usar o [!DNL Flow Service] Você pode criar uma conexão de destino especificando esses identificadores junto com o conjunto de dados que conterá os dados de origem de entrada.

**Formato da API**

```http
POST /targetConnections
```

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Target Connection for a customer success connector",
        "description": "Target Connection for a customer success connector",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/deb3e1096c35d8311b5d80868c4bd5b3cdfd4b3150e7345f",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5e543e8a60b15218ad44b95f"
        },
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `data.schema.id` | O `$id` do esquema XDM de destino. |
| `data.schema.version` | A versão do schema. Este valor deve ser definido `application/vnd.adobe.xed-full+json;version=1`, que retorna a versão secundária mais recente do esquema. |
| `params.dataSetId` | A ID do conjunto de dados de destino. |
| `connectionSpec.id` | A ID de especificação de conexão usada para conexão com o Data Lake. Essa ID é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo da nova conexão de destino (`id`). Esse valor é necessário em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "1f5af99c-f1ef-4076-9af9-9cf1ef507678",
    "etag": "\"530013e2-0000-0200-0000-5ebc4c110000\""
}
```

## Criar um mapeamento {#mapping}

Para que os dados de origem sejam assimilados em um conjunto de dados de destino, eles devem primeiro ser mapeados para o schema de destino ao qual o conjunto de dados de destino adere.

Para criar um conjunto de mapeamento, faça uma solicitação de POST para a função `mappingSets` endpoint da variável [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) ao fornecer seu esquema XDM de destino `$id` e os detalhes dos conjuntos de mapeamento que deseja criar.

**Formato da API**

```http
POST /mappingSets
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/b750bd161fef405bc324d0c8809b02c494d73e60e7ae9b3e",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.fullName",
                "sourceAttribute": "Name",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_repo.createDate",
                "sourceAttribute": "CreatedDate",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `xdmSchema` | O `$id` do esquema XDM de destino. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes do mapeamento recém-criado, incluindo seu identificador exclusivo (`id`). Essa ID é necessária em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "7c3547d3cfc14f568a51c32b4c0ed739",
    "version": 0,
    "createdDate": 1590792069173,
    "modifiedDate": 1590792069173,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Recuperar especificações do fluxo de dados {#specs}

Um fluxo de dados é responsável por coletar dados de fontes e trazê-los para a plataforma. Para criar um fluxo de dados, primeiro obtenha as especificações do fluxo de dados executando uma solicitação do GET para a API do Serviço de fluxo. As especificações de fluxo de dados são responsáveis por coletar dados de um sistema bem-sucedido de clientes de terceiros.

**Formato da API**

```http
GET /flowSpecs?property=name=="CRMToAEP"
```

**Solicitação**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="CRMToAEP"' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da especificação de fluxo de dados responsável por trazer os dados da fonte para a Plataforma. A resposta inclui as especificações exclusivas de fluxo `id` necessário para criar um novo fluxo de dados.

```json
{
    "items": [
        {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "name": "CRMToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "3416976c-a9ca-4bba-901a-1f08f66978ff",
                "38ad80fe-8b06-4938-94f4-d4ee80266b07",
                "d771e9c1-4f26-40dc-8617-ce58c4b53702",
                "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
                "3000eb99-cd47-43f3-827c-43caf170f015",
                "26d738e0-8963-47ea-aadf-c60de735468a",
                "74a1c565-4e59-48d7-9d67-7c03b8a13137",
                "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
                "cb66ab34-8619-49cb-96d1-39b37ede86ea",
                "eb13cb25-47ab-407f-ba89-c0125281c563",
                "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
                "37b6bf40-d318-4655-90be-5cd6f65d334b",
                "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
                "221c7626-58f6-4eec-8ee2-042b0226f03b",
                "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
                "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
                "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
                "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
                "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
                "102706fb-a5cd-42ee-afe0-bc42f017ff43",
                "09182899-b429-40c9-a15a-bf3ddbc8ced7",
                "0479cc14-7651-4354-b233-7480606c2ac3",
                "d6b52d86-f0f8-475f-89d4-ce54c8527328",
                "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
                "1fe283f6-9bec-11ea-bb37-0242ac130002"
            ],
            "targetConnectionSpecIds": [
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
            ],
            "optionSpec": {
                "name": "OptionSpec",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "errorDiagnosticsEnabled": {
                            "title": "Error diagnostics.",
                            "description": "Flag to enable detailed and sample error diagnostics summary.",
                            "type": "boolean",
                            "default": false
                        },
                        "partialIngestionPercent": {
                            "title": "Partial ingestion threshold.",
                            "description": "Percentage which defines the threshold of errors allowed before the run is marked as failed.",
                            "type": "number",
                            "exclusiveMinimum": 0
                        }
                    }
                }
            },
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
                        "frequency": {
                            "type": "string",
                            "enum": [
                                "once",
                                "minute",
                                "hour",
                                "day",
                                "week"
                            ]
                        },
                        "interval": {
                            "type": "integer"
                        },
                        "backfill": {
                            "type": "boolean",
                            "default": true
                        }
                    },
                    "required": [
                        "startTime",
                        "frequency"
                    ],
                    "if": {
                        "properties": {
                            "frequency": {
                                "const": "once"
                            }
                        }
                    },
                    "then": {
                        "allOf": [
                            {
                                "not": {
                                    "required": [
                                        "interval"
                                    ]
                                }
                            },
                            {
                                "not": {
                                    "required": [
                                        "backfill"
                                    ]
                                }
                            }
                        ]
                    },
                    "else": {
                        "required": [
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
            },
            "attributes": {
                "notification": {
                    "category": "sources",
                    "flowRun": {
                        "enabled": true
                    }
                }
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        }
    ]
}
```

## Criar um fluxo de dados

A última etapa para coletar dados é criar um fluxo de dados. Neste ponto, você deve preparar os seguintes valores obrigatórios:

* [ID de conexão de origem](#source)
* [ID de conexão do Target](#target)
* [ID de mapeamento](#mapping)
* [ID de especificação do fluxo de dados](#specs)

Para agendar uma assimilação, primeiro defina o valor de hora de início como época em segundos. Em seguida, você deve definir o valor de frequência para uma das cinco opções: `once`, `minute`, `hour`, `day`ou `week`. O valor de intervalo designa o período entre duas ingestões consecutivas e a criação de uma ingestão única não requer a definição de um intervalo. Para todas as outras frequências, o valor do intervalo deve ser definido como igual ou superior a `15`.

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
        "name": "Creating a dataflow for a Customer Success connector",
        "description": "Creating a dataflow for a Customer Success connector",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "17faf955-2cf8-4b15-baf9-552cf88b1540"
        ],
        "targetConnectionIds": [
            "bc36ecd6-3b04-4067-b6ec-d63b04b0673d"
        ],
        "transformations": [
            {
                "name": "Copy",
                "params": {
                    "deltaColumn": {
                        "name": "updatedAt",
                        "dateFormat": "YYYY-MM-DD",
                        "timezone": "UTC"
                    }
                }
            },
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "7c3547d3cfc14f568a51c32b4c0ed739",
                    "mappingVersion": 0
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1590792316",
            "frequency": "minute",
            "interval": "15",
            "backfill": "true"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `flowSpec.id` | O [ID de especificação de fluxo](#specs) recuperada na etapa anterior. |
| `sourceConnectionIds` | O [ID de conexão de origem](#source) recuperada em uma etapa anterior. |
| `targetConnectionIds` | O [target connection ID](#target-connection) recuperada em uma etapa anterior. |
| `transformations.params.mappingId` | O [ID de mapeamento](#mapping) recuperada em uma etapa anterior. |
| `transformations.params.deltaColum` | A coluna designada usada para diferenciar dados novos e existentes. Os dados incrementais serão assimilados com base no carimbo de data e hora da coluna selecionada. O formato de data compatível para `deltaColumn` é `yyyy-MM-dd HH:mm:ss`. |
| `transformations.params.mappingId` | A ID de mapeamento associada ao banco de dados. |
| `scheduleParams.startTime` | A hora de início do fluxo de dados em época. |
| `scheduleParams.frequency` | A frequência com que o fluxo de dados coletará dados. Os valores aceitáveis incluem: `once`, `minute`, `hour`, `day`ou `week`. |
| `scheduleParams.interval` | O intervalo designa o período entre duas execuções consecutivas de fluxo. O valor do intervalo deve ser um número inteiro diferente de zero. O intervalo não é necessário quando a frequência é definida como `once` e deve ser maior que ou igual a `15` para outros valores de frequência. |

**Resposta**

Uma resposta bem-sucedida retorna a ID `id` do fluxo de dados recém-criado.

```json
{
    "id": "e0bd8463-0913-4ca1-bd84-6309134ca1f6",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

## Monitorar o fluxo de dados

Depois que o fluxo de dados tiver sido criado, você poderá monitorar os dados que estão sendo assimilados por meio dele para ver informações sobre execuções de fluxo, status de conclusão e erros. Para obter mais informações sobre como monitorar fluxos de dados, consulte o tutorial em [monitoramento de fluxos de dados na API ](../monitor.md)

## Próximas etapas

Ao seguir este tutorial, você criou um conector de origem para coletar dados de um sistema bem-sucedido do cliente de forma agendada. Os dados recebidos agora podem ser usados pelo downstream [!DNL Platform] serviços como [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Consulte os seguintes documentos para obter mais detalhes:

* [Visão geral do perfil do cliente em tempo real](../../../../profile/home.md)
* [Visão geral do Data Science Workspace](../../../../data-science-workspace/home.md)

## Apêndice

A seção a seguir lista os diferentes conectores de origem de armazenamento em nuvem e suas especificações de conexões.

### Especificação de conexão

| Nome do conector | Especificação de conexão |
| -------------- | --------------- |
| [!DNL Salesforce Service Cloud] | `cb66ab34-8619-49cb-96d1-39b37ede86ea` |
| [!DNL ServiceNow] | `eb13cb25-47ab-407f-ba89-c0125281c563` |
