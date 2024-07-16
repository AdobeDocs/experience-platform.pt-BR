---
keywords: Experience Platform;página inicial;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados de experiência;modelo de dados de experiência;modelo de dados;modelo de dados;modelo de dados;registro de esquemas;ad-hoc;ad hoc;adhoc;Ad hoc;tutorial;tutorial;criar;criar;esquema;esquema
solution: Experience Platform
title: Criar um esquema ad-hoc
description: Em circunstâncias específicas, pode ser necessário criar um esquema do Experience Data Model (XDM) com campos com namespace para uso somente por um único conjunto de dados. Isso é chamado de esquema "ad-hoc". Esquemas ad-hoc são usados em vários workflows de assimilação de dados para o Experience Platform, incluindo a assimilação de arquivos CSV e a criação de determinados tipos de conexões de origem.
type: Tutorial
exl-id: bef01000-909a-4594-8cf4-b9dbe0b358d5
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 3%

---

# Criar um esquema ad-hoc

Em circunstâncias específicas, pode ser necessário criar um esquema do [!DNL Experience Data Model] (XDM) com campos com namespace para uso apenas por um único conjunto de dados. Isso é chamado de esquema &quot;ad-hoc&quot;. Esquemas ad-hoc são usados em vários fluxos de trabalho de assimilação de dados para [!DNL Experience Platform], incluindo a assimilação de arquivos CSV e a criação de determinados tipos de conexões de origem.

Este documento fornece as etapas gerais para a criação de um esquema ad hoc usando a [API do Registro de Esquemas](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Ela deve ser usada em conjunto com outros tutoriais do [!DNL Experience Platform] que exigem a criação de um esquema ad-hoc como parte do fluxo de trabalho. Cada um desses documentos fornece informações detalhadas sobre como configurar corretamente um schema ad-hoc para seu caso de uso específico.

## Introdução

Este tutorial requer uma compreensão funcional do Sistema [!DNL Experience Data Model] (XDM). Antes de iniciar este tutorial, revise a seguinte documentação do XDM:

- [Visão geral do sistema XDM](../home.md): uma visão geral de alto nível do XDM e sua implementação em [!DNL Experience Platform].
- [Noções básicas sobre a composição de esquema](../schema/composition.md): uma visão geral dos componentes básicos de esquemas XDM.

Antes de iniciar este tutorial, consulte o [guia do desenvolvedor](../api/getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API [!DNL Schema Registry] com êxito. Isso inclui o `{TENANT_ID}`, o conceito de &quot;contêineres&quot; e os cabeçalhos necessários para fazer solicitações (com atenção especial ao cabeçalho Aceitar e seus valores possíveis).

## Criar uma classe ad-hoc

O comportamento dos dados de um esquema XDM é determinado por sua classe subjacente. A primeira etapa na criação de um esquema ad-hoc é criar uma classe baseada no comportamento `adhoc`. Isso é feito fazendo uma solicitação POST para o ponto de extremidade `/tenant/classes`.

**Formato da API**

```http
POST /tenant/classes
```

**Solicitação**

A solicitação a seguir cria uma nova classe XDM, configurada pelos atributos fornecidos na carga. Ao fornecer uma propriedade `$ref` definida como `https://ns.adobe.com/xdm/data/adhoc` na matriz `allOf`, essa classe herda o comportamento `adhoc`. A solicitação também define um objeto `_adhoc`, que contém os campos personalizados da classe.

>[!NOTE]
>
>Os campos personalizados definidos em `_adhoc` variam dependendo do caso de uso do esquema ad-hoc. Consulte o fluxo de trabalho específico no tutorial apropriado para obter os campos personalizados necessários com base no caso de uso.

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

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da nova classe, substituindo o nome do objeto `properties._adhoc` por uma GUID que seja um identificador exclusivo somente leitura gerado pelo sistema para a classe. O atributo `meta:datasetNamespace` também é gerado automaticamente e incluído na resposta.

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
| `$id` | Um URI que serve como somente leitura, identificador exclusivo gerado pelo sistema para a nova classe ad-hoc. Esse valor é usado na próxima etapa da criação de um schema ad-hoc. |

{style="table-layout:auto"}

## Criar um esquema ad-hoc

Depois de criar uma classe ad-hoc, você pode criar um novo esquema que implementa essa classe fazendo uma solicitação POST para o ponto de extremidade `/tenant/schemas`.

**Formato da API**

```http
POST /tenant/schemas
```

**Solicitação**

A solicitação a seguir cria um novo esquema, fornecendo uma referência (`$ref`) ao `$id` da classe ad-hoc criada anteriormente em sua carga.

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

Uma resposta bem-sucedida retorna os detalhes do esquema recém-criado, incluindo seu `$id` somente leitura gerado pelo sistema.

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
>Esta etapa é opcional. Se não quiser inspecionar a estrutura de campo do esquema ad-hoc, pule para a seção [próximas etapas](#next-steps) no final deste tutorial.

Depois que o esquema ad-hoc for criado, você poderá fazer uma solicitação de pesquisa (GET) para exibir o esquema em sua forma expandida. Isso é feito usando o cabeçalho Aceitar apropriado na solicitação do GET, conforme demonstrado abaixo.

**Formato da API**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SCHEMA_ID}` | O URI `$id` codificado na URL ou `meta:altId` do esquema ad-hoc que você deseja acessar. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir usa o cabeçalho Accept `application/vnd.adobe.xed-full+json; version=1`, que retorna a forma expandida do esquema. Observe que, ao recuperar um recurso específico de [!DNL Schema Registry], o cabeçalho Aceitar da solicitação deve incluir a versão principal do recurso em questão.

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

Uma resposta bem-sucedida retorna os detalhes do esquema, incluindo todos os campos aninhados em `properties`.

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

Ao seguir este tutorial, você criou um novo esquema ad-hoc com sucesso. Se você foi trazido a este documento como parte de outro tutorial, agora pode usar o `$id` do esquema ad-hoc para concluir o fluxo de trabalho conforme determinado.

Para obter mais informações sobre como trabalhar com a API [!DNL Schema Registry], consulte o [guia do desenvolvedor](../api/getting-started.md).
