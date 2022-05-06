---
title: Endpoint de notas
description: Saiba como fazer chamadas ao endpoint /notes na API do Reactor.
exl-id: fa3bebc0-215e-4515-87b9-d195c9ab76c1
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 98%

---

# Endpoint de notas

Na API do Reactor, as notas são anotações textuais que podem ser adicionadas a determinados recursos. Basicamente, as notas são comentários sobre os respectivos recursos. O conteúdo das notas não tem impacto sobre o comportamento dos recursos e pode ser usados para diversos casos de uso, inclusive os seguintes:

* Fornecer informações de referência
* Funcionar como listas de tarefas
* Repassar conselhos sobre o uso de recursos
* Dar instruções a outros membros da equipe
* Registrar contexto histórico

O endpoint `/notes` na API do Reactor permite gerenciar essas notas de forma programática.

As notas podem ser aplicadas aos seguintes recursos:

* [Elementos de dados](./data-elements.md)
* [Extensões](./extensions.md)
* [Bibliotecas](./libraries.md)
* [Propriedades](./properties.md)
* [Componentes da regra](./rule-components.md)
* [Regras](./rules.md)
* [Segredos](./secrets.md)

Esses seis tipos são coletivamente conhecidos como recursos “anotáveis”. Quando um recurso anotável é excluído, as notas associadas a ele também são excluídas.

>[!NOTE]
>
>Para recursos que podem ter várias revisões, quaisquer notas devem ser criadas na revisão atual (head). Elas não podem ser anexadas a outras revisões.
>
>No entanto, as notas ainda podem ser lidas nas revisões. Nesses casos, a API retorna apenas as notas existentes antes da criação da revisão. É fornecida uma captura de tela que mostra a aparência das anotações antes de a revisão ser removida. Por outro lado, a leitura de notas na revisão atual (head) retorna todas as notas.

## Introdução

O endpoint usado neste manual faz parte da [API do Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Antes de continuar, consulte novamente o [guia de introdução](../getting-started.md) para obter informações importantes sobre como realizar a autenticação para a API.

## Recuperar uma lista de notas {#list}

Você pode recuperar uma lista de notas para um recurso acrescentando `/notes` ao caminho de uma solicitação GET para o recurso em questão.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
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

## Pesquisar uma nota {#lookup}

É possível pesquisar uma nota fornecendo a respectiva ID no caminho de uma solicitação GET.

**Formato da API**

```http
GET /notes/{NOTE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `NOTE_ID` | O `id` da nota que você deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
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
>Antes de criar uma nova nota, lembre-se de que elas não são editáveis e a única maneira de excluí-las é excluir o recurso correspondente.

Você pode criar uma nova nota acrescentando `/notes` ao caminho de uma solicitação POST para o recurso em questão.

**Formato da API**

```http
POST /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| Parâmetro | Descrição |
| --- | --- |
| `RESOURCE_TYPE` | O tipo de recurso para o qual você está criando uma nota. Deve ser um dos seguintes valores: <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | A `id` do recurso específico para o qual você deseja criar uma nota. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir cria uma nova nota para uma propriedade.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `type` | **(Obrigatório)** O tipo de recurso que está sendo atualizado. Para esse endpoint, o valor deve ser `notes`. |
| `attributes.text` | **(Obrigatório)** O texto que compõe a nota. Cada nota é limitada a 512 caracteres Unicode. |

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
