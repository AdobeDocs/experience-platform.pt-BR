---
title: Utilização do Offer Decisioning com o SDK da Web da plataforma
description: O SDK da Web da Adobe Experience Platform pode fornecer e renderizar ofertas personalizadas gerenciadas no Offer Decisioning. Você pode criar suas ofertas e outros objetos relacionados usando a interface do usuário ou a API do Offer Decisioning.
keywords: offer decisioning;decisão;SDK da Web;SDK da Web da plataforma;ofertas personalizadas;entregar ofertas;entrega de ofertas;personalização de ofertas;
exl-id: 4ab51f9d-3c44-4855-b900-aa2cde673a9a
source-git-commit: 5f2358c2e102c66a13746004ad73e2766e933705
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 5%

---

# Utilização do Offer Decisioning com o SDK da Web da plataforma

>[!NOTE]
>
>O uso do Offer Decisioning no SDK da Web da Adobe Experience Platform está disponível no acesso antecipado a usuários selecionados. Essa funcionalidade não está disponível para todas as organizações.

Adobe Experience Platform [!DNL Web SDK] O pode entregar e renderizar ofertas personalizadas que são gerenciadas no Offer Decisioning. É possível criar suas ofertas e outros objetos relacionados usando a interface ou as APIs do Offer Decisioning.

## Pré-requisitos

* A organização está habilitada para decisão de borda
* Ofertas, Atividades criadas
* A sequência de dados é publicada

## Terminologia

É importante entender a seguinte terminologia ao trabalhar com o Offer Decisioning. Para obter mais informações e visualizar os termos adicionais, visite o [glossário do Offer Decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html).

* **Contêiner:** Um container é um mecanismo de isolamento destinado a manter diferentes problemas separados. A ID do container é o primeiro elemento de caminho para todas as APIs do repositório. Todos os objetos de decisão residem em um container.

* **Escopos de decisão:** Para o Offer Decisioning, os escopos de decisão são as cadeias de caracteres codificadas na Base64 de JSON que contêm as IDs de atividade e posicionamento que você deseja que o serviço do offer decisioning use para propor ofertas.

  *Escopo de decisão JSON:*

  ```json
  {
    "activityId":"xcore:offer-activity:11cfb1fa93381aca",
    "placementId":"xcore:offer-placement:1175009612b0100c"
  }
  ```

  *Sequência de caracteres codificada Base64 do escopo de decisão:*

  ```json
  "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
  ```

  >[!TIP]
  >
  >Você pode copiar o valor do escopo de decisão do **Visão geral da atividade** na interface do usuário do.

  ![](assets/decision-scope-copy.png)

* **Sequências de dados:** Para obter mais informações, leia a [sequências de dados](../../../datastreams/overview.md) documentação.

* **Identidade**: para obter mais informações, leia esta documentação descrevendo como [O SDK da Web da Platform usa o Serviço de identidade](../../identity/overview.md).

## Ativar o Offer Decisioning

Para ativar o Offer Decisioning, execute as seguintes etapas:

1. Ativação do Adobe Experience Platform no [sequência de dados](../../../datastreams/overview.md) e marque a caixa &quot;Offer Decisioning&quot;

   ![offer-decisão-edge-config](./assets/offer-decisioning-edge-config.png)

