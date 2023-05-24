---
keywords: Experience Platform;página inicial;tópicos populares;preparação de dados;guia de api;conjuntos de mapeamento;
solution: Experience Platform
title: Mapeamento Define o Ponto de Extremidade da API
description: Você pode usar o endpoint `/mappingSets` na API do Adobe Experience Platform para recuperar, criar, atualizar e validar programaticamente conjuntos de mapeamento.
exl-id: a4e4ddcd-164e-42aa-b7d1-ba59d70da142
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 5%

---

# Ponto final dos conjuntos de mapeamento

Os conjuntos de mapeamento podem ser usados para definir como os dados em um esquema de origem são mapeados para o de um esquema de destino. Você pode usar o `/mappingSets` endpoint na API de Preparo de dados para recuperar, criar, atualizar e validar conjuntos de mapeamento de forma programática.

## Listar conjuntos de mapeamento

Você pode recuperar uma lista de todos os conjuntos de mapeamentos para sua organização fazendo uma solicitação GET para `/mappingSets` terminal.

**Formato da API**

A variável `/mappingSets` O endpoint oferece suporte a vários parâmetros de consulta para ajudar a filtrar os resultados. Embora a maioria desses parâmetros seja opcional, seu uso é altamente recomendado para ajudar a reduzir a sobrecarga cara. No entanto, você deve incluir os `start` e `limit` parâmetros como parte da solicitação. Vários parâmetros podem ser incluídos, separados por &quot;E&quot; comercial (`&`).

```http
GET /mappingSets?limit={LIMIT}&start={START}
GET /mappingSets?limit={LIMIT}&start={START}&name={NAME}
GET /mappingSets?limit={LIMIT}&start={START}&orderBy={ORDER_BY}
GET /mappingSets?limit={LIMIT}&start={START}&expandSchema={EXPAND_SCHEMA}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{LIMIT}` | (**Obrigatório**) Especifica o número de conjuntos de mapeamento retornados. |
| `{START}` | (**Obrigatório**) Especifica o deslocamento das páginas de resultados. Para obter a primeira página de resultados, defina o valor como `start=0`. |
| `{NAME}` | Filtra os conjuntos de mapeamento por nome. |
| `{ORDER_BY}` | Classifica a ordem dos resultados. Os únicos campos compatíveis são `createdDate` e `updatedDate`. Você pode anexar a propriedade ao `+` ou `-` para classificá-la por ordem crescente ou decrescente, respectivamente. |
| `{EXPAND_SCHEMA}` | Um booleano que determina se o esquema de saída completo é retornado como parte da resposta. |

**Solicitação**

A solicitação a seguir recuperará os dois últimos conjuntos de mapeamento em sua organização.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/mappingSets?limit=2&start=0 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

```json
{
    "data": [
        {
            "id": "428beb15b4864daaaa9dc3f005448005",
            "version": 1,
            "createdDate": 1582250953000,
            "modifiedDate": 1582251156000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_ui_platform",
            "supportVersion": "1.1",
            "inputSchema": {
                "id": "e660142cab8e438382abc5691b364b30",
                "version": 0,
                "sampleId": "f9e83882e3e34c1f8b873a3b8113c01e"
            },
            "outputSchema": {
                "id": "1956affc28be468aa452e5e47c680c6b",
                "version": 0,
                "schemaRef": {
                    "id": "https://ns.adobe.com/xdm/context/profile__union",
                    "contentType": "1.0"
                }
            },
            "mappings": [
                {
                    "id": "af809223484341009ce0db13d4b32a3a",
                    "version": 0,
                    "createdDate": 1582250953000,
                    "modifiedDate": 1582250953000,
                    "createdBy": "acp_xql_gateway",
                    "modifiedBy": "acp_xql_gateway",
                    "sourceType": "text/x.schema-path",
                    "source": "id",
                    "destination": "person.name.firstName",
                    "identity": false,
                    "primaryIdentity": false,
                    "matchScore": 0.0,
                    "functionVersion": 1,
                    "sourceAttribute": "id",
                    "destinationXdmPath": "person.name.firstName"
                }
            ],
            "status": "PUBLISHED",
            "strictMapping": false,
            "allowNullValues": false,
            "xdmVersion": "1.0",
            "schemaRef": {
                "id": "https://ns.adobe.com/xdm/context/profile__union",
                "contentType": "1.0"
            },
            "xdmSchema": "https://ns.adobe.com/xdm/context/profile__union"
        },
        {
            "id": "8afb1351833a4a4692ea61074b60813b",
            "version": 0,
            "createdDate": 1582250893000,
            "modifiedDate": 1582250893000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "supportVersion": "1.1",
            "inputSchema": {
                "id": "97fe2ecf4faa400bb66dd6be88a53fe4",
                "version": 0,
                "sampleId": "0248bfb352214f908bdd6cf9c19447e1"
            },
            "outputSchema": {
                "id": "e9c3696715d94905bb4e9bfc2c508e66",
                "version": 0,
                "schemaRef": {
                    "id": "https://ns.adobe.com/xdm/context/profile__union",
                    "contentType": "1.0"
                }
            },
            "mappings": [
                {
                    "id": "74647d8bf3b742f289534bee2fdeb732",
                    "version": 0,
                    "createdDate": 1582250893000,
                    "modifiedDate": 1582250893000,
                    "createdBy": "acp_xql_gateway",
                    "modifiedBy": "acp_xql_gateway",
                    "sourceType": "text/x.schema-path",
                    "source": "last_name",
                    "destination": "person.name.lastName",
                    "identity": false,
                    "primaryIdentity": false,
                    "matchScore": 0.0,
                    "functionVersion": 1,
                    "sourceAttribute": "last_name",
                    "destinationXdmPath": "person.name.lastName"
                }
            ],
            "status": "DRAFT",
            "strictMapping": false,
            "allowNullValues": false,
            "xdmVersion": "1.0",
            "schemaRef": {
                "id": "https://ns.adobe.com/xdm/context/profile__union",
                "contentType": "1.0"
            },
            "xdmSchema": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "_page": {
        "count": 0,
        "limit": 2
    }
}
```

