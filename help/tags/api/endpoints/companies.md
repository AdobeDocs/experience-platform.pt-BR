---
title: Ponto de extremidade de empresas
description: Saiba como fazer chamadas para o ponto de extremidade /company na API do reator.
exl-id: ee435358-ed34-4e0c-93af-796133fb11fc
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 97%

---

# Ponto de extremidade de empresas

Uma empresa representa uma organização de cliente, geralmente um negócio. Na API do Reactor, essas empresas correspondem 1:1 à ID de organização IMS. Os usuários da API só têm visibilidade das empresas às quais têm acesso. Uma empresa pode conter muitas [propriedades](./properties.md). Uma propriedade pertence a exatamente uma empresa.

O ponto de extremidade `/companies` na API do reator permite recuperar programaticamente as empresas às quais você tem acesso no aplicativo de experiência.

## Introdução

O endpoint usado neste manual faz parte da [API do Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Antes de continuar, consulte o [guia de introdução](../getting-started.md) para obter informações importantes sobre como realizar a autenticação na API.

## Recuperar uma lista de empresas {#list}

É possível listar as empresas às quais você têm autorização de acesso fazendo uma solicitação GET para o ponto de extremidade `/companies`. Na maioria dos casos, há exatamente um.

**Formato da API**

```http
GET /companies
```

>[!NOTE]
>
>Usando parâmetros de consulta, as empresas listadas podem ser filtradas com base nos seguintes atributos:<ul><li>`created_at`</li><li>`name`</li><li>`org_id`</li><li>`token`</li><li>`updated_at`</li></ul>Consulte o manual sobre [filtragem de respostas](../guides/filtering.md) para obter mais informações.

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/companies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de empresas às quais você tem acesso.

```json
{
  "data": [
    {
      "id": "COdb0cd64ad4524440be94b8496416ec7d",
      "type": "companies",
      "attributes": {
        "created_at": "2020-08-13T17:13:30.667Z",
        "name": "Example Company",
        "org_id": "{ORG_ID}",
        "updated_at": "2020-08-13T17:13:30.667Z",
        "token": "d5a4f682bbae",
        "cjm_enabled": false,
        "edge_enabled": false,
        "edge_events_allotment": null,
        "edge_fanout_ratio": null
      },
      "relationships": {
        "properties": {
          "links": {
            "related": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d",
        "properties": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
      },
      "meta": {
        "rights": [
          "develop_extensions",
          "manage_properties"
        ],
        "platform_rights": {
          "web": [
            "develop_extensions",
            "manage_properties"
          ],
          "mobile": [
            "develop_extensions",
            "manage_properties"
          ]
        }
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

## Pesquisar uma empresa {#lookup}

Você pode pesquisar uma empresa específica incluindo a respectiva ID no caminho de uma solicitação GET.

**Formato da API**

```http
GET /companies/{COMPANY_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{COMPANY_ID}` | O valor `id` da empresa que você deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da empresa.

```json
{
  "data": {
    "id": "COdb0cd64ad4524440be94b8496416ec7d",
    "type": "companies",
    "attributes": {
      "created_at": "2020-08-13T17:13:30.667Z",
      "name": "Example Company",
      "org_id": "{ORG_ID}",
      "updated_at": "2020-08-13T17:13:30.667Z",
      "token": "d5a4f682bbae",
      "cjm_enabled": false,
      "edge_enabled": false,
      "edge_events_allotment": null,
      "edge_fanout_ratio": null
    },
    "relationships": {
      "properties": {
        "links": {
          "related": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d",
      "properties": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
    },
    "meta": {
      "rights": [
        "develop_extensions",
        "manage_properties"
      ],
      "platform_rights": {
        "web": [
          "develop_extensions",
          "manage_properties"
        ],
        "mobile": [
          "develop_extensions",
          "manage_properties"
        ]
      }
    }
  }
}
```
