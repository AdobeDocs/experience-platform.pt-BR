---
keywords: Experience Platform, home, tópicos populares, dados de armazenamento na nuvem
solution: Experience Platform
title: Colete dados de armazenamento em nuvem usando conectores e APIs de origem
topic: visão geral
type: Tutorial
description: Este tutorial aborda as etapas para recuperar dados de um armazenamento em nuvem de terceiros e trazê-los para a plataforma usando conectores de origem e APIs.
translation-type: tm+mt
source-git-commit: 8b85b25112ee16b09b1411c5d001bf13fb7fbcaa
workflow-type: tm+mt
source-wordcount: '1768'
ht-degree: 2%

---


# Colete dados de armazenamento em nuvem usando conectores de origem e APIs

Este tutorial aborda as etapas para recuperar dados de um armazenamento em nuvem de terceiros e trazê-los para a Plataforma por meio de conectores de origem e da [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Introdução

Este tutorial requer que você tenha acesso a um armazenamento em nuvem de terceiros por meio de uma conexão válida e informações sobre o arquivo que deseja trazer para a Platform, incluindo o caminho e a estrutura do arquivo. Se não tiver essas informações, consulte o tutorial em [explorar um armazenamento em nuvem de terceiros usando a  [!DNL Flow Service] API](../explore/cloud-storage.md) antes de tentar este tutorial.

Este tutorial também requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   - [Noções básicas da composição](../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Guia](../../../../xdm/api/getting-started.md) do desenvolvedor do Registro de Schema: Inclui informações importantes que você precisa saber para executar com sucesso chamadas para a API do Registro de Esquema. Isso inclui seu `{TENANT_ID}`, o conceito de &quot;contêineres&quot; e os cabeçalhos necessários para fazer solicitações (com especial atenção ao cabeçalho Accept e seus possíveis valores).
- [[!DNL Catalog Service]](../../../../catalog/home.md): Catálogo é o sistema de registro para localização e linhagem de dados no Experience Platform.
- [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md): A API de assimilação em lote permite assimilar dados no Experience Platform como arquivos em lote.
- [Sandboxes](../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.
As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a um armazenamento em nuvem usando a API [!DNL Flow Service].

### Lendo exemplos de chamadas de API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas do Experience Platform.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para APIs da plataforma, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API do Experience Platform, conforme mostrado abaixo:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos no Experience Platform, incluindo aqueles pertencentes a [!DNL Flow Service], são isolados para sandboxes virtuais específicas. Todas as solicitações para APIs da plataforma exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

- `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

- `Content-Type: application/json`

## Criar uma conexão de origem {#source}

Você pode criar uma conexão de origem fazendo uma solicitação POST para a API [!DNL Flow Service]. Uma conexão de origem consiste em uma ID de conexão, um caminho para o arquivo de dados de origem e uma ID de especificação de conexão.

Para criar uma conexão de origem, você também deve definir um valor enum para o atributo de formato de dados.

Use os seguintes valores enum para fontes baseadas em arquivo:

| Formato dos dados | Valor de enumeração |
| ----------- | ---------- |
| Delimitado | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Para todas as fontes baseadas em tabela, defina o valor como `tabular`.

- [Criar uma conexão de origem usando arquivos personalizados delimitados](#using-custom-delimited-files)
- [Criar uma conexão de origem usando arquivos compactados](#using-compressed-files)

**Formato da API**

```http
POST /sourceConnections
```

### Crie uma conexão de origem usando arquivos personalizados {#using-custom-delimited-files}

**Solicitação**

Você pode assimilar um arquivo delimitado com um delimitador personalizado especificando um `columnDelimiter` como uma propriedade. Qualquer valor de caractere único é um delimitador de coluna permitido. Se não fornecido, uma vírgula `(,)` é usada como o valor padrão.

A solicitação de exemplo a seguir cria uma conexão de origem para um tipo de arquivo delimitado usando valores separados por tabulação.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cloud storage source connection for delimited files",
        "description": "Cloud storage source connector",
        "baseConnectionId": "9e2541a0-b143-4d23-a541-a0b143dd2301",
        "data": {
            "format": "delimited",
            "columnDelimiter": "\t"
        },
        "params": {
            "path": "/ingestion-demos/leads/tsv_data/*.tsv",
            "recursive": "true"
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `baseConnectionId` | A ID de conexão exclusiva do sistema de armazenamento em nuvem de terceiros que você está acessando. |
| `data.format` | Um valor enum que define o atributo de formato de dados. |
| `data.columnDelimiter` | Você pode usar qualquer delimitador de coluna de caractere único para coletar arquivos simples. Essa propriedade só é necessária ao assimilar arquivos CSV ou TSV. |
| `params.path` | O caminho do arquivo de origem que você está acessando. |
| `connectionSpec.id` | A ID de especificação de conexão associada ao sistema de armazenamento em nuvem de terceiros específico. Consulte o [apêndice](#appendix) para obter uma lista de IDs de especificação de conexão. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada. Essa ID é necessária em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

### Criar uma conexão de origem usando arquivos compactados {#using-compressed-files}

**Solicitação**

Você também pode assimilar arquivos compactados JSON ou delimitados especificando seu `compressionType` como uma propriedade. A lista de tipos de arquivos compactados suportados é:

- `bzip2`
- `gzip`
- `deflate`
- `zipDeflate`
- `tarGzip`
- `tar`

A solicitação de exemplo a seguir cria uma conexão de origem para um arquivo delimitado compactado usando um tipo de arquivo `gzip` .

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cloud storage source connection for compressed files",
        "description": "Cloud storage source connection for compressed files",
        "baseConnectionId": "9e2541a0-b143-4d23-a541-a0b143dd2301",
        "data": {
            "format": "delimited",
            "properties": {
                "compressionType" : "gzip"
            }
        },
        "params": {
            "path": "/compressed/files.gzip"
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
     }'
```

| Propriedade | Descrição |
| --- | --- |
| `data.properties.compressionType` | Determina o tipo de arquivo compactado para assimilação. Essa propriedade só é necessária ao assimilar arquivos compactados JSON ou delimitados. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada. Essa ID é necessária em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

## Criar um esquema XDM de destino {#target-schema}

Para que os dados de origem sejam usados na Platform, um schema de target deve ser criado para estruturar os dados de origem de acordo com suas necessidades. O schema de destino é usado para criar um conjunto de dados da plataforma no qual os dados de origem estão contidos.

Um esquema XDM de destino pode ser criado executando uma solicitação de POST para a [API do Registro de Schema](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

**Formato da API**

```http
POST /schemaregistry/tenant/schemas
```

**Solicitação**

A solicitação de exemplo a seguir cria um esquema XDM que estende a classe Perfil individual XDM.

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

Uma resposta bem-sucedida retorna detalhes do schema recém-criado, incluindo seu identificador exclusivo (`$id`). Essa ID é necessária em etapas posteriores para criar um conjunto de dados de destino, mapeamento e fluxo de dados.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
    "meta:altId": "_{TENANT_ID}.schemas.995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema cloud storage",
    "type": "object",
    "description": "Target schema for cloud storage",
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
        "repo:createdDate": 1597783248870,
        "repo:lastModifiedDate": 1597783248870,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "596661ec6c7a9c6ae530676e98290a4a58ca29540ed92489cf4478b2bf013a65",
        "meta:globalLibVersion": "1.13.3"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "{TENANT_ID}"
}
```

## Criar um conjunto de dados de destino

Um conjunto de dados de destino pode ser criado executando uma solicitação POST para a [API do Serviço de catálogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), fornecendo a ID do esquema de destino dentro da carga útil.

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
        "name": "Target dataset for cloud storage",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `schemaRef.id` | A ID do esquema XDM de destino. |

**Resposta**

Uma resposta bem-sucedida retorna uma matriz contendo a ID do conjunto de dados recém-criado no formato `"@/datasets/{DATASET_ID}"`. A ID do conjunto de dados é uma string gerada pelo sistema e somente leitura, usada para fazer referência ao conjunto de dados nas chamadas de API. A ID do conjunto de dados de destino é necessária em etapas posteriores para criar uma conexão de destino e um fluxo de dados.

```json
[
    "@/dataSets/5f3c3cedb2805c194ff0b69a"
]
```

## Criar uma conexão de destino {#target-connection}

Uma conexão target representa a conexão com o destino onde os dados assimilados chegam. Para criar uma conexão de destino, você deve fornecer a ID de especificação de conexão fixa associada ao Data Lake. Essa ID de especificação de conexão é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Agora você tem os identificadores exclusivos em um esquema de destino em um conjunto de dados de destino e a ID de especificação de conexão no Data Lake. Usando esses identificadores, você pode criar uma conexão de destino usando a API [!DNL Flow Service] para especificar o conjunto de dados que conterá os dados de origem de entrada.

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
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5f3c3cedb2805c194ff0b69a"
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
| `params.dataSetId` | A ID do conjunto de dados de destino. |
| `connectionSpec.id` | A ID de especificação de conexão fixa para o Data Lake. Essa ID é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo da nova conexão de destino (`id`). Essa ID é necessária em etapas posteriores.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Criar um mapeamento {#mapping}

Para que os dados de origem sejam assimilados em um conjunto de dados de destino, eles devem primeiro ser mapeados para o schema de destino ao qual o conjunto de dados de destino adere. Isso é feito executando uma solicitação POST para o Serviço de conversão com mapeamentos de dados definidos na carga da solicitação.

>[!TIP]
>
>Você pode mapear tipos de dados complexos, como matrizes em arquivos JSON, usando um conector de origem de armazenamento na nuvem.

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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
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
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "FirstName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "LastName",
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
| `xdmSchema` | A ID do esquema XDM de destino. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes do mapeamento recém-criado, incluindo seu identificador exclusivo (`id`). Esse valor é necessário em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Recuperar especificações do fluxo de dados {#specs}

Um fluxo de dados é responsável por coletar dados de fontes e trazê-los para a plataforma. Para criar um fluxo de dados, primeiro você deve obter as especificações do fluxo de dados responsáveis pela coleta de dados do armazenamento em nuvem.

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

Uma resposta bem-sucedida retorna os detalhes da especificação de fluxo de dados responsável por trazer os dados da fonte para a Plataforma. A resposta inclui a especificação de fluxo exclusiva `id` necessária para criar um novo fluxo de dados.

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

A última etapa para coletar dados de armazenamento em nuvem é criar um fluxo de dados. Por enquanto, você terá os seguintes valores obrigatórios preparados:

- [ID de conexão de origem](#source)
- [ID de conexão do Target](#target)
- [ID de mapeamento](#mapping)
- [ID de especificação do fluxo de dados](#specs)

Um fluxo de dados é responsável por agendar e coletar dados de uma fonte. Você pode criar um fluxo de dados executando uma solicitação de POST e, ao mesmo tempo, fornecendo os valores mencionados anteriormente dentro da carga útil.

Para agendar uma assimilação, primeiro defina o valor de hora de início como época em segundos. Em seguida, você deve definir o valor de frequência para uma das cinco opções: `once`, `minute`, `hour`, `day` ou `week`. O valor de intervalo designa o período entre duas ingestões consecutivas e a criação de uma ingestão única não requer a definição de um intervalo. Para todas as outras frequências, o valor do intervalo deve ser definido como igual ou maior que `15`.

>[!IMPORTANT]
>
>É altamente recomendável agendar seu fluxo de dados para uma assimilação única ao usar o [conector FTP](../../../connectors/cloud-storage/ftp.md).

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
        "name": "Cloud Storage flow to Platform",
        "description": "Cloud Storage flow to Platform",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "26b53912-1005-49f0-b539-12100559f0e2"
        ],
        "targetConnectionIds": [
            "f7eb08fa-5f04-4e45-ab08-fa5f046e45ee"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1597784298",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `flowSpec.id` | O [ID de especificação do fluxo](#specs) recuperado na etapa anterior. |
| `sourceConnectionIds` | A [ID da conexão de origem](#source) recuperada em uma etapa anterior. |
| `targetConnectionIds` | A [ID da conexão de destino](#target-connection) recuperada em uma etapa anterior. |
| `transformations.params.mappingId` | O [ID de mapeamento](#mapping) recuperado em uma etapa anterior. |
| `scheduleParams.startTime` | A hora de início do fluxo de dados em época. |
| `scheduleParams.frequency` | A frequência com que o fluxo de dados coletará dados. Os valores aceitáveis incluem: `once`, `minute`, `hour`, `day` ou `week`. |
| `scheduleParams.interval` | O intervalo designa o período entre duas execuções consecutivas de fluxo. O valor do intervalo deve ser um número inteiro diferente de zero. O intervalo não é necessário quando a frequência é definida como `once` e deve ser maior ou igual a `15` para outros valores de frequência. |

**Resposta**

Uma resposta bem-sucedida retorna a ID (`id`) do fluxo de dados recém-criado.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Monitorar o fluxo de dados

Depois que o fluxo de dados tiver sido criado, você poderá monitorar os dados que estão sendo assimilados por meio dele para ver informações sobre execuções de fluxo, status de conclusão e erros. Para obter mais informações sobre como monitorar fluxos de dados, consulte o tutorial em [monitorando fluxos de dados na API](../monitor.md)

## Próximas etapas

Ao seguir este tutorial, você criou um conector de origem para coletar dados do armazenamento em nuvem de forma agendada. Os dados recebidos agora podem ser usados por serviços downstream da plataforma, como [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Consulte os seguintes documentos para obter mais detalhes:

- [Visão geral do perfil do cliente em tempo real](../../../../profile/home.md)
- [Visão geral do Data Science Workspace](../../../../data-science-workspace/home.md)

## Apêndice {#appendix}

A seção a seguir lista os diferentes conectores de origem de armazenamento em nuvem e suas especificações de conexões.

### Especificação de conexão

| Nome do conector | Especificação de conexão |
| -------------- | --------------- |
| [!DNL Amazon S3] (S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| [!DNL Amazon Kinesis] (Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| [!DNL Azure Blob] (Blob) | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| [!DNL Azure Data Lake Storage Gen2] (ADLS Gen2) | `0ed90a81-07f4-4586-8190-b40eccef1c5a` |
| [!DNL Azure Event Hubs] (Hubs de eventos) | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| [!DNL Azure File Storage] | `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |
| [!DNL Google Cloud Storage] | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| [!DNL HDFS] | `54e221aa-d342-4707-bcff-7a4bceef0001` |
| [!DNL Oracle Object Storage] | `c85f9425-fb21-426c-ad0b-405e9bd8a46c` |
| [!DNL SFTP] | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |