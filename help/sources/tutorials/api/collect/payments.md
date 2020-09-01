---
keywords: Experience Platform;home;popular topics;Collect payment data;payment data
solution: Experience Platform
title: Coletar dados de pagamento por meio de conectores de origem e APIs
topic: overview
description: Este tutorial aborda as etapas para recuperar dados de um aplicativo de pagamentos e assimilá-los na Plataforma por meio de conectores de origem e APIs.
translation-type: tm+mt
source-git-commit: 6f4714561c2946a084eed4e89d3148df5b8044f5
workflow-type: tm+mt
source-wordcount: '1743'
ht-degree: 2%

---


# Coletar dados de pagamento por meio de conectores de origem e APIs

[!DNL Flow Service] é usada para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial aborda as etapas para recuperar dados de um sistema de pagamento de terceiros e assimilá-los [!DNL Platform] por meio de conectores de origem e da API [[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) .

## Introdução

Este tutorial requer que você tenha acesso a um sistema de pagamento por meio de uma conexão válida, bem como informações sobre o arquivo que deseja inserir [!DNL Platform] (incluindo o caminho e a estrutura do arquivo). Se você não tiver essas informações, consulte o tutorial sobre como [explorar um aplicativo de pagamentos usando a API](../explore/payments.md) de Serviço de Fluxo antes de tentar este tutorial.

Este tutorial também exige que você tenha uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema do [!DNL Experience Data Model (XDM)](../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Guia](../../../../xdm/api/getting-started.md)do desenvolvedor do Registro do schema: Inclui informações importantes que você precisa saber para executar com êxito chamadas para a API do Registro do Schema. Isso inclui seu `{TENANT_ID}`, o conceito de &quot;container&quot; e os cabeçalhos necessários para fazer solicitações (com atenção especial ao cabeçalho Accept e seus possíveis valores).
* [[!DNL Catalog Service]](../../../../catalog/home.md): Catálogo é o sistema de registro para localização e linhagem de dados dentro [!DNL Experience Platform].
* [[!DNL ingestão em lote]](../../../../ingestion/batch-ingestion/overview.md): A API de ingestão em lote permite que você ingira dados [!DNL Experience Platform] como arquivos em lote.
* [Caixas de proteção](../../../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a um aplicativo de pagamentos usando a [!DNL Flow Service] API.

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
        "name": "Paypal source connection",
        "baseConnectionId": "24151d58-ffa7-4960-951d-58ffa7396097",
        "description": "Paypal",
        "data": {
            "format": "tabular",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/396f583b57577b2f2fca79c2cb88e9254992f5fa70ce5f1a",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "PayPal.Catalog_Products"
        },
        "connectionSpec": {
            "id": "221c7626-58f6-4eec-8ee2-042b0226f03b",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `baseConnectionId` | A ID de conexão exclusiva do aplicativo de pagamentos de terceiros que você está acessando. |
| `data.schema.id` | A `$id` do schema XDM ad-hoc. |
| `params.path` | O caminho do arquivo de origem. |
| `connectionSpec.id` | A ID da especificação de conexão do aplicativo de pagamento. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada. Essa ID é necessária em etapas posteriores para criar uma conexão de público alvo.

```json
{
    "id": "2c48a152-3d49-43cb-88a1-523d49e3cbcb",
    "etag": "\"8000c843-0000-0200-0000-5e8917ea0000\""
}
```

## Criar um schema XDM de público alvo {#target-schema}

Em etapas anteriores, um schema XDM ad-hoc foi criado para estruturar os dados de origem. Para que os dados de origem sejam usados em [!DNL Platform], um schema de público alvo também deve ser criado para estruturar os dados de origem de acordo com suas necessidades. O schema do público alvo é então usado para criar um [!DNL Platform] conjunto de dados no qual os dados de origem estão contidos. Esse schema XDM do público alvo também estende a classe XDM. [!DNL Individual Profile]

É possível criar um schema XDM de público alvo, executando uma solicitação POST para a API [do Registro de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)Schemas. Se você preferir usar a interface do usuário no [!DNL Experience Platform], o tutorial [do Editor de](https://docs.adobe.com/content/help/pt-BR/experience-platform/xdm/tutorials/create-schema-ui.html) Schemas fornece instruções passo a passo para executar ações semelhantes no Editor de Schemas.

**Formato da API**

```https
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
        "title": "Target schema for payments",
        "description": "Target schema for payments",
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

Uma resposta bem-sucedida retorna detalhes do schema recém-criado, incluindo seu identificador exclusivo (`$id`). Essa ID é necessária em etapas posteriores para criar um conjunto de dados de público alvo, mapeamento e fluxo de dados.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/14d89c5bb88e2ff488f23db896be469e7e30bb166bda8722",
    "meta:altId": "_{TENANT_ID}.schemas.14d89c5bb88e2ff488f23db896be469e7e30bb166bda8722",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for payments",
    "type": "object",
    "description": "Target schema for Paypal",
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
        "repo:createdDate": 1586042956286,
        "repo:lastModifiedDate": 1586042956286,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "952e8912724d7f43cbc1471e3987bc5b6899519c186126b7c50619f2dddf8650"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Criar um conjunto de dados de público alvo

É possível criar um conjunto de dados de público alvo executando uma solicitação de POST para a API [do serviço de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)catálogo, fornecendo a ID do schema de público alvo dentro da carga.

**Formato da API**

```https
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
        "name": "Target dataset for payments",
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
    "@/dataSets/5e8918669cbbee18ad9771f3"
]
```

## Criar uma conexão de público alvo {#target-connection}

Uma conexão de público alvo representa a conexão com o destino onde os dados ingeridos chegam. Para criar uma conexão de público alvo, é necessário fornecer a ID de especificação de conexão fixa associada ao registro de dados. Esta ID de especificação de conexão é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Agora você tem os identificadores exclusivos de um schema de público alvo de um conjunto de dados de público alvo e a ID de especificação de conexão para o registro de dados. Usando esses identificadores, é possível criar uma conexão de público alvo usando a [!DNL Flow Service] API para especificar o conjunto de dados que conterá os dados de origem de entrada.

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
        "name": "Target Connection for payments",
        "description": "Target Connection for payments",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/14d89c5bb88e2ff488f23db896be469e7e30bb166bda8722"
            }
        },
        "params": {
            "dataSetId": "5e8918669cbbee18ad9771f3"
        },
            "connectionSpec": {
            "id": "221c7626-58f6-4eec-8ee2-042b0226f03b",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `data.schema.id` | A `$id` do schema XDM do público alvo. |
| `params.dataSetId` | A ID do conjunto de dados do público alvo. |
| `connectionSpec.id` | A ID de especificação de conexão fixa para o registro de dados. Esta ID é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da nova conexão com o público alvo. Esse valor é necessário em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "c8e12917-ac33-44d7-a129-17ac3364d7b7",
    "etag": "\"0f015874-0000-0200-0000-5e8918e60000\""
}
```

## Criar um mapeamento {#mapping}

Para que os dados de origem sejam ingeridos em um conjunto de dados de público alvo, eles devem primeiro ser mapeados para o schema de público alvo ao qual o conjunto de dados de público alvo adere. Isso é feito executando uma solicitação POST para a API [do Serviço de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/mapping-service-api.yaml) conversão com mapeamentos de dados definidos na carga da solicitação.

**Formato da API**

```https
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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/14d89c5bb88e2ff488f23db896be469e7e30bb166bda8722",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Product_Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "product.name",
                "sourceAttribute": "Product_Name",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "product.description",
                "sourceAttribute": "Description",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "product.type",
                "sourceAttribute": "Type",
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
    "id": "b54a8dc38e8d4e31a2dc096e413ae8e5",
    "version": 0,
    "createdDate": 1586043319604,
    "modifiedDate": 1586043319604,
    "createdBy": "28AF22BA5DE6B0B40A494036@AdobeID",
    "modifiedBy": "28AF22BA5DE6B0B40A494036@AdobeID"
}
```

## Pesquisar especificações de fluxo de dados {#specs}

Um dataflow é responsável por coletar dados de fontes e trazê-los para [!DNL Platform]. Para criar um fluxo de dados, primeiro você deve obter as especificações do fluxo de dados executando uma solicitação de GET para a [!DNL Flow Service] API. As especificações de fluxo de dados são responsáveis por coletar dados de um banco de dados externo ou de um sistema NoSQL.

**Formato da API**

```https
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

Uma resposta bem-sucedida retorna os detalhes da especificação de fluxo de dados responsável por inserir os dados do seu aplicativo de pagamentos para [!DNL Platform]. Essa ID é necessária na próxima etapa para criar um novo fluxo de dados.

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
        "name": "Dataflow between payments Platform",
        "description": "Inbound data to Platform",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "2c48a152-3d49-43cb-88a1-523d49e3cbcb"
        ],
        "targetConnectionIds": [
            "c8e12917-ac33-44d7-a129-17ac3364d7b7"
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
                    "mappingId": "b54a8dc38e8d4e31a2dc096e413ae8e5",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1567411548",
            "frequency": "minute",
            "interval":"30"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `flowSpec.id` | A ID [de especificação de](#specs) fluxo recuperada na etapa anterior. |
| `sourceConnectionIds` | A ID [de conexão](#source) de origem recuperada em uma etapa anterior. |
| `targetConnectionIds` | A ID [de conexão do](#target-connection) público alvo recuperada em uma etapa anterior. |
| `transformations.params.mappingId` | A ID [de](#mapping) mapeamento recuperada em uma etapa anterior. |
| `transformations.params.deltaColum` | A coluna designada usada para diferenciar entre dados novos e existentes. Os dados incrementais serão ingeridos com base no carimbo de data e hora da coluna selecionada. O formato de data suportado para `deltaColumn` é `yyyy-MM-dd HH:mm:ss`. |
| `transformations.params.mappingId` | A ID de mapeamento associada ao banco de dados. |
| `scheduleParams.startTime` | A hora de start do fluxo de dados em cada época. |
| `scheduleParams.frequency` | A frequência com que o fluxo de dados coletará dados. Os valores aceitáveis incluem: `once`, `minute`, `hour`, `day`ou `week`. |
| `scheduleParams.interval` | O intervalo designa o período entre duas execuções consecutivas de fluxo. O valor do intervalo deve ser um número inteiro diferente de zero. O intervalo não é necessário quando a frequência é definida como `once` e deve ser maior ou igual a `15` outros valores de frequência. |

**Resposta**

Uma resposta bem-sucedida retorna a ID `id` do fluxo de dados recém-criado.

```json
{
    "id": "e0bd8463-0913-4ca1-bd84-6309134ca1f6",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

## Monitore seu fluxo de dados

Depois que seu fluxo de dados for criado, você poderá monitorar os dados que estão sendo assimilados por ele para ver informações sobre execuções de fluxo, status de conclusão e erros. Para obter mais informações sobre como monitorar fluxos de dados, consulte o tutorial sobre como [monitorar fluxos de dados na API ](../monitor.md)


## Próximas etapas

Ao seguir este tutorial, você criou um conector de origem para coletar dados de um aplicativo de pagamentos de forma programada. Os dados recebidos agora podem ser usados por [!DNL Platform] serviços de downstream, como [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Consulte os seguintes documentos para obter mais detalhes:

* [Visão geral do Perfil do cliente em tempo real](../../../../profile/home.md)
* [Visão geral da Análise do espaço de trabalho da Data Science](../../../../data-science-workspace/home.md)