## Criar um conjunto de mapeamento

Você pode criar um novo conjunto de mapeamento fazendo uma solicitação POST para o `/mappingSets` terminal.

**Formato da API**

```http
POST /mappingSets
```

**Solicitação**

A solicitação a seguir cria um novo conjunto de mapeamento, configurado pelos parâmetros fornecidos na carga.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/mappingSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "id",
            "destination": "_id",
            "name": "id",
            "description": "Identifier field"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "firstName",
            "destination": "person.name.firstName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "lastName",
            "destination": "person.name.lastName"
        }
    ]
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `outputSchema.schemaRef.id` | A ID do esquema XDM que você está referenciando. |
| `outputSchema.schemaRef.contentType` | Determina o formato de resposta do esquema referenciado. Mais informações sobre esse campo podem ser encontradas no [Guia do desenvolvedor do Registro de esquema](../../xdm/api/schemas.md#lookup). |
| `mappings.sourceType` | O tipo de origem descreve como o valor será extraído da origem para o destino. O tipo de origem suporta dois valores possíveis: <ul><li>`ATTRIBUTE`: o tipo de origem `ATTRIBUTE` é usado quando o atributo de entrada é de um schema de origem.</li><li>`EXPRESSION`: o tipo de origem `EXPRESSION` é usado quando o mapeamento é concluído usando um campo calculado.</li></ul> **AVISO**: definir incorretamente os valores do tipo de origem pode tornar os conjuntos de mapeamento não editáveis. |
| `mappings.source` | O local de onde você deseja mapear os dados. |
| `mappings.destination` | O local para onde você deseja mapear os dados. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações sobre o conjunto de mapeamentos recém-criado.

```json
{
    "id": "e7c80e4c0d8f4a98a7d400b4e178b635",
    "version": 0,
    "createdDate": 1614901254724,
    "modifiedDate": 1614901254724,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Validar mapeamentos

Você pode validar se seus mapeamentos funcionam corretamente fazendo uma solicitação POST para o `/mappingSets/validate` terminal.

**Formato da API**

```http
POST /mappingSets/validate
```

**Solicitação**

A solicitação a seguir valida os mapeamentos fornecidos na carga.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/mappingSets/validate \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "id",
            "destination": "_id",
            "name": "id",
            "description": "Identifier field"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "firstName",
            "destination": "person.name.firstName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "lastName",
            "destination": "person.name.lastName"
        }
    ]
}
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações de validação para o mapeamento proposto.

```json
{
    "validationResponse": [
        {
            "status": "SUCCESS",
            "errors": null
        },
        {
            "status": "SUCCESS",
            "errors": null
        },
        {
            "status": "SUCCESS",
            "errors": null
        }
    ]
}
```

## Visualizar dados de mapeamentos

Você pode visualizar para que seus dados serão mapeados fazendo uma solicitação POST para o `/mappingSets/preview` terminal.

**Formato da API**

```http
POST /mappingSets/preview
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/mappingSets/preview \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
{
    "data": [
        {
            "id": 1234,
            "firstName": "Jim",
            "lastName": "Seltzer"
        }
    ],
    "mappingSet": {
        "outputSchema": {
            "schemaRef": {
                "id": "https://ns.adobe.com/stardust/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "mappings": [
            {
                "sourceType": "ATTRIBUTE",
                "source": "id",
                "destination": "_id",
                "name": "id",
                "description": "Identifier field"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "firstName",
                "destination": "person.name.firstName"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "lastName",
                "destination": "person.name.lastName"
            }
        ]
    }
}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma visualização de seus dados mapeados.

```json
[
    {
        "data": {
            "person": {
                "name": {
                    "firstName": "Jim",
                    "lastName": "Seltzer"
                }
            },
            "_id": "1234"
        },
        "errors": null
    }
]
```

## Pesquisar um conjunto de mapeamento

Você pode recuperar um conjunto de mapeamentos específico fornecendo a respectiva ID no caminho de uma solicitação GET para o `/mappingSets` terminal. Esse endpoint também oferece suporte a vários parâmetros de consulta para ajudar você a recuperar detalhes sobre a versão do conjunto de mapeamentos especificada.

**Formato da API**

```http
GET /mappingSets/{MAPPING_SET_ID}
GET /mappingSets/{MAPPING_SET_ID}?expandSchema={EXPAND_SCHEMA}
GET /mappingSets/{MAPPING_SET_ID}?version={VERSION}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{MAPPING_SET_ID}` | (**Obrigatório**) A ID do conjunto de mapeamento que você deseja recuperar. |
| `{EXPAND_SCHEMA}` | Um parâmetro de consulta booleano que determina se o esquema de saída deve ser retornado como parte da resposta. |
| `{VERSION}` | Um parâmetro de consulta de número inteiro que determina qual versão do conjunto de mapeamento deve ser recuperada. |

**Solicitação**

A solicitação a seguir recupera informações detalhadas sobre um conjunto de mapeamento especificado.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/mappingSets/e7c80e4c0d8f4a98a7d400b4e178b635 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre o conjunto de mapeamento que você deseja recuperar.

>[!NOTE]
>
>A resposta a seguir foi truncada por questões de espaço.

```json
{
    "id": "e7c80e4c0d8f4a98a7d400b4e178b635",
    "version": 0,
    "createdDate": 1614901255000,
    "modifiedDate": 1614901255000,
    "createdBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "modifiedBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "supportVersion": "1.1",
    "outputSchema": {
        "id": "cf0a57df22354cfdb5f32a747b63a456",
        "version": 0,
        "jsonSchema": {
            "title": "A sample schema",
            "description": "My sample schema",
            "type": "object",
            "properties": {
                "_id": {
                    "title": "Identifier",
                    "description": "A unique identifier for the record.",
                    "type": "string"
                },
                "_repo": {
                    "type": "object",
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time"
                        }
                    }
                },
                "createdByBatchID": {
                    "type": "string",
                    "format": "uri-reference"
                },
                "modifiedByBatchID": {
                    "type": "string",
                    "format": "uri-reference"
                },
                "person": {
                    "type": "object",
                    "properties": {
                        "birthDate": {
                            "type": "string",
                            "format": "date"
                        },
                        "birthDayAndMonth": {
                            "type": "string",
                            "pattern": "[0-1][0-9]-[0-9][0-9]"
                        },
                        "birthYear": {
                            "type": "integer",
                            "minimum": 1,
                            "maximum": 32767
                        },
                        "gender": {
                            "type": "string",
                            "default": "not_specified",
                            "enum": [
                                "non_specific",
                                "not_specified",
                                "female",
                                "male"
                            ]
                        },
                        "name": {
                            "title": "Full name",
                            "description": "The person's full name.",
                            "type": "object",
                            "properties": {
                                "firstName": {
                                    "title": "First name",
                                    "type": "string"
                                },
                                "fullName": {
                                    "title": "Full name",
                                    "type": "string"
                                },
                                "lastName": {
                                    "title": "Last name",
                                    "type": "string"
                                },
                                "middleName": {
                                    "title": "Middle name",
                                    "type": "string"
                                }
                            }
                        }
                    }
                },
                "personID": {
                    "title": "Person ID",
                    "type": "string"
                },
                "repositoryCreatedBy": {
                    "title": "Created by user identifier",
                    "type": "string"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by user identifier",
                    "type": "string"
                }
            },
            "version": "1.0",
            "imsOrg": "{ORG_ID}",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305"
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "id": "a11f44b0214d4fdcb79cbb5e1d93e638",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "id",
            "destination": "_id",
            "name": "id",
            "description": "Identifier field"
        },
        {
            "id": "b9bf7873451f4b7ba767ca3ba9327750",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "firstName",
            "destination": "person.name.firstName",
        },
        {
            "id": "bab961fc18f54789b9268ec04c6f6f9b",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "lastName",
            "destination": "person.name.lastName",
        }
    ],
    "status": "DRAFT",
    "strictMapping": false,
    "allowNullValues": false,
    "xdmVersion": "application/vnd.adobe.xed-full+json;version=1",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
    },
    "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305"
}
```

## Atualizar um conjunto de mapeamento

É possível atualizar um conjunto de mapeamento fornecendo a respectiva ID no caminho de um `PUT` solicitação à `mappingSets` terminal.

**Formato da API**

```http
PUT /mappingSets/{MAPPING_SET_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{MAPPING_SET_ID}` | A ID do conjunto de mapeamento que você deseja atualizar. |

**Solicitação**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/conversion/mappingSets/e7c80e4c0d8f4a98a7d400b4e178b635 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "id",
            "destination": "_id",
            "name": "id",
            "description": "Identifier field"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "firstName",
            "destination": "person.name.firstName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "lastName",
            "destination": "person.name.lastName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "nationality",
            "destination": "person.nationality"           
        }
    ]
}
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre o conjunto de mapeamento recém-atualizado.

