---
title: Ponto de extremidade de ambientes
description: Saiba como fazer chamadas para o endpoint /ambientes na API do Reator.
source-git-commit: 53612919dc040a8a3ad35a3c5c0991554ffbea7c
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 8%

---

# Ponto de extremidade de ambientes

Quando uma [biblioteca](./libraries.md) é compilada em uma [build](./builds.md) na API do reator, o conteúdo exato da build depende das configurações do ambiente e dos recursos incluídos na biblioteca. Especificamente, o ambiente determina o seguinte:

1. **Destino**: O local em que você deseja que a build seja implantada. Isso é controlado selecionando um [host](./hosts.md) para o ambiente a ser usado.
1. **Arquivar**: Você pode optar por recuperar a build como um conjunto implantável de arquivos ou compactá-la em um formato de arquivo. Isso é controlado pela configuração `archive` no ambiente.

O formato de destino e arquivamento configurado pelo ambiente altera a forma como você faz referência à build em seu aplicativo (que faz referência a um [código integrado](../../ui/publishing/environments.md#embed-code)). Se você fizer alterações no destino ou no formato de arquivo, deverá fazer uma atualização correspondente no aplicativo para usar a nova referência.

Os ambientes vêm em três tipos (ou estágios), com cada tipo tendo um limite diferente para o número total que você pode ter:

| Tipo de ambiente | Número permitido |
| --- | --- |
| Desenvolvimento | (Sem limite) |
| Armazenamento temporário | One |
| Produção | One |

{style=&quot;table-layout:auto&quot;}

Esses tipos de ambiente têm comportamento semelhante, mas são usados em estágios diferentes do [fluxo de trabalho de publicação de tags](../../ui/publishing/publishing-flow.md).

Um ambiente pertence a exatamente uma [propriedade](./properties.md).

Para obter informações mais gerais sobre ambientes, consulte a seção sobre [ambientes](../../ui/publishing/environments.md) nos documentos de publicação.

## Introdução

O endpoint usado neste guia faz parte da [API do reator](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Antes de continuar, reveja o [guia de introdução](../getting-started.md) para obter informações importantes sobre como autenticar para a API.

## Recuperar uma lista de ambientes {#list}

Você pode recuperar uma lista de ambientes para uma propriedade incluindo a ID da propriedade no caminho de uma solicitação do GET.

**Formato da API**

```http
GET /properties/{PROPERTY_ID}/environments
```

| Parâmetro | Descrição |
| --- | --- |
| `PROPERTY_ID` | O `id` da propriedade que possui os ambientes. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Usando parâmetros de consulta, os ambientes listados podem ser filtrados com base nos seguintes atributos:<ul><li>`archive`</li><li>`created_at`</li><li>`name`</li><li>`stage`</li><li>`token`</li><li>`updated_at`</li></ul>Consulte o guia sobre [respostas de filtragem](../guides/filtering.md) para obter mais informações.

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/environments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de ambientes para a propriedade especificada.

```json
{
  "data": [
    {
      "id": "ENbe322acb4fc64dfdb603254ffe98b5d3",
      "type": "environments",
      "attributes": {
        "archive": false,
        "created_at": "2020-12-14T17:38:51.047Z",
        "library_path": "f9fd106ab399/cb29d726b35e",
        "library_name": "launch-c0331746ae03-development.min.js",
        "library_entry_points": [
          {
            "library_name": "launch-c0331746ae03-development.min.js",
            "minified": true,
            "references": [
              "f9fd106ab399/cb29d726b35e/launch-c0331746ae03-development.min.js"
            ],
            "license_path": "f9fd106ab399/cb29d726b35e/launch-c0331746ae03-development.js"
          },
          {
            "library_name": "launch-c0331746ae03-development.js",
            "minified": false,
            "references": [
              "f9fd106ab399/cb29d726b35e/launch-c0331746ae03-development.js"
            ]
          }
        ],
        "name": "Development Environment A",
        "path": "https://assets.adobedtm.com/staging",
        "stage": "development",
        "updated_at": "2020-12-14T17:38:51.047Z",
        "status": "succeeded",
        "token": "c0331746ae03"
      },
      "relationships": {
        "library": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/library"
          },
          "data": null
        },
        "builds": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/builds"
          }
        },
        "host": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/host",
            "self": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/relationships/host"
          },
          "data": {
            "id": "HTc5cae9ce1e3943aab185bdba939f98bd",
            "type": "hosts"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/property"
          },
          "data": {
            "id": "PR06c9196bc57048dd8ff169c27baeeca8",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR06c9196bc57048dd8ff169c27baeeca8",
        "self": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3"
      },
      "meta": {
        "archive_encrypted": false
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

## Pesquisar um ambiente {#lookup}

Você pode pesquisar um ambiente fornecendo sua ID no caminho de uma solicitação do GET.

**Formato da API**

```http
GET /environments/{ENVIRONMENT_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `ENVIRONMENT_ID` | O `id` do ambiente que você deseja visualizar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do ambiente.

```json
{
  "data": {
    "id": "ENb0c1fbfdc1fd4b8593bfd269f827b3e6",
    "type": "environments",
    "attributes": {
      "archive": false,
      "created_at": "2020-12-14T17:38:30.378Z",
      "library_path": "f9fd106ab399/2f67fccade5e",
      "library_name": "launch-4436c89f6839-development.min.js",
      "library_entry_points": [
        {
          "library_name": "launch-4436c89f6839-development.min.js",
          "minified": true,
          "references": [
            "f9fd106ab399/2f67fccade5e/launch-4436c89f6839-development.min.js"
          ],
          "license_path": "f9fd106ab399/2f67fccade5e/launch-4436c89f6839-development.js"
        },
        {
          "library_name": "launch-4436c89f6839-development.js",
          "minified": false,
          "references": [
            "f9fd106ab399/2f67fccade5e/launch-4436c89f6839-development.js"
          ]
        }
      ],
      "name": "Development Environment A",
      "path": "https://assets.adobedtm.com/staging",
      "stage": "development",
      "updated_at": "2020-12-14T17:38:30.378Z",
      "status": "succeeded",
      "token": "4436c89f6839"
    },
    "relationships": {
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6/library"
        },
        "data": null
      },
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6/builds"
        }
      },
      "host": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6/host",
          "self": "https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6/relationships/host"
        },
        "data": {
          "id": "HTecb76453c8284f84a3c55fe981b5e6c9",
          "type": "hosts"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6/property"
        },
        "data": {
          "id": "PRadbee4fb64754081a945ed2a5b66627a",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRadbee4fb64754081a945ed2a5b66627a",
      "self": "https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6"
    },
    "meta": {
      "archive_encrypted": false
    }
  }
}
```

## Criar um ambiente {#create}

Você pode criar um novo ambiente fazendo uma solicitação POST.

**Formato da API**

```http
POST /properties/{PROPERTY_ID}/environments
```

| Parâmetro | Descrição |
| --- | --- |
| `PROPERTY_ID` | O `id` da [propriedade](./properties.md) em que você está definindo o ambiente. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir cria um novo ambiente para a propriedade especificada. A chamada também associa o ambiente a um host existente por meio da propriedade `relationships` . Consulte o guia sobre [relações](../guides/relationships.md) para obter mais informações.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/environments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Development Environment A",
            "archive": true,
            "archive_passphrase": "pass12345",
            "path": "/development-a",
            "stage": "development"
          },
          "relationships": {
            "host": {
              "data": {
                "id": "HT5d3fbe7bd34d4f65a46fad4598aefd4e",
                "type": "hosts"
              }
            }
          },
          "type": "environments"
        }
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `attributes.name` | **(Obrigatório)** Um nome legível para o ambiente. |
| `attributes.archive` | Um valor booleano que indica se a build está no formato de arquivamento. |
| `attributes.archive_passphrase` | Uma senha da string que pode ser usada para desbloquear o arquivo de arquivamento. |
| `attributes.path` | Um caminho do URL do host para o ambiente. |
| `attributes.stage` | O estágio para o ambiente (desenvolvimento, armazenamento temporário ou produção). |
| `id` | O `id` do ambiente que você deseja atualizar. Isso deve corresponder ao valor `{ENVIRONMENT_ID}` fornecido no caminho da solicitação. |
| `type` | O tipo de recurso que está sendo atualizado. Para esse ponto de extremidade, o valor deve ser `environments`. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do ambiente recém-criado.

```json
{
  "data": {
    "id": "EN867c480dc5ea4158be3ea68e5543bd85",
    "type": "environments",
    "attributes": {
      "archive": false,
      "created_at": "2020-12-14T17:31:57.857Z",
      "library_path": "f9fd106ab399/bd007122e3e3",
      "library_name": "launch-4d5a31f6ca53-development.min.js",
      "library_entry_points": [
        {
          "library_name": "launch-4d5a31f6ca53-development.min.js",
          "minified": true,
          "references": [
            "f9fd106ab399/bd007122e3e3/launch-4d5a31f6ca53-development.min.js"
          ],
          "license_path": "f9fd106ab399/bd007122e3e3/launch-4d5a31f6ca53-development.js"
        },
        {
          "library_name": "launch-4d5a31f6ca53-development.js",
          "minified": false,
          "references": [
            "f9fd106ab399/bd007122e3e3/launch-4d5a31f6ca53-development.js"
          ]
        }
      ],
      "name": "Development Environment A",
      "path": "https://assets.adobedtm.com/staging",
      "stage": "development",
      "updated_at": "2020-12-14T17:31:57.857Z",
      "status": "succeeded",
      "token": "4d5a31f6ca53"
    },
    "relationships": {
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85/library"
        },
        "data": null
      },
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85/builds"
        }
      },
      "host": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85/host",
          "self": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85/relationships/host"
        },
        "data": {
          "id": "HT5d3fbe7bd34d4f65a46fad4598aefd4e",
          "type": "hosts"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85/property"
        },
        "data": {
          "id": "PRa41874e4d1604efd9c3c67d7a123f4c6",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRa41874e4d1604efd9c3c67d7a123f4c6",
      "self": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85"
    },
    "meta": {
      "archive_encrypted": false
    }
  }
}
```

## Atualizar um ambiente {#update}

Você pode atualizar um ambiente ao incluir sua ID no caminho de uma solicitação do PATCH.

**Formato da API**

```http
PATCH /environments/{ENVIRONMENT_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `ENVIRONMENT_ID` | O `id` do ambiente que você deseja atualizar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir atualiza o `name` para um ambiente existente.

```shell
curl -X PATCH \
  https://reactor.adobe.io/environments/DE3fab176ccf8641838b3da59f716fc42b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "New Environment Name"
          },
          "id": "ENeb00d8f62d244732bd27765301b1410f",
          "type": "environments"
        }
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `attributes` | Um objeto cujas propriedades representam os atributos a serem atualizados para o ambiente. Os seguintes atributos de ambiente podem ser atualizados: <ul><li>`archive`</li><li>`archive_passphrase`</li><li>`include_debug_library`</li><li>`name`</li><li>`path`</li></ul> Consulte o exemplo de chamada para [criar um ambiente](#create) para obter uma lista de atributos e seu caso de uso. |
| `id` | O `id` do ambiente que você deseja atualizar. Isso deve corresponder ao valor `{ENVIRONMENT_ID}` fornecido no caminho da solicitação. |
| `type` | O tipo de recurso que está sendo atualizado. Para esse ponto de extremidade, o valor deve ser `environments`. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do ambiente atualizado.

```json
{
  "data": {
    "id": "ENeb00d8f62d244732bd27765301b1410f",
    "type": "environments",
    "attributes": {
      "archive": false,
      "created_at": "2020-12-14T17:38:40.608Z",
      "library_path": "f9fd106ab399/1eb59e88f015",
      "library_name": "launch-caa955ee58ff-development.min.js",
      "library_entry_points": [
        {
          "library_name": "launch-caa955ee58ff-development.min.js",
          "minified": true,
          "references": [
            "f9fd106ab399/1eb59e88f015/launch-caa955ee58ff-development.min.js"
          ],
          "license_path": "f9fd106ab399/1eb59e88f015/launch-caa955ee58ff-development.js"
        },
        {
          "library_name": "launch-caa955ee58ff-development.js",
          "minified": false,
          "references": [
            "f9fd106ab399/1eb59e88f015/launch-caa955ee58ff-development.js"
          ]
        }
      ],
      "name": "New environment name",
      "path": "https://assets.adobedtm.com/staging",
      "stage": "development",
      "updated_at": "2020-12-14T17:38:41.210Z",
      "status": "succeeded",
      "token": "caa955ee58ff"
    },
    "relationships": {
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/library"
        },
        "data": null
      },
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/builds"
        }
      },
      "host": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/host",
          "self": "https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/relationships/host"
        },
        "data": {
          "id": "HT7ea0b7c5c556476bafae8240da2d657d",
          "type": "hosts"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/property"
        },
        "data": {
          "id": "PR558b6514e529409fa740a34e5f974dd8",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR558b6514e529409fa740a34e5f974dd8",
      "self": "https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f"
    },
    "meta": {
      "archive_encrypted": false
    }
  }
}
```

## Excluir um ambiente

Você pode excluir um ambiente ao incluir sua ID no caminho de uma solicitação do DELETE.

**Formato da API**

```http
DELETE /environments/{ENVIRONMENT_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `ENVIRONMENT_ID` | O `id` do ambiente que você deseja excluir. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X DELETE \
  https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) sem corpo de resposta, indicando que o ambiente foi excluído.

## Recuperar recursos relacionados para um ambiente {#related}

As chamadas a seguir demonstram como recuperar os recursos relacionados para um ambiente. Quando [procurar um ambiente](#lookup), esses relacionamentos são listados na propriedade `relationships`.

Consulte o [guia de relacionamentos](../guides/relationships.md) para obter mais informações sobre relacionamentos na API de Reator.

### Listar as criações relacionadas de um ambiente {#builds}

Você pode listar as builds que usam um ambiente ao anexar `/builds` ao caminho de uma solicitação de pesquisa.

**Formato da API**

```http
GET  /environments/{ENVIRONMENT_ID}/builds
```

| Parâmetro | Descrição |
| --- | --- |
| `{ENVIRONMENT_ID}` | O `id` do ambiente cujas criações você deseja listar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/builds \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de builds que usam o ambiente especificado.

```json
{
  "data": [
    {
      "id": "BL775f919553aa4c6c8116cbf1da8baec8",
      "type": "builds",
      "attributes": {
        "created_at": "2020-12-14T17:32:43.113Z",
        "status": "pending",
        "updated_at": "2020-12-14T17:32:43.113Z",
        "token": "983989bcdad4"
      },
      "relationships": {
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8/extensions"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8/rules"
          }
        },
        "environment": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8/environment"
          },
          "data": {
            "id": "ENd8b1aee9d1674e7aa6135752ce839f82",
            "type": "environments"
          }
        },
        "library": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8/library"
          },
          "data": {
            "id": "LB9bca25483e0849a089524c5ca655f2fe",
            "type": "libraries"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8/property"
          },
          "data": {
            "id": "PRbe32d7f41b2741ecae1c06f6fd2d3906",
            "type": "properties"
          }
        }
      },
      "links": {
        "environment": "https://reactor.adobe.io/environments/ENd8b1aee9d1674e7aa6135752ce839f82",
        "library": "https://reactor.adobe.io/libraries/LB9bca25483e0849a089524c5ca655f2fe",
        "self": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8"
      },
      "meta": {
        "artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/70ee12a3f313/launch-d481f2d29bd0-development.min.js",
        "direct_artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/70ee12a3f313/983989bcdad4/launch-d481f2d29bd0-development.min.js",
        "archive": false,
        "host_type_of": "akamai"
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

### Procurar um ambiente no host relacionado {#host}

Você pode procurar o host que utiliza um ambiente ao anexar `/host` ao caminho de uma solicitação do GET.

>[!NOTE]
>
>Você pode pesquisar o próprio objeto de relação de host por meio de uma chamada [separada](#host-relationship).

**Formato da API**

```http
GET  /environments/{ENVIRONMENT_ID}/host
```

| Parâmetro | Descrição |
| --- | --- |
| `{ENVIRONMENT_ID}` | O `id` do ambiente cujo host você deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/host \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do host que usa o ambiente especificado.

```json
{
  "data": {
    "id": "HT621241cf4fbb4f7da5b6415ee1b15ac0",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:43:05.382Z",
      "server": null,
      "name": "Example Akamai Host",
      "path": null,
      "port": null,
      "status": "succeeded",
      "type_of": "akamai",
      "updated_at": "2020-12-14T17:43:05.382Z",
      "username": null
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HT621241cf4fbb4f7da5b6415ee1b15ac0/property"
        },
        "data": {
          "id": "PR50586546f7764fc59997342b8ff7647c",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR50586546f7764fc59997342b8ff7647c",
      "self": "https://reactor.adobe.io/hosts/HT621241cf4fbb4f7da5b6415ee1b15ac0"
    }
  }
}
```

### Pesquisar a biblioteca relacionada de um ambiente {#library}

Você pode pesquisar a biblioteca que usa um ambiente ao anexar `/library` ao caminho de uma solicitação do GET.

**Formato da API**

```http
GET  /environments/{ENVIRONMENT_ID}/library
```

| Parâmetro | Descrição |
| --- | --- |
| `{ENVIRONMENT_ID}` | O `id` do ambiente cuja biblioteca você deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/library \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da biblioteca que usa o ambiente especificado.

```json
{
  "data": {
    "id": "LB6ce27064ebe04ceab3d6942e9de563db",
    "type": "libraries",
    "attributes": {
      "created_at": "2020-12-14T17:50:06.695Z",
      "name": "My Library",
      "published_at": null,
      "state": "development",
      "updated_at": "2020-12-14T17:50:06.695Z",
      "build_required": true
    },
    "relationships": {
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/builds"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/environment",
          "self": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/relationships/environment"
        },
        "data": {
          "id": "EN3287da6fafa143c289afd2f578b4d33d",
          "type": "environments"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/data_elements",
          "self": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/relationships/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/extensions",
          "self": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/relationships/extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/notes"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/rules",
          "self": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/relationships/rules"
        }
      },
      "upstream_library": {
        "data": null
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/property"
        },
        "data": {
          "id": "PR95eaa16990c745a78f5bee8439fe4c34",
          "type": "properties"
        }
      },
      "last_build": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/last_build"
        },
        "data": null
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR95eaa16990c745a78f5bee8439fe4c34",
      "self": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db"
    },
    "meta": {
      "build_status": null,
      "build_required_detail": "No build found since last state change"
    }
  }
}
```

### Pesquisar a propriedade relacionada de um ambiente {#property}

Você pode pesquisar a propriedade que possui um ambiente ao anexar `/property` ao caminho de uma solicitação do GET.

**Formato da API**

```http
GET  /environments/{ENVIRONMENT_ID}/property
```

| Parâmetro | Descrição |
| --- | --- |
| `{ENVIRONMENT_ID}` | O `id` do ambiente cuja propriedade você deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da propriedade proprietária do ambiente especificado.

```json
{
  "data": {
    "id": "PR7688dba9f1384507bbd20f10947536f2",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:52:55.254Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:52:55.254Z",
      "platform": "web",
      "development": false,
      "token": "9611419d84a4",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/environments",
      "extensions": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/extensions",
      "rules": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/rules",
      "self": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2"
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
