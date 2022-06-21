---
title: Exportar ponto de extremidade da API
description: O endpoint /export na API do Registro de Schema permite compartilhar recursos XDM entre sandboxes.
source-git-commit: 2a58236031834bbe298576e2fcab54b04ec16ac3
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 2%

---

# Exportar ponto de extremidade

Todos os recursos da [!DNL Schema Library] estão contidos em uma sandbox específica no Adobe Experience Platform. Em alguns casos, você pode compartilhar os recursos do Experience Data Model (XDM) entre sandboxes e organizações. O `/rpc/export` endpoint no [!DNL Schema Registry] A API permite gerar uma carga de exportação para qualquer esquema, grupo de campos de esquema ou tipo de dados no [!DNL Schema Library]e, em seguida, use essa carga para importar esse recurso (e todos os recursos dependentes) para uma sandbox e organização de destino por meio do [`/rpc/import` endpoint](./import.md).

## Introdução

O `/rpc/export` o ponto de extremidade é parte do [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Antes de continuar, reveja o [guia de introdução](./getting-started.md) para links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

O `/rpc/export` o ponto de extremidade faz parte das chamadas de procedimento remoto (RPCs) suportadas pelo [!DNL Schema Registry]. Diferente de outros endpoints no [!DNL Schema Registry] A API, os pontos de extremidade RPC não exigem cabeçalhos adicionais como `Accept` ou `Content-Type`e não use um `CONTAINER_ID`. Em vez disso, eles devem usar o `/rpc` namespace, conforme demonstrado nas chamadas de API abaixo.

## Gerar uma carga de exportação para um recurso {#export}

Para qualquer esquema, grupo de campos ou tipo de dados existente na [!DNL Schema Library], você pode gerar uma carga de exportação fazendo uma solicitação GET para a variável `/export` endpoint, fornecendo a ID do recurso no caminho.

**Formato da API**

```http
GET /rpc/export/{RESOURCE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{RESOURCE_ID}` | O `meta:altId` ou codificado por URL `$id` do recurso XDM que você deseja exportar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir recupera uma carga de exportação para um `Restaurant` grupo de campos.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/export/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

**Resposta**

Uma resposta bem-sucedida retorna uma matriz de objetos, que representam o recurso XDM de destino e todos os seus recursos dependentes. Neste exemplo, o primeiro objeto na matriz é um locatário criado `Property` tipo de dados que a variável `Restaurant` grupo de campos emprega, enquanto o segundo objeto é o `Restaurant` grupo de campos. Essa carga pode ser usada para [importar o recurso](#import) em uma sandbox diferente ou Organização IMS.

Observe que todas as instâncias da ID de locatário do recurso são substituídas por `<XDM_TENANTID_PLACEHOLDER>`. Isso permite que o Registro de esquema aplique automaticamente a ID de locatário correta aos recursos, dependendo de onde eles são enviados na chamada de importação subsequente.

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

## Importar o recurso {#import}

Depois de gerar a carga de exportação do arquivo CSV, você pode enviar essa carga para o `/rpc/import` endpoint para gerar o schema .

Consulte a [guia de endpoint de importação](./import.md) para obter detalhes sobre como gerar schemas a partir de cargas de exportação.
