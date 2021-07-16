---
title: Ponto de extremidade de notas
description: Saiba como fazer chamadas para o endpoint /notes na API do Reator.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 7%

---

# Ponto de extremidade de notas

Na API do reator, as notas são anotações textuais que podem ser adicionadas a determinados recursos. As notas são essencialmente comentários sobre os respectivos recursos. O conteúdo das notas não tem impacto no comportamento dos recursos e pode ser usado para uma variedade de casos de uso, incluindo o seguinte:

* Fornecimento de informações de fundo
* Funcionando como listas de itens
* Envio de conselhos de uso de recursos
* Dar instruções aos outros membros da equipe
* Registro do contexto histórico

O endpoint `/notes` na API do reator permite gerenciar essas notas de forma programática.

As observações podem ser aplicadas aos seguintes recursos:

* [Elementos de dados](./data-elements.md)
* [Extensões](./extensions.md)
* [Bibliotecas](./libraries.md)
* [Propriedades](./properties.md)
* [Componentes da regra](./rule-components.md)
* [Regras](./rules.md)

Esses seis tipos são coletivamente conhecidos como recursos &quot;notáveis&quot;. Quando um recurso notável é excluído, as notas associadas também são excluídas.

>[!NOTE]
>
>Para recursos que podem ter várias revisões, quaisquer notas devem ser criadas na revisão (head) atual. Não podem ser anexadas a outras revisões.
>
>Todavia, as notas podem ainda ser lidas com base em revisões. Nesses casos, a API retorna apenas as notas existentes antes da criação da revisão. Eles fornecem um instantâneo das anotações como eram quando a revisão foi recortada. Por outro lado, a leitura de notas da revisão (head) atual retorna todas as suas notas.

## Introdução

O endpoint usado neste guia faz parte da [API do reator](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Antes de continuar, reveja o [guia de introdução](../getting-started.md) para obter informações importantes sobre como autenticar para a API.

## Recuperar uma lista de notas {#list}

Você pode recuperar uma lista de observações para um recurso ao anexar `/notes` ao caminho de uma solicitação do GET para o recurso em questão.

**Formato da API**

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| Parâmetro | Descrição |
| --- | --- |
| `RESOURCE_TYPE` | O tipo de recurso para o qual você está buscando notas. Deve ser um dos seguintes valores: <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | O `id` do recurso específico cujas notas você deseja listar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir lista as notas anexadas a uma biblioteca.

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de notas anexadas ao recurso especificado.

```json
{
  "data": [
    {
      "id": "NTa40de8d76bfd4e40835830900ce83b7b",
      "type": "notes",
      "attributes": {
        "author_display_name": "John Smith",
        "author_email": "jsmith@example.com",
        "created_at": "2020-12-14T17:51:00.411Z",
        "text": "this is a note on a library"
      },
      "relationships": {
        "resource": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d"
          },
          "data": {
            "id": "LBcffea1a38c52408cae2398868625a12d",
            "type": "libraries"
          }
        }
      },
      "links": {
        "resource": "https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d",
        "self": "https://reactor.adobe.io/notes/NTa40de8d76bfd4e40835830900ce83b7b"
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

## Procurar uma nota {#lookup}

Você pode pesquisar uma nota fornecendo sua ID no caminho de uma solicitação do GET.

**Formato da API**

```http
GET /notes/{NOTE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `NOTE_ID` | O `id` da nota que pretende procurar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da nota.

```json
{
  "data": {
    "id": "NT550b7a17ab304d49ba289a2978d673e5",
    "type": "notes",
    "attributes": {
      "author_display_name": "John Smith",
      "author_email": "jsmith@example.com",
      "created_at": "2020-12-14T17:51:10.316Z",
      "text": "this is a note on a property"
    },
    "relationships": {
      "resource": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8"
        },
        "data": {
          "id": "PR4537ac6f1f204ffd864ec47c4b27c2e8",
          "type": "properties"
        }
      }
    },
    "links": {
      "resource": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8",
      "self": "https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5"
    }
  }
}
```

## Criar notas {#create}

>[!WARNING]
>
>Antes de criar uma nova nota, lembre-se de que as notas não são editáveis e que a única maneira de excluí-las é excluir o recurso correspondente.

Você pode criar uma nova nota ao anexar `/notes` ao caminho de uma solicitação POST para o recurso em questão.

**Formato da API**

```http
POST /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| Parâmetro | Descrição |
| --- | --- |
| `RESOURCE_TYPE` | O tipo de recurso para o qual você está criando uma nota. Deve ser um dos seguintes valores: <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | O `id` do recurso específico para o qual você deseja criar uma nota. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir cria uma nova nota para uma propriedade.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "type": "notes",
          "attributes": {
            "text": "this is a note on a property"
          }
        }
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `type` | **(Obrigatório)** O tipo de recurso que está sendo atualizado. Para esse ponto de extremidade, o valor deve ser `notes`. |
| `attributes.text` | **(Obrigatório)** O texto que compreende a nota. Cada nota é limitada a 512 caracteres Unicode. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da nota recém-criada.

```json
{
  "data": {
    "id": "NT550b7a17ab304d49ba289a2978d673e5",
    "type": "notes",
    "attributes": {
      "author_display_name": "John Smith",
      "author_email": "jsmith@example.com",
      "created_at": "2020-12-14T17:51:10.316Z",
      "text": "This is a note on a property"
    },
    "relationships": {
      "resource": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8"
        },
        "data": {
          "id": "PR4537ac6f1f204ffd864ec47c4b27c2e8",
          "type": "properties"
        }
      }
    },
    "links": {
      "resource": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8",
      "self": "https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5"
    }
  }
}
```
