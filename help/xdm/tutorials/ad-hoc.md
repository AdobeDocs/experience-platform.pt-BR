---
keywords: Experience Platform, home, tópicos populares, api, API, XDM, sistema XDM, modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados, Modelo de dados, Modelo de dados, Registro de esquema, Registro de esquema, ad-hoc, ad-hoc, Ad-hoc, Ad-hoc, Ad-hoc, Ad-hoc, tutorial, Tutorial, criar, criar, esquema, Esquema
solution: Experience Platform
title: Criar um esquema ad-hoc
description: Em circunstâncias específicas, pode ser necessário criar um esquema do Experience Data Model (XDM) com campos que são namespacados para uso somente por um único conjunto de dados. Isso é chamado de schema "ad-hoc". Esquemas ad-hoc são usados em vários workflows de assimilação de dados para o Experience Platform, incluindo a assimilação de arquivos CSV e a criação de determinados tipos de conexões de origem.
topic-legacy: tutorial
type: Tutorial
exl-id: bef01000-909a-4594-8cf4-b9dbe0b358d5
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 4%

---

# Criar um esquema ad-hoc

Em circunstâncias específicas, pode ser necessário criar um [!DNL Experience Data Model] (XDM) com campos que são namespacados para uso somente por um único conjunto de dados. Isso é chamado de schema &quot;ad-hoc&quot;. Esquemas ad-hoc são usados em vários workflows de assimilação de dados para [!DNL Experience Platform], incluindo a assimilação de arquivos CSV e a criação de determinados tipos de conexões de origem.