>[!NOTE]
>
>A resposta a seguir foi truncada por questões de espaço.

```json
{
    "id": "e7c80e4c0d8f4a98a7d400b4e178b635",
    "version": 1,
    "createdDate": 1614901255000,
    "modifiedDate": 1614909614227,
    "createdBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "modifiedBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "supportVersion": "1.1",
    "outputSchema": {
        "id": "cf0a57df22354cfdb5f32a747b63a456",
        "version": 0,
        "jsonSchema": {
            "title": "A sample schema",
            "description": "My sample schema",
            "type": "object",
            "properties": {
                "_id": {
                    "title": "Identifier",
                    "description": "A unique identifier for the record.",
                    "type": "string",
                },
                "_repo": {
                    "type": "object",
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time"
                        }
                    }
                },
                "createdByBatchID": {
                    "type": "string",
                    "format": "uri-reference"
                },
                "modifiedByBatchID": {
                    "type": "string",
                    "format": "uri-reference"
                },
                "person": {
                    "type": "object",
                    "properties": {
                        "birthDate": {
                            "type": "string",
                            "format": "date"
                        },
                        "birthDayAndMonth": {
                            "type": "string",
                            "pattern": "[0-1][0-9]-[0-9][0-9]"
                        },
                        "birthYear": {
                            "type": "integer",
                            "minimum": 1,
                            "maximum": 32767
                        },
                        "gender": {
                            "type": "string",
                            "default": "not_specified",
                            "enum": [
                                "non_specific",
                                "not_specified",
                                "female",
                                "male"
                            ]
                        },
                        "name": {
                            "title": "Full name",
                            "description": "The person's full name.",
                            "type": "object",
                            "properties": {
                                "firstName": {
                                    "title": "First name",
                                    "type": "string"
                                },
                                "fullName": {
                                    "title": "Full name",
                                    "type": "string"
                                },
                                "lastName": {
                                    "title": "Last name",
                                    "type": "string"
                                },
                                "middleName": {
                                    "title": "Middle name",
                                    "type": "string"
                                },
                                "suffix": {
                                    "title": "Suffix",
                                    "type": "string"
                                }
                            }
                        }
                },
                "personID": {
                    "title": "Person ID",
                    "type": "string"
                },
                "repositoryCreatedBy": {
                    "title": "Created by user identifier",
                    "type": "string"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by user identifier",
                    "type": "string"
                }
            },
            "version": "1.0",
            "imsOrg": "6A29340459CA8D350A49413A@AdobeOrg",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305"
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "id": "1bb13ec5929f4847a8ea0f1d9e60d3e6",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "id",
            "destination": "_id",
            "name": "id"
        },
        {
            "id": "394bec970d54410b98e1d4c55a3843ca",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "firstName",
            "destination": "person.name.firstName"
        },
        {
            "id": "a78729629b22418998b528755b3e0fb1",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "lastName",
            "destination": "person.name.lastName"
        },
        {
            "id": "c5211e1e295f48018c125c24a04e925a",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "nationality",
            "destination": "person.nationality"
        }
    ],
    "strictMapping": false,
    "allowNullValues": false,
    "xdmVersion": "application/vnd.adobe.xed-full+json;version=1",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
    },
    "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305"
}
```

