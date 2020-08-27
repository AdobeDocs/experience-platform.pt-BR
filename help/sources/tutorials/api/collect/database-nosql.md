---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Coletar dados de um banco de dados de terceiros por meio de conectores de origem e APIs
topic: overview
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '1745'
ht-degree: 1%

---


# Coletar dados de um banco de dados de terceiros por meio de conectores de origem e APIs

[O [!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) é usado para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial aborda as etapas para recuperar dados de um banco de dados de terceiros e assimilá-los [!DNL Platform] por meio de conectores de origem e APIs.

## Introdução

Este tutorial requer uma conexão válida com um banco de dados de terceiros, bem como informações sobre o arquivo que você deseja trazer [!DNL Platform] (incluindo o caminho e a estrutura do arquivo). Se você não tiver essas informações, consulte o tutorial sobre como [explorar um banco de dados usando a API](../explore/database-nosql.md) do Serviço de Fluxo antes de tentar este tutorial.

Este tutorial também exige que você tenha uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema](../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Guia](../../../../xdm/api/getting-started.md)do desenvolvedor do Registro do schema: Inclui informações importantes que você precisa saber para executar com êxito chamadas para a API do Registro do Schema. Isso inclui seu `{TENANT_ID}`, o conceito de &quot;container&quot; e os cabeçalhos necessários para fazer solicitações (com atenção especial ao cabeçalho Accept e seus possíveis valores).
* [Serviço](../../../../catalog/home.md)de catálogo: Catálogo é o sistema de registro para localização e linhagem de dados dentro [!DNL Experience Platform].
* [Ingestão](../../../../ingestion/batch-ingestion/overview.md)em lote: A API de ingestão em lote permite que você ingira dados [!DNL Experience Platform] como arquivos em lote.
* [Caixas de proteção](../../../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a um banco de dados de terceiros usando a API [[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) .

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de [!DNL Experience Platform] solução de problemas.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o tutorial [de](../../../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de [!DNL Experience Platform] API, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo os pertencentes a [!DNL Flow Service], são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

## Criar uma classe e um schema XDM ad hoc

Para trazer dados externos para dentro [!DNL Platform] por meio de conectores de origem, uma classe e um schema XDM ad-hoc devem ser criados para os dados de fonte bruta.

Para criar uma classe e um schema ad-hoc, siga as etapas descritas no tutorial [do schema](../../../../xdm/tutorials/ad-hoc.md)ad-hoc. Ao criar uma classe ad-hoc, todos os campos encontrados nos dados de origem devem ser descritos no corpo da solicitação.

Continue seguindo as etapas descritas no guia do desenvolvedor até que você tenha criado um schema ad-hoc. Obtenha e armazene o identificador exclusivo (`$id`) do schema ad-hoc e prossiga para a próxima etapa deste tutorial.

## Criar uma conexão de origem {#source}

Com um schema XDM ad-hoc criado, uma conexão de origem agora pode ser criada usando uma solicitação POST para a [!DNL Flow Service] API. Uma conexão de origem consiste em uma ID de conexão, um arquivo de dados de origem e uma referência ao schema que descreve os dados de origem.

Para criar uma conexão de origem, você também deve definir um valor enum para o atributo de formato de dados.

Use os seguintes valores enum para conectores **baseados em** arquivo:

| Data.format | Valor Enum |
| ----------- | ---------- |
| Arquivos delimitados | `delimited` |
| Arquivos JSON | `json` |
| Arquivos de parâmetro | `parquet` |

Para todos os conectores **baseados em** tabela, use o valor enum: `tabular`.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Database Source Connector",
        "baseConnectionId": "d5cbb5bc-44cc-41a2-8bb5-bc44ccf1a2fb",
        "description": "A test source connector for a third-party database",
        "data": {
            "format": "tabular",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/21b30fa2c00a2a8d7c3010272dffa16d3cc9eec504aa6c7",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "ADMIN.E2E"
        },
        "connectionSpec": {
            "id": "d6b52d86-f0f8-475f-89d4-ce54c8527328",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `baseConnectionId` | A ID de conexão da fonte de banco de dados de terceiros. |
| `data.schema.id` | A `$id` do schema XDM ad-hoc. |
| `params.path` | O caminho do arquivo de origem. |
| `connectionSpec.id` | A ID de especificação de conexão da fonte de banco de dados de terceiros. Consulte o [Apêndice](#appendix) para obter uma lista das IDs de especificações do banco de dados. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada. Essa ID é necessária em etapas posteriores para criar uma conexão de público alvo.

```json
{
    "id": "2f7356d9-a866-47ea-b356-d9a86687ea7a",
    "etag": "\"c8006055-0000-0200-0000-5ecd79520000\""
}
```

## Criar um schema XDM de público alvo {#target-schema}

Em etapas anteriores, um schema XDM ad-hoc foi criado para estruturar os dados de origem. Para que os dados de origem sejam usados em [!DNL Platform], um schema de público alvo também deve ser criado para estruturar os dados de origem de acordo com suas necessidades. O schema do público alvo é então usado para criar um [!DNL Platform] conjunto de dados no qual os dados de origem estão contidos. Esse schema XDM do público alvo também estende a [!DNL XDM Individual Profile] classe.

É possível criar um schema XDM de público alvo, executando uma solicitação POST para a API [do Registro de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)Schemas. Se você preferir usar a interface do usuário no [!DNL Experience Platform], o tutorial [do Editor de](../../../../xdm/tutorials/create-schema-ui.md) Schemas fornece instruções passo a passo para executar ações semelhantes no Editor de Schemas.

**Formato da API**

```http
POST /tenant/schemas
```

**Solicitação**

A solicitação de exemplo a seguir cria um schema XDM que estende a [!DNL Individual Profile] classe XDM.

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
        "title": "Database Source Connector Target Schema",
        "description": "Target schema for a third-party database",
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

Uma resposta bem-sucedida retorna detalhes do schema recém-criado, incluindo seu identificador exclusivo (`$id`). Essa ID é necessária em etapas posteriores para criar um conjunto de dados de público alvo, mapeamento e fluxo de dados.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/c44dd18673370dbf16243ba6e6fd9ae62c7916ec10477727",
    "meta:altId": "_{TENANT_ID}.schemas.c44dd18673370dbf16243ba6e6fd9ae62c7916ec10477727",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for an Oracle connector 5/26/20",
    "type": "object",
    "description": "Target schema for Database",
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
        "repo:createdDate": 1590523478581,
        "repo:lastModifiedDate": 1590523478581,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "34fdf36fc3029999a07270c4e7719d8a627f7e93e2fbc13888b3c11fb08983c0",
        "meta:globalLibVersion": "1.10.2.1"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Criar um conjunto de dados de público alvo

É possível criar um conjunto de dados de público alvo executando uma solicitação de POST para a API [do serviço de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)catálogo, fornecendo a ID do schema de público alvo dentro da carga.

**Formato da API**

```http
POST /dataSets
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
        "name": "Target dataset for a third-party database source connector",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c44dd18673370dbf16243ba6e6fd9ae62c7916ec10477727",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `schemaRef.id` | A ID do schema XDM do público alvo. |

**Resposta**

Uma resposta bem-sucedida retorna uma matriz que contém a ID do conjunto de dados recém-criado no formato `"@/datasets/{DATASET_ID}"`. A ID do conjunto de dados é uma sequência de caracteres somente leitura, gerada pelo sistema, usada para fazer referência ao conjunto de dados em chamadas de API. Armazene a ID do conjunto de dados do público alvo conforme necessário em etapas posteriores para criar uma conexão de público alvo e um fluxo de dados.

```json
[
    "@/dataSets/5ecd766e4bab17191b78e892"
]
```

## Criar uma conexão de público alvo {#target-connection}

Agora você tem os identificadores exclusivos para uma conexão básica de conjunto de dados, um schema de público alvo e um conjunto de dados de público alvo. Usando esses identificadores, você pode criar uma conexão de público alvo usando a API [[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) para especificar o conjunto de dados que conterá os dados de origem de entrada.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Target Connection for a third-party database source connector",
        "description": "Target Connection for a third-party database source connector",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c44dd18673370dbf16243ba6e6fd9ae62c7916ec10477727",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5ecd766e4bab17191b78e892"
        },
            "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `data.schema.id` | A `$id` do schema XDM do público alvo. |
| `params.dataSetId` | A ID do conjunto de dados do público alvo reunido na etapa anterior. |
| `connectionSpec.id` | A ID de especificação de conexão fixa para o registro de dados. Esta ID de especificação de conexão é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da nova conexão com o público alvo. Esse valor é necessário em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "e66fdb22-06df-48ac-afdb-2206dff8ac10",
    "etag": "\"7e03773a-0000-0200-0000-5ecd768d0000\""
}
```

## Criar um mapeamento {#mapping}

Para que os dados de origem sejam ingeridos em um conjunto de dados de público alvo, eles devem primeiro ser mapeados para o schema de público alvo ao qual o conjunto de dados de público alvo adere. Isso é feito executando uma solicitação POST para a [!DNL Conversion Service] API com mapeamentos de dados definidos na carga da solicitação.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c44dd18673370dbf16243ba6e6fd9ae62c7916ec10477727",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "person.name.fullName",
                "sourceAttribute": "NAME",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_repo.createDate",
                "sourceAttribute": "DOB",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "ID",
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
| `xdmSchema` | A `$id` do schema XDM do público alvo. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes do mapeamento recém-criado, incluindo seu identificador exclusivo (`id`). Essa ID é necessária em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "d9d94124417d4df48ea3d00e28eb4327",
    "version": 0,
    "createdDate": 1590523552440,
    "modifiedDate": 1590523552440,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Recuperar especificações de fluxo de dados {#specs}

Um dataflow é responsável por coletar dados de fontes e trazê-los para [!DNL Platform]. Para criar um fluxo de dados, primeiro você deve obter as especificações do fluxo de dados executando uma solicitação de GET para a API [[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) . As especificações de fluxo de dados são responsáveis por coletar dados de um banco de dados externo ou de um sistema NoSQL.

**Formato da API**

```http
GET /flowSpecs?property=name=="CRMToAEP"
```

**Solicitação**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="CRMToAEP"' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da especificação de fluxo de dados responsável por trazer dados do banco de dados ou do sistema NoSQL para [!DNL Platform]. Essa ID é necessária na próxima etapa para criar um novo fluxo de dados.

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

A última etapa para coletar dados é criar um fluxo de dados. Neste ponto, você deve ter os seguintes valores obrigatórios preparados:

* [ID da conexão de origem](#source)
* [ID de conexão do público alvo](#target)
* [ID de mapeamento](#mapping)
* [ID de especificação do fluxo de dados](#specs)

Um fluxo de dados é responsável por programar e coletar dados de uma fonte. Você pode criar um fluxo de dados executando uma solicitação de POST ao fornecer os valores mencionados anteriormente dentro da carga.

Para agendar uma ingestão, é necessário primeiro definir o valor de tempo do start para cada tempo em segundos. Em seguida, você deve definir o valor de frequência para uma das cinco opções: `once`, `minute`, `hour`, `day`ou `week`. O valor do intervalo designa o período entre duas ingestões consecutivas e a criação de uma ingestão única não requer a definição de um intervalo. Para todas as outras frequências, o valor do intervalo deve ser definido como igual ou maior que `15`.

**Formato da API**

```http
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
        "name": "Dataflow for a third-party database and Platform,
        "description": "collecting ADMIN.E2E",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "89cf81c9-47b4-463a-8f81-c947b4863afb"
        ],
        "targetConnectionIds": [
            "e66fdb22-06df-48ac-afdb-2206dff8ac10"
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
                    "mappingId": "d9d94124417d4df48ea3d00e28eb4327",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1590523836",
            "frequency":"minute",
            "interval":"15",
            "backfill": "true"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `flowSpec.id` | A ID [de especificação de](#specs) fluxo recuperada na etapa anterior. |
| `sourceConnectionIds` | A ID [de conexão](#source) de origem recuperada em uma etapa anterior. |
| `targetConnectionIds` | A ID [de conexão do](#target-connection) público alvo recuperada em uma etapa anterior. |
| `transformations.params.mappingId` | A ID [de](#mapping) mapeamento recuperada em uma etapa anterior. |
| `transformations.params.deltaColum` | A coluna designada usada para diferenciar entre dados novos e existentes. Os dados incrementais serão ingeridos com base no carimbo de data e hora da coluna selecionada. O formato de data suportado para `deltaColumn` é `yyyy-MM-dd HH:mm:ss`. Se você estiver usando o Armazenamento de Tabela do Azure, o formato suportado para `deltaColumn` será `yyyy-MM-ddTHH:mm:ssZ`. |
| `transformations.params.mappingId` | A ID de mapeamento associada ao banco de dados. |
| `scheduleParams.startTime` | A hora de start do fluxo de dados em cada época. |
| `scheduleParams.frequency` | A frequência com que o fluxo de dados coletará dados. Os valores aceitáveis incluem: `once`, `minute`, `hour`, `day`ou `week`. |
| `scheduleParams.interval` | O intervalo designa o período entre duas execuções consecutivas de fluxo. O valor do intervalo deve ser um número inteiro diferente de zero. O intervalo não é necessário quando a frequência é definida como `once` e deve ser maior ou igual a `15` outros valores de frequência. |

**Resposta**

Uma resposta bem-sucedida retorna a ID (`id`) do fluxo de dados recém-criado.

```json
{
    "id": "e0bd8463-0913-4ca1-bd84-6309134ca1f6",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

## Monitore seu fluxo de dados

Depois que seu fluxo de dados for criado, você poderá monitorar os dados que estão sendo assimilados por ele para ver informações sobre execuções de fluxo, status de conclusão e erros. Para obter mais informações sobre como monitorar fluxos de dados, consulte o tutorial sobre como [monitorar fluxos de dados na API ](../monitor.md)


## Próximas etapas

Ao seguir este tutorial, você criou um conector de origem para coletar dados de um banco de dados de terceiros de forma programada. Os dados recebidos agora podem ser usados por [!DNL Platform] serviços de downstream, como [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Consulte os seguintes documentos para obter mais detalhes:

* [Visão geral do Perfil do cliente em tempo real](../../../../profile/home.md)
* [Visão geral da Análise do espaço de trabalho da Data Science](../../../../data-science-workspace/home.md)

## Apêndice

A seção a seguir lista os diferentes conectores de origem do armazenamento de nuvem e suas especificações de conexões.

### Especificação da conexão

| Nome do conector | ID de especificação da conexão |
| -------------- | --------------- |
| [!DNL Amazon Redshift] | `3416976c-a9ca-4bba-901a-1f08f66978ff` |
| [!DNL Apache Hive] em [!DNL Azure HDInsights] | `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f` |
| [!DNL Apache Spark] em [!DNL Azure HDInsights] | `6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |
| [!DNL Azure Data Explorer] | `0479cc14-7651-4354-b233-7480606c2ac3` |
| [!DNL Azure Synapse Analytics] | `a49bcc7d-8038-43af-b1e4-5a7a089a7d79` |
| [!DNL Azure Table Storage] | `ecde33f2-c56f-46cc-bdea-ad151c16cd69` |
| [!DNL CouchBase] | `1fe283f6-9bec-11ea-bb37-0242ac130002` |
| [!DNL Google BigQuery] | `3c9b37f8-13a6-43d8-bad3-b863b941fedd` |
| [!DNL IBM DB2] | `09182899-b429-40c9-a15a-bf3ddbc8ced7` |
| [!DNL MariaDB] | `000eb99-cd47-43f3-827c-43caf170f015` |
| [!DNL Microsoft SQL Server] | `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec` |
| [!DNL MySQL] | `26d738e0-8963-47ea-aadf-c60de735468a` |
| [!DNL Oracle] | `d6b52d86-f0f8-475f-89d4-ce54c8527328` |
| [!DNL Phoenix] | `102706fb-a5cd-42ee-afe0-bc42f017ff43` |
| [!DNL PostgreSQL] | `74a1c565-4e59-48d7-9d67-7c03b8a13137` |