Este documento fornece etapas gerais para a criação de um esquema ad hoc usando o [API do Registro de Schema](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Destina-se a ser utilizado juntamente com outros [!DNL Experience Platform] tutoriais que exigem a criação de um schema ad-hoc como parte de seu fluxo de trabalho. Cada um desses documentos fornece informações detalhadas sobre como configurar corretamente um esquema ad hoc para seu caso de uso específico.

## Introdução

Este tutorial requer uma compreensão funcional do [!DNL Experience Data Model] (XDM) Sistema. Antes de iniciar este tutorial, reveja a seguinte documentação XDM:

- [Visão geral do sistema XDM](../home.md): Uma visão geral de alto nível do XDM e sua implementação no [!DNL Experience Platform].
- [Noções básicas da composição do schema](../schema/composition.md): Uma visão geral dos componentes básicos dos esquemas XDM.

Antes de iniciar este tutorial, reveja o [guia do desenvolvedor](../api/getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para o [!DNL Schema Registry] API. Isso inclui as `{TENANT_ID}`, o conceito de &quot;contêineres&quot; e os cabeçalhos necessários para fazer solicitações (com especial atenção ao cabeçalho Accept e seus possíveis valores).

## Criar uma classe ad-hoc

O comportamento de dados de um esquema XDM é determinado por sua classe subjacente. A primeira etapa na criação de um schema ad-hoc é criar uma classe com base no `adhoc` comportamento. Isso é feito fazendo uma solicitação de POST para o `/tenant/classes` endpoint .

**Formato da API**

```http
POST /tenant/classes
```

**Solicitação**

A solicitação a seguir cria uma nova classe XDM, configurada pelos atributos fornecidos na carga útil. Ao fornecer uma `$ref` propriedade definida como `https://ns.adobe.com/xdm/data/adhoc` no `allOf` matriz, essa classe herda o `adhoc` comportamento. A solicitação também define um `_adhoc` objeto , que contém os campos personalizados da classe .

>[!NOTE]
>
>Os campos personalizados definidos em `_adhoc` varia dependendo do caso de uso do schema ad-hoc. Consulte o fluxo de trabalho específico no tutorial apropriado para campos personalizados necessários com base em casos de uso.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"New ad-hoc class",
        "description": "New ad-hoc class description",
        "type":"object",
        "allOf": [
          {
            "$ref":"https://ns.adobe.com/xdm/data/adhoc"
          },
          {
            "properties": {
              "_adhoc": {
                "type":"object",
                "properties": {
                  "field1": {
                    "type":"string"
                  },
                  "field2": {
                    "type":"string"
                  }
                }
              }
            }
          }
        ]
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `$ref` | O comportamento dos dados para a nova classe. Para classes ad-hoc, esse valor deve ser definido como `https://ns.adobe.com/xdm/data/adhoc`. |
| `properties._adhoc` | Um objeto que contém os campos personalizados da classe, expressos como pares de valores chave de nomes de campos e tipos de dados. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da nova classe, substituindo a `properties._adhoc` Nome do objeto com um GUID que é um identificador exclusivo gerado pelo sistema e somente leitura para a classe. O `meta:datasetNamespace` também é gerado automaticamente e incluído na resposta.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:altId": "_{TENANT_ID}.classes.6395cbd58812a6d64c4e5344f7b9120f",
    "meta:resourceType": "classes",
    "version": "1.0",
    "title": "New Class",
    "description": "New class description",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/data/adhoc"
        },
        {
            "properties": {
                "_6395cbd58812a6d64c4e5344f7b9120f": {
                    "type": "object",
                    "properties": {
                        "field1": {
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "field2": {
                            "type": "string",
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:extends": [
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557527784822,
        "repo:lastModifiedDate": 1557527784822,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "Jggrlh4PQdZUvDUhQHXKx38iTQo="
    }
}
```

| Propriedade | Descrição |
| --- | --- |
| `$id` | Um URI que serve como o identificador exclusivo gerado pelo sistema somente leitura para a nova classe ad-hoc. Esse valor é usado na próxima etapa da criação de um schema ad-hoc. |

{style=&quot;table-layout:auto&quot;}

## Criar um esquema ad-hoc

Depois de criar uma classe ad hoc, você pode criar um novo schema que implementa essa classe fazendo uma solicitação POST para a `/tenant/schemas` endpoint .

**Formato da API**

```http
POST /tenant/schemas
```

**Solicitação**

A solicitação a seguir cria um novo schema, fornecendo uma referência (`$ref`) à `$id` da classe ad-hoc criada anteriormente em sua carga útil.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"New Schema",
        "description": "New schema description.",
        "type":"object",
        "allOf": [
          {
            "$ref":"https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f"
          }
        ]
      }'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do schema recém-criado, incluindo somente leitura gerada pelo sistema `$id`.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d",
    "meta:altId": "_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "New Schema",
    "description": "New schema description.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f"
        }
    ],
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557528570542,
        "repo:lastModifiedDate": 1557528570542,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "Jggrlh4PQdZUvDUhQHXKx38iTQo="
    }
}
```

## Exibir o esquema ad-hoc completo

>[!NOTE]
>
>Esta etapa é opcional. Se não quiser inspecionar a estrutura de campo do seu schema ad hoc, ignore o [próximas etapas](#next-steps) no final deste tutorial.

Depois que o schema ad hoc tiver sido criado, você poderá fazer uma solicitação de pesquisa (GET) para exibir o schema em seu formulário expandido. Isso é feito usando o cabeçalho Accept apropriado na solicitação do GET, conforme demonstrado abaixo.

**Formato da API**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O URL codificado `$id` URI ou `meta:altId` do esquema ad-hoc que você deseja acessar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir usa o cabeçalho Accept `application/vnd.adobe.xed-full+json; version=1`, que retorna o formulário expandido do schema. Observe que ao recuperar um recurso específico do [!DNL Schema Registry], o cabeçalho Accept da solicitação deve incluir a versão principal do recurso em questão.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do schema, incluindo todos os campos aninhados em `properties`.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d",
    "meta:altId": "_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "New Schema",
    "description": "New schema description.",
    "type": "object",
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "properties": {
        "_6395cbd58812a6d64c4e5344f7b9120f": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "field1": {
                    "type": "string",
                    "meta:xdmType": "string"
                },
                "field2": {
                    "type": "string",
                    "meta:xdmType": "string"
                }
            }
        }
    },
    "meta:registryMetadata": {
        "repo:createdDate": 1557528570542,
        "repo:lastModifiedDate": 1557528570542,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "bTogM1ON2LO/F7rlcc1iOWmNVy0="
    }
}
```

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você criou com êxito um novo schema ad hoc. Se você foi trazido para este documento como parte de outro tutorial, agora é possível usar a variável `$id` do esquema ad-hoc para concluir o fluxo de trabalho conforme indicado.

Para obter mais informações sobre como trabalhar com a [!DNL Schema Registry] Consulte a API [guia do desenvolvedor](../api/getting-started.md).
