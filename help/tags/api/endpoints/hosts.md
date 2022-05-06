---
title: Ponto de extremidade de hosts
description: Saiba como fazer chamadas para o ponto de extremidade /hosts na API do reator.
exl-id: 9d0d2a65-49e9-429c-a665-754b59a11cf1
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 99%

---

# Ponto de extremidade de hosts

>[!NOTE]
>
>Este documento aborda como gerenciar hosts na API do reator. Para obter mais informações sobre hosts para tags, consulte o manual sobre [visão geral de hosts](../../ui/publishing/hosts/hosts-overview.md) na documentação de publicação.

Na API do Reactor, um host define um destino em que um [build](./builds.md) pode ser entregue.

Quando um build é solicitado por um usuário de tags na Adobe Experience Platform, o sistema verifica a biblioteca para determinar para qual [ambiente](./environments.md) a biblioteca deve ser criada. Cada ambiente tem um relacionamento com um host, indicando onde entregar o build.

Um host pertence a exatamente uma [propriedade](./properties.md), enquanto uma propriedade pode ter muitos hosts. Uma propriedade deve ter pelo menos um host para que você possa realizar a publicação.

Um host pode ser usado por mais de um ambiente em uma propriedade. É comum ter um único host em uma propriedade e ter todos os ambientes nessa propriedade usando o mesmo host.

## Introdução

O endpoint usado neste manual faz parte da [API do Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Antes de continuar, consulte o [guia de introdução](../getting-started.md) para obter informações importantes sobre como realizar a autenticação para a API.

## Recuperar uma lista de hosts {#list}

Você pode recuperar uma lista de hosts para uma propriedade, incluindo a ID da propriedade no caminho de uma solicitação GET.

**Formato da API**

```http
GET /properties/{PROPERTY_ID}/hosts
```

| Parâmetro | Descrição |
| --- | --- |
| `PROPERTY_ID` | O `id` da propriedade que tem os hosts. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Usando parâmetros de consulta, os hosts listados podem ser filtrados com base nos seguintes atributos:<ul><li>`created_at`</li><li>`name`</li><li>`type_of`</li><li>`updated_at`</li></ul>Consulte o manual sobre [filtragem de respostas](../guides/filtering.md) para obter mais informações.

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737/hosts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de hosts para a propriedade especificada.

```json
{
  "data": [
    {
      "id": "HT405b8d9306004eb38106e66c8a4afc09",
      "type": "hosts",
      "attributes": {
        "created_at": "2020-12-14T17:42:35.239Z",
        "server": null,
        "name": "Example Akamai Host",
        "path": null,
        "port": null,
        "status": "succeeded",
        "type_of": "akamai",
        "updated_at": "2020-12-14T17:42:35.239Z",
        "username": null
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/hosts/HT405b8d9306004eb38106e66c8a4afc09/property"
          },
          "data": {
            "id": "PRd428c2a25caa4b32af61495f5809b737",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737",
        "self": "https://reactor.adobe.io/hosts/HT405b8d9306004eb38106e66c8a4afc09"
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

## Pesquisar um host {#lookup}

Você pode pesquisar um host fornecendo sua ID no caminho de uma solicitação GET.

**Formato da API**

```http
GET /hosts/{HOST_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `HOST_ID` | O `id` do host que você deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do host.

```json
{
  "data": {
    "id": "HT5d90148e72224224aac9bc0b01498b84",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:25.353Z",
      "server": "https://server.example.com",
      "name": "Example Akamai Host",
      "path": "/akamai",
      "port": 8000,
      "status": "succeeded",
      "type_of": "akamai",
      "updated_at": "2020-12-14T17:42:25.353Z",
      "username": null
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84/property"
        },
        "data": {
          "id": "PRd7cf174259f34057b5c435ef873a79bf",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRd7cf174259f34057b5c435ef873a79bf",
      "self": "https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84"
    }
  }
}
```

## Criar um host {#create}

Você pode criar um novo host fazendo uma solicitação POST.

**Formato da API**

```http
POST /properties/{PROPERTY_ID}/hosts
```

| Parâmetro | Descrição |
| --- | --- |
| `PROPERTY_ID` | O `id` da [propriedade](./properties.md) em que você está definindo o host. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir cria um novo host para a propriedade especificada. A chamada também associa o host a uma extensão existente por meio da propriedade `relationships`. Consulte o manual sobre [relações](../guides/relationships.md) para obter mais informações.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/hosts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Example SFTP Host",
            "type_of": "sftp",
            "username": "John Doe",
            "encrypted_private_key": "{PRIVATE_KEY}",
            "server": "https://example.com",
            "path": "assets",
            "port": 22
          },
          "type": "hosts"
        }
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `attributes.name` | **(Obrigatório)** Um nome legível para o host. |
| `attributes.type_of` | **(Obrigatório)** O tipo de host. Pode ser uma destas duas opções: <ul><li>`akamai` para [hosts gerenciados pela Adobe](../../ui/publishing/hosts/managed-by-adobe-host.md)</li><li>`sftp` para [hosts SFTP](../../ui/publishing/hosts/sftp-host.md)</li></ul> |
| `attributes.encrypted_private_key` | Uma chave privada opcional que será usada para autenticação de host. |
| `attributes.path` | O caminho a ser anexado ao URL `server`. |
| `attributes.port` | Um número inteiro que indica a porta específica do servidor que será usada. |
| `attributes.server` | O URL do host do servidor. |
| `attributes.username` | Um nome de usuário opcional para autenticação. |
| `type` | O tipo de recurso que está sendo atualizado. Para esse endpoint, o valor deve ser `hosts`. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do host recém-criado.

