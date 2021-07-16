---
title: Ponto de extremidade de eventos de auditoria
description: Saiba como fazer chamadas para o endpoint /audit_events na API do reator.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 4%

---

# Ponto de extremidade de eventos de auditoria

>[!WARNING]
>
>A implementação do endpoint `/audit_events` está em fluxo à medida que os recursos são adicionados, removidos e retrabalhados.

Um evento de auditoria é um registro de uma alteração específica para outro recurso na API do Reator, gerada no momento em que a alteração é feita. Esses são eventos do sistema que podem ser inscritos por meio do uso de um [callback](./callbacks.md). O endpoint `/audit_events` na API do reator permite gerenciar programaticamente eventos de auditoria no aplicativo de experiência.

Os eventos de auditoria são estruturados no formato de `{RESOURCE_TYPE}.{EVENT}`, como `build.created` ou `rule.updated`.

O tipo de recurso pode ser qualquer um dos seguintes:

* `property`
* `extension`
* `data_element`
* `rule`
* `rule_component`
* `library`
* `build`
* `environment`
* `host`

Os seguintes eventos são compatíveis para cada tipo de recurso:

* `created`
* `updated`
* `deleted`

## Introdução

O endpoint usado neste guia faz parte da [API do reator](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Antes de continuar, reveja o [guia de introdução](../getting-started.md) para obter informações importantes sobre como autenticar para a API.

## Recuperar uma lista de eventos de auditoria {#list}

Você pode recuperar uma lista de eventos de auditoria para todas as propriedades de sua organização, fazendo uma solicitação de GET para o endpoint `/audit_events`.

**Formato da API**

```http
GET /audit_events
```

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/audit_events \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de eventos de auditoria. O exemplo de resposta abaixo foi truncado para espaço.

```json
{
  "data": [
    {
      "id": "AEa98742de8ef044d8b86767aa6a15a674",
      "type": "audit_events",
      "attributes": {
        "attributed_to_display_name": "John Smith",
        "attributed_to_email": "jsmith@example.com",
        "created_at": "2020-12-14T17:31:21.836Z",
        "display_name": "Kessel Apns App",
        "type_of": "app_configuration.updated",
        "updated_at": "2020-12-14T17:31:21.836Z",
        "entity": "{\"data\":{\"id\":\"AC40c339ab80d24c958b90d67b698602eb\",\"type\":\"app_configurations\",\"links\":{\"self\":\"https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb\",\"company\":\"https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1\"},\"attributes\":{\"name\":\"Kessel Apns App\",\"app_id\":\"com.adobe.test_app_2\",\"key_type\":\"p8_file\",\"platform\":\"mobile\",\"created_at\":\"2020-12-14T17:31:10.626Z\",\"updated_at\":\"2020-12-14T17:31:21.787Z\",\"messaging_service\":\"apns\"},\"relationships\":{\"company\":{\"data\":{\"id\":\"CO2bf094214ffd4785bb4bcf88c952a7c1\",\"type\":\"companies\"},\"links\":{\"related\":\"https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company\"}}}}}"
      },
      "relationships": {
        "property": {
          "links": {
            "related": null
          },
          "data": null
        },
        "entity": {
          "links": {
            "related": null
          },
          "data": {
            "type": "app_configurations",
            "id": "AC40c339ab80d24c958b90d67b698602eb"
          }
        }
      },
      "links": {
        "entity": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb",
        "property": null,
        "self": "https://reactor.adobe.io/audit_events/AEa98742de8ef044d8b86767aa6a15a674"
      }
    },
    {
      "id": "AE7320b6c1c3f84bb69405fcfe9cb58189",
      "type": "audit_events",
      "attributes": {
        "attributed_to_display_name": "John Smith",
        "attributed_to_email": "jsmith@example.com",
        "created_at": "2020-12-14T17:31:10.672Z",
        "display_name": "Kessel Apns App",
        "type_of": "app_configuration.created",
        "updated_at": "2020-12-14T17:31:10.672Z",
        "entity": "{\"data\":{\"id\":\"AC40c339ab80d24c958b90d67b698602eb\",\"type\":\"app_configurations\",\"links\":{\"self\":\"https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb\",\"company\":\"https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1\"},\"attributes\":{\"name\":\"Kessel Apns App\",\"app_id\":\"com.adobe.test_app\",\"key_type\":\"p8_file\",\"platform\":\"mobile\",\"created_at\":\"2020-12-14T17:31:10.626Z\",\"updated_at\":\"2020-12-14T17:31:10.626Z\",\"messaging_service\":\"apns\"},\"relationships\":{\"company\":{\"data\":{\"id\":\"CO2bf094214ffd4785bb4bcf88c952a7c1\",\"type\":\"companies\"},\"links\":{\"related\":\"https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company\"}}}}}"
      },
      "relationships": {
        "property": {
          "links": {
            "related": null
          },
          "data": null
        },
        "entity": {
          "links": {
            "related": null
          },
          "data": {
            "type": "app_configurations",
            "id": "AC40c339ab80d24c958b90d67b698602eb"
          }
        }
      },
      "links": {
        "entity": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb",
        "property": null,
        "self": "https://reactor.adobe.io/audit_events/AE7320b6c1c3f84bb69405fcfe9cb58189"
      }
    }
  ],
  "links": {
    "self": "https://reactor.adobe.io/audit_events?page%5Bnumber%5D=1&page%5Bsize%5D=25",
    "next": "https://reactor.adobe.io/audit_events?page%5Bnumber%5D=2&page%5Bsize%5D=25",
    "last": "https://reactor.adobe.io/audit_events?page%5Bnumber%5D=129&page%5Bsize%5D=25"
  },
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 2
    }
  }
}
```

## Pesquisar um evento de auditoria {#lookup}

Você pode pesquisar um evento de auditoria fornecendo sua ID no caminho de uma solicitação do GET.

**Formato da API**

```http
GET /audit_events/{AUDIT_EVENT_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `AUDIT_EVENT_ID` | O `id` do evento de auditoria que você deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/audit_events/AEa98742de8ef044d8b86767aa6a15a674 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do evento de auditoria.

```json
{
  "data": {
    "id": "AEd6a3b381fb8241818d7520001f8bd459",
    "type": "audit_events",
    "attributes": {
      "attributed_to_display_name": "John Smith",
      "attributed_to_email": "jsmith@example.com",
      "created_at": "2020-12-14T17:31:46.956Z",
      "display_name": "Example Rule",
      "type_of": "rule.created",
      "updated_at": "2020-12-14T17:31:46.956Z",
      "entity": "{\"data\":{\"id\":\"RL52d156a9074844b89ca20c987dbafd3b\",\"meta\":{\"latest_revision_number\":0},\"type\":\"rules\",\"links\":{\"self\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b\",\"origin\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b\",\"property\":\"https://reactor.adobe.io/properties/PR03cc61073ef74fd2af21e4cfb6ed97a7\",\"rule_components\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/rule_components\"},\"attributes\":{\"name\":\"Example Rule\",\"dirty\":true,\"enabled\":true,\"published\":false,\"created_at\":\"2020-12-14T17:31:46.883Z\",\"deleted_at\":null,\"updated_at\":\"2020-12-14T17:31:46.883Z\",\"published_at\":null,\"review_status\":\"unsubmitted\",\"revision_number\":0},\"relationships\":{\"notes\":{\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/notes\"}},\"origin\":{\"data\":{\"id\":\"RL52d156a9074844b89ca20c987dbafd3b\",\"type\":\"rules\"},\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/origin\"}},\"property\":{\"data\":{\"id\":\"PR03cc61073ef74fd2af21e4cfb6ed97a7\",\"type\":\"properties\"},\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/property\"}},\"libraries\":{\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/libraries\"}},\"revisions\":{\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/revisions\"}},\"rule_components\":{\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/rule_components\"}}}}}"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/audit_events/AEd6a3b381fb8241818d7520001f8bd459/property"
        },
        "data": {
          "id": "PR03cc61073ef74fd2af21e4cfb6ed97a7",
          "type": "properties"
        }
      },
      "entity": {
        "links": {
          "related": "https://reactor.adobe.io/audit_events/AEd6a3b381fb8241818d7520001f8bd459/rule"
        },
        "data": {
          "type": "rules",
          "id": "RL52d156a9074844b89ca20c987dbafd3b"
        }
      }
    },
    "links": {
      "entity": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b",
      "property": "https://reactor.adobe.io/properties/PR03cc61073ef74fd2af21e4cfb6ed97a7",
      "self": "https://reactor.adobe.io/audit_events/AEd6a3b381fb8241818d7520001f8bd459"
    },
    "meta": {
      "property_name": "Kessel Example Property"
    }
  }
}
```
