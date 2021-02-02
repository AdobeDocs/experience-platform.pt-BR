---
keywords: Experience Platform;home;popular topics;api;API;XDM;sistema XDM;modelo de dados da experiência;Modelo de dados da experiência;Modelo de dados da experiência;modelo de dados;Modelo de dados;exportar;importar;rpc;
solution: Experience Platform
title: Guia de ponto de extremidade Exportar/Importar
description: Os pontos finais /export e /import na API do Registro de Schemas permitem que você compartilhe recursos XDM entre organizações IMS e caixas de proteção.
topic: developer guide
translation-type: tm+mt
source-git-commit: dfa91e387b6fcd0d528a523a06d2516bc8befc20
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---


# Exportar/Importar pontos finais

Todos os recursos dentro de [!DNL Schema Library] estão contidos em uma caixa de proteção específica dentro de uma Organização IMS. Em alguns casos, você pode compartilhar recursos do Experience Data Model (XDM) entre caixas de proteção e Organizações IMS. A API [!DNL Schema Registry] fornece dois pontos de extremidade que permitem gerar uma carga de exportação para qualquer schema, combinação ou tipo de dados na [!DNL  Schema Library] e, em seguida, usar essa carga para importar esse recurso (e todos os recursos dependentes) para uma caixa de proteção de público alvo e uma Organização IMS.

## Introdução

Os pontos de extremidade usados neste guia fazem parte da [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/mixin-registry.yaml). Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de amostra neste documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API de Experience Platform.

Os pontos finais de exportação/importação fazem parte das chamadas de procedimento remoto (RPCs) suportadas pelo [!DNL Schema Registry]. Ao contrário de outros pontos de extremidade na API [!DNL Schema Registry], os pontos de extremidade RPC não exigem cabeçalhos adicionais como `Accept` ou `Content-Type` e não usam um `CONTAINER_ID`. Em vez disso, eles devem usar a namespace `/rpc`, como demonstrado nas chamadas de API abaixo.

## Recuperar uma carga de exportação para um recurso {#export}

Para qualquer schema, combinação ou tipo de dados existente no [!DNL Schema Library], você pode gerar uma carga de exportação, fazendo uma solicitação de GET para o terminal `/export`, fornecendo a ID do recurso no caminho.

**Formato da API**

```http
GET /rpc/export/{RESOURCE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{RESOURCE_ID}` | O `meta:altId` ou `$id` codificado por URL do recurso XDM que você deseja exportar. |

**Solicitação**

A solicitação a seguir recupera uma carga de exportação para uma combinação `Restaurant`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/export/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

**Resposta**

