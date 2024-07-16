---
keywords: Experience Platform;página inicial;tópicos populares;preparação de dados;guia de api;esquemas;
solution: Experience Platform
title: Endpoint da API de esquemas
description: Você pode usar o endpoint "/schemas" na API do Adobe Experience Platform para recuperar, criar e atualizar esquemas de forma programática para uso com o Mapeador na plataforma.
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 4%

---



# Endpoint de esquemas

Os esquemas podem ser usados com o Mapeador para garantir que os dados assimilados na Adobe Experience Platform correspondam ao que você deseja assimilar. Você pode usar o ponto de extremidade `/schemas` para criar, listar e obter esquemas personalizados de forma programática para usar com o Mapeador na Plataforma.

>[!NOTE]
>
>Os esquemas criados usando esse endpoint são usados exclusivamente com Mapeadores e conjuntos de mapeamento. Para criar esquemas acessíveis por outros serviços da Platform, leia o [guia do desenvolvedor do Registro de Esquemas](../../xdm/api/schemas.md).

## Obter todos os esquemas

Você pode recuperar uma lista de todos os esquemas do Mapeador disponíveis para sua organização fazendo uma solicitação GET para o ponto de extremidade `/schemas`.

**Formato da API**

O ponto de extremidade `/schemas` dá suporte a vários parâmetros de consulta para ajudar você a filtrar os resultados. Embora a maioria desses parâmetros seja opcional, seu uso é altamente recomendado para ajudar a reduzir a sobrecarga cara. No entanto, você deve incluir os parâmetros `start` e `limit` como parte de sua solicitação. Vários parâmetros podem ser incluídos, separados por &quot;E&quot; comercial (`&`).

```http
GET /schemas?limit={LIMIT}&start={START}
GET /schemas?limit={LIMIT}&start={START}&name={NAME}
GET /schemas?limit={LIMIT}&start={START}&orderBy={ORDER_BY}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{LIMIT}` | **Obrigatório**. Especifica o número de esquemas retornados. |
| `{START}` | **Obrigatório**. Especifica o deslocamento das páginas de resultados. Para obter a primeira página de resultados, defina o valor como `start=0`. |
| `{NAME}` | Filtra o esquema com base no nome. |
| `{ORDER_BY}` | Classifica a ordem dos resultados. Os campos com suporte são `modifiedDate` e `createdDate`. Você pode anexar a propriedade a `+` ou `-` como prefixo para classificá-la por ordem crescente ou decrescente, respectivamente. |

**Solicitação**

A solicitação a seguir recupera os dois últimos esquemas criados para sua organização.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas&start=0&limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A resposta a seguir retorna o status HTTP 200 com uma lista dos esquemas solicitados.

>[!NOTE]
>
>A resposta a seguir foi truncada por questões de espaço.

```json
{
    "data": [
        {
            "id": "823ac494f35e4e84bcb2f061378fcca6",
            "version": 0,
            "jsonSchema": {
                "title": "Sample schema",
                "type": "object",
                "properties": {
                    "_id": {
                        "title": "Identifier",
                        "description": "A unique identifier for the record.",
                        "type": "string",
                        "format": "uri-reference",
                        "meta:xdmField": "@id",
                        "meta:xdmType": "string"
                    },
                    "city": {
                        "title": "City",
                        "description": "The name of the city.",
                        "type": "string",
                        "meta:xdmField": "xdm:city",
                        "meta:xdmType": "string"
                    }
                }
            },
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc",
                "contentType": "1.0"
            }
        },
        {
            "id": "0f868d3a1b804fb0abf738306290ae79",
            "version": 0,
            "jsonSchema": {
                "title": "Sample schema 2",
                "type": "object",
                "properties": {
                    "_id": {
                        "title": "Identifier",
                        "description": "A unique identifier for the record.",
                        "type": "string",
                        "format": "uri-reference",
                        "meta:xdmField": "@id",
                        "meta:xdmType": "string"
                    },
                    "city": {
                        "title": "City",
                        "description": "The name of the city.",
                        "type": "string",
                        "meta:xdmField": "xdm:city",
                        "meta:xdmType": "string"
                    }
                }
            },
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/0f868d3a1b804fb0abf738306290ae79",
                "contentType": "1.0"
            }
        }
    ],
    "_page": {
        "count": 2,
        "limit": 2
    }
}
```

## Criar um esquema

