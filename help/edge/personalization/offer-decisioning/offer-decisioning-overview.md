---
title: Usar o Offer Decisioning com o SDK da Web da plataforma
description: O SDK da Web da Adobe Experience Platform pode fornecer e renderizar ofertas personalizadas gerenciadas no Offer Decisioning. É possível criar suas ofertas e outros objetos relacionados usando a interface do usuário do Offer Decisioning ou a API.
keywords: offer decisioning, decisão, Web SDK, Platform Web SDK, ofertas personalizadas, delivery de ofertas, delivery de ofertas, personalização de ofertas;
exl-id: 4ab51f9d-3c44-4855-b900-aa2cde673a9a
translation-type: tm+mt
source-git-commit: 2113eb265020b1d1c2e73dba95554c8bf97acf13
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 9%

---

# Usar o Offer Decisioning com o SDK da Web da plataforma

>[!NOTE]
>
>O uso do Offer Decisioning no Adobe Experience Platform Web SDK está disponível no momento com acesso antecipado a usuários selecionados. Essa funcionalidade não está disponível para todas as organizações IMS.

O Adobe Experience Platform [!DNL Web SDK] pode fornecer e renderizar ofertas personalizadas que são gerenciadas no Offer Decisioning. É possível criar suas ofertas e outros objetos relacionados usando a interface do usuário (UI) ou as APIs do Offer Decisioning.

## Pré-requisitos

* A organização IMS está habilitada para a decisão de borda
* Ofertas, atividades criadas
* A configuração de borda foi publicada

## Terminologia

É importante entender a seguinte terminologia ao trabalhar com o Offer Decisioning. Para obter mais informações e exibir termos adicionais, visite o glossário de Offers decisioning [e](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html).

* **Contêiner:** um contêiner é um mecanismo de isolamento para manter diferentes preocupações separadas. A ID do contêiner é o primeiro elemento de caminho para todas as APIs do repositório. Todos os objetos de decisão residem em um contêiner.

* **Escopos de decisão:** no Offer Decisioning, essas são as strings codificadas em Base64 do JSON que contêm as IDs de atividade e disposição que você deseja que o serviço offer decisioning use para propor ofertas.

   *Âmbito de decisão JSON:*

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
   >Você pode copiar o valor do escopo de decisão da página **Visão geral da atividade** na interface do usuário.

   ![](assets/decision-scope-copy.png)

* **Configuração de borda:** para obter mais informações, leia a documentação  [de ](../../fundamentals/edge-configuration.md) configuração de borda.

* **Identidade**: Para obter mais informações, leia esta documentação descrevendo como o  [Platform Web SDK usa o Serviço de identidade](../../identity/overview.md).

## Ativar o Offer Decisioning

Para ativar o Offer Decisioning, é necessário executar as seguintes etapas:

1. Ativação do Adobe Experience Platform em sua [configuração de borda](../../fundamentals/edge-configuration.md) e marque a caixa &quot;Offer decisioning&quot;
   ![offer-decisioning-edge-config](./assets/offer-decisioning-edge-config.png)
2. Siga as instruções para [instalar o SDK](../../fundamentals/installing-the-sdk.md) (O SDK pode ser instalado independentemente ou por meio de [Adobe Experience Platform Launch](http://launch.adobe.com/br). Este é um [guia de início rápido para Platform launch](https://docs.adobe.com/content/help/pt-BR/launch/using/intro/get-started/quick-start.html)).
3. [Configure o ](../../fundamentals/configuring-the-sdk.md) SDK para Offer Decisioning. Etapas adicionais específicas do Offer decisioning são fornecidas abaixo.
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

   * SDK instalado do Platform launch
      1. [Criar uma propriedade de Platform launch](https://docs.adobe.com/content/help/pt-BR/launch/using/reference/admin/companies-and-properties.html)
      2. [Adicionar o código incorporado do Platform launch](https://docs.adobe.com/content/help/en/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html)
      3. Instale e configure a extensão SDK da Web da plataforma com a Configuração de borda que você acabou de criar, selecionando a configuração no menu suspenso &quot;Configuração de borda&quot;. Documentação útil sobre [extensões](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html).
         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)
      4. Crie os [Elementos de Dados](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/data-elements.html) necessários. No mínimo, você precisará criar um Mapa de identidade do SDK da Web da plataforma e um elemento de dados do Objeto XDM do SDK da Web da plataforma.
         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)
      5. Crie suas [Regras](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/rules.html).
         * Adicione uma ação Platform Web SDK Send Event e adicione o `decisionScopes` relevante à configuração dessa ação
            ![send-event-action-decisionScopes](./assets/send-event-action-decisionScopes.png)
      6. [Crie e publique uma ](https://docs.adobe.com/content/help/pt-BR/launch/using/reference/publish/libraries.html) biblioteca contendo todas as regras, elementos de dados e extensões relevantes que você configurou



## Solicitações e respostas de exemplo

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
| `identityMap` | Sim | Consulte esta [documentação do Serviço de identidade](../../identity/overview.md). | Uma identidade por solicitação. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
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
| `activity.id` | A ID exclusiva da atividade de oferta. | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | A ID exclusiva da disposição da oferta. | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | A ID da oferta proposta. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | O schema do conteúdo associado à oferta proposta. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | A ID da oferta proposta. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | O formato do conteúdo associado à oferta proposta. | `"format": "text/html"` |
| `language` | Uma matriz de idiomas associados ao conteúdo da oferta proposta. | `"language": [ "en-US" ]` |
| `content` | Conteúdo associado à oferta proposta no formato de uma string. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Conteúdo da imagem associada à oferta proposta no formato de um URL. | `"deliveryURL": "https://image.jpeg"` |
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
| `identityMap` | Sim | Consulte esta [documentação do Serviço de identidade](../../identity/overview.md). | Uma identidade por solicitação. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
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
| `activity.id` | A ID exclusiva da atividade de oferta. | `"id": "xcore:offer-activity:11cfb1fa93381123"` |
| `placement.id` | A ID exclusiva da disposição da oferta. | `"xcore:offer-placement:1175009612b01123"` |
| `items.id` | A ID da oferta proposta. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `schema` | O schema do conteúdo associado à oferta proposta. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-text"` |
| `data.id` | A ID da oferta proposta. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `format` | O formato do conteúdo associado à oferta proposta. | `"format": "text/text"` |
| `language` | Uma matriz de idiomas associados ao conteúdo da oferta proposta. | `"language": [ "en-US" ]` |
| `content` | Conteúdo associado à oferta proposta no formato de uma string. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Conteúdo da imagem associada à oferta proposta no formato de um URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Características associadas à oferta proposta no formato de um objeto JSON. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |
