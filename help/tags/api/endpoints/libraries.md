---
title: Ponto de extremidade de bibliotecas
description: Saiba como fazer chamadas para o endpoint /bibliotecas na API do Reator.
source-git-commit: 53612919dc040a8a3ad35a3c5c0991554ffbea7c
workflow-type: tm+mt
source-wordcount: '1588'
ht-degree: 8%

---

# Ponto de extremidade de bibliotecas

Uma biblioteca é uma coleção de recursos de tag ([extensions](./extensions.md), [rules](./rules.md) e [data elements](./data-elements.md)) que representam o comportamento desejado de uma [propriedade](./properties.md). O endpoint `/libraries` na API do Reator permite gerenciar programaticamente as bibliotecas nas propriedades da tag.

Uma biblioteca pertence a exatamente uma propriedade. Uma propriedade pode ter muitas bibliotecas.

## Introdução

O endpoint usado neste guia faz parte da [API do reator](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Antes de continuar, reveja o [guia de introdução](../getting-started.md) para obter informações importantes sobre como autenticar para a API.

Antes de trabalhar com bibliotecas na API do Reator, é importante entender as funções que os ambientes e o estado da biblioteca desempenham ao determinar quais ações você pode realizar em uma biblioteca específica. Consulte o guia no [fluxo de publicação da biblioteca](../../ui/publishing/publishing-flow.md) para obter mais informações.

## Recuperar uma lista de bibliotecas {#list}

Você pode recuperar uma lista de bibliotecas para uma propriedade, incluindo a ID da propriedade no caminho de uma solicitação do GET.

**Formato da API**

```http
GET /properties/{PROPERTY_ID}/libraries
```

| Parâmetro | Descrição |
| --- | --- |
| `PROPERTY_ID` | O `id` da propriedade que possui as bibliotecas. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Usando parâmetros de consulta, as bibliotecas listadas podem ser filtradas com base nos seguintes atributos:<ul><li>`created_at`</li><li>`name`</li><li>`published_at`</li><li>`stale`</li><li>`state`</li><li>`updated_at`</li></ul>Consulte o guia sobre [respostas de filtragem](../guides/filtering.md) para obter mais informações.

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR4bc17fb09ed845b1acfb0f6600a1f3c0/libraries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de bibliotecas para a propriedade especificada.

```json
{
  "data": [
    {
      "id": "LBb174d60bdbd34f87a2e9466fadaacae0",
      "type": "libraries",
      "attributes": {
        "created_at": "2020-12-14T17:44:10.776Z",
        "name": "My Library",
        "published_at": null,
        "state": "development",
        "updated_at": "2020-12-14T17:44:10.776Z",
        "build_required": true
      },
      "relationships": {
        "builds": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/builds"
          }
        },
        "environment": {
          "links": {
            "self": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/relationships/environment"
          },
          "data": null
        },
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/data_elements",
            "self": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/relationships/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/extensions",
            "self": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/relationships/extensions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/notes"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/rules",
            "self": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/relationships/rules"
          }
        },
        "upstream_library": {
          "data": null
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/property"
          },
          "data": {
            "id": "PR4bc17fb09ed845b1acfb0f6600a1f3c0",
            "type": "properties"
          }
        },
        "last_build": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/last_build"
          },
          "data": null
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR4bc17fb09ed845b1acfb0f6600a1f3c0",
        "self": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0"
      },
      "meta": {
        "build_status": null,
        "build_required_detail": "No build found since last state change"
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

## Pesquisar uma biblioteca {#lookup}

Você pode pesquisar uma biblioteca fornecendo sua ID no caminho de uma solicitação do GET.

**Formato da API**

```http
GET /libraries/{LIBRARY_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `LIBRARY_ID` | O `id` da biblioteca que você deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da biblioteca.

```json
{
  "data": {
    "id": "LB5862ee2dc21b4646a5536c8d6edb0c84",
    "type": "libraries",
    "attributes": {
      "created_at": "2020-12-14T17:44:00.476Z",
      "name": "My Library",
      "published_at": null,
      "state": "development",
      "updated_at": "2020-12-14T17:44:00.476Z",
      "build_required": true
    },
    "relationships": {
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/builds"
        }
      },
      "environment": {
        "links": {
          "self": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/relationships/environment"
        },
        "data": null
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/data_elements",
          "self": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/relationships/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/extensions",
          "self": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/relationships/extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/notes"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/rules",
          "self": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/relationships/rules"
        }
      },
      "upstream_library": {
        "data": null
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/property"
        },
        "data": {
          "id": "PRc90084c615844db58201d4e70d47b8bf",
          "type": "properties"
        }
      },
      "last_build": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/last_build"
        },
        "data": null
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRc90084c615844db58201d4e70d47b8bf",
      "self": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84"
    },
    "meta": {
      "build_status": null,
      "build_required_detail": "No build found since last state change"
    }
  }
}
```

## Criar uma biblioteca {#create}

Você pode criar uma nova biblioteca fazendo uma solicitação de POST.

**Formato da API**

```http
POST /properties/{PROPERTY_ID}/libraries
```

| Parâmetro | Descrição |
| --- | --- |
| `PROPERTY_ID` | O `id` da [propriedade](./properties.md) em que você está definindo a biblioteca. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir cria uma nova biblioteca para a propriedade especificada. Ao criar uma biblioteca pela primeira vez, somente seu atributo `name` pode ser configurado. Para adicionar elementos de dados, extensões e regras à biblioteca, você deve criar relacionamentos. Consulte a seção sobre [gerenciamento de recursos da biblioteca](#resources) para obter mais informações.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/libraries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "My Library"
          },
          "type": "libraries"
        }
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `attributes.name` | **(Obrigatório)** Um nome legível para a biblioteca. |
| `type` | O tipo de recurso que está sendo atualizado. Para esse ponto de extremidade, o valor deve ser `libraries`. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da biblioteca recém-criada.

```json
{
  "data": {
    "id": "DE8667bc64ceba4b599e8458ea4ab58b8f",
    "type": "libraries",
    "attributes": {
      "created_at": "2020-12-14T17:33:21.774Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "My library 2020-12-14 17:33:21 +0000",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:33:21.774Z",
      "clean_text": false,
      "default_value": null,
      "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
      "force_lower_case": false,
      "review_status": "unsubmitted",
      "storage_duration": null,
      "settings": "{\"elementSelector\":\".target-element\",\"elementProperty\":\"html\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/property"
        },
        "data": {
          "id": "PR05ad70a8078f44c1a229ecf0da2802f2",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/origin"
        },
        "data": {
          "id": "DE8667bc64ceba4b599e8458ea4ab58b8f",
          "type": "libraries"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/extension"
        },
        "data": {
          "id": "EX28788723a8e24a2f927fce1b55eb7ffc",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/updated_with_extension"
        },
        "data": {
          "id": "EXd6bf04b143e64fe0ae7efe55a6655fa9",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR05ad70a8078f44c1a229ecf0da2802f2",
      "origin": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f",
      "self": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f",
      "extension": "https://reactor.adobe.io/extensions/EX28788723a8e24a2f927fce1b55eb7ffc"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## Gerenciar recursos de uma biblioteca {#resources}

Os elementos de dados, extensões, regras e ambientes associados a uma biblioteca são estabelecidos por meio de relacionamentos. As seções abaixo abordam como gerenciar esses relacionamentos por meio de chamadas de API.

### Adicionar recursos a uma biblioteca {#add-resources}

Você pode adicionar recursos a uma biblioteca ao anexar `/relationships` ao caminho de uma solicitação do POST, seguido pelo tipo de recurso.

**Formato da API**

```http
POST /libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| Parâmetro | Descrição |
| --- | --- |
| `{LIBRARY_ID}` | A ID da biblioteca à qual você deseja adicionar recursos. |
| `{RESOURCE_TYPE}` | O tipo de recurso que você está adicionando à biblioteca. Os seguintes valores são aceitos: <ul><li>`data_elements`</li><li>`extensions`</li><li>`rules`</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir adiciona dois elementos de dados a uma biblioteca.

```shell
curl -X POST \
  https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/relationships/data_elements \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": [
          {
            "id": "DEce7fdee2afe44efeb4d974247d1e8dbe",
            "type": "data_elements"
          },
          {
            "id": "DE8097636264104451ac3a18c95d5ff833",
            "type": "data_elements"
          }
        ]
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID do recurso que você está adicionando à biblioteca. |
| `type` | O tipo de recurso que você está adicionando à biblioteca. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes dos relacionamentos adicionados. Executar uma solicitação de pesquisa [](#lookup) para a biblioteca mostra os relacionamentos adicionados na propriedade `relationships`.

```json
{
  "data": [
    {
      "type": "data_elements",
      "id": "DEce7fdee2afe44efeb4d974247d1e8dbe"
    },
    {
      "id": "DE8097636264104451ac3a18c95d5ff833",
      "type": "data_elements"
    }
  ],
  "links": {
    "related": "https://reactor.adobe.io/libraries/LB09eca17e012842b49466506f419283a7/data_elements",
    "self": "https://reactor.adobe.io/libraries/LB09eca17e012842b49466506f419283a7/relationships/data_elements"
  }
}
```

### Substituir os recursos de uma biblioteca {#replace-resources}

Você pode substituir todos os recursos existentes de um determinado tipo para uma biblioteca ao anexar `/relationships` ao caminho de uma solicitação do PATCH, seguido pelo tipo de recurso que está substituindo.

**Formato da API**

```http
PATCH /libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| Parâmetro | Descrição |
| --- | --- |
| `{LIBRARY_ID}` | A ID da biblioteca cujos relacionamentos você deseja substituir. |
| `{RESOURCE_TYPE}` | O tipo de recurso que você está substituindo. Os seguintes valores são aceitos: <ul><li>`data_elements`</li><li>`extensions`</li><li>`rules`</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir substitui as extensões de uma biblioteca pelas fornecidas na matriz `data`.

```shell
curl -X PATCH \
  https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/relationships/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": [
          {
            "id": "EX58312732fd0f43f98037d765ef96c4cd",
            "type": "extensions"
          }
        ]
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID do recurso que você está adicionando à biblioteca. |
| `type` | O tipo de recurso que você está adicionando à biblioteca. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes dos relacionamentos atualizados. Executar uma solicitação de pesquisa [](#lookup) para a biblioteca mostra os relacionamentos sob a propriedade `relationships`.

```json
{
  "data": [
    {
      "type": "extensions",
      "id": "EX58312732fd0f43f98037d765ef96c4cd"
    }
  ],
  "links": {
    "related": "https://reactor.adobe.io/libraries/LBdbc7c49ac8f040bc9576db26b127444d/extensions",
    "self": "https://reactor.adobe.io/libraries/LBdbc7c49ac8f040bc9576db26b127444d/relationships/extensions"
  }
}
```

### Remover recursos de uma biblioteca {#remove-resources}

Você pode remover recursos existentes de uma biblioteca ao anexar `/relationships` ao caminho de uma solicitação do DELETE, seguido pelo tipo de recurso que está removendo.

**Formato da API**

```http
DELETE /libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| Parâmetro | Descrição |
| --- | --- |
| `{LIBRARY_ID}` | A ID da biblioteca cujos recursos você deseja remover. |
| `{RESOURCE_TYPE}` | O tipo de recurso que você está removendo. Os seguintes valores são aceitos: <ul><li>`data_elements`</li><li>`extensions`</li><li>`rules`</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir remove uma regra de uma biblioteca. Quaisquer regras existentes que não estejam incluídas na matriz `data` não são excluídas.

```shell
curl -X DELETE \
  https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/relationships/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": [
          {
            "id": "RLa16f7859c7404239940c2cf2ec02b03c",
            "type": "rules"
          }
        ]
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID do recurso que você está removendo da biblioteca. |
| `type` | O tipo de recurso que você está removendo da biblioteca. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes dos relacionamentos atualizados para o tipo de recurso. Se não houver relações para esse tipo de recurso, a propriedade `data` será retornada como uma matriz vazia. Executar uma solicitação de pesquisa [](#lookup) para a biblioteca mostra os relacionamentos sob a propriedade `relationships`.

```json
{
  "data": [

  ],
  "links": {
    "related": "https://reactor.adobe.io/libraries/LBbde5759742844fe59458ca0c988ecd61/rules",
    "self": "https://reactor.adobe.io/libraries/LBbde5759742844fe59458ca0c988ecd61/relationships/rules"
  }
}
```

## Atribuir uma biblioteca a um ambiente {#environment}

Você pode atribuir uma biblioteca a um ambiente `/relationships/environment` ao caminho de uma solicitação de POST.

**Formato da API**

```http
POST /libraries/{LIBRARY_ID}/relationships/environment
```

| Parâmetro | Descrição |
| --- | --- |
| `{LIBRARY_ID}` | A ID da biblioteca que você deseja atribuir. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X POST \
  https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/relationships/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "id": "EN867c480dc5ea4158be3ea68e5543bd85",
          "type": "environments"
        }
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID do ambiente ao qual você atribui a biblioteca. |
| `type` | Deve ser definido como `environments`. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da relação. Executar uma solicitação de pesquisa [](#lookup) para a biblioteca mostra o relacionamento adicionado sob a propriedade `relationships`.

```json
{
  "data": {
    "id": "EN867c480dc5ea4158be3ea68e5543bd85",
    "type": "environments"
  },
  "links": {
    "related": "https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/environment",
    "self": "https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/relationships/environment"
  }
}
```

## Transição de uma biblioteca {#transition}

Você pode fazer a transição de uma biblioteca para um estado de publicação diferente ao incluir sua ID no caminho de uma solicitação do PATCH e fornecer um valor `meta.action` apropriado no payload.

**Formato da API**

```http
PATCH /libraries/{LIBRARY_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `LIBRARY_ID` | O `id` da biblioteca que você deseja fazer a transição. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir transita o estado de uma biblioteca existente, com base no valor de `meta.action` fornecido no payload. As ações disponíveis para uma biblioteca dependem do estado de publicação atual, conforme descrito no [fluxo de publicação](../../ui/publishing/publishing-flow.md#state).

```shell
curl -X PATCH \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "id": "LB80c337c956804738b2db2ea2f69fcdf0",
          "type": "libraries",
          "meta": {
            "action": "submit"
          }
        }
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `meta.action` | A ação de transição específica que você deseja realizar na biblioteca. As seguintes ações estão disponíveis, dependendo do estado de publicação atual da biblioteca: <ul><li>`develop`</li><li>`submit`</li><li>`approve`</li><li>`reject`</li></ul> |
| `id` | O `id` da biblioteca que deseja atualizar. Isso deve corresponder ao valor `{LIBRARY_ID}` fornecido no caminho da solicitação. |
| `type` | O tipo de recurso que está sendo atualizado. Para esse ponto de extremidade, o valor deve ser `libraries`. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da biblioteca atualizada.

```json
{
  "data": {
    "id": "LB80c337c956804738b2db2ea2f69fcdf0",
    "type": "libraries",
    "attributes": {
      "created_at": "2020-12-14T17:47:57.783Z",
      "name": "My Library",
      "published_at": null,
      "state": "submitted",
      "updated_at": "2020-12-14T17:48:06.431Z",
      "build_required": true
    },
    "relationships": {
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/builds"
        }
      },
      "environment": {
        "links": {
          "self": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/relationships/environment"
        },
        "data": null
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/data_elements",
          "self": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/relationships/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/extensions",
          "self": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/relationships/extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/notes"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/rules",
          "self": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/relationships/rules"
        }
      },
      "upstream_library": {
        "data": null
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/property"
        },
        "data": {
          "id": "PRbc84c93c1c9f48c9836ade5ea4199006",
          "type": "properties"
        }
      },
      "last_build": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/last_build"
        },
        "data": {
          "id": "BL8d6e931f2f6d48ea96d6730122f13bcc",
          "type": "builds"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRbc84c93c1c9f48c9836ade5ea4199006",
      "self": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0"
    },
    "meta": {
      "build_status": null,
      "build_required_detail": "No build found since last state change"
    }
  }
}
```

## Publicar uma biblioteca {#publish}

>[!NOTE]
>
>Somente as bibliotecas aprovadas podem ser publicadas para produção.

Para publicar uma biblioteca na produção, verifique se um ambiente de produção foi adicionado à biblioteca e crie uma build.

**Formato da API**

```http
POST /libraries/{LIBRARY_ID}/builds
```

| Parâmetro | Descrição |
| --- | --- |
| `LIBRARY_ID` | O `id` da biblioteca que você deseja publicar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

Essa solicitação não requer uma carga.

```shell
curl -X POST \
  https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/builds \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json'
```

**Resposta**

```json
{
  "data": {
    "id": "BL162b63703eb74c6bb3c12471e0062c05",
    "type": "builds",
    "attributes": {
      "created_at": "2020-12-14T17:48:18.731Z",
      "status": "pending",
      "updated_at": "2020-12-14T17:48:18.731Z",
      "token": "b223fc55df1c"
    },
    "relationships": {
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/rules"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/environment"
        },
        "data": {
          "id": "EN5428335fff304c749f06a241db137a60",
          "type": "environments"
        }
      },
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/library"
        },
        "data": {
          "id": "LBa937e62887e94d85b77cbe703f5dfc56",
          "type": "libraries"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/property"
        },
        "data": {
          "id": "PR7e2b7aaaffcb499398010ba964603415",
          "type": "properties"
        }
      }
    },
    "links": {
      "environment": "https://reactor.adobe.io/environments/EN5428335fff304c749f06a241db137a60",
      "library": "https://reactor.adobe.io/libraries/LBa937e62887e94d85b77cbe703f5dfc56",
      "self": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05"
    },
    "meta": {
      "artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/8b659dd115cf/launch-5986a1b644a4-development.min.js",
      "direct_artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/8b659dd115cf/b223fc55df1c/launch-5986a1b644a4-development.min.js",
      "archive": false,
      "host_type_of": "akamai"
    }
  }
}
```

## Gerenciar notas de uma biblioteca {#notes}

As bibliotecas são recursos &quot;notáveis&quot;, o que significa que você pode criar e recuperar notas baseadas em texto em cada recurso individual. Consulte o [guia de ponto de extremidade de notas](./notes.md) para obter mais informações sobre como gerenciar notas para bibliotecas e outros recursos compatíveis.

## Recuperar recursos relacionados para uma biblioteca {#related}

As chamadas a seguir demonstram como recuperar os recursos relacionados para uma biblioteca. Quando [procurar uma biblioteca](#lookup), esses relacionamentos são listados na propriedade `relationships`.

Consulte o [guia de relacionamentos](../guides/relationships.md) para obter mais informações sobre relacionamentos na API de Reator.

### Listar os elementos de dados relacionados para uma biblioteca {#data-elements}

Você pode listar os elementos de dados que uma biblioteca usa ao anexar `/data_elements` ao caminho de uma solicitação de pesquisa.

**Formato da API**

```http
GET  /libraries/{LIBRARY_ID}/data_elements
```

| Parâmetro | Descrição |
| --- | --- |
| `{LIBRARY_ID}` | O `id` da biblioteca cujos elementos de dados você deseja listar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/data_elements \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de elementos de dados que usam a biblioteca especificada.

```json
{
  "data": [
    {
      "id": "DE4956628e8baa4b358cc592337049b37b",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:45:11.694Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "My Data Element 2020-12-14 17:45:10 +0000",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:45:11.694Z",
        "clean_text": false,
        "default_value": null,
        "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
        "force_lower_case": false,
        "review_status": "unsubmitted",
        "storage_duration": null,
        "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/property"
          },
          "data": {
            "id": "PR245ca5e560784249b2a88ef82f2851b6",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/origin"
          },
          "data": {
            "id": "DE4c027939f2004fdcb15e3b4099e70974",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/extension"
          },
          "data": {
            "id": "EX5942ffd7fac94428875bd664e397bd47",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/updated_with_extension"
          },
          "data": {
            "id": "EXbf411638b90843c486254b5ca0fe47d6",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR245ca5e560784249b2a88ef82f2851b6",
        "origin": "https://reactor.adobe.io/data_elements/DE4c027939f2004fdcb15e3b4099e70974",
        "self": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b",
        "extension": "https://reactor.adobe.io/extensions/EX5942ffd7fac94428875bd664e397bd47"
      },
      "meta": {
        "latest_revision_number": 1
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

### Listar as extensões relacionadas para uma biblioteca {#extensions}

Você pode listar as extensões que uma biblioteca usa ao anexar `/extensions` ao caminho de uma solicitação de pesquisa.

**Formato da API**

```http
GET  /libraries/{LIBRARY_ID}/extensions
```

| Parâmetro | Descrição |
| --- | --- |
| `{LIBRARY_ID}` | O `id` da biblioteca cujas extensões você deseja listar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/extensions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de extensões que usam a biblioteca especificada.

```json
{
  "data": [
    {
      "id": "EXac1e55883e5b47eb9a3589b311960677",
      "type": "extensions",
      "attributes": {
        "created_at": "2020-12-14T17:45:23.759Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "kessel-test",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:45:23.759Z",
        "delegate_descriptor_id": null,
        "display_name": "Kessel Test",
        "review_status": "unsubmitted",
        "version": "1.2.0",
        "settings": "{}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/property"
          },
          "data": {
            "id": "PR2d1f3ba867204dc7a4c17614d23bbab0",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/origin"
          },
          "data": {
            "id": "EX63cf3b91ec8146889759bbacb15627c3",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR2d1f3ba867204dc7a4c17614d23bbab0",
        "origin": "https://reactor.adobe.io/extensions/EX63cf3b91ec8146889759bbacb15627c3",
        "self": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677",
        "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
        "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
      },
      "meta": {
        "latest_revision_number": 1
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

### Listar as regras relacionadas para uma biblioteca {#rules}

Você pode listar as regras que uma biblioteca usa ao anexar `/rules` ao caminho de uma solicitação de pesquisa.

**Formato da API**

```http
GET  /libraries/{LIBRARY_ID}/rules
```

| Parâmetro | Descrição |
| --- | --- |
| `{LIBRARY_ID}` | O `id` da biblioteca cujas regras você deseja listar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/rules \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de regras que usam a biblioteca especificada.

```json
{
  "data": [
    {
      "id": "RL460e550125054fffb824cce56c8cb1ac",
      "type": "rules",
      "attributes": {
        "created_at": "2020-12-14T17:45:36.405Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "Example Rule",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:45:36.405Z",
        "review_status": "unsubmitted"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/property"
          },
          "data": {
            "id": "PRa68d0d2c6e0a4ae380fb30f17f7c435d",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/origin"
          },
          "data": {
            "id": "RL04911614524d463a9c115bea442bce72",
            "type": "rules"
          }
        },
        "rule_components": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/rule_components"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRa68d0d2c6e0a4ae380fb30f17f7c435d",
        "origin": "https://reactor.adobe.io/rules/RL04911614524d463a9c115bea442bce72",
        "self": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac",
        "rule_components": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/rule_components"
      },
      "meta": {
        "latest_revision_number": 1
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

### Procure uma biblioteca no ambiente relacionado {#related-environment}

Você pode pesquisar o ambiente ao qual uma biblioteca é atribuída ao anexar `/environment` ao caminho de uma solicitação do GET.

**Formato da API**

```http
GET  /libraries/{LIBRARY_ID}/environment
```

| Parâmetro | Descrição |
| --- | --- |
| `{LIBRARY_ID}` | O `id` da biblioteca cujo ambiente você deseja visualizar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do ambiente ao qual a biblioteca especificada está atribuída.

```json
{
  "data": {
    "id": "ENe66122e6793641d8a8453f63c42e4270",
    "type": "environments",
    "attributes": {
      "archive": false,
      "created_at": "2020-12-14T17:39:12.484Z",
      "library_path": "f9fd106ab399/2df53b69e8a2",
      "library_name": "launch-1d2ffee7eef5-development.min.js",
      "library_entry_points": [
        {
          "library_name": "launch-1d2ffee7eef5-development.min.js",
          "minified": true,
          "references": [
            "f9fd106ab399/2df53b69e8a2/launch-1d2ffee7eef5-development.min.js"
          ],
          "license_path": "f9fd106ab399/2df53b69e8a2/launch-1d2ffee7eef5-development.js"
        },
        {
          "library_name": "launch-1d2ffee7eef5-development.js",
          "minified": false,
          "references": [
            "f9fd106ab399/2df53b69e8a2/launch-1d2ffee7eef5-development.js"
          ]
        }
      ],
      "name": "Development Environment A",
      "path": "https://assets.adobedtm.com/staging",
      "stage": "development",
      "updated_at": "2020-12-14T17:39:13.988Z",
      "status": "succeeded",
      "token": "1d2ffee7eef5"
    },
    "relationships": {
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270/library"
        },
        "data": {
          "id": "LB52ccd7f1e99146999f90cb3bca4940a2",
          "type": "libraries"
        }
      },
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270/builds"
        }
      },
      "host": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270/host",
          "self": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270/relationships/host"
        },
        "data": {
          "id": "HT53a4ebcb177d431e8fd26929930de0af",
          "type": "hosts"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270/property"
        },
        "data": {
          "id": "PR79de7e0885a9451786f1bf4b9136a72c",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR79de7e0885a9451786f1bf4b9136a72c",
      "self": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270"
    },
    "meta": {
      "archive_encrypted": false
    }
  }
}
```

### Pesquisar a propriedade relacionada de uma biblioteca {#property}

Você pode pesquisar a propriedade que possui uma biblioteca ao anexar `/property` ao caminho de uma solicitação do GET.

**Formato da API**

```http
GET  /libraries/{LIBRARY_ID}/property
```

| Parâmetro | Descrição |
| --- | --- |
| `{LIBRARY_ID}` | O `id` da biblioteca cuja propriedade você deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da propriedade proprietária da biblioteca especificada.

```json
{
  "data": {
    "id": "PRb18ac8f8b69d4f99af43870e91c17543",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:51:56.180Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:51:56.180Z",
      "platform": "web",
      "development": false,
      "token": "9d97006b0f9b",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/data_elements",
      "environments": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/environments",
      "extensions": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/extensions",
      "rules": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/rules",
      "self": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```

### Procure uma biblioteca no upstream {#upstream}

Você pode procurar a próxima biblioteca upstream de uma biblioteca ao anexar `/upstream_library` ao caminho de uma solicitação do GET.

**Formato da API**

```http
GET  /libraries/{LIBRARY_ID}/upstream_library
```

| Parâmetro | Descrição |
| --- | --- |
| `{LIBRARY_ID}` | O `id` da biblioteca cuja biblioteca upstream você deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/upstream_library \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da biblioteca upstream.

```json
{
  "data": {
    "id": "LB29cc2f86b3684e00a10d196a60f4b0c0",
    "type": "libraries",
    "attributes": {
      "created_at": "2020-12-14T17:49:32.459Z",
      "name": "My Library",
      "published_at": null,
      "state": "submitted",
      "updated_at": "2020-12-14T17:49:41.070Z",
      "build_required": true
    },
    "relationships": {
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/builds"
        }
      },
      "environment": {
        "links": {
          "self": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/relationships/environment"
        },
        "data": null
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/data_elements",
          "self": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/relationships/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/extensions",
          "self": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/relationships/extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/notes"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/rules",
          "self": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/relationships/rules"
        }
      },
      "upstream_library": {
        "data": null
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/property"
        },
        "data": {
          "id": "PR7c206ed399644222aef329488cee7fa7",
          "type": "properties"
        }
      },
      "last_build": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/last_build"
        },
        "data": {
          "id": "BL87cde018ecd44ac7a20b0271ab06d04b",
          "type": "builds"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR7c206ed399644222aef329488cee7fa7",
      "self": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0"
    },
    "meta": {
      "build_status": null,
      "build_required_detail": "No build found since last state change"
    }
  }
}
```