1. Siga as instruções para [instalar o SDK](../../fundamentals/installing-the-sdk.md) (O SDK pode ser instalado de forma independente ou por meio da interface do usuário. Consulte a [guia de início rápido das tags](../../../tags/quick-start/quick-start.md)) para obter mais informações.
1. [Configurar o SDK](../../fundamentals/configuring-the-sdk.md) para Offer Decisioning. As etapas adicionais específicas para o Offer decisioning são fornecidas a seguir.

   * Instalar o SDK independente

      1. Configure a ação &quot;sendEvent&quot; com o `decisionScopes`

         ```javascript
          alloy("sendEvent", {
             ...
             "decisionScopes": [
                 "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIwOWMxM2JkZDIyNCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMDZhODRkMDViMTEifQ==",
                 "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIyNWI5NTUwNWIxZiIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMjFmOTQzMDE0MmIifQ=="
             ]
          })
         ```

   * Instalar o SDK por meio de tags

      1. [Criar uma propriedade de tag](../../../tags/ui/administration/companies-and-properties.md)
      1. [Adicionar o código incorporado do](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html)
      1. Instale e configure a extensão SDK da Web da Platform com a sequência de dados criada selecionando a configuração na lista suspensa &quot;Sequência de dados&quot;. Consulte a documentação em [extensões](../../../tags/ui/managing-resources/extensions/overview.md).

         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)

      1. Crie o necessário [Elementos de dados](../../../tags/ui/managing-resources/data-elements.md). No mínimo, você deve criar um Mapa de identidade do SDK da Web da plataforma e um elemento de dados do Objeto XDM do SDK da Web da plataforma.

         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)

      1. Crie seu [Regras](../../../tags/ui/managing-resources/rules.md).

         * Adicione uma ação Enviar evento do SDK da Web da plataforma e adicione as ações relevantes `decisionScopes` à configuração dessa ação

           ![send-event-action-decisionScopes](./assets/send-event-action-decisionScopes.png)

      1. [Criar e publicar uma biblioteca](../../../tags/ui/publishing/libraries.md) contendo todas as Regras, Elementos de dados e Extensões relevantes que você configurou

## Solicitações e respostas de exemplo

### Um `decisionScopes` value

**Solicitação**

```json
{
  "events": [
    {
      "xdm": {
        "identityMap": {
          "ECID": [
            {
              "id": "91133425615229052182584359620783097099"
            }
          ]
        }
      },
      "query": {
        "personalization": {
          "decisionScopes": [
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
          ]
        }
      }
    }
  ]
}
```

