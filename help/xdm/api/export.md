---
title: Exportar endpoint de API
description: O ponto de extremidade /export na API do Registro de esquema permite compartilhar recursos XDM entre sandboxes.
exl-id: 1dcbfa59-af98-4db5-b6f4-f848e5bf5e81
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 1%

---

# Exportar endpoint

Todos os recursos em [!DNL Schema Library] estão contidos em uma sandbox específica no Adobe Experience Platform. Em alguns casos, é possível compartilhar recursos do Experience Data Model (XDM) entre sandboxes e organizações. O ponto de extremidade `/rpc/export` na API [!DNL Schema Registry] permite gerar uma carga de exportação para qualquer esquema, grupo de campos de esquema ou tipo de dados no [!DNL Schema Library] e, em seguida, usar essa carga para importar esse recurso (e todos os recursos dependentes) para uma sandbox e organização de destino por meio do ponto de extremidade [`/rpc/import`](./import.md).

## Introdução

O ponto de extremidade `/rpc/export` faz parte da [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas para qualquer API Experience Platform com êxito.

O ponto de extremidade `/rpc/export` faz parte das chamadas de procedimento remoto (RPCs) para as quais o [!DNL Schema Registry] oferece suporte. Ao contrário de outros pontos de extremidade na API [!DNL Schema Registry], os pontos de extremidade RPC não exigem cabeçalhos adicionais como `Accept` ou `Content-Type` e não usam `CONTAINER_ID`. Em vez disso, eles devem usar o namespace `/rpc`, conforme demonstrado nas chamadas de API abaixo.

## Gerar uma carga de exportação para um recurso {#export}

Para qualquer esquema, grupo de campos ou tipo de dados existente no [!DNL Schema Library], você pode gerar uma carga de exportação fazendo uma solicitação GET para o ponto de extremidade `/export`, fornecendo a ID do recurso no caminho.

**Formato da API**

```http
GET /rpc/export/{RESOURCE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{RESOURCE_ID}` | O `meta:altId` ou o `$id` codificado em URL do recurso XDM que você deseja exportar. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir recupera uma carga de exportação para um grupo de campos `Restaurant`.

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

Uma resposta bem-sucedida retorna uma matriz de objetos, que representa o recurso XDM de destino e todos os recursos dependentes. Neste exemplo, o primeiro objeto na matriz é um tipo de dados `Property` criado por locatário que o grupo de campos `Restaurant` emprega, enquanto o segundo objeto é o próprio grupo de campos `Restaurant`. Essa carga pode ser usada para [importar o recurso](#import) para uma sandbox ou organização diferente.

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

Depois de gerar a carga de exportação do arquivo CSV, você pode enviar essa carga para o ponto de extremidade `/rpc/import` para gerar o esquema.

Consulte o [manual de endpoint de importação](./import.md) para obter detalhes sobre como gerar esquemas a partir de cargas de exportação.
