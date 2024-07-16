---
title: Substituir um campo XDM na API
description: Saiba como descontinuar campos do Experience Data Model (XDM) na API do registro de esquema.
exl-id: e49517c4-608d-4e05-8466-75724ca984a8
source-git-commit: f9f783b75bff66d1bf3e9c6d1ed1c543bd248302
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 6%

---

# Substituir um campo XDM na API

No Experience Data Model (XDM), você pode descontinuar um campo em um esquema ou recurso personalizado usando a [API do Registro de esquema](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). A descontinuação de um campo faz com que ele fique oculto nas interfaces downstream, como o espaço de trabalho e o Customer Journey Analytics [!UICONTROL Perfis], mas caso contrário é uma alteração ininterrupta e não afeta negativamente os fluxos de dados existentes.

Este documento aborda como descontinuar campos para diferentes recursos XDM. Para obter etapas sobre como descontinuar um campo XDM usando o Editor de esquemas na interface do usuário do Experience Platform, consulte o tutorial sobre [como descontinuar um campo XDM na interface do usuário](./field-deprecation-ui.md).

## Introdução

Este tutorial requer a realização de chamadas para a API do registro de esquema. Consulte o [guia do desenvolvedor](../api/getting-started.md) para obter informações importantes que você precisa saber para fazer essas chamadas de API. Isso inclui o `{TENANT_ID}`, o conceito de &quot;contêineres&quot; e os cabeçalhos necessários para fazer solicitações (com atenção especial ao cabeçalho `Accept` e seus valores possíveis).

## Substituir um campo personalizado {#custom}

Para descontinuar um campo em uma classe personalizada, grupo de campos ou tipo de dados, atualize o recurso personalizado por meio de uma solicitação PUT ou PATCH e adicione o atributo `meta:status: deprecated` ao campo em questão.

>[!NOTE]
>
>Para obter informações gerais sobre como atualizar recursos personalizados no XDM, consulte a seguinte documentação:
>
>* [Atualizar uma classe](../api/classes.md#patch)
>* [Atualizar um grupo de campos](../api/field-groups.md#patch)
>* [Atualizar um tipo de dados](../api/data-types.md#patch)

A chamada de API de exemplo abaixo substitui um campo em um tipo de dados personalizado.

**Formato da API**

```http
PATCH /tenant/datatypes/{DATA_TYPE_ID}
```

**Solicitação**

A solicitação a seguir substitui o campo `expansionArea` para um tipo de dados que descreve uma propriedade imobiliária.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { 
          "op": "add",
          "path": "/properties/expansionArea/meta:status",
          "value": "deprecated"
        }
      ]'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes de atualização do recurso personalizado, com o campo obsoleto contendo um valor `meta:status` de `deprecated`. O exemplo de resposta a seguir foi truncado por questões de espaço.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "datatypes",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Details relating to a real-estate property operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type":"object",
        "properties": {
            "expansionArea": {
              "title": "Expansion Area",
              "description": "Square footage for renovated additions to the property.",
              "type": "integer",
              "meta:status": "deprecated",
            },
            "propertyName": {
              "title": "Property Name",
              "description": "Name of the property",
              "type": "string"
            },
            "propertyCity": {
              "title": "Property City",
              "description": "City where the property is located.",
              "type": "string"
            },
            "propertyCountry": {
              "title": "Property Country",
              "description": "Country where the property is located.",
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
            },
            "squareFeet": {
              "title": "Expansion Area",
              "description": "Square footage for renovated additions to the property.",
              "type": "integer",
            }
          }
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
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1594941263588,
    "repo:lastModifiedDate": 1594941538433,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "5e8a5e508eb2ed344c08cb23ed27cfb60c841bec59a2f7513deda0f7af903021",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Substituir um campo padrão em um esquema {#standard}

Campos de classes padrão, grupos de campos e tipos de dados não podem ser descontinuados diretamente. Em vez disso, você pode descontinuar o uso deles nos esquemas individuais que empregam esses recursos padrão usando um descritor.

### Criar um descritor de descontinuação de campo {#create-descriptor}

Para criar um descritor para os campos de esquema que você deseja descontinuar, faça uma solicitação POST para o ponto de extremidade `/tenant/descriptors`.

**Formato da API**

```http
POST /tenant/descriptors
```

**Solicitação**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:descriptorDeprecated",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/faxPhone"
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `@type` | O tipo de descritor. Para um descritor de substituição de campo, este valor deve ser definido como `xdm:descriptorDeprecated`. |
| `xdm:sourceSchema` | O URI `$id` do esquema ao qual você está aplicando o descritor. |
| `xdm:sourceVersion` | A versão do esquema ao qual você está aplicando o descritor. Deve ser definido como `1`. |
| `xdm:sourceProperty` | O caminho para a propriedade no esquema ao qual você está aplicando o descritor. Se quiser aplicar o descritor a várias propriedades, você pode fornecer uma lista de caminhos na forma de uma matriz (por exemplo, `["/firstName", "/lastName"]`). |

**Resposta**

```json
{
    "@id": "d882b1202bac0ac71f1e31fbcd9afbcc37f364270186b4b3",
    "@type": "xdm:descriptorDeprecated",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/faxPhone",
    "imsOrg": "{IMS_ORG}",
    "version": "1",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production"
}
```

### Verificar o campo obsoleto {#verify-deprecation}

Após a aplicação do descritor, é possível verificar se o campo foi descontinuado pesquisando o esquema em questão ao usar o cabeçalho `Accept` apropriado.

>[!NOTE]
>
>No momento, não há suporte para a exibição de campos obsoletos ao listar esquemas.

**Formato da API**

```http
GET /tenant/schemas
```

**Solicitação**

Para incluir informações sobre campos obsoletos na resposta da API, você deve definir o cabeçalho `Accept` como `application/vnd.adobe.xed-deprecatefield+json; version=1`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-deprecatefield+json; version=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do esquema, com o campo obsoleto contendo um valor `meta:status` de `deprecated`. O exemplo de resposta a seguir foi truncado por questões de espaço.

```json
"faxPhone": {
    "title": "Fax phone",
    "description": "Fax phone number.",
    "type": "object",
    "meta:xdmType": "object",
    "properties": {},
    "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
    "meta:xdmField": "xdm:faxPhone",
    "meta:status": "deprecated"
}
```

## Próximas etapas

Este documento abordou como descontinuar campos XDM usando a API do registro de esquema. Para obter mais informações sobre como configurar campos para recursos personalizados, consulte o manual em [definindo campos XDM na API](./custom-fields-api.md). Para obter mais informações sobre o gerenciamento de descritores, consulte o [manual de ponto de extremidade de descritores](../api/descriptors.md).
