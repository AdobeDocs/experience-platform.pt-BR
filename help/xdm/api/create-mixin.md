---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;mixin;Mixin;mixins;Mixins;create
solution: Experience Platform
title: Criar uma mistura
topic: developer guide
description: Mixins são um conjunto de campos usados para descrever um conceito específico, como "endereço" ou "preferências de perfil". Há várias combinações padrão disponíveis ou você pode definir suas próprias quando quiser capturar informações exclusivas de sua organização.
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---


# Criar uma mistura

Mixins são um conjunto de campos usados para descrever um conceito específico, como &quot;endereço&quot; ou &quot;preferências de perfil&quot;. Há várias combinações padrão disponíveis ou você pode definir suas próprias quando quiser capturar informações exclusivas de sua organização. Cada mistura contém um `meta:intendedToExtend` campo que lista as classes com as quais a mistura é compatível.

Você pode achar útil revisar todas as combinações disponíveis para se familiarizar com os campos incluídos em cada uma. Você pode lista (GET) todas as combinações compatíveis com uma classe específica executando uma solicitação em relação a cada um dos container &quot;global&quot; e &quot;locatário&quot;, retornando somente as combinações nas quais o campo &quot;meta:pretendidoToExtend&quot; corresponde à classe que você está usando. Os exemplos abaixo retornarão todas as combinações que podem ser usadas com a [!DNL XDM Individual Profile] classe:

```http
GET /global/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
GET /tenant/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
```

A solicitação de API de exemplo abaixo cria uma nova combinação no container do locatário.

**Formato da API**

```http
POST /tenant/mixins
```

**Solicitação**

Ao definir uma nova combinação, ela deve incluir um `meta:intendedToExtend` `$id` atributo, listando as classes com as quais a mistura é compatível. Neste exemplo, a combinação é compatível com a classe Property definida anteriormente. Campos personalizados devem ser aninhados em `_{TENANT_ID}` (como mostrado no exemplo) para evitar colisões com outras combinações ou campos dos schemas de classe. Observe que o `propertyConstruction` campo é uma referência ao tipo de dados criado na chamada anterior.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Details",
        "description":"Detailed information related to the properties owned and operated by the company.",
        "type":"object",
        "meta:intendedToExtend":["https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"],
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
              "type":"object",
              "properties": {
                  "propertyName": {
                    "type": "string",
                    "title": "Property Name",
                    "description": "Name of the property"
                  },
                  "propertyCity": {
                    "title": "Property City",
                    "description": "City where the property is located.",
                    "type": "string"
                  },
                  "phoneNumber": {
                    "title": "Phone Number",
                    "description": "Primary phone number for the property.",
                    "type": "string"
                  },
                  "propertyType": {
                    "type": "string",
                    "title": "Property Type",
                    "description": "Type and primary use of property.",
                    "enum": [
                        "retail",
                        "yoga",
                        "fitness"
                    ],
                    "meta:enum": {
                        "retail": "Retail Store",
                        "yoga": "Yoga Studio",
                        "fitness": "Fitness Center"
                    }
                  },
                  "propertyConstruction": {
                    "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
                  }
                }
              }
            }
          }
        },
        "allOf": [
            {
                "$ref": "#/definitions/property"
            }
        ]
}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) e uma carga que contém os detalhes da combinação recém-criada, incluindo o `$id`, `meta:altId`e `version`. Esses valores são somente leitura e são atribuídos pelo [!DNL Schema Registry].

```JSON
{
    "title": "Property Details",
    "description": "Detailed information related to the properties owned and operated by the company.",
    "type": "object",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
    ],
    "definitions": {
        "property": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "propertyName": {
                            "type": "string",
                            "title": "Property Name",
                            "description": "Name of the property",
                            "meta:xdmType": "string"
                        },
                        "propertyCity": {
                            "title": "Property City",
                            "description": "City where the property is located.",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "phoneNumber": {
                            "title": "Phone Number",
                            "description": "Primary phone number for the property.",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "propertyType": {
                            "type": "string",
                            "title": "Property Type",
                            "description": "Type and primary use of property.",
                            "enum": [
                                "retail",
                                "yoga",
                                "fitness"
                            ],
                            "meta:enum": {
                                "retail": "Retail Store",
                                "yoga": "Yoga Studio",
                                "fitness": "Fitness Center"
                            },
                            "meta:xdmType": "string"
                        },
                        "propertyConstruction": {
                            "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/property"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.mixins.e49cbb2eec33618f686b8344b4597ecf",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf",
    "version": "1.0",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1552088205144,
        "repo:lastModifiedDate": 1552088205144,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

A execução de uma solicitação de GET para lista de todas as combinações no container locatário agora inclui a combinação Detalhes do veículo, ou você pode executar uma solicitação de pesquisa (GET) usando o `$id` URI codificado por URL para visualização direta da nova combinação. Lembre-se de incluir o `version` no cabeçalho Aceitar para todas as solicitações de pesquisa.
