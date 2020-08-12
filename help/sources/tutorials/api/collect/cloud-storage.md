---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Coletar dados de armazenamento em nuvem por meio de conectores de origem e APIs
topic: overview
translation-type: tm+mt
source-git-commit: 773823333fe0553515ebf169b4fd956b8737a9c3
workflow-type: tm+mt
source-wordcount: '1680'
ht-degree: 1%

---


# Coletar dados de armazenamento em nuvem por meio de conectores de origem e APIs

[!DNL Flow Service] é usada para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial aborda as etapas para recuperar dados de um armazenamento em nuvem de terceiros e trazê-los para dentro [!DNL Platform] por meio de conectores de origem e APIs.

## Introdução

Este tutorial requer que você tenha acesso a um armazenamento em nuvem de terceiros por meio de uma conexão válida e informações sobre o arquivo que deseja inserir [!DNL Platform], incluindo o caminho e a estrutura do arquivo. Se você não tiver essas informações, consulte o tutorial sobre como [explorar um armazenamento em nuvem de terceiros usando a API](../explore/cloud-storage.md) do Serviço de Fluxo antes de tentar este tutorial.

Este tutorial também exige que você tenha uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Sistema](../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   - [Noções básicas da composição](../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Guia](../../../../xdm/api/getting-started.md)do desenvolvedor do Registro do schema: Inclui informações importantes que você precisa saber para executar com êxito chamadas para a API do Registro do Schema. Isso inclui seu `{TENANT_ID}`, o conceito de &quot;container&quot; e os cabeçalhos necessários para fazer solicitações (com atenção especial ao cabeçalho Accept e seus possíveis valores).
- [Serviço](../../../../catalog/home.md)de catálogo: Catálogo é o sistema de registro para localização e linhagem de dados dentro [!DNL Experience Platform].
- [Ingestão](../../../../ingestion/batch-ingestion/overview.md)em lote: A API de ingestão em lote permite que você ingira dados [!DNL Experience Platform] como arquivos em lote.
- [Caixas de proteção](../../../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a um armazenamento em nuvem usando a [!DNL Flow Service] API.

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de [!DNL Experience Platform] solução de problemas.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o tutorial [de](../../../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de [!DNL Experience Platform] API, como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo os pertencentes a [!DNL Flow Service], são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

- Tipo de conteúdo: `application/json`

## Criar uma classe e um schema XDM ad hoc

Para trazer dados externos para dentro [!DNL Platform] por meio de conectores de origem, uma classe e um schema XDM ad-hoc devem ser criados para os dados de fonte bruta.

Para criar uma classe e um schema ad-hoc, siga as etapas descritas no tutorial [do schema](../../../../xdm/tutorials/ad-hoc.md)ad-hoc. Ao criar uma classe ad-hoc, todos os campos encontrados nos dados de origem devem ser descritos no corpo da solicitação.

Continue seguindo as etapas descritas no guia do desenvolvedor até que você tenha criado um schema ad-hoc. O identificador exclusivo (`$id`) do schema ad-hoc é necessário para prosseguir para a próxima etapa deste tutorial.

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
        "name": "Test source connection for a Cloud Storage connector",
        "baseConnectionId": "ac33bd66-1565-4915-b3bd-6615657915c4",
        "description": "Test source connection for a Cloud Storage connector",
        "data": {
            "format": "delimited",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/22a4ab59462a64de551d42dd10ec1f19d8d7246e3f90072a",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "/backfil/data8.csv",
            "recursive": "true"
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `baseConnectionId` | A ID exclusiva de conexão do sistema de armazenamento em nuvem de terceiros que você está acessando. |
| `data.schema.id` | A ID do schema XDM ad-hoc. |
| `params.path` | O caminho do arquivo de origem que você está acessando. |
| `connectionSpec.id` | A ID de especificação de conexão associada ao sistema de armazenamento em nuvem de terceiros específico. Consulte o [apêndice](#appendix) para obter uma lista de IDs de especificação de conexão. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada. Essa ID é necessária em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "8bae595c-8548-4716-ae59-5c85480716e9",
    "etag": "\"4a00038b-0000-0200-0000-5ebc47fd0000\""
}
```

## Criar um schema XDM de público alvo {#target-schema}

Em etapas anteriores, um schema XDM ad-hoc foi criado para estruturar os dados de origem. Para que os dados de origem sejam usados em [!DNL Platform], um schema de público alvo também deve ser criado para estruturar os dados de origem de acordo com suas necessidades. O schema do público alvo é então usado para criar um [!DNL Platform] conjunto de dados no qual os dados de origem estão contidos.

É possível criar um schema XDM de público alvo, executando uma solicitação POST para a API [do Registro de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)Schemas.

Se você preferir usar a interface do usuário no [!DNL Experience Platform], o tutorial [do Editor de](../../../../xdm/tutorials/create-schema-ui.md) Schemas fornece instruções passo a passo para executar ações semelhantes no Editor de Schemas.

**Formato da API**

```http
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
        "title": "Target schema for a Cloud Storage connector",
        "description": "Target schema for a Cloud Storage connector",
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
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e28dd48fab732263816f8b80ae4fdf49ca7ad229ca62e5d6",
    "meta:altId": "_{TENANT_ID}.schemas.e28dd48fab732263816f8b80ae4fdf49ca7ad229ca62e5d6",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for a Cloud Storage connector",
    "type": "object",
    "description": "Target schema for Cloud Storage",
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
        "repo:createdDate": 1589398474190,
        "repo:lastModifiedDate": 1589398474190,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "f07723475e933dc30ed411d97986a36f13aa20c820463dd8cf7b74e63f4e7801",
        "meta:globalLibVersion": "1.10.1.1"
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
        "name": "Target dataset for a Cloud Storage connector",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT}/schemas/e28dd48fab732263816f8b80ae4fdf49ca7ad229ca62e5d6",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `schemaRef.id` | A ID do schema XDM do público alvo. |

**Resposta**

Uma resposta bem-sucedida retorna uma matriz que contém a ID do conjunto de dados recém-criado no formato `"@/datasets/{DATASET_ID}"`. A ID do conjunto de dados é uma sequência de caracteres somente leitura, gerada pelo sistema, usada para fazer referência ao conjunto de dados em chamadas de API. A ID do conjunto de dados do público alvo é necessária em etapas posteriores para criar uma conexão de público alvo e um fluxo de dados.

```json
[
    "@/dataSets/5ebc4be8590b1b191a8dc4ca"
]
```

## Criar uma conexão de público alvo {#target-connection}

Uma conexão de público alvo representa a conexão com o destino onde os dados ingeridos chegam. Para criar uma conexão de público alvo, é necessário fornecer a ID de especificação de conexão fixa associada ao registro de dados. Esta ID de especificação de conexão é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Agora você tem os identificadores exclusivos de um schema de público alvo de um conjunto de dados de público alvo e a ID de especificação de conexão para o registro de dados. Usando esses identificadores, é possível criar uma conexão de público alvo usando a [!DNL Flow Service] API para especificar o conjunto de dados que conterá os dados de origem de entrada.

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
        "name": "Target Connection for a Cloud Storage connector",
        "description": "Target Connection for a Cloud Storage connector",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e28dd48fab732263816f8b80ae4fdf49ca7ad229ca62e5d6",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5ebc4be8590b1b191a8dc4ca"
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
| `params.dataSetId` | A ID do conjunto de dados do público alvo. |
| `connectionSpec.id` | A ID de especificação de conexão fixa para o registro de dados. Esta ID é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da nova conexão com o público alvo. Essa ID é necessária em etapas posteriores.

```json
{
    "id": "1f5af99c-f1ef-4076-9af9-9cf1ef507678",
    "etag": "\"530013e2-0000-0200-0000-5ebc4c110000\""
}
```

## Criar um mapeamento {#mapping}

Para que os dados de origem sejam ingeridos em um conjunto de dados de público alvo, eles devem primeiro ser mapeados para o schema de público alvo ao qual o conjunto de dados de público alvo adere. Isso é feito executando uma solicitação POST para o Serviço de conversão com mapeamentos de dados definidos na carga da solicitação.

**Formato da API**

```http
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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/e28dd48fab732263816f8b80ae4fdf49ca7ad229ca62e5d6",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "first_name",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "last_name",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "personalEmail.address",
                "sourceAttribute": "email",
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

Uma resposta bem-sucedida retorna detalhes do mapeamento recém-criado, incluindo seu identificador exclusivo (`id`). Esse valor é necessário em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "febec6a6785e45ea9ed594422cc483d7",
    "version": 0,
    "createdDate": 1589398562232,
    "modifiedDate": 1589398562232,
    "createdBy": "28AF22BA5DE6B0B40A494036@AdobeID",
    "modifiedBy": "28AF22BA5DE6B0B40A494036@AdobeID"
}
```

## Recuperar especificações de fluxo de dados {#specs}

Um dataflow é responsável por coletar dados de fontes e trazê-los para [!DNL Platform]. Para criar um fluxo de dados, primeiro você deve obter as especificações de fluxo de dados responsáveis pela coleta de dados de armazenamentos em nuvem.

**Formato da API**

```http
GET /flowSpecs?property=name=="CloudStorageToAEP"
```

**Solicitação**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CloudStorageToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da especificação do fluxo de dados responsável por inserir os dados do armazenamento em nuvem [!DNL Platform]. A resposta inclui uma ID exclusiva de especificação de fluxo. Essa ID é necessária na próxima etapa para criar um novo fluxo de dados.

```json
{
    "items": [
        {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "name": "CloudStorageToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
                "ecadc60c-7455-4d87-84dc-2a0e293d997b",
                "b7829c2f-2eb0-4f49-a6ee-55e33008b629",
                "4c10e202-c428-4796-9208-5f1f5732b1cf",
                "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
                "32e8f412-cdf7-464c-9885-78184cb113fd",
                "b7bf2577-4520-42c9-bae9-cad01560f7bc",
                "998b8ae3-cec0-43b7-8abe-40b1eb4ee069",
                "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8"
            ],
            "targetConnectionSpecIds": [
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
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

A última etapa para coletar dados de armazenamento em nuvem é criar um fluxo de dados. Agora, você tem os seguintes valores obrigatórios preparados:

- [ID da conexão de origem](#source)
- [ID de conexão do público alvo](#target)
- [ID de mapeamento](#mapping)
- [ID de especificação do fluxo de dados](#specs)

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
        "name": "Cloud Storage flow to AEP",
        "description": "Cloud Storage flow to AEP",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "8bae595c-8548-4716-ae59-5c85480716e9"
        ],
        "targetConnectionIds": [
            "1f5af99c-f1ef-4076-9af9-9cf1ef507678"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "febec6a6785e45ea9ed594422cc483d7",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1589398646",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `flowSpec.id` | A ID [de especificação de](#specs) fluxo recuperada na etapa anterior. |
| `sourceConnectionIds` | A ID [de conexão](#source) de origem recuperada em uma etapa anterior. |
| `targetConnectionIds` | A ID [de conexão do](#target-connection) público alvo recuperada em uma etapa anterior. |
| `transformations.params.mappingId` | A ID [de](#mapping) mapeamento recuperada em uma etapa anterior. |
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

Ao seguir este tutorial, você criou um conector de origem para coletar dados do seu armazenamento em nuvem de forma programada. Os dados recebidos agora podem ser usados por [!DNL Platform] serviços de downstream, como [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Consulte os seguintes documentos para obter mais detalhes:

- [Visão geral do Perfil do cliente em tempo real](../../../../profile/home.md)
- [Visão geral da Análise do espaço de trabalho da Data Science](../../../../data-science-workspace/home.md)

## Apêndice {#appendix}

A seção a seguir lista os diferentes conectores de origem do armazenamento de nuvem e suas especificações de conexões.

### Especificação da conexão

| Nome do conector | Especificação da conexão |
| -------------- | --------------- |
| [!DNL Amazon S3] (S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| [!DNL Amazon Kinesis] (Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| [!DNL Azure Blob] (Blob) | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| [!DNL Azure Data Lake Storage Gen2] (ADLS Gen2) | `0ed90a81-07f4-4586-8190-b40eccef1c5a` |
| [!DNL Azure Event Hubs] (Hubs de Evento) | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| [!DNL Azure File Storage] | `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |
| [!DNL Google Cloud Storage] | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| HDFS | `54e221aa-d342-4707-bcff-7a4bceef0001` |
| SFTP | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |