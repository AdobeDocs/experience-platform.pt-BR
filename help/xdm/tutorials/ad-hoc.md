---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um schema ad-hoc
topic: tutorials
translation-type: tm+mt
source-git-commit: 956d1e5b4a994c9ea52d818f3dd6d3ff88cb16b6

---


# Criar um schema ad-hoc

Em circunstâncias específicas, pode ser necessário criar um schema do Modelo de Dados de Experiência (XDM) com campos que são namespacados para uso somente por um único conjunto de dados. Isso é conhecido como um schema &quot;ad-hoc&quot;. Os schemas ad-hoc são usados em vários workflows de ingestão de dados para a Experience Platform, incluindo a inclusão de arquivos CSV e a criação de certos tipos de conexões de origem.

Este documento fornece etapas gerais para a criação de um schema ad-hoc usando a API [do Registro do](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)Schema. Ela deve ser usada em conjunto com outros tutoriais da plataforma de experiência que exigem a criação de um schema ad-hoc como parte de seu fluxo de trabalho. Cada um desses documentos fornece informações detalhadas sobre como configurar corretamente um schema ad-hoc para seu caso de uso específico.

## Introdução

Este tutorial requer uma compreensão funcional do sistema do Experience Data Model (XDM). Antes de iniciar este tutorial, reveja a seguinte documentação XDM:

- [Visão geral](../home.md)do sistema XDM: Uma visão geral de alto nível do XDM e sua implementação na plataforma da experiência.
- [Noções básicas da composição](../schema/composition.md)do schema: Uma visão geral dos componentes básicos dos schemas XDM.

Antes de iniciar este tutorial, consulte o guia [do](../api/getting-started.md) desenvolvedor para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API do Registro do Schema. Isso inclui seu `{TENANT_ID}`, o conceito de &quot;container&quot; e os cabeçalhos necessários para fazer solicitações (com atenção especial ao cabeçalho Accept e seus possíveis valores).

## Criar uma classe ad-hoc

O comportamento de dados de um schema XDM é determinado pela classe subjacente. A primeira etapa na criação de um schema ad-hoc é criar uma classe com base no `adhoc` comportamento. Isso é feito fazendo uma solicitação POST ao `/tenant/classes` terminal.

**Formato da API**

```http
POST /tenant/classes
```

**Solicitação**

A solicitação a seguir cria uma nova classe XDM, configurada pelos atributos fornecidos na carga. Ao fornecer uma `$ref` propriedade definida como `https://ns.adobe.com/xdm/data/adhoc` na `allOf` matriz, essa classe herda o `adhoc` comportamento. A solicitação também define um `_adhoc` objeto, que contém os campos personalizados para a classe.

>[!NOTE] Os campos personalizados definidos em `_adhoc` variam dependendo do caso de uso do schema ad-hoc. Consulte o fluxo de trabalho específico no tutorial apropriado para ver os campos personalizados necessários com base em casos de uso.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `properties._adhoc` | Um objeto que contém os campos personalizados para a classe, expressos como pares de valores chave de nomes de campos e tipos de dados. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da nova classe, substituindo o nome do `properties._adhoc` objeto por um GUID que é um identificador exclusivo de leitura gerado pelo sistema para a classe. O `meta:datasetNamespace` atributo também é gerado automaticamente e incluído na resposta.

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
    "imsOrg": "{IMS_ORG}",
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
| `$id` | Um URI que serve como identificador exclusivo somente leitura gerado pelo sistema para a nova classe ad-hoc. Esse valor é usado na próxima etapa da criação de um schema ad-hoc. |

## Criar um schema ad-hoc

Depois de criar uma classe ad-hoc, você pode criar um novo schema que implemente essa classe, fazendo uma solicitação POST para o `/tenant/schemas` ponto de extremidade.

**Formato da API**

```http
POST /tenant/schemas
```

**Solicitação**

A solicitação a seguir cria um novo schema, fornecendo uma referência (`$ref`) à classe ad-hoc criada anteriormente `$id` em sua carga útil.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Uma resposta bem-sucedida retorna os detalhes do schema recém-criado, incluindo somente leitura gerado pelo sistema `$id`.

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
    "imsOrg": "{IMS_ORG}",
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

## Visualização do schema ad-hoc completo

>[!NOTE] Esta etapa é opcional. Se você não quiser inspecionar a estrutura de campo do seu schema ad-hoc, vá para a seção de [próximas etapas](#next-steps) no final deste tutorial.

Depois que o schema ad-hoc for criado, você poderá fazer uma solicitação de pesquisa (GET) para visualização o schema em seu formulário expandido. Isso é feito usando o cabeçalho Accept apropriado na solicitação GET, como demonstrado abaixo.

**Formato da API**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O `$id` URI codificado por URL ou `meta:altId` o schema ad-hoc que você deseja acessar. |

**Solicitação**

A solicitação a seguir usa o cabeçalho Aceitar `application/vnd.adobe.xed-full+json; version=1`, que retorna a forma expandida do schema. Observe que ao recuperar um recurso específico do Registro de Schemas, o cabeçalho Aceitar da solicitação deve incluir a versão principal do recurso em questão.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "imsOrg": "{IMS_ORG}",
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

Ao seguir este tutorial, você criou com êxito um novo schema ad-hoc. Se você tiver sido direcionado para esse documento como parte de outro tutorial, agora é possível usar o `$id` de seu schema ad-hoc para concluir o fluxo de trabalho como indicado.

Para obter mais informações sobre como trabalhar com a API de registro do Schema, consulte o guia [do](../api/getting-started.md)desenvolvedor.