## Listar os mapeamentos de um conjunto de mapeamento

Você pode exibir todos os mapeamentos que pertencem a um conjunto de mapeamentos específico fornecendo a respectiva ID no caminho de uma solicitação GET para o endpoint seguinte.

**Formato da API**

```http
GET /mappingSets/{MAPPING_SET_ID}/mappings
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{MAPPING_SET_ID}` | A ID do conjunto de mapeamento para o qual você deseja recuperar mapeamentos. |

**Solicitação**

A solicitação a seguir retorna todos os mapeamentos do conjunto de mapeamentos especificado.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/mappingSets/e7c80e4c0d8f4a98a7d400b4e178b635/mappings \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

```json
[
    {
        "id": "1bb13ec5929f4847a8ea0f1d9e60d3e6",
        "version": 0,
        "createdDate": 1614909614000,
        "modifiedDate": 1614909614000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceType": "text/x.schema-path",
        "source": "id",
        "destination": "_id",
        "name": "id",
        "description": "Identifier field",
        "identity": false,
        "primaryIdentity": false,
        "matchScore": 0.0,
        "functionVersion": 1,
        "sourceAttribute": "id",
        "destinationXdmPath": "_id"
    },
    {
        "id": "394bec970d54410b98e1d4c55a3843ca",
        "version": 0,
        "createdDate": 1614909614000,
        "modifiedDate": 1614909614000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceType": "text/x.schema-path",
        "source": "firstName",
        "destination": "person.name.firstName",
        "identity": false,
        "primaryIdentity": false,
        "matchScore": 0.0,
        "functionVersion": 1,
        "sourceAttribute": "firstName",
        "destinationXdmPath": "person.name.firstName"
    },
    {
        "id": "a78729629b22418998b528755b3e0fb1",
        "version": 0,
        "createdDate": 1614909614000,
        "modifiedDate": 1614909614000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceType": "text/x.schema-path",
        "source": "lastName",
        "destination": "person.name.lastName",
        "identity": false,
        "primaryIdentity": false,
        "matchScore": 0.0,
        "functionVersion": 1,
        "sourceAttribute": "lastName",
        "destinationXdmPath": "person.name.lastName"
    },
    {
        "id": "c5211e1e295f48018c125c24a04e925a",
        "version": 0,
        "createdDate": 1614909614000,
        "modifiedDate": 1614909614000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceType": "text/x.schema-path",
        "source": "nationality",
        "destination": "person.nationality",
        "identity": false,
        "primaryIdentity": false,
        "matchScore": 0.0,
        "functionVersion": 1,
        "sourceAttribute": "nationality",
        "destinationXdmPath": "person.nationality"
    }
]
```

