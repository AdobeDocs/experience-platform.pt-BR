---
keywords: Experience Platform;página inicial;tópicos populares;api;Controle de acesso baseado em atributo;controle de acesso baseado em atributo
solution: Experience Platform
title: Endpoint da API de produtos
description: O endpoint /products na API de controle de acesso baseado em atributos permite gerenciar programaticamente os produtos no Adobe Experience Platform.
role: Developer
exl-id: 44ee9a9d-7a13-4d59-a1a9-97764dbd3763
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 4%

---

# Endpoint de produtos

>[!NOTE]
>
>Se um token de usuário for transmitido, o usuário do token deverá ter uma função de &quot;org admin&quot; para a organização solicitada.

A variável `/products` O endpoint na API de controle de acesso baseada em atributos permite gerenciar de forma programática os produtos, bem como as categorias de permissões e os conjuntos de permissões associados aos produtos em sua organização.

## Introdução

O endpoint da API usado neste guia faz parte da API de controle de acesso baseada em atributos. Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API de Experience Platform.

## Recuperar uma lista de produtos autorizados {#list}

Você pode recuperar uma lista de produtos autorizados fazendo uma solicitação GET para o `/products` terminal.

**Formato da API**

```http
GET /products/
```

**Solicitação**

A solicitação a seguir recupera uma lista de produtos autorizados pertencentes à sua organização.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de produtos qualificados pertencentes à sua organização.

```json
{
  "products": [
    {
      "id": "{ID}",
      "name": "Adobe Experience Platform",
      "serviceCode": "{SERVICE_CODE}"
    }
  ]
}
```

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID correspondente do produto consultado. |
| `name` | O nome do produto consultado. |
| `serviceCode` | O código de serviço correspondente do produto consultado. |

## Pesquisar categorias de permissão por ID de produto

É possível pesquisar categorias de permissão para um determinado produto fazendo uma solicitação GET ao `/products/{PRODUCT_ID}/categories` ao especificar a ID do produto.

**Formato da API**

```http
GET /products/{PRODUCT_ID}/categories
```

| Parâmetro | Descrição |
| --- | --- |
| {PRODUCT_ID} | A ID do produto associado às categorias de permissão que você deseja pesquisar. |

**Solicitação**

A solicitação a seguir recupera categorias de permissão associadas a `{PRODUCT_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/categories \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Resposta**

Uma resposta bem-sucedida retorna as categorias de permissão associadas à ID do produto consultada.

```json
{
  "categories": [
    {
        "name": "Profile Management"
    },
    {
        "name": "Data Ingestion"
    },
    {
        "name": "Sandbox Administration"
    },
    {
        "name": "Query Service"
    },
    {
        "name": "Data Management"
    },
    {
        "name": "Identity Management"
    },
    {
        "name": "Data Modeling"
    },
    {
        "name": "Data Science Workspace"
    },
    {
        "name": "Dashboards"
    },
    {
        "name": "Alerts"
    },
    {
        "name": "Data Governance"
    }
  ]
}
```

| Propriedade | Descrição |
| --- | --- |
| `category` | As categorias de permissão disponíveis na ID do produto consultada. |
| `name` | O nome da categoria de permissão. |

## Pesquisar conjuntos de permissões por ID de produto

Você pode pesquisar conjuntos de permissões para um determinado produto fazendo uma solicitação GET ao `/products/{PRODUCT_ID}/permission-sets` ao especificar a ID do produto.

**Formato da API**

```http
GET /products/{PRODUCT_ID}/permission-sets
```

| Parâmetro | Descrição |
| --- | --- |
| {PRODUCT_ID} | A ID do produto associado aos conjuntos de permissões que você deseja pesquisar. |

**Solicitação**

A solicitação a seguir recupera conjuntos de permissões associados a `{PRODUCT_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/permission-sets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Resposta**

Uma resposta bem-sucedida retorna os conjuntos de permissões associados à ID do produto consultada.

```json
{
  "permission-sets": [
      {
          "id": "manage-schemas",
          "name": "Manage Schemas",
          "category": "Data Modeling",
          "permissions": [
              {
                  "resource": "schemas",
                  "actions": [
                      "read",
                      "write",
                      "delete"
                  ]
              },
              {
                  "resource": "schema-fields",
                  "actions": [
                      "read",
                      "write",
                      "delete"
                  ]
              },
              {
                  "resource": "sandboxes",
                  "actions": [
                      "view"
                  ]
              }
          ]
      },
      {
          "id": "view-schemas",
          "name": "View Schemas",
          "category": "Data Modeling",
          "permissions": [
              {
                  "resource": "schemas",
                  "actions": [
                      "read"
                  ]
              },
              {
                  "resource": "schema-fields",
                  "actions": [
                      "read"
                  ]
              },
              {
                  "resource": "sandboxes",
                  "actions": [
                      "view"
                  ]
              }
          ]
      },
  ]
}
```

| Propriedade | Descrição |
| --- | --- |
| `permission-sets` | Os conjuntos de permissões representam um grupo de permissões que um administrador pode aplicar a uma função. Um administrador pode atribuir conjuntos de permissões a uma função, em vez de atribuir permissões individuais. Isso permite criar funções personalizadas com base em uma função predefinida que contém um grupo de permissões. |
| `id` | A ID correspondente do conjunto de permissões consultado. |
| `name` | O nome correspondente do conjunto de permissões consultado. |
| `category` | A categoria de permissão disponível. |
| `permissions` | As permissões incluem a capacidade de visualizar e/ou usar recursos da Platform, como criar sandboxes, definir esquemas e gerenciar conjuntos de dados. |
| `permissions.resource` | O ativo ou objeto que um assunto pode ou não acessar. Os recursos podem ser arquivos, aplicativos, servidores ou até mesmo APIs. |
| `permissions.actions` | A ação que um assunto tem permissão para realizar em um recurso consultado. Os valores possíveis incluem: `view`, `read`, `create`, `edit`, e `delete` |