| Propriedade | Obrigatório | Descrição | Limites | Exemplo |
|---|---|---|---|---|
| `identityMap` | Sim | Consulte esta [Documentação do Serviço de identidade](../../identity/overview.md). | Uma identidade por solicitação. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`. <br><br> Observação: os usuários não precisam incluir a variável `ECID` na chamada de API. Esse parâmetro é adicionado automaticamente à chamada do, se necessário. |
| `decisionScopes` | Sim | Uma matriz de sequências de caracteres codificadas na Base64 de JSON que contém as IDs de atividade e posicionamento. | Máximo 30 `decisionScopes` por solicitação. | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

**Resposta**

```json
{
  "requestId": "94c4f2f1-9218-43ce-afd3-eb0d853c5174",
  "handle": [
    {
      "payload": [
        {
          "id": "2862bb89-5df2-4bc6-85c2-d8f7e1a091de",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381aca",
            "etag": "2"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b0100c",
            "etag": "1"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:124cc332095cfa74",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-html",
              "etag": "1",
              "data": {
                "id": "xcore:personalized-offer:124cc332095cfa74",
                "format": "text/html",
                "language": [
                  "en-US"
                ],
                "content": "<p>20% Off on shipping</p>",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

| Propriedade | Descrição | Exemplo |
|---|---|---|
| `scope` | O escopo de decisão que resultou nas ofertas propostas. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | O identificador exclusivo da atividade de oferta. | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | O identificador exclusivo do posicionamento da oferta. | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | A ID da oferta proposta. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | O schema do conteúdo associado à oferta proposta. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | A ID da oferta proposta. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | O formato do conteúdo associado à oferta proposta. | `"format": "text/html"` |
| `language` | Uma matriz de idiomas associados ao conteúdo da oferta proposta. | `"language": [ "en-US" ]` |
| `content` | Conteúdo associado à oferta proposta no formato de uma cadeia de caracteres. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Conteúdo de imagem associado à oferta proposta no formato de um URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Características associadas à oferta proposta no formato de um objeto JSON. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

### Múltiplo `decisionScopes` valores

**Solicitação**

```json
{
  "events": [
    {
      "xdm": {
        "identityMap": {
          "ECID": [
            {
              "id": "91133425615229052182584359620783097099"
            }
          ]
        }
      },
      "query": {
        "personalization": {
          "decisionScopes": [
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ==",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyYzkxMzg1Mjc2MDE4YyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMzMxZjU2MTYyYWEyZjcifQ=="
          ]
        }
      }
    }
  ]
}
```

| Propriedade | Obrigatório | Descrição | Limites | Exemplo |
|---|---|---|---|---|
| `identityMap` | Sim | Consulte esta [Documentação do Serviço de identidade](../../identity/overview.md). | Uma identidade por solicitação. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`. <br><br> Observação: os usuários não precisam incluir a variável `ECID` na chamada de API. Esse parâmetro é adicionado automaticamente à chamada do, se necessário. |
| `decisionScopes` | Sim | Uma matriz de sequências de caracteres codificadas na Base64 de JSON que contém as IDs de atividade e posicionamento. | Máximo 30 `decisionScopes` por solicitação. | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

**Resposta**

```json
{
  "requestId": "94c4f2f1-9218-43ce-afd3-eb0d853c5174",
  "handle": [
    {
      "payload": [
        {
          "id": "a2804dfb-a0ec-4df9-8311-59d3ecdeb642",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MTEyMyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDExMjMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381123",
            "etag": "1"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b01123",
            "etag": "3"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:11e36d4a22954123",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-text",
              "etag": "2",
              "data": {
                "id": "xcore:personalized-offer:11e36d4a22954123",
                "format": "text/text",
                "language": [
                  "en"
                ],
                "content": "20% Off on shipping",
                "characteristics": {
                  "foo2": "bar2"
                }
              }
            }
          ]
        },
        {
          "id": "a2804dfb-a0ec-4df9-8311-59d3ecdeb642",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381aca",
            "etag": "2"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b0100c",
            "etag": "1"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:11e36d4a2295415d",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
              "etag": "1",
              "data": {
                "id": "xcore:personalized-offer:11e36d4a2295415d",
                "format": "image/png",
                "language": [
                  "en"
                ],
                "deliveryURL": "https://image.jpeg",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

| Propriedade | Descrição | Exemplo |
|---|---|---|
| `scope` | O escopo de decisão que resultou nas ofertas propostas. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | O identificador exclusivo da atividade de oferta. | `"id": "xcore:offer-activity:11cfb1fa93381123"` |
| `placement.id` | O identificador exclusivo do posicionamento da oferta. | `"xcore:offer-placement:1175009612b01123"` |
| `items.id` | A ID da oferta proposta. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `schema` | O schema do conteúdo associado à oferta proposta. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-text"` |
| `data.id` | A ID da oferta proposta. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `format` | O formato do conteúdo associado à oferta proposta. | `"format": "text/text"` |
| `language` | Uma matriz de idiomas associados ao conteúdo da oferta proposta. | `"language": [ "en-US" ]` |
| `content` | Conteúdo associado à oferta proposta no formato de uma cadeia de caracteres. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Conteúdo de imagem associado à oferta proposta no formato de um URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Características associadas à oferta proposta no formato de um objeto JSON. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

## Limitações

No momento, algumas restrições de oferta não são compatíveis com os fluxos de trabalho móveis do Experience Edge, por exemplo, Limite. O valor do campo Limite especifica o número de vezes que uma oferta pode ser apresentada a todos os usuários. Para obter mais detalhes, consulte [Documentação de regras de elegibilidade e restrições da oferta](https://experienceleague.adobe.com/docs/offer-decisioning/using/managing-offers-in-the-offer-library/creating-personalized-offers.html#eligibility).