```json
{
  "data": {
    "id": "HT69bfe634dead4a9a8c659f5d4d94cecd",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:07.033Z",
      "server": "//example.com",
      "name": "Example SFTP Host",
      "path": "assets",
      "port": 22,
      "status": "pending",
      "type_of": "sftp",
      "updated_at": "2020-12-14T17:42:07.033Z",
      "username": "John Doe"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HT69bfe634dead4a9a8c659f5d4d94cecd/property"
        },
        "data": {
          "id": "PRb25a704c0b7c4562835ccdf96d3afd31",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31",
      "self": "https://reactor.adobe.io/hosts/HT69bfe634dead4a9a8c659f5d4d94cecd"
    }
  }
}
```

## Atualizar um host {#update}

>[!NOTE]
>
>Somente hosts SFTP podem ser atualizados.

Você pode atualizar um host incluindo a ID dele no caminho de uma solicitação PATCH.

**Formato da API**

```http
PATCH /hosts/{HOST_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `HOST_ID` | O `id` do host que você deseja atualizar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir atualiza o `name` para um host existente.

```shell
curl -X PATCH \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "New host Name"
          },
          "id": "HT5d90148e72224224aac9bc0b01498b84",
          "type": "hosts"
        }
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `attributes` | Um objeto cujas propriedades representam os atributos que serão atualizados para o host. Os seguintes atributos podem ser atualizados para um host: <ul><li>`encrypted_private_key`</li><li>`name`</li><li>`path`</li><li>`port`</li><li>`server`</li><li>`type_of`</li><li>`username`</li></ul> |
| `id` | O `id` do host que você deseja atualizar. Ele deve corresponder ao valor `{HOST_ID}` fornecido no caminho da solicitação. |
| `type` | O tipo de recurso que está sendo atualizado. Para esse endpoint, o valor deve ser `hosts`. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do host atualizado.

```json
{
  "data": {
    "id": "HTb14e136a6fe147459b298a4645d2a6f5",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:45.087Z",
      "server": null,
      "name": "My SFTP host",
      "path": null,
      "port": null,
      "status": "succeeded",
      "type_of": "sftp",
      "updated_at": "2020-12-14T17:42:45.696Z",
      "username": null
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HTb14e136a6fe147459b298a4645d2a6f5/property"
        },
        "data": {
          "id": "PR8f240526f7b54a4dbd46965e79519fde",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR8f240526f7b54a4dbd46965e79519fde",
      "self": "https://reactor.adobe.io/hosts/HTb14e136a6fe147459b298a4645d2a6f5"
    }
  }
}
```

## Excluir um host

Você pode excluir um host incluindo sua ID no caminho de uma solicitação DELETE.

**Formato da API**

```http
DELETE /hosts/{HOST_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `HOST_ID` | O `id` do host que você deseja excluir. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X DELETE \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) sem corpo de resposta, indicando que o host foi excluído.

## Recuperar recursos relacionados de um host {#related}

As chamadas a seguir demonstram como recuperar os recursos relacionados de um host. Quando você [procura um host](#lookup), essas relações são listadas na propriedade `relationships`.

Consulte o [manual de relações](../guides/relationships.md) para obter mais informações sobre relacionamentos na API do Reactor.

### Pesquisar a propriedade relacionada de um host {#property}

Para pesquisar a propriedade que possui um host, anexe `/property` ao caminho de uma solicitação de pesquisa.

**Formato da API**

```http
GET /hosts/{HOST_ID}/property
```

| Parâmetro | Descrição |
| --- | --- |
| `{HOST_ID}` | O `id` do host cuja propriedade você deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da propriedade do host especificado.

```json
{
  "data": {
    "id": "PRbdfaffb7bf374b87be50e672f0cf9309",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:52:05.900Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:52:05.900Z",
      "platform": "web",
      "development": false,
      "token": "47d65c7c98db",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/data_elements",
      "environments": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/environments",
      "extensions": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/extensions",
      "rules": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/rules",
      "self": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309"
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
