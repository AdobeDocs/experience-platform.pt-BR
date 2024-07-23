---
title: Ponto de Extremidade de Autorizações de Uso do Pacote de Extensão
description: Saiba como fazer chamadas para o endpoint de autorizações /extension_package_usage na API do Reator.
exl-id: ad3fb704-7d2f-45ec-b80b-ea4d327f2205
source-git-commit: 9cdd349e0eccb4498d88f24a84b0f1c116b0adfe
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 16%

---

# Ponto de acesso de autorizações de uso do pacote de extensão

Um pacote de extensão representa uma [extensão](./extensions.md) criada por um desenvolvedor de extensões. As funcionalidades adicionais que podem ser disponibilizadas para usuários de tags são definidas por um pacote de extensão. Esses recursos podem incluir módulos principais e compartilhados, embora sejam fornecidos com mais frequência como [componentes de regra](./rule-components.md) (eventos, condições e ações) e [elementos de dados](./data-elements.md).

Um pacote de extensão pertence à [empresa](./companies.md) do desenvolvedor. Os proprietários de pacotes de extensão podem autorizar outras empresas a usar suas versões privadas dos pacotes. Cada empresa autorizada recebe uma autorização de uso para um único pacote de extensão, que é válido para todas as versões privadas futuras e atuais do pacote.

## Introdução

