---
title: Descontinuar um campo XDM
description: Saiba como descontinuar os campos do Experience Data Model (XDM) na API do Registro de Schema.
source-git-commit: a1b86e6976cdb5b2bd3c2ecee933dfde337c9880
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 6%

---

# Descontinuar um campo XDM

No Experience Data Model (XDM), é possível descontinuar um campo em um esquema ou recurso personalizado usando o [API do Registro de Schema](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). A desaprovação de um campo faz com que ele fique oculto das interfaces do usuário downstream, como o [!UICONTROL Perfis] espaço de trabalho e Customer Journey Analytics, mas é uma alteração sem quebra e não afeta negativamente os fluxos de dados existentes.

Este documento aborda como descontinuar campos para diferentes recursos XDM.

## Introdução

Este tutorial requer fazer chamadas para a API do Registro de Schema. Revise o [guia do desenvolvedor](../api/getting-started.md) para obter informações importantes que você precisa saber para fazer essas chamadas de API. Isso inclui as `{TENANT_ID}`, o conceito de &quot;contêineres&quot; e os cabeçalhos necessários para fazer solicitações (com especial atenção para a `Accept` e seus possíveis valores).

## Descontinuar um campo personalizado {#custom}

Para descontinuar um campo em uma classe personalizada, grupo de campos ou tipo de dados, atualize o recurso personalizado por meio de uma solicitação PUT ou PATCH e adicione o atributo `meta:status: deprecated` para o campo em questão.

>[!NOTE]
>
>Para obter informações gerais sobre como atualizar recursos personalizados no XDM, consulte a seguinte documentação:
>
>* [Atualizar uma classe](../api/classes.md#patch)
>* [Atualizar um grupo de campos](../api/field-groups.md#patch)
>* [Atualizar um tipo de dados](../api/data-types.md#patch)


A chamada de API de exemplo abaixo descontinuará um campo em um tipo de dados personalizado.

**Formato da API**

```http
PATCH /tenant/datatypes/{DATA_TYPE_ID}
```

**Solicitação**

A solicitação a seguir descontinuará o `expansionArea` para um tipo de dados que descreve uma propriedade imobiliária.

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

Uma resposta bem-sucedida retorna os detalhes de atualização do recurso personalizado, com o campo obsoleto contendo um `meta:status` valor de `deprecated`. O exemplo de resposta a seguir foi truncado por questões de espaço.

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

## Descontinuar um campo padrão em um schema {#standard}

Os campos de classes padrão, grupos de campos e tipos de dados não podem ser preteridos diretamente. Em vez disso, você pode descontinuar o uso nos esquemas individuais que empregam esses recursos padrão usando um descritor.

### Criar um descritor de descontinuação de campo {#create-descriptor}

Para criar um descritor para os campos de esquema que deseja descontinuar, faça uma solicitação de POST para a variável `/tenant/descriptors` endpoint .

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
| `@type` | O tipo de descritor. Para um descritor de descontinuação de campo, esse valor deve ser definido como `xdm:descriptorDeprecated`. |
| `xdm:sourceSchema` | O URI `$id` do esquema ao qual você está aplicando o descritor. |
| `xdm:sourceVersion` | A versão do esquema à qual você está aplicando o descritor. Deve ser definido como `1`. |
| `xdm:sourceProperty` | O caminho para a propriedade no esquema ao qual você está aplicando o descritor. Se quiser aplicar o descritor a várias propriedades, é possível fornecer uma lista de caminhos na forma de uma matriz (por exemplo, `["/firstName", "/lastName"]`). |

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

Após a aplicação do descritor, é possível verificar se o campo foi descontinuado, pesquisando o esquema em questão e usando o `Accept` cabeçalho.

>[!NOTE]
>
>No momento, não há suporte para a exibição de campos obsoletos ao listar schemas.

**Formato da API**

```http
GET /tenant/schemas
```

**Solicitação**

Para incluir informações sobre campos obsoletos na resposta da API, você deve definir a variável `Accept` cabeçalho para `application/vnd.adobe.xed-deprecatefield+json; version=1`.

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

Uma resposta bem-sucedida retorna os detalhes do schema, com o campo obsoleto contendo um `meta:status` valor de `deprecated`. O exemplo de resposta a seguir foi truncado por questões de espaço.

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

Este documento cobriu como descontinuar campos XDM usando a API do Registro de Schema. Para obter mais informações sobre como configurar campos para recursos personalizados, consulte o guia sobre [definição de campos XDM na API](./custom-fields-api.md). Para obter mais informações sobre o gerenciamento de descritores, consulte o [guia do endpoint de descritores](../api/descriptors.md).