Uma resposta bem-sucedida retorna uma matriz de objetos, que representam o recurso XDM do público alvo e todos os seus recursos dependentes. Neste exemplo, o primeiro objeto na matriz é um tipo de dados `Property` criado pelo locatário que a combinação `Restaurant` emprega, enquanto o segundo objeto é a própria mistura `Restaurant`. Esta carga pode ser usada para [importar o recurso](#import) para uma caixa de proteção ou Organização IMS diferente.

Observe que todas as instâncias da ID de locatário do recurso são substituídas por `<XDM_TENANTID_PLACEHOLDER>`. Isso permite que o Registro do Schema aplique automaticamente a ID do locatário correta aos recursos, dependendo de onde eles são enviados na chamada de importação subsequente.

```json
[
    {
        "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
        "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.datatypes.fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
        "meta:resourceType": "datatypes",
        "version": "1.0",
        "title": "Property",
        "type": "object",
        "description": "",
        "definitions": {
            "customFields": {
                "properties": {
                    "propertyId": {
                        "title": "Property ID",
                        "description": "ID for a company-owned property.",
                        "type": "string",
                        "isRequired": false,
                        "meta:ui": {
                            "ref": [
                                "schema://5fbc29ec292534000055dd55",
                                "#/definitions/customFields"
                            ],
                            "path": "{}._<XDM_TENANTID_PLACEHOLDER>{}.property{}.propertyId",
                            "editable": true,
                            "generateDate": 1606168175975
                        },
                        "meta:xdmType": "string"
                    },
                    "jurisdiction": {
                        "title": "Jurisdiction",
                        "description": "",
                        "type": "string",
                        "isRequired": false,
                        "enum": [
                            "NA",
                            "UK",
                            "EU"
                        ],
                        "meta:enum": {
                            "NA": "North America",
                            "UK": "United Kingdom",
                            "EU": "European Union"
                        },
                        "meta:ui": {
                            "ref": [
                                "schema://5fbc29ec292534000055dd55",
                                "#/definitions/customFields"
                            ],
                            "path": "{}._<XDM_TENANTID_PLACEHOLDER>{}.property{}.jurisdiction",
                            "editable": true,
                            "generateDate": 1606168175975
                        },
                        "meta:xdmType": "string"
                    }
                }
            }
        },
        "allOf": [
            {
                "$ref": "#/definitions/customFields",
                "type": "object",
                "meta:xdmType": "object"
            }
        ],
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:xdmType": "object",
        "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "meta:sandboxType": "production"
    },
    {
        "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:resourceType": "mixins",
        "version": "1.0",
        "title": "Restaurant",
        "type": "object",
        "description": "",
        "definitions": {
            "customFields": {
                "type": "object",
                "properties": {
                    "_<XDM_TENANTID_PLACEHOLDER>": {
                        "type": "object",
                        "properties": {
                            "capacity": {
                                "title": "Capacity",
                                "description": "Restaurant capacity",
                                "type": "string",
                                "isRequired": false,
                                "meta:xdmType": "string"
                            },
                            "kitchen": {
                                "title": "Kitchen Style",
                                "description": "Style of kitchen",
                                "type": "string",
                                "isRequired": false,
                                "meta:xdmType": "string"
                            },
                            "rating": {
                                "title": "Rating",
                                "description": "",
                                "type": "integer",
                                "isRequired": false,
                                "meta:xdmType": "int"
                            },
                            "property": {
                                "title": "Property",
                                "description": "",
                                "$ref": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
                                "type": "object",
                                "meta:xdmType": "object"
                            }
                        },
                        "meta:xdmType": "object"
                    }
                },
                "meta:xdmType": "object"
            }
        },
        "allOf": [
            {
                "$ref": "#/definitions/customFields",
                "type": "object",
                "meta:xdmType": "object"
            }
        ],
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [],
        "meta:xdmType": "object",
        "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "meta:sandboxType": "production"
    }
]
```

## Importar um recurso {#import}

Depois que [tiver gerado uma carga de exportação](#export) para um recurso XDM, você poderá usar essa carga em uma solicitação de POST para o terminal `/import` para importar esse recurso para uma Organização IMS de público alvo e uma caixa de proteção.

**Formato da API**

```http
POST /rpc/import
```

**Solicitação**

A solicitação a seguir pega a carga retornada no exemplo [export](#export) anterior para importar a combinação `Restaurant` para uma nova Organização IMS e caixa de proteção, conforme determinado pelos cabeçalhos `x-gw-ims-org-id` e `x-sandbox-name`, respectivamente.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/import \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
          "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.datatypes.fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
          "meta:resourceType": "datatypes",
          "version": "1.0",
          "title": "Property",
          "type": "object",
          "description": "",
          "definitions": {
            "customFields": {
              "properties": {
                "propertyId": {
                  "title": "Property ID",
                  "description": "ID for a company-owned property.",
                  "type": "string",
                  "isRequired": false,
                  "meta:ui": {
                    "ref": [
                      "schema://5fbc29ec292534000055dd55",
                      "#/definitions/customFields"
                    ],
                    "path": "{}._<XDM_TENANTID_PLACEHOLDER>{}.property{}.propertyId",
                    "editable": true,
                    "generateDate": 1606168175975
                  },
                  "meta:xdmType": "string"
                },
                "jurisdiction": {
                  "title": "Jurisdiction",
                  "description": "",
                  "type": "string",
                  "isRequired": false,
                  "enum": [
                    "NA",
                    "UK",
                    "EU"
                  ],
                  "meta:enum": {
                    "NA": "North America",
                    "UK": "United Kingdom",
                    "EU": "European Union"
                  },
                  "meta:ui": {
                    "ref": [
                      "schema://5fbc29ec292534000055dd55",
                      "#/definitions/customFields"
                    ],
                    "path": "{}._<XDM_TENANTID_PLACEHOLDER>{}.property{}.jurisdiction",
                    "editable": true,
                    "generateDate": 1606168175975
                  },
                  "meta:xdmType": "string"
                }
              }
            }
          },
          "allOf": [
            {
              "$ref": "#/definitions/customFields",
              "type": "object",
              "meta:xdmType": "object"
            }
          ],
          "meta:extensible": true,
          "meta:abstract": true,
          "meta:xdmType": "object",
          "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
          "meta:sandboxType": "production"
        },
        {
          "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
          "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
          "meta:resourceType": "mixins",
          "version": "1.0",
          "title": "Restaurant",
          "type": "object",
          "description": "",
          "definitions": {
            "customFields": {
              "type": "object",
              "properties": {
                "_<XDM_TENANTID_PLACEHOLDER>": {
                  "type": "object",
                  "properties": {
                    "capacity": {
                      "title": "Capacity",
                      "description": "Restaurant capacity",
                      "type": "string",
                      "isRequired": false,
                      "meta:xdmType": "string"
                    },
                    "kitchen": {
                      "title": "Kitchen Style",
                      "description": "Style of kitchen",
                      "type": "string",
                      "isRequired": false,
                      "meta:xdmType": "string"
                    },
                    "rating": {
                      "title": "Rating",
                      "description": "",
                      "type": "integer",
                      "isRequired": false,
                      "meta:xdmType": "int"
                    },
                    "property": {
                      "title": "Property",
                      "description": "",
                      "$ref": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
                      "type": "object",
                      "meta:xdmType": "object"
                    }
                  },
                  "meta:xdmType": "object"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "allOf": [
            {
              "$ref": "#/definitions/customFields",
              "type": "object",
              "meta:xdmType": "object"
            }
          ],
          "meta:extensible": true,
          "meta:abstract": true,
          "meta:intendedToExtend": [
            
          ],
          "meta:xdmType": "object",
          "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
          "meta:sandboxType": "production"
        }
      ]'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista dos recursos importados, com os valores apropriados de ID de locatário e Organização IMS aplicados.

```json
[
    {
        "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
        "meta:altId": "_{TENANT_ID}.datatypes.fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
        "meta:resourceType": "datatypes",
        "version": "1.0",
        "title": "Property",
        "type": "object",
        "description": "",
        "definitions": {
            "customFields": {
                "properties": {
                    "propertyId": {
                        "title": "Property ID",
                        "description": "ID for a company-owned property.",
                        "type": "string",
                        "isRequired": false,
                        "meta:ui": {
                            "ref": [
                                "schema://5fbc29ec292534000055dd55",
                                "#/definitions/customFields"
                            ],
                            "path": "{}._{TENANT_ID}{}.property{}.propertyId",
                            "editable": true,
                            "generateDate": 1606168175975
                        },
                        "meta:xdmType": "string"
                    },
                    "jurisdiction": {
                        "title": "Jurisdiction",
                        "description": "",
                        "type": "string",
                        "isRequired": false,
                        "enum": [
                            "NA",
                            "UK",
                            "EU"
                        ],
                        "meta:enum": {
                            "NA": "North America",
                            "UK": "United Kingdom",
                            "EU": "European Union"
                        },
                        "meta:ui": {
                            "ref": [
                                "schema://5fbc29ec292534000055dd55",
                                "#/definitions/customFields"
                            ],
                            "path": "{}._{TENANT_ID}{}.property{}.jurisdiction",
                            "editable": true,
                            "generateDate": 1606168175975
                        },
                        "meta:xdmType": "string"
                    }
                }
            }
        },
        "allOf": [
            {
                "$ref": "#/definitions/customFields",
                "type": "object",
                "meta:xdmType": "object"
            }
        ],
        "refs": [],
        "imsOrg": "{IMS_ORG}",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:xdmType": "object",
        "meta:registryMetadata": {
            "repo:createdDate": 1606250624257,
            "repo:lastModifiedDate": 1606250624257,
            "xdm:createdClientId": "{CLIENT_ID}",
            "xdm:lastModifiedClientId": "{CLIENT_ID}",
            "xdm:createdUserId": "{USER_ID}",
            "xdm:lastModifiedUserId": "{USER_ID}",
            "eTag": "9dadfaf8168af30eae1a745de95eace760680cfc9a69bcc938f68fe3caf57317",
            "meta:globalLibVersion": "1.16.3"
        },
        "meta:containerId": "tenant",
        "meta:sandboxId": "52c8dbe0-ced2-11e9-a524-cd79ba95ea3a",
        "meta:sandboxType": "production",
        "meta:tenantNamespace": "_{TENANT_ID}"
    },
    {
        "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:altId": "_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:resourceType": "mixins",
        "version": "1.0",
        "title": "Restaurant",
        "type": "object",
        "description": "",
        "definitions": {
            "customFields": {
                "type": "object",
                "properties": {
                    "_{TENANT_ID}": {
                        "type": "object",
                        "properties": {
                            "capacity": {
                                "title": "Capacity",
                                "description": "Restaurant capacity",
                                "type": "string",
                                "isRequired": false,
                                "meta:xdmType": "string"
                            },
                            "kitchen": {
                                "title": "Kitchen Style",
                                "description": "Style of kitchen",
                                "type": "string",
                                "isRequired": false,
                                "meta:xdmType": "string"
                            },
                            "rating": {
                                "title": "Rating",
                                "description": "",
                                "type": "integer",
                                "isRequired": false,
                                "meta:xdmType": "int"
                            },
                            "property": {
                                "title": "Property",
                                "description": "",
                                "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
                                "type": "object",
                                "meta:xdmType": "object"
                            }
                        },
                        "meta:xdmType": "object"
                    }
                },
                "meta:xdmType": "object"
            }
        },
        "allOf": [
            {
                "$ref": "#/definitions/customFields",
                "type": "object",
                "meta:xdmType": "object"
            }
        ],
        "refs": [
            "https://ns.adobe.com/{TENANT_ID}/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495"
        ],
        "imsOrg": "{IMS_ORG}",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [],
        "meta:xdmType": "object",
        "meta:registryMetadata": {
            "repo:createdDate": 1606250624357,
            "repo:lastModifiedDate": 1606250624357,
            "xdm:createdClientId": "{CLIENT_ID}",
            "xdm:lastModifiedClientId": "{CLIENT_ID}",
            "xdm:createdUserId": "{USER_ID}",
            "xdm:lastModifiedUserId": "{USER_ID}",
            "eTag": "5a5401ba8e6845b2f42d330002331e6e96c031c4e228f860423a3d5cd3598b40",
            "meta:globalLibVersion": "1.16.3"
        },
        "meta:containerId": "tenant",
        "meta:sandboxId": "52c8dbe0-ced2-11e9-a524-cd79ba95ea3a",
        "meta:sandboxType": "production",
        "meta:tenantNamespace": "_{TENANT_ID}"
    }
]
```