Você pode criar um esquema para validação fazendo uma solicitação POST para o ponto de extremidade `/schemas`. Há três maneiras de criar um esquema: enviar um [Esquema JSON](https://json-schema.org/), usar dados de exemplo ou fazer referência a um esquema XDM existente.

```http
POST /schemas
```

### Uso de um esquema JSON

**Solicitação**

A solicitação a seguir permite criar um esquema enviando um [Esquema JSON](https://json-schema.org/).

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações sobre o esquema recém-criado.

```json
{
    "id": "6daffabf14b1425292add3719afc8fab",
    "version": 0,
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}
```

### Uso de dados de amostra

**Solicitação**

A solicitação a seguir permite criar um esquema usando dados de amostra carregados anteriormente.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "sampleId": "45439a93d48d47d098d26e0f0840cc02"  
 }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `sampleId` | A ID dos dados de amostra dos quais você está baseando o esquema. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações sobre o esquema recém-criado.

```json
{
    "id": "b2ee78bd55ac45f781a93fb8b90d99b2",
    "version": 0,
    "jsonSchema": {
        "title": "SampleSchema:45439a93d48d47d098d26e0f0840cc02",
        "type": "object",
        "properties": {
            "gender": {
                "title": "gender",
                "type": "string"
            },
            "last_name": {
                "title": "last_name",
                "type": "string"
            },
            "id": {
                "title": "id",
                "type": "string"
            },
            "ip_address": {
                "title": "ip_address",
                "type": "string"
            },
            "first_name": {
                "title": "first_name",
                "type": "string"
            },
            "email": {
                "title": "email",
                "type": "string"
            }
        }
    },
    "sampleId": "45439a93d48d47d098d26e0f0840cc02"
}
```

### Consulte um esquema XDM

**Solicitação**

A solicitação a seguir permite criar um esquema fazendo referência a um esquema XDM existente.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "name": "outputSchema1",
     "schemaRef": {
         "id": "https://ns.adobe.com/{TENANT_ID}/schemas/0d555890502224d187b619f23c35c8d1",
         "contentType": "application/vnd.adobe.xed-full+json;version=1"
     }  
 }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `name` | O nome do esquema que você deseja criar. |
| `schemaRef.id` | A ID do esquema que você está referenciando. |
| `schemaRef.contentType` | Determina o formato de resposta do esquema referenciado. Mais informações sobre este campo podem ser encontradas no [guia do desenvolvedor do registro de esquema](../../xdm/api/schemas.md#lookup) |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações sobre o esquema recém-criado.

>[!NOTE]
>
>A resposta a seguir foi truncada por questões de espaço.

```json
{
    "id": "4b64daa51b774cb2ac21b61d80125ed0",
    "version": 0,
    "name": "schemaName",
    "jsonSchema": "{\"id\":null,\"schema\":null,\"_refId\":null,\"title\":\"SimpleUser\",...,\"imsOrg\":\"{ORG_ID}\",\"$id\":\"https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96\"}",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96",
        "contentType": "application/vnd.adobe.xed+json;version=1.0"
    }
}
```

## Criar um esquema usando o upload de arquivo

Você pode criar um esquema fazendo upload de um arquivo JSON para ele converter de.

**Formato da API**

```http
POST /schemas/upload
```

**Solicitação**

A solicitação a seguir permite criar um esquema a partir de um arquivo JSON carregado.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas/upload \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: multipart/form-data' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -F 'file=@{PATH_TO_FILE}.json'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações sobre o esquema recém-criado.

```json
{
    "id": "292add3716daffabf14b14259afc8fab",
    "version": 0,
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}
```

## Recuperar um esquema específico

Você pode recuperar informações sobre um esquema específico fazendo uma solicitação GET para o ponto de extremidade `/schemas` e fornecendo a ID do esquema que você deseja recuperar no caminho da solicitação.

**Formato da API**

```http
GET /schemas/{SCHEMA_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{SCHEMA_ID}` | A ID do esquema que você está pesquisando. |

**Solicitação**

A solicitação a seguir recupera informações sobre o esquema especificado.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas/0f868d3a1b804fb0abf738306290ae79 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações sobre o esquema especificado.

```json
{
    "id": "0f868d3a1b804fb0abf738306290ae79",
    "version": 0,
    "jsonSchema": {
        "title": "Sample schema",
        "description": "Sample description",
        "type": "object",
        "properties": {
            "_id": {
                "title": "Identifier",
                "description": "A unique identifier for the record.",
                "type": "string",
                "format": "uri-reference",
                "meta:xdmField": "@id",
                "meta:xdmType": "string"
            },
            "personalEmail": {
                "title": "Personal Email",
                "description": "A personal email address.",
                "type": "object",
                "properties": {
                    "primary": {
                        "title": "Primary",
                        "description": "Primary email indicator.\n\nA Profile can have only one `primary` email address at a given point of time.\n",
                        "type": "boolean",
                        "meta:xdmField": "xdm:primary",
                        "meta:xdmType": "boolean"
                    },
                    "address": {
                        "title": "Address",
                        "description": "The technical address, e.g 'name@domain.com' as commonly defined in RFC2822 and subsequent standards.",
                        "type": "string",
                        "format": "email",
                        "meta:xdmField": "xdm:address",
                        "meta:xdmType": "string"
                    }
                },
                "meta:xdmField": "xdm:personalEmail",
                "meta:referencedFrom": "https://ns.adobe.com/xdm/context/emailaddress",
                "meta:xdmType": "object"
            }
        },
        "imsOrg": "6A29340459CA8D350A49413A@AdobeOrg",
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc"
    },
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc",
        "contentType": "1.0"
    }
}
```
