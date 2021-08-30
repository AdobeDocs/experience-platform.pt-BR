---
title: Endpoint de retornos de chamada
description: Saiba como fazer chamadas para o endpoint /callbacks na API do Reactor.
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 99%

---

# Endpoint de retornos de chamada

Um retorno de chamada é uma mensagem que a API do Reactor envia a uma URL específica (geralmente, uma que é hospedada por sua organização).

Os retornos de chamada devem ser usados juntamente com [eventos de auditoria](./audit-events.md) para rastrear atividades na API do Reactor. Sempre que um evento de auditoria de determinado tipo é gerado, um retorno de chamada pode enviar uma mensagem correspondente à URL especificada.

O serviço por trás da URL especificada no retorno de chamada deve responder com o código de status HTTP 200 (OK) ou 201 (Criado). Se o serviço não responder com nenhum desses códigos de status, o envio da mensagem será repetido nos seguintes intervalos:

* 1 minuto
* 5 minutos
* 30 minutos
* 1 hora
* 12 horas
* 1 dia
* 3 dias

>[!NOTE]
>
>Os intervalos de repetição são relativos ao intervalo anterior. Por exemplo, se a repetição em um minuto falhar, a próxima tentativa será agendada para cinco minutos após a tentativa de um minuto que falhou (seis minutos após a mensagem ter sido gerada).

Se todas as tentativas de envio falharem, a mensagem será descartada.

Um retorno de chamada pertence a apenas uma [propriedade](./properties.md). Uma propriedade pode ter muitos retornos de chamada.

## Introdução

O endpoint usado neste manual faz parte da [API do Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Antes de continuar, consulte novamente o [guia de introdução](../getting-started.md) para obter informações importantes sobre como realizar a autenticação para a API.

## Listar retornos de chamada {#list}

Você pode listar todos os retornos de chamada em uma propriedade fazendo uma solicitação GET.

**Formato da API**

```http
GET  /properties/{PROPERTY_ID}/callbacks
```

| Parâmetro | Descrição |
| --- | --- |
| `{PROPERTY_ID}` | O `id` da propriedade cujos retornos de chamada você deseja listar. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Usando parâmetros de consulta, os retornos de chamada listados podem ser filtrados com base nos seguintes atributos:<ul><li>`created_at`</li><li>`updated_at`</li></ul>Consulte o manual sobre [filtragem de respostas](../guides/filtering.md) para obter mais informações.

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de retornos de chamada da propriedade especificada.

```json
{
  "data": [
    {
      "id": "CB26edef8d709243579589107bcda034da",
      "type": "callbacks",
      "attributes": {
        "created_at": "2020-12-14T17:34:47.082Z",
        "subscriptions": [
          "rule.created"
        ],
        "updated_at": "2020-12-14T17:34:47.082Z",
        "url": "https://www.example.com"
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da/property"
          },
          "data": {
            "id": "PR66a3356c73fc4aabb67ee22caae53d70",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70",
        "self": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da"
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

## Pesquisar um retorno de chamada {#lookup}

Você pode pesquisar um retorno de chamada fornecendo a respectiva ID no caminho de uma solicitação GET.

**Formato de API**

```http
GET /callbacks/{CALLBACK_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `CALLBACK_ID` | O `id` do retorno de chamada que você deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do retorno de chamada.

```json
{
  "data": {
    "id": "CBeef389cee8d84e69acef8665e4dcbef6",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:36.872Z",
      "subscriptions": [
        "rule.created"
      ],
      "updated_at": "2020-12-14T17:34:36.872Z",
      "url": "https://www.example.com"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6/property"
        },
        "data": {
          "id": "PRb513bbab52114573ac87f9848eea6ead",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRb513bbab52114573ac87f9848eea6ead",
      "self": "https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6"
    }
  }
}
```

## Criar um retorno de chamada {#create}

Você pode criar um novo retorno de chamada fazendo uma solicitação POST.

**Formato da API**

```http
POST /properties/{PROPERTY_ID}/callbacks
```

| Parâmetro | Descrição |
| --- | --- |
| `PROPERTY_ID` | O `id` da [propriedade](./properties.md) sob a qual o retorno de chamada está sendo definido. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR5e22de986a7c4070965e7546b2bb108d/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "url": "https://www.example.com",
            "subscriptions": [
              "rule.created"
            ]
          }
        }
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `url` | O destino da URL para a mensagem de retorno de chamada. A URL deve usar a extensão de protocolo HTTPS. |
| `subscriptions` | Uma matriz de strings, indicando os tipos de evento de auditoria que acionarão o retorno de chamada. Consulte o [manual de endpoint de eventos de auditoria](./audit-events.md) para obter uma lista de tipos de eventos possíveis. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do retorno de chamada recém-criado.

```json
{
  "data": {
    "id": "CB32d8f23d5ee548278d32076af4c442a0",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:27.059Z",
      "subscriptions": [
        "rule.created"
      ],
      "updated_at": "2020-12-14T17:34:27.059Z",
      "url": "https://www.example.com"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CB32d8f23d5ee548278d32076af4c442a0/property"
        },
        "data": {
          "id": "PR5e22de986a7c4070965e7546b2bb108d",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR5e22de986a7c4070965e7546b2bb108d",
      "self": "https://reactor.adobe.io/callbacks/CB32d8f23d5ee548278d32076af4c442a0"
    }
  }
}
```

## Atualizar um retorno de chamada

É possível atualizar um retorno de chamada incluindo a respectiva ID no caminho de uma solicitação PUT.

**Formato da API**

```http
PUT /callbacks/{CALLBACK_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `CALLBACK_ID` | A `id` do retorno de chamada que você deseja atualizar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir atualiza a matriz `subscriptions` para um retorno de chamada existente.

```shell
curl -X PUT \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "subscriptions": [
              "rule.created",
              "build.created"
            ]
          },
          "type": "callbacks",
          "id": "CB4310904d415549888cc9e31ebe1e1e45"
        }
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `attributes` | Um objeto cujas propriedades representam os atributos a serem atualizados para o retorno de chamada. Cada chave representa o atributo de retorno de chamada específico a ser atualizado, juntamente com o valor correspondente para o qual ele deve ser atualizado.<br><br>Os seguintes atributos podem ser atualizados para retornos de chamada:<ul><li>`subscriptions`</li><li>`url`</li></ul> |
| `id` | A `id` do retorno de chamada que você deseja atualizar. Isso deve corresponder ao valor `{CALLBACK_ID}` informado no caminho da solicitação. |
| `type` | O tipo de recurso que está sendo atualizado. Para esse endpoint, o valor deve ser `callbacks`. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do retorno de chamada atualizado.

```json
{
  "data": {
    "id": "CB4310904d415549888cc9e31ebe1e1e45",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:56.884Z",
      "subscriptions": [
        "rule.created",
        "build.created"
      ],
      "updated_at": "2020-12-14T17:34:57.614Z",
      "url": "https://www.example.net"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45/property"
        },
        "data": {
          "id": "PR0a8ef3ca31dc456a8566e9288960bd79",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR0a8ef3ca31dc456a8566e9288960bd79",
      "self": "https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45"
    }
  }
}
```

## Excluir um retorno de chamada

É possível excluir um retorno de chamada incluindo a respectiva ID no caminho de uma solicitação DELETE.

**Formato da API**

```http
DELETE /callbacks/{CALLBACK_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `CALLBACK_ID` | A `id` do retorno de chamada que você deseja excluir. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X DELETE \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) sem corpo de resposta, indicando que o retorno de chamada foi excluído.
