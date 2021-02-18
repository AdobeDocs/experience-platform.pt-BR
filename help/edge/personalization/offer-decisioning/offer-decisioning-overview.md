---
title: Usar o Offer Decisioning com o SDK da Web da plataforma
description: O Adobe Experience Platform Web SDK pode fornecer e renderizar ofertas personalizadas gerenciadas no Offer Decisioning. Você pode criar suas ofertas e outros objetos relacionados usando a interface do usuário ou a API do Offer Decisioning.
keywords: decisão de oferta;decisão;Web SDK;Plataforma Web SDK;ofertas personalizadas;fornecer ofertas;delivery de oferta;personalização de oferta;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 9%

---


# Usar o Offer Decisioning com o SDK da Web da plataforma

>[!NOTE]
>
>O uso do Offer Decisioning no Adobe Experience Platform Web SDK está disponível no momento no acesso antecipado para usuários selecionados. Esta funcionalidade não está disponível para todas as organizações IMS.

A Adobe Experience Platform [!DNL Web SDK] pode fornecer e renderizar ofertas personalizadas que são gerenciadas no Offer Decisioning. Você pode criar suas ofertas e outros objetos relacionados usando a interface do usuário (UI) ou as APIs do Offer Decisioning.

## Pré-requisitos

* A organização IMS está habilitada para decisão de borda
* Ofertas, Atividades criadas
* A configuração do Edge foi publicada

## Terminologia

É importante entender a seguinte terminologia ao trabalhar com a Offer Decisioning. Para obter mais informações e visualização de termos adicionais, visite o glossário [Offer Decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html).

* **Container:** Um container é um mecanismo de isolamento para manter diferentes preocupações separadas. A ID do container é o primeiro elemento de caminho para todas as APIs do repositório. Todos os objetos de decisão residem em um container.

* **Escopos de decisão:** para Offer Decisioning, essas são as strings codificadas em Base64 do JSON que contêm as IDs de atividade e posicionamento que você deseja que o serviço de decisão de oferta use para propor ofertas.

   *Âmbito de decisão JSON:*

   ```json
   {
     "activityId":"xcore:offer-activity:11cfb1fa93381aca",
     "placementId":"xcore:offer-placement:1175009612b0100c"
   }
   ```

   *Sequência codificada Base64 do escopo de decisão:*

   ```json
   "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
   ```

   >[!TIP]
   >
   >Você pode copiar o valor do escopo de decisão da página **Visão geral da Atividade** na interface do usuário.

   ![](assets/decision-scope-copy.png)

* **Configuração de borda:** Para obter mais informações, leia a documentação de  [ ](../../fundamentals/edge-configuration.md) configuração de borda.

* **Identidade**: Para obter mais informações, leia esta documentação descrevendo como o SDK da Web da  [plataforma aproveita o Serviço](../../identity/overview.md) de identidade.

## Ativação do Offer Decisioning

Para habilitar o Offer Decisioning, é necessário executar as seguintes etapas:

1. Habilitada a Adobe Experience Platform na [configuração de borda](../../fundamentals/edge-configuration.md) e marque a caixa &quot;Offer Decisioning&quot;
   ![oferta-decisão-borda-configuração](./assets/offer-decisioning-edge-config.png)
2. Siga as instruções para [instalar o SDK](../../fundamentals/installing-the-sdk.md) (O SDK pode ser instalado separadamente ou por meio de [Adobe Experience Platform Launch](http://launch.adobe.com/br). Este é um [guia de start rápido para o Platform Launch](https://docs.adobe.com/content/help/pt-BR/launch/using/intro/get-started/quick-start.html)).
3. [Configure o ](../../fundamentals/configuring-the-sdk.md) SDK para Offer Decisioning. Etapas adicionais específicas da Offer Decisioning são fornecidas abaixo.
   * SDK instalado independente
      1. Configure a ação &quot;sendEvent&quot; com seu `decisionScopes`

      ```javascript
      alloy("sendEvent", {
          ...
          "decisionScopes": [
              "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIwOWMxM2JkZDIyNCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMDZhODRkMDViMTEifQ==",
              "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIyNWI5NTUwNWIxZiIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMjFmOTQzMDE0MmIifQ=="
          ]
      })
      ```
   * SDK instalado do Launch da plataforma
      1. [Criar uma propriedade de lançamento de plataforma](https://docs.adobe.com/content/help/pt-BR/launch/using/reference/admin/companies-and-properties.html)
      2. [Adicione o código incorporado de inicialização da plataforma](https://docs.adobe.com/content/help/en/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html)
      3. Instale e configure a extensão AEP Web SDK com a Configuração de borda que você acabou de criar selecionando a configuração no menu suspenso &quot;Configuração de borda&quot;. Documentação útil sobre [extensões](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html).
         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)
      4. Crie os [Elementos de dados](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/data-elements.html) necessários. No mínimo, você precisará criar um Mapa de identidade do SDK da Web da plataforma e um elemento de dados do Objeto XDM do SDK da Web da plataforma.
         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)
      5. Crie [Regras](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/rules.html).
         * Adicione uma ação Enviar Evento do SDK da Web da plataforma e adicione o `decisionScopes` relevante à configuração dessa ação
            ![send-evento-action-decisionsScopes](./assets/send-event-action-decisionScopes.png)
      6. [Crie e publique uma ](https://docs.adobe.com/content/help/pt-BR/launch/using/reference/publish/libraries.html) biblioteca contendo todas as Regras, Elementos de dados e Extensões relevantes configuradas por você


## Amostra de solicitações e respostas

### Um valor `decisionScopes`

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
| `identityMap` | Sim | Consulte esta [documentação do Serviço de Identidade](../../identity/overview.md). | Uma identidade por solicitação. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | Sim | Uma matriz de strings codificadas em Base64 do JSON que contém as IDs de atividade e posicionamento. | Máximo de 30 `decisionScopes` por solicitação. | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

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
| `scope` | O âmbito de decisão que resultou nas ofertas propostas. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | A ID exclusiva da atividade da oferta. | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | A ID exclusiva da disposição da oferta. | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | A ID da oferta proposta. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | O schema do conteúdo associado à oferta proposta. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | A ID da oferta proposta. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | O formato do conteúdo associado à oferta proposta. | `"format": "text/html"` |
| `language` | Uma matriz de idiomas associados ao conteúdo da oferta proposta. | `"language": [ "en-US" ]` |
| `content` | Conteúdo associado à oferta proposta no formato de uma string. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Conteúdo de imagem associado à oferta proposta no formato de um URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Características associadas à oferta proposta no formato de um objeto JSON. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

### Vários valores `decisionScopes`

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
| `identityMap` | Sim | Consulte esta [documentação do Serviço de Identidade](../../identity/overview.md). | Uma identidade por solicitação. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | Sim | Uma matriz de strings codificadas em Base64 do JSON que contém as IDs de atividade e posicionamento. | Máximo de 30 `decisionScopes` por solicitação. | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

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
| `scope` | O âmbito de decisão que resultou nas ofertas propostas. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | A ID exclusiva da atividade da oferta. | `"id": "xcore:offer-activity:11cfb1fa93381123"` |
| `placement.id` | A ID exclusiva da disposição da oferta. | `"xcore:offer-placement:1175009612b01123"` |
| `items.id` | A ID da oferta proposta. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `schema` | O schema do conteúdo associado à oferta proposta. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-text"` |
| `data.id` | A ID da oferta proposta. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `format` | O formato do conteúdo associado à oferta proposta. | `"format": "text/text"` |
| `language` | Uma matriz de idiomas associados ao conteúdo da oferta proposta. | `"language": [ "en-US" ]` |
| `content` | Conteúdo associado à oferta proposta no formato de uma string. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Conteúdo de imagem associado à oferta proposta no formato de um URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Características associadas à oferta proposta no formato de um objeto JSON. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |
