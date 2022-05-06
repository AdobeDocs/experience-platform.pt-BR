---
title: Endpoint de extensões
description: Saiba como fazer chamadas para o ponto de extremidade /extensions na API do Reactor.
exl-id: cc02b2aa-d107-463a-930c-5a9fcc5b4a5a
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 99%

---

# Endpoint de extensões

Na API do Reactor, uma extensão representa a instância instalada de um [pacote de extensão](./extension-packages.md). Uma extensão disponibiliza os recursos definidos por um pacote de extensão para uma [propriedade](./properties.md). Esses recursos são aproveitados ao serem criadas [extensões](./data-elements.md) e [componentes de regra](./rule-components.md).

Uma extensão pertence a exatamente uma propriedade. Uma propriedade pode ter muitas extensões, mas não mais de uma instância instalada de um pacote de extensão específico.

## Introdução

O endpoint usado neste manual faz parte da [API do Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Antes de continuar, consulte o [guia de introdução](../getting-started.md) para obter informações importantes sobre como realizar a autenticação para a API.

## Recuperar uma lista de extensões {#list}

Você pode recuperar uma lista de extensões para uma propriedade fazendo uma solicitação GET.

**Formato da API**

```http
GET properties/{PROPERTY_ID}/extensions
```

| Parâmetro | Descrição |
| --- | --- |
| `{PROPERTY_ID}` | O `id` da propriedade cujas extensões você deseja listar. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Usando parâmetros de consulta, as extensões listadas podem ser filtradas com base nos seguintes atributos:<ul><li>`created_at`</li><li>`dirty`</li><li>`display_name`</li><li>`enabled`</li><li>`name`</li><li>`origin_id`</li><li>`published`</li><li>`published_at`</li><li>`revision_number`</li><li>`updated_at`</li><li>`version`</li></ul>Consulte o manual sobre [filtragem de respostas](../guides/filtering.md) para obter mais informações.

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRee071cb5b7794f42b74c913e1ad2e325/extensions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de extensões definidas na propriedade especificada.

```json
{
  "data": [
    {
      "id": "EXd9d80c87afb6432ba823a58d3e78299b",
      "type": "extensions",
      "attributes": {
        "created_at": "2020-12-14T17:40:21.000Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "kessel-test",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:40:21.000Z",
        "delegate_descriptor_id": null,
        "display_name": "Kessel Test",
        "review_status": "unsubmitted",
        "version": "1.2.0",
        "settings": "{}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/property"
          },
          "data": {
            "id": "PRee071cb5b7794f42b74c913e1ad2e325",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/origin"
          },
          "data": {
            "id": "EXd9d80c87afb6432ba823a58d3e78299b",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRee071cb5b7794f42b74c913e1ad2e325",
        "origin": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b",
        "self": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b",
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

## Pesquisar uma extensão {#lookup}

Você pode pesquisar uma extensão fornecendo a respectiva ID no caminho de uma solicitação GET.

>[!NOTE]
>
>Quando as extensões são excluídas, elas são sinalizadas como excluídas no sistema, mas não são realmente removidas. Portanto, é possível recuperar uma extensão excluída. As extensões excluídas podem ser identificadas pela presença de uma propriedade `deleted_at` no `meta` dos dados de extensão retornados.

**Formato da API**

```http
GET /extensions/{EXTENSION_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `EXTENSION_ID` | O `id` da extensão que você deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da extensão.

```json
{
  "data": {
    "id": "EX2ba586f436ac48e390a1ee7e8c9a8f6e",
    "type": "extensions",
    "attributes": {
      "created_at": "2020-12-14T17:40:09.823Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "kessel-test",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:40:09.823Z",
      "delegate_descriptor_id": null,
      "display_name": "Kessel Test",
      "review_status": "unsubmitted",
      "version": "1.2.0",
      "settings": "{}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e/property"
        },
        "data": {
          "id": "PR2254ac6a096c4df38508700093d3e153",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e/origin"
        },
        "data": {
          "id": "EX2ba586f436ac48e390a1ee7e8c9a8f6e",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e/extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR2254ac6a096c4df38508700093d3e153",
      "origin": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e",
      "self": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e",
      "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
      "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

## Criar ou atualizar uma extensão {#create}

As extensões são criadas referenciando um [pacote de extensão](./extension-packages.md) e adicionando a extensão instalada a uma propriedade. Quando a tarefa de instalação for concluída, uma resposta será retornada para indicar se a extensão foi instalada com êxito.

**Formato da API**

```http
POST /properties/{PROPERTY_ID}/extensions
```

| Parâmetro | Descrição |
| --- | --- |
| `PROPERTY_ID` | O `id` da propriedade em que você deseja instalar a extensão. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRee071cb5b7794f42b74c913e1ad2e325/extensions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "delegate_descriptor_id": "example-package::extensionConfiguration::config",
            "enabled": true,
            "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
          },
          "relationships": {
            "extension_package": {
              "data": {
                "id": "EP75db2452065b44e2b8a38ca883ce369a",
                "type": "extension_packages"
              }
            }
          },
          "type": "extensions"
        }
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `relationships.extension_package` | **(Obrigatório)** Um objeto que faz referência à ID do pacote de extensão que está sendo instalado. |
| `attributes.delegate_descriptor_id` | Se sua extensão exigir configurações personalizadas, ela também exigirá uma ID de descritor delegado. Consulte o manual sobre [IDs de descritor delegado](../guides/delegate-descriptor-ids.md) para obter mais informações. |
| `attributes.enabled` | Um booliano que indica se a extensão está ativada. |
| `attributes.settings` | Um objeto JSON de configurações representado como uma string. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da extensão recém-criada.

```json
{
  "data": {
    "id": "EX8ce7ced633f34bd48d33089ff8fad082",
    "type": "extensions",
    "attributes": {
      "created_at": "2020-12-14T17:32:56.137Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "kessel-test",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:32:56.137Z",
      "delegate_descriptor_id": "example-package::extensionConfiguration::config",
      "display_name": "Kessel Test",
      "review_status": "unsubmitted",
      "version": "1.2.0",
      "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/property"
        },
        "data": {
          "id": "PRcf1f3e4c218b4caab8191fab003a8355",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/origin"
        },
        "data": {
          "id": "EX8ce7ced633f34bd48d33089ff8fad082",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRcf1f3e4c218b4caab8191fab003a8355",
      "origin": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082",
      "self": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082",
      "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
      "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

## Revisar uma extensão {#revise}

É possível revisar uma extensão incluindo a respectiva ID no caminho de uma solicitação PATCH.

**Formato da API**

```http
PATCH /extensions/{EXTENSION_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `EXTENSION_ID` | O `id` da extensão que você deseja revisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

Assim como ocorre na [criação de uma extensão](#create), uma versão local do pacote revisado deve ser carregada por meio de dados de formulário.

```shell
curl -X PATCH \
  https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "enabled": false,
          },
          "meta": {
            "action": "revise"
          },
          "id": "EX85509bc7baea4f8599bc44024ed3f110",
          "type": "extensions"
        }
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `attributes` | Os atributos que você deseja revisar. Para extensões, você pode revisar os atributos `delegate_descriptor_id`, `enabled` e `settings`. |
| `meta.action` | Deve ser incluído com um valor `revise` ao ser feita uma revisão. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da extensão revisada, com a propriedade `meta.latest_revision_number` aumentada em 1.

```json
{
  "data": {
    "id": "EX8ce7ced633f34bd48d33089ff8fad082",
    "type": "extensions",
    "attributes": {
      "created_at": "2020-12-14T17:32:56.137Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": false,
      "name": "kessel-test",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:32:56.137Z",
      "delegate_descriptor_id": "example-package::extensionConfiguration::config",
      "display_name": "Kessel Test",
      "review_status": "unsubmitted",
      "version": "1.2.0",
      "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/property"
        },
        "data": {
          "id": "PRcf1f3e4c218b4caab8191fab003a8355",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/origin"
        },
        "data": {
          "id": "EX8ce7ced633f34bd48d33089ff8fad082",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRcf1f3e4c218b4caab8191fab003a8355",
      "origin": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082",
      "self": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082",
      "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
      "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    },
    "meta": {
      "latest_revision_number": 2
    }
  }
}
```

## Excluir uma extensão {#private-release}

Você pode excluir uma extensão incluindo a respectiva ID no caminho de uma solicitação DELETE.

**Formato da API**

```http
DELETE /extensions/{EXTENSION_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `EXTENSION_ID` | O `id` da extensão que você deseja excluir. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X DELETE \
  https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) sem corpo de resposta, indicando que a extensão foi excluída.

## Gerenciar notas de uma extensão {#notes}

As extensões são recursos &quot;anotáveis&quot;, o que significa que você pode criar e recuperar notas baseadas em texto em cada recurso individual. Consulte o [manual de endpoint de notas](./notes.md) para obter mais informações sobre como gerenciar notas de extensões e outros recursos compatíveis.

## Recuperar recursos relacionados a uma extensão {#related}

As chamadas a seguir demonstram como recuperar os recursos relacionados a uma extensão. Quando você [pesquisa uma extensão](#lookup), esses relacionamentos são listados na propriedade `relationships`.

Consulte o [manual de relacionamentos](../guides/relationships.md) para obter mais informações sobre relacionamentos na API do reator.

### Listar as bibliotecas relacionadas a uma extensão {#libraries}

Você pode listar as bibliotecas que utilizam uma extensão anexando `/libraries` ao caminho de uma solicitação de pesquisa.

**Formato da API**

```http
GET  /extensions/{EXTENSION_ID}/libraries
```

| Parâmetro | Descrição |
| --- | --- |
| `{EXTENSION_ID}` | O `id` da extensão cujas bibliotecas você deseja listar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/libraries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de bibliotecas que usam a extensão especificada.

```json
{
  "data": [
    {
      "id": "LB62d20ad807a949e6b13b0a2c7299eb65",
      "type": "libraries",
      "attributes": {
        "created_at": "2020-12-14T17:50:19.589Z",
        "name": "My Library",
        "published_at": null,
        "state": "development",
        "updated_at": "2020-12-14T17:50:19.589Z",
        "build_required": true
      },
      "relationships": {
        "builds": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/builds"
          }
        },
        "environment": {
          "links": {
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/environment"
          },
          "data": null
        },
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/data_elements",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/extensions",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/extensions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/notes"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/rules",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/rules"
          }
        },
        "upstream_library": {
          "data": null
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/property"
          },
          "data": {
            "id": "PR241ba9cd56324ac192de68d658f20cb0",
            "type": "properties"
          }
        },
        "last_build": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/last_build"
          },
          "data": null
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR241ba9cd56324ac192de68d658f20cb0",
        "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65"
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

### Listar as revisões relacionadas de uma extensão {#revisions}

Você pode listar as revisões anteriores de uma extensão anexando `/revisions` ao caminho de uma solicitação de pesquisa.

**Formato da API**

```http
GET  /extensions/{EXTENSION_ID}/revisions
```

| Parâmetro | Descrição |
| --- | --- |
| `{EXTENSION_ID}` | O `id` da extensão cujas revisões você deseja listar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/revisions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de revisões da extensão especificada.

```json
{
  "data": [
    {
      "id": "EXbfcca9f3ce9d40318b9115159a951e09",
      "type": "extensions",
      "attributes": {
        "created_at": "2020-12-14T17:41:09.023Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "kessel-test",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:41:09.023Z",
        "delegate_descriptor_id": null,
        "display_name": "Kessel Test",
        "review_status": "unsubmitted",
        "version": "1.2.0",
        "settings": "{}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXbfcca9f3ce9d40318b9115159a951e09/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXbfcca9f3ce9d40318b9115159a951e09/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXbfcca9f3ce9d40318b9115159a951e09/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXbfcca9f3ce9d40318b9115159a951e09/property"
          },
          "data": {
            "id": "PR92de152ae31e48a692142ea65c1efeb9",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXbfcca9f3ce9d40318b9115159a951e09/origin"
          },
          "data": {
            "id": "EXd485e07fb3d3429b997768ae40de8f02",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXbfcca9f3ce9d40318b9115159a951e09/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXbfcca9f3ce9d40318b9115159a951e09/extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR92de152ae31e48a692142ea65c1efeb9",
        "origin": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02",
        "self": "https://reactor.adobe.io/extensions/EXbfcca9f3ce9d40318b9115159a951e09",
        "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
        "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
      },
      "meta": {
        "latest_revision_number": 1
      }
    },
    {
      "id": "EXd485e07fb3d3429b997768ae40de8f02",
      "type": "extensions",
      "attributes": {
        "created_at": "2020-12-14T17:41:09.002Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "kessel-test",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:41:09.002Z",
        "delegate_descriptor_id": null,
        "display_name": "Kessel Test",
        "review_status": "unsubmitted",
        "version": "1.2.0",
        "settings": "{}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02/property"
          },
          "data": {
            "id": "PR92de152ae31e48a692142ea65c1efeb9",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02/origin"
          },
          "data": {
            "id": "EXd485e07fb3d3429b997768ae40de8f02",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02/extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR92de152ae31e48a692142ea65c1efeb9",
        "origin": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02",
        "self": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02",
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
      "total_count": 2
    }
  }
}
```

### Procurar o pacote relacionado a uma extensão {#extension}

Você pode pesquisar o pacote no qual uma extensão se baseia anexando `/extension_package` ao caminho de uma solicitação GET.

**Formato da API**

```http
GET  /extensions/{EXTENSION_ID}/extension_package
```

| Parâmetro | Descrição |
| --- | --- |
| `{EXTENSION_ID}` | O `id` da extensão cuja extensão você deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/extension \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do pacote em que a extensão especificada se baseia. O exemplo de resposta a seguir foi truncado por questões de espaço.

```json
{
  "data": {
    "id": "EP75db2452065b44e2b8a38ca883ce369a",
    "type": "extension_packages",
    "attributes": {
      "actions": [
        {
          "id": "kessel-test::actions::custom-code",
          "name": "custom-code",
          "schema": {
            "type": "object",
            "oneOf": [
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "global": {
                    "type": "boolean"
                  },
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "javascript"
                    ]
                  }
                },
                "additionalProperties": false
              },
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "html"
                    ]
                  }
                },
                "additionalProperties": false
              }
            ],
            "$schema": "http://json-schema.org/draft-04/schema#"
          },
          "libPath": "src/lib/actions/customCode.js",
          "viewPath": "actions/customCode.html",
          "displayName": "Custom Code"
        }
      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP75db2452065b44e2b8a38ca883ce369a",
      "conditions": [
        {
          "id": "kessel-test::conditions::browser",
          "name": "browser",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "browsers"
            ],
            "properties": {
              "browsers": {
                "type": "array",
                "items": {
                  "enum": [
                    "Chrome",
                    "Firefox",
                    "IE",
                    "Edge",
                    "Safari",
                    "Mobile Safari"
                  ],
                  "type": "string"
                }
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/conditions/browser.js",
          "viewPath": "conditions/browser.html",
          "displayName": "Browser",
          "categoryName": "Technology"
        }
      ],
      "configuration": null,
      "created_at": "2020-11-09T17:51:59.433Z",
      "data_elements": [
        {
          "id": "kessel-test::dataElements::cookie",
          "name": "cookie",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "name"
            ],
            "properties": {
              "name": {
                "type": "string",
                "minLength": 1
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/dataElements/cookie.js",
          "viewPath": "dataElements/cookie.html",
          "displayName": "Cookie"
        }
      ],
      "description": "Provides default event, condition, and data element types available to all tags users.",
      "discontinued": false,
      "display_name": "Kessel Test",
      "events": [
        {
          "id": "kessel-test::events::blur",
          "name": "blur",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "properties": {
              "bubbleStop": {
                "type": "boolean"
              },
              "elementSelector": {
                "type": "string",
                "minLength": 1
              },
              "elementProperties": {
                "type": "array",
                "items": {
                  "type": "object",
                  "required": [
                    "name",
                    "value"
                  ],
                  "properties": {
                    "name": {
                      "type": "string",
                      "minLength": 1
                    },
                    "value": {
                      "type": "string"
                    },
                    "valueIsRegex": {
                      "type": "boolean"
                    }
                  },
                  "additionalProperties": false
                }
              },
              "bubbleFireIfParent": {
                "type": "boolean"
              },
              "bubbleFireIfChildFired": {
                "type": "boolean"
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/events/blur.js",
          "viewPath": "events/blur.html",
          "displayName": "Blur",
          "categoryName": "Form"
        }
      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "kessel-test",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-11-09T17:54:01.487Z",
      "version": "1.2.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    }
  }
}
```

### Procurar a origem relacionada a uma extensão {#origin}

É possível pesquisar a origem de uma extensão anexando `/origin` ao caminho de uma solicitação GET. A origem de uma extensão é a revisão anterior que foi atualizada para criar a revisão atual.

**Formato da API**

```http
GET  /extensions/{EXTENSION_ID}/origin
```

| Parâmetro | Descrição |
| --- | --- |
| `{EXTENSION_ID}` | O `id` da extensão cuja origem você deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/origin \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da origem da extensão especificada.

```json
{
  "data": {
    "id": "EX524f2cd22ae4490eaf73cc9214eb217d",
    "type": "extensions",
    "attributes": {
      "created_at": "2020-12-14T17:41:21.397Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "kessel-test",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:41:21.397Z",
      "delegate_descriptor_id": null,
      "display_name": "Kessel Test",
      "review_status": "unsubmitted",
      "version": "1.2.0",
      "settings": "{}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d/property"
        },
        "data": {
          "id": "PR88d6b8ee423b44a49de1dee26391e25b",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d/origin"
        },
        "data": {
          "id": "EX524f2cd22ae4490eaf73cc9214eb217d",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d/extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR88d6b8ee423b44a49de1dee26391e25b",
      "origin": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d",
      "self": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d",
      "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
      "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

### Pesquisar uma extensão na propriedade relacionada {#property}

Você pode pesquisar a propriedade que possui uma extensão anexando `/property` ao caminho de uma solicitação GET.

**Formato da API**

```http
GET  /extensions/{EXTENSION_ID}/property
```

| Parâmetro | Descrição |
| --- | --- |
| `{EXTENSION_ID}` | O `id` da extensão cuja propriedade você deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da propriedade que possui a extensão especificada.

```json
{
  "data": {
    "id": "PR96fd3675be144ddc8c4540d79430355a",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:53:06.993Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:53:06.993Z",
      "platform": "web",
      "development": false,
      "token": "bf75a40b3c34",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/environments",
      "extensions": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/extensions",
      "rules": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/rules",
      "self": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a"
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