O endpoint usado neste manual faz parte da [API do Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Antes de continuar, consulte o [Guia de introdução](../getting-started.md) para obter informações importantes sobre como realizar a autenticação na API.

## Recuperar autorizações de uso do pacote de extensão para um pacote de extensão {#list}

Para recuperar uma lista de autorizações de uso para um pacote de extensão, faça uma solicitação GET para o endpoint a seguir.

**Formato da API**

```http
GET /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| Parâmetro | Descrição |
| --- | --- |
| `{PROPERTY_ID}` | O `ID` da propriedade cuja autorização de uso de pacote de extensão você deseja listar. |

{style="table-layout:auto"}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de pacotes de extensão.

```json
{
  "data": [
    {
      "id": "EA722482c30fe44b54aa6a7317890b3bdb",
      "type": "extension_package_usage_authorizations",
      "attributes": {
        "created_at": "2024-06-05T23:17:35.776Z",
        "updated_at": "2024-06-05T23:17:35.776Z",
        "name": "Acme",
        "platform": "web",
        "owner_org_id": "{ORG_ID}",
        "owner_org_name": "Reactor QE",
        "authorized_org_id": "{ORG_ID}",
        "authorized_org_name": "Acme Inc'",
        "state": "pending_approval",
        "created_by_email": "example@adobe.com",
        "created_by_display_name": "john snow",
        "updated_by_email": "Restricted",
        "updated_by_display_name": "Restricted"
      },
      "relationships": {
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA722482c30fe44b54aa6a7317890b3bdb/extension_package"
          },
          "data": {
            "id": "EPecefc8291ae346c3b3887d5b2da533b8",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA722482c30fe44b54aa6a7317890b3bdb"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## Criar uma autorização de uso de pacote de extensão {#create}

Crie uma autorização de uso de pacote de extensão para cada [pacote de extensão](./extension-packages.md) e `{ORG_ID}` da organização que você deseja autorizar. Para criar uma nova autorização de uso de pacote de extensão, faça uma solicitação POST para o endpoint abaixo.

**Formato da API**

```http
POST /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| Parâmetro | Descrição |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | O `ID` do pacote de extensão para o qual você deseja criar uma autorização.&quot; |

{style="table-layout:auto"}

**Solicitação**

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "authorized_org_id": "{ORG_ID}"
          },
          "type": "extension_package_usage_authorizations"
        }
      } 
```

| Propriedade | Descrição |
| --- | --- |
| `attributes.authorized_org_id` | O `ID` da organização que você deseja autorizar. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da autorização de uso do pacote de extensão recém-criado.

```json
{
  "data": {
    "id": "EA35d0e731f73645e6972df9fcac101434",
    "type": "extension_package_usage_authorizations",
    "attributes": {
      "created_at": "2024-06-05T23:17:30.308Z",
      "updated_at": "2024-06-05T23:17:30.308Z",
      "name": "Acme",
      "platform": "web",
      "owner_org_id": "{ORG_ID}",
      "owner_org_name": "Reactor QE",
      "authorized_org_id": "{ORG_ID}",
      "authorized_org_name": "Acme Inc'",
      "state": "pending_approval",
      "created_by_email": "example@adobe.com",
      "created_by_display_name": "john snow",
      "updated_by_email": "Restricted",
      "updated_by_display_name": "Restricted"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434/extension_package"
        },
        "data": {
          "id": "EP43649cc8856d4f09a7c2a21a4b1e449d",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434"
    }
  }
}
```

>[!NOTE]
>
>No exemplo de resposta acima, a autorização está atualmente no estágio `pending_approval`. Antes de usar o pacote de extensão, a organização deve aprovar a autorização. Os usuários da organização podem navegar pelo pacote de extensão privado enquanto a autorização estiver pendente de aprovação, mas não podem instalá-lo e não podem encontrá-lo no catálogo de extensões.

## Recuperar uma lista de autorizações de uso do pacote de extensão {#list-authorizations}

Você pode recuperar uma lista de autorizações de uso do pacote de extensão fazendo uma solicitação GET.

**Formato da API**

```http
GET /extension_package_usage_authorizations
```

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de pacotes de extensão.

```json
{
  "data": [
    {
      "id": "EA35d0e731f73645e6972df9fcac101434",
      "type": "extension_package_usage_authorizations",
      "attributes": {
        "created_at": "2024-06-05T23:17:30.308Z",
        "updated_at": "2024-06-05T23:17:30.308Z",
        "name": "Acme",
        "platform": "web",
        "owner_org_id": "{ORG_ID}",
        "owner_org_name": "Reactor QE",
        "authorized_org_id": "{ORG_ID}",
        "authorized_org_name": "Acme Inc'",
        "state": "pending_approval",
        "created_by_email": "Restricted",
        "created_by_display_name": "Restricted",
        "updated_by_email": "example@adobe.com",
        "updated_by_display_name": "john snow"
      },
      "relationships": {
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434/extension_package"
          },
          "data": null
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434"
      }
    }
  ],
  "links": {
    "self": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=1&page%5Bsize%5D=25",
    "next": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=2&page%5Bsize%5D=25",
    "last": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=3&page%5Bsize%5D=25"
  },
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": 2,
      "prev_page": null,
      "total_pages": 3,
      "total_count": 57
    }
  }
}
```

## Excluir uma autorização de uso de pacote de extensão {#delete}

Para excluir uma autorização de uso de pacote de extensão, inclua seu `ID` no caminho de uma solicitação DELETE. Isso impede que a organização autorizada exiba as versões privadas do pacote de extensão no catálogo e o instale em suas propriedades.

>[!NOTE]
>
>Todas as versões privadas instaladas anteriormente continuarão a funcionar conforme esperado.

**Formato da API**

```http
DELETE /extension_package_usage_authorizations/{ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `ID` | O `ID` da autorização de uso do pacote de extensão que você deseja excluir. |

{style="table-layout:auto"}

**Solicitação**

```shell
curl -X DELETE \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) sem corpo de resposta. Isso indica que a extensão foi excluída.

## Atualizar uma autorização de uso de pacote de extensão {#update}

Para aprovar ou rejeitar uma autorização de uso de pacote de extensão, inclua seu `ID` no caminho de uma solicitação PATCH.

>[!NOTE]
>
>Para aprovar ou rejeitar uma autorização de uso de pacote de extensão para sua empresa, você deve ter `manage_properties` direitos.

**Formato da API**

```http
PATCH /extension_package_usage_authorizations/{ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `ID` | O `ID` da autorização de uso do pacote de extensão que você deseja excluir. |

{style="table-layout:auto"}

**Solicitação**

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "state": "approved"
          },
          "type": "extension_package_usage_authorizations",
          "id": "EA86f54b48dd7042a68686508e03be8ba9"
        }
      } 
```

| Propriedade | Descrição |
| --- | --- |
| `attributes` | Os atributos que você deseja revisar. Para obter autorizações de uso do pacote de extensão, você pode revisar o `state`. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da autorização de uso do pacote de extensão revisado.

```json
{
  "data": {
    "id": "EA86f54b48dd7042a68686508e03be8ba9",
    "type": "extension_package_usage_authorizations",
    "attributes": {
      "created_at": "2024-06-05T23:17:59.480Z",
      "updated_at": "2024-06-05T23:18:00.115Z",
      "name": "Acme",
      "platform": "web",
      "owner_org_id": "{ORG_ID}",
      "owner_org_name": "Reactor QE",
      "authorized_org_id": "{ORG_ID}",
      "authorized_org_name": "Acme Inc'",
      "state": "approved",
      "created_by_email": "Restricted",
      "created_by_display_name": "Restricted",
      "updated_by_email": "example@adobe.com",
      "updated_by_display_name": "john snow"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA86f54b48dd7042a68686508e03be8ba9/extension_package"
        },
        "data": {
          "id": "EPb91d54cad9f749dba4e5566459f84c9c",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA86f54b48dd7042a68686508e03be8ba9"
    }
  }
}
```

>[!NOTE]
>
>Depois que a autorização for aprovada, sua organização poderá instalar o pacote de extensão em suas propriedades.

## Recuperar dados do pacote de extensão para uma autorização de uso de pacote de extensão {#retrieve-data}

Você pode recuperar dados do pacote de extensão para uma autorização de uso de pacote de extensão fazendo uma solicitação GET.

**Formato da API**

```http
GET /extension_package_usage_authorizations/{ID}/extension_package
```

| Parâmetro | Descrição |
| --- | --- |
| `ID` | O `ID` da autorização de uso do pacote de extensão que você deseja recuperar. |

{style="table-layout:auto"}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID}/extension_package \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna dados para um pacote de extensão para uma autorização de pacote de extensão.

```json
{
  "data": {
    "id": "EP45ae063fd75c4c22936d3d456c858cfa",
    "type": "extension_packages",
    "attributes": {
      "actions": [],
      "author": {
        "url": "http://adobe.com",
        "name": "Acme",
        "email": "acme@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP45ae063fd75c4c22936d3d456c858cfa",
      "conditions": [],
      "configuration": null,
      "created_at": "2024-06-05T23:17:48.607Z",
      "data_elements": [],
      "description": "Provides nothing.",
      "discontinued": false,
      "display_name": "Acme Template Test",
      "ecma_version": null,
      "events": [],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": "null",
      "name": "Acme",
      "owner_org_id": "{ORG_ID}",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2024-06-05T23:17:53.806Z",
      "version": "1.0.0",
      "view_base_path": "dist/",
      "created_by_email": "example@adobe.com",
      "created_by_display_name": "john snow",
      "updated_by_email": "example@adobe.com",
      "updated_by_display_name": "john snow"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_packages/EP45ae063fd75c4c22936d3d456c858cfa/extension_package_usage_authorizations"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP45ae063fd75c4c22936d3d456c858cfa"
    }
  }
}
```