## Pesquisar um mapeamento em um conjunto de mapeamento

Você pode recuperar um mapeamento específico para um conjunto de mapeamentos, fornecendo as IDs no caminho de uma solicitação GET para o endpoint seguinte.

**Formato da API**

```http
GET /mappingSets/{MAPPING_SET_ID}/mappings/{MAPPING_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{MAPPING_SET_ID}` | A ID do conjunto de mapeamento sobre o qual você deseja pesquisar informações de mapeamento. |
| `{MAPPING_ID}` | A ID do mapeamento que você deseja pesquisar. |

**Solicitação**

A solicitação a seguir recupera informações sobre um mapeamento específico no conjunto de mapeamentos especificado.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/mappingSets/e7c80e4c0d8f4a98a7d400b4e178b635/mappings/394bec970d54410b98e1d4c55a3843ca \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre o mapeamento especificado.

```json
{
    "id": "394bec970d54410b98e1d4c55a3843ca",
    "version": 0,
    "createdDate": 1614909614000,
    "modifiedDate": 1614909614000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sourceType": "text/x.schema-path",
    "source": "firstName",
    "destination": "person.name.firstName",
    "identity": false,
    "primaryIdentity": false,
    "matchScore": 0.0,
    "functionVersion": 1,
    "sourceAttribute": "firstName",
    "destinationXdmPath": "person.name.firstName"
}
```
