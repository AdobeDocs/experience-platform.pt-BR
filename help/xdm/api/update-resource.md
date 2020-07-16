---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Atualizar um recurso
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 2%

---


# Atualizar um recurso

Você pode modificar ou atualizar recursos no container locatário usando uma solicitação PATCH. O [!DNL Schema Registry] oferece suporte a todas as operações padrão de Patch JSON, incluindo adicionar, remover e substituir.

Para obter mais informações sobre o Patch JSON, incluindo operações disponíveis, consulte a documentação [oficial do Patch](http://jsonpatch.com/)JSON.

>[!NOTE]
>
>Se quiser substituir um recurso inteiro por novos valores em vez de atualizar campos individuais, consulte o documento sobre a [substituição de um recurso usando uma operação](replace-resource.md)PUT.

## Adicionar misturas a um schema

Uma das operações PATCH mais comuns envolve a adição de misturas previamente definidas a um schema XDM, como demonstrado pelo exemplo abaixo.

**Formato da API**

```http
PATCH /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parâmetro | Descrição |
| --- | --- |
| `{RESOURCE_TYPE}` | O tipo de recurso a ser atualizado do [!DNL Schema Library]. Os tipos válidos são `datatypes`, `mixins`, `schemas`e `classes`. |
| `{RESOURCE_ID}` | O `$id` URI codificado por URL ou `meta:altId` do recurso. |

**Solicitação**

Usando uma operação PATCH, você pode atualizar um schema para incluir campos definidos em uma combinação criada anteriormente. Para fazer isso, você deve executar uma solicitação PATCH para o schema usando sua `meta:altId` ou a `$id` URL codificada.

O corpo da solicitação inclui a operação (`op`) que você deseja executar, onde (`path`) você gostaria de executar a operação e que informações (`value`) você gostaria de incluir na operação. Neste exemplo, o `$id` valor do mixin está sendo adicionado aos campos `meta:extends` e `allOf` do schema do público alvo.

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "add", "path": "/meta:extends/-", "value":  "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"},
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"}}
      ]'
```

**Resposta**

A resposta mostra que ambas as operações foram executadas com êxito. A mistura `$id` foi adicionada à `meta:extends` matriz e uma referência (`$ref`) à mistura `$id` agora aparece na `allOf` matriz.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Atualizar campos individuais para um recurso

Você também pode enviar solicitações PATCH que fazem várias alterações em campos individuais dentro de um recurso de Registro de Schemas.

**Formato da API**

```SHELL
PATCH /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parâmetro | Descrição |
| --- | --- |
| `{RESOURCE_TYPE}` | O tipo de recurso a ser atualizado do [!DNL Schema Library]. Os tipos válidos são `datatypes`, `mixins`, `schemas`e `classes`. |
| `{RESOURCE_ID}` | O `$id` URI codificado por URL ou `meta:altId` do recurso. |

**Solicitação**

O corpo da solicitação inclui a operação (`op`), o local (`path`) e as informações (`value`) necessárias para atualizar o mixin. Esta solicitação atualiza a combinação Detalhes da propriedade para remover o campo &quot;propertyCity&quot; e adicionar um novo campo &quot;propertyAddress&quot; que faz referência a um tipo de dados padrão que contém informações de endereço. Ele também adiciona um novo campo &quot;emailAddress&quot; que faz referência a um tipo de dados padrão com informações de email.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.e49cbb2eec33618f686b8344b4597ecf \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
          { "op": "remove", "path": "/definitions/vehicles/properties/_{TENANT_ID}/properties/propertyCity"},
          { "op": "add", "path": "/definitions/property/properties/_{TENANT_ID}/properties/propertyAddress", "value":
            {
              "title": "Property Address",
              "description": "Address of the Property",
              "$ref": "https://ns.adobe.com/xdm/common/address"
            } 
          },
          { "op": "add", "path": "/definitions/property/properties/_{TENANT_ID}/properties/emailAddress", "value":
            {
              "title": "Property Email Address",
              "description": "Email address of the Property",
              "$ref": "https://ns.adobe.com/xdm/context/emailaddress"
            } 
          },
      ]'
```

**Resposta**

Uma resposta bem-sucedida mostra que as operações foram concluídas com êxito porque os novos campos estão presentes e o campo &quot;propertyCity&quot; foi removido.

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
                        },
                        "propertyAddress": {
                            "title": "Property Address",
                            "description": "Address of the Property",
                            "$ref": "https://ns.adobe.com/xdm/common/address"
                        },
                        "emailAddress": {
                            "title": "Property Email Address",
                            "description": "Email address of the Property",
                            "$ref": "https://ns.adobe.com/xdm/context/emailaddress"
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
    "version": "1.1",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1552088205144,
        "repo:lastModifiedDate": 1552089776535,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```
