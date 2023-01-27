---
title: Adicionar campos específicos a um esquema usando a API do Registro de esquema
description: Saiba como adicionar campos individuais de grupos de campos pré-existentes a um esquema do Experience Data Model (XDM) usando a API do Registro de Schema.
source-git-commit: 4bcd949e901c11bb933000f7ae76f17134dda496
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 2%

---

# Adicionar campos específicos a um esquema usando a API do Registro de esquema

Os esquemas do Experience Data Model (XDM) são compostos de uma classe base, com campos adicionais incluídos por meio do uso de grupos de campos padrão definidos pelo Adobe e grupos de campos personalizados definidos pela sua organização.

Ao criar um schema, você pode usar alguns campos de um determinado grupo de campos, enquanto exclui outros do mesmo grupo que você não precisa. Este tutorial mostra como adicionar campos individuais de um grupo de campos a um esquema usando a API do Registro de Esquema.

>[!NOTE]
>
>Para obter informações sobre como adicionar e remover campos de esquema individuais na interface do usuário do Adobe Experience Platform, consulte o guia em [fluxos de trabalho baseados em campo](../ui/field-based-workflows.md) (atualmente em beta).

## Pré-requisitos

Este tutorial envolve fazer chamadas para o [API do Registro de Schema](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Antes de começar, reveja o [guia do desenvolvedor](../api/getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo `{TENANT_ID}`, o conceito de contêineres e os cabeçalhos necessários para fazer solicitações.

## Noções básicas sobre o `meta:refProperty` campo

Para qualquer schema, a classe e os grupos de campos que compõem sua estrutura são referenciados em sua `allOf` matriz. Cada componente é representado como um objeto contendo um `$ref` propriedade que se refere ao URI do componente `$id`.

O JSON a seguir representa um schema simplificado que usa uma única classe (`experienceevent`) e grupo de campos (`experienceevent-all`):

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all"
    }
  ]
}
```

Para qualquer objeto na `allOf` matriz que faz referência a um grupo de campos, é possível adicionar um irmão `meta:refProperty` para especificar quais campos do grupo devem ser incluídos no schema.

>[!NOTE]
>
>Cada campo é especificado usando uma string de ponteiro JSON, representando o caminho para o campo dentro de seu respectivo grupo de campos. A string deve começar com uma barra à esquerda (`/`) e não deve incluir qualquer `properties` namespaces. Por exemplo: `/_experience/campaign/message/id`.

Quando incluído como uma string, `meta:refProperty` pode se referir a um único campo em um grupo. Outros campos do mesmo grupo podem ser incluídos usando o mesmo `$ref` em outro objeto com um valor diferente `meta:refProperty` valor.

```json
{
  "title": "My Sample Schema",
  "description": "An example schema that uses the XDM ExperienceEvent class.",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": "/_experience/campaign/message/id"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": "/_experience/campaign/message/size"
    }
  ]
}
```

Em alternativa, `meta:refProperty` pode ser fornecido como uma matriz, permitindo que você especifique vários campos para inclusão de um determinado grupo em um único `allOf` item de lista:

```json
{
  "title": "My Sample Schema",
  "description": "An example schema that uses the XDM ExperienceEvent class.",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ]
}
```

## Adicionar campos usando uma operação PUT

Você pode usar uma solicitação do PUT para reescrever um esquema inteiro e configurar os campos que deseja incluir em `allOf`.

**Formato da API**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O `meta:altId` ou codificado por URL `$id` do esquema que deseja reescrever. |

**Solicitação**

A solicitação a seguir atualiza os campos específicos incluídos do grupo de campos na variável `allOf` matriz.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "title": "My Sample Schema",
        "description": "My Sample Description",
        "type": "object",
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
          },
          {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
            "meta:refProperty": [
              "/_experience/campaign/message/id",
              "/_experience/campaign/message/size",
              "/_experience/campaign/message/variant"
            ]
          }
        ]
      }'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do schema atualizado.

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ],
  "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
  "meta:abstract": false,
  "meta:extensible": false,
  "meta:extends": [
      "https://ns.adobe.com/xdm/context/experienceevent",
      "https://ns.adobe.com/xdm/data/time-series"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
  "version": "1.0",
  "meta:resourceType": "schemas",
  "meta:registryMetadata": {
      "repo:createDate": 1552088461236,
      "repo:lastModifiedDate": 1552088470592,
      "xdm:createdClientId": "{CREATED_CLIENT}",
      "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

>[!NOTE]
>
>Para obter informações mais detalhadas sobre solicitações PUT para schemas, consulte [guia do endpoint de schemas](../api/schemas.md#put).

## Adicionar campos usando uma operação PATCH

Você pode usar uma solicitação de PATCH para adicionar campos individuais a um schema sem substituir outros. O Registro de Esquema suporta todas as operações padrão de Patch JSON, incluindo `add`, `remove`e `replace`. Para obter mais informações sobre o Patch JSON, consulte o [Guia de fundamentos da API](../../landing/api-fundamentals.md#json-patch).

**Formato da API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O `meta:altId` ou codificado por URL `$id` do esquema que deseja reescrever. |

**Solicitação**

A solicitação a seguir adiciona um novo objeto ao `allOf` matriz, especificando campos a serem adicionados.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "op": "add",
          "path": "/allOf/-",
          "value":  {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
            "meta:refProperty": [
              "/_experience/campaign/message/id",
              "/_experience/campaign/message/size",
              "/_experience/campaign/message/variant"
            ]
          }
        }
      ]'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do schema atualizado.

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ],
  "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
  "meta:abstract": false,
  "meta:extensible": false,
  "meta:extends": [
      "https://ns.adobe.com/xdm/context/experienceevent",
      "https://ns.adobe.com/xdm/data/time-series"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
  "version": "1.0",
  "meta:resourceType": "schemas",
  "meta:registryMetadata": {
      "repo:createDate": 1552088461236,
      "repo:lastModifiedDate": 1552088470592,
      "xdm:createdClientId": "{CREATED_CLIENT}",
      "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

>[!NOTE]
>
>Para obter informações mais detalhadas sobre solicitações PATCH para schemas, consulte [guia do endpoint de schemas](../api/schemas.md#patch).

## Próximas etapas

Este guia cobriu como usar chamadas de API para adicionar campos individuais de um grupo de campos existente a um esquema. Para obter detalhes sobre como executar tarefas semelhantes baseadas em campo na interface do usuário da plataforma, consulte o guia em [fluxos de trabalho baseados em campo](../ui/field-based-workflows.md).

Para obter mais informações sobre os recursos da API do Registro de Schema, consulte [Visão geral da API](../api/overview.md) para obter uma lista completa de endpoints e processos.
