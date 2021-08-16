---
title: Ponto de extremidade de retornos de chamada
description: Saiba como fazer chamadas para o endpoint /callbacks na API do Reator.
source-git-commit: 59592154eeb8592fa171b5488ecb0385e0e59f39
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 8%

---

# Ponto de extremidade de retornos de chamada

Um retorno de chamada é uma mensagem que a API de reator envia para um URL específico (geralmente um que é hospedado por sua organização).

Os retornos de chamada devem ser usados junto com [eventos de auditoria](./audit-events.md) para rastrear atividades na API do reator. Cada vez que um evento de auditoria de um determinado tipo é gerado, um retorno de chamada pode enviar uma mensagem correspondente ao URL especificado.

O serviço por trás do URL especificado no retorno de chamada deve responder com o código de status HTTP 200 (OK) ou 201 (Created). Se o serviço não responder com nenhum desses códigos de status, o delivery da mensagem será repetido nos seguintes intervalos:

* 1 minuto
* 5 minutos
* 30 minutos
* 1 hora
* 12 horas
* 1 dia
* 3 dias

>[!NOTE]
>
>Os intervalos de repetição são relativos ao intervalo anterior. Por exemplo, se a tentativa de um minuto falhar, a próxima tentativa será agendada por cinco minutos após a falha da tentativa de um minuto (seis minutos após a mensagem ter sido gerada).

Se todas as tentativas de delivery não forem bem-sucedidas, a mensagem será descartada.

Um retorno de chamada pertence a exatamente um [propriedade](./properties.md). Uma propriedade pode ter muitos retornos de chamada.

## Introdução

O endpoint usado neste guia faz parte da [API do reator](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Antes de continuar, reveja o [guia de introdução](../getting-started.md) para obter informações importantes sobre como autenticar para a API.

## Listar retornos de chamada {#list}

Você pode listar todos os retornos de chamada em uma propriedade, fazendo uma solicitação do GET.

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
>Usando parâmetros de consulta, retornos de chamada listados podem ser filtrados com base nos seguintes atributos:<ul><li>`created_at`</li><li>`updated_at`</li></ul>Consulte o guia sobre [respostas de filtragem](../guides/filtering.md) para obter mais informações.

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

Uma resposta bem-sucedida retorna uma lista de retornos de chamada para a propriedade especificada.

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

Você pode pesquisar um retorno de chamada fornecendo sua ID no caminho de uma solicitação do GET.

**Formato da API**

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

Uma resposta bem-sucedida retorna os detalhes da chamada de retorno.

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

Você pode criar um novo retorno de chamada fazendo uma solicitação de POST.

**Formato da API**

```http
POST /properties/{PROPERTY_ID}/callbacks
```

| Parâmetro | Descrição |
| --- | --- |
| `PROPERTY_ID` | O `id` do [propriedade](./properties.md) em que você está definindo o retorno de chamada. |

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
| `url` | O destino do URL da mensagem de retorno de chamada. O URL deve usar a extensão de protocolo HTTPS. |
| `subscriptions` | Uma matriz de sequências de caracteres, indicando os tipos de evento de auditoria que acionarão a chamada de retorno. Consulte o [guia de ponto de extremidade de eventos de auditoria](./audit-events.md) para obter uma lista de tipos de eventos possíveis. |

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

Você pode atualizar um retorno de chamada ao incluir sua ID no caminho de uma solicitação do PUT.

**Formato da API**

```http
PUT /callbacks/{CALLBACK_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `CALLBACK_ID` | O `id` do retorno de chamada que você deseja atualizar. |

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
| `attributes` | Um objeto cujas propriedades representam os atributos a serem atualizados para o retorno de chamada. Cada chave representa o atributo de retorno de chamada específico a ser atualizado, juntamente com o valor correspondente ao qual deve ser atualizado.<br><br>Os atributos a seguir podem ser atualizados para retornos de chamada:<ul><li>`subscriptions`</li><li>`url`</li></ul> |
| `id` | O `id` do retorno de chamada que você deseja atualizar. Isso deve corresponder ao valor `{CALLBACK_ID}` fornecido no caminho da solicitação. |
| `type` | O tipo de recurso que está sendo atualizado. Para esse ponto de extremidade, o valor deve ser `callbacks`. |

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

Você pode excluir um retorno de chamada ao incluir sua ID no caminho de uma solicitação do DELETE.

**Formato da API**

```http
DELETE /callbacks/{CALLBACK_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `CALLBACK_ID` | O `id` do retorno de chamada que você deseja excluir. |

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

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) sem nenhum corpo de resposta, indicando que o retorno de chamada foi excluído.
