---
title: Visão geral do Offer Decisioning
seo-title: Offer Decisioning e Adobe Experience Platform Web SDK
description: O Adobe Experience Platform Web SDK pode fornecer e renderizar ofertas personalizadas gerenciadas no Offer Decisioning. Você pode criar suas ofertas e outros objetos relacionados usando a interface do usuário ou a API do Offer Decisioning.
seo-description: O Adobe Experience Platform Web SDK pode fornecer e renderizar ofertas personalizadas gerenciadas no Offer Decisioning. Você pode criar suas ofertas e outros objetos relacionados usando a interface do usuário ou a API do Offer Decisioning.
keywords: offer decisioning;decisioning;Web SDK;Platform Web SDK;personalized offers;deliver offers;offer delivery;offer personalization;
translation-type: tm+mt
source-git-commit: a0ede8c7d3088fe80d6ea014b4a4f9f08ee8a7aa
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 9%

---


# [!DNL Offer Decisioning] Visão geral

>[!NOTE]
>
>O uso do Offer Decisioning no Adobe Experience Platform Web SDK está disponível no momento no acesso antecipado para usuários selecionados. Esta funcionalidade não está disponível para todas as organizações IMS.

A Adobe Experience Platform [!DNL Web SDK] pode fornecer e renderizar ofertas personalizadas que são gerenciadas no Offer Decisioning. Você pode criar suas ofertas e outros objetos relacionados usando a interface do usuário (UI) ou as APIs do Offer Decisioning.

## Pré-requisitos

* A organização IMS está habilitada para decisão de borda
* Ofertas, Atividades criadas
* A configuração do Edge foi publicada

## Terminologia

É importante entender a seguinte terminologia ao trabalhar com a Offer Decisioning. <!--For more information and to view additional terms, please visit the [Offer Decisioning glossary](/docs/offer-decisioning/using/get-started/glossary.html)-->.

* **Container:** Um container é um mecanismo de isolamento para manter diferentes preocupações separadas. A ID do container é o primeiro elemento de caminho para todas as APIs do repositório. Todos os objetos de decisão residem em um container.

* **Escopos de decisão:** Para Offer Decisioning, essas são as strings codificadas em Base64 do JSON que contêm as IDs de atividade e posicionamento que você deseja que o serviço de decisão de oferta use para propor ofertas.

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
   >Você pode copiar o valor do escopo de decisão da página Visão geral **da** Atividade na interface do usuário.

   ![](assets/decision-scope-copy.png)

* **Configuração do Edge:** Para obter mais informações, leia a documentação de configuração [da](../../fundamentals/edge-configuration.md) borda.

* **Identidade**: Para obter mais informações, leia esta documentação descrevendo como o SDK da Web da [plataforma aproveita o Serviço](../../identity/overview.md)de identidade.

## Ativação do Offer Decisioning

Para habilitar o Offer Decisioning, é necessário executar as seguintes etapas:

1. Habilitada a Adobe Experience Platform na configuração [da](../../fundamentals/edge-configuration.md) borda e marque a caixa &quot;Offer Decisioning&quot;
   ![oferta-decisão-borda-configuração](./assets/offer-decisioning-edge-config.png)
2. Siga as instruções para [instalar o SDK](../../fundamentals/installing-the-sdk.md) (o SDK pode ser instalado independentemente ou por meio do [Adobe Experience Platform Launch](http://launch.adobe.com/br). Este é um guia de start [rápido para o lançamento](https://docs.adobe.com/content/help/pt-BR/launch/using/intro/get-started/quick-start.html)da plataforma).
3. [Configure o SDK](../../fundamentals/configuring-the-sdk.md) para Offer Decisioning. Etapas adicionais específicas da Offer Decisioning são fornecidas abaixo.
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
      4. Crie os elementos [de dados](https://docs.adobe.com/content/help/pt-BR/launch/using/reference/manage-resources/data-elements.html)necessários. No mínimo, você precisará criar um Mapa de identidade do SDK da Web da plataforma e um elemento de dados do Objeto XDM do SDK da Web da plataforma.
         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)
      5. Crie suas [regras](https://docs.adobe.com/content/help/pt-BR/launch/using/reference/manage-resources/rules.html).
         * Adicione uma ação Enviar Evento do SDK da Web da plataforma e adicione a ação relevante `decisionScopes` à configuração dessa ação
            ![send-evento-action-decisionsScopes](./assets/send-event-action-decisionScopes.png)
      6. [Crie e publique uma biblioteca](https://docs.adobe.com/content/help/pt-BR/launch/using/reference/publish/libraries.html) contendo todas as Regras, Elementos de dados e Extensões relevantes configuradas por você


## Amostra de solicitações e respostas

### Um `decisionScopes` valor

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
| `identityMap` | Sim | Consulte esta documentação [do Serviço de](../../identity/overview.md)Identidade. | Uma identidade por solicitação. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
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
          "items": [
            {
              "id": "xcore:personalized-offer:124cc332095cfa74",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-html",
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
| `items.id` | A ID da oferta proposta. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | O schema do conteúdo associado à oferta proposta. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | A ID da oferta proposta. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | O formato do conteúdo associado à oferta proposta. | `"format": "text/html"` |
| `language` | Uma matriz de idiomas associados ao conteúdo da oferta proposta. | `"language": [ "en-US" ]` |
| `content` | Conteúdo associado à oferta proposta no formato de uma string. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Conteúdo de imagem associado à oferta proposta no formato de um URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Características associadas à oferta proposta no formato de um objeto JSON. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

### Vários `decisionScopes` valores

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
| `identityMap` | Sim | Consulte esta documentação [do Serviço de](../../identity/overview.md)Identidade. | Uma identidade por solicitação. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | Sim | Uma matriz de strings codificadas em Base64 do JSON que contém as IDs de atividade e posicionamento. | Máximo de 30 `decisionScopes` por solicitação. | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

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
          "items": [
            {
              "id": "xcore:personalized-offer:124cc332095cfa74",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-html",
              "data": {
                "id": "xcore:personalized-offer:124cc332095cfa74",
                "format": "text/html",
                "language": [
                  "en-US"
                ],
                "content": "<p style=\"color:red;\">20% Off on shipping</p>",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "payload": [
        {
          "id": "2862bb89-5df2-4bc6-85c2-d8f7e1a091de",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ==",
          "items": [
            {
              "id": "xcore:personalized-offer:235fe313094cdb75",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-text",
              "data": {
                "id": "xcore:personalized-offer:235fe313094cdb75",
                "format": "text/text",
                "language": [
                  "en-US"
                ],
                "content": "20% Off on shipping",
                "characteristics": {
                  "foo2": "bar2",
                  "foo3": "bar3"
                }
              }
            }
          ]
        }
      ],
      "payload": [
        {
          "id": "2862bb89-5df2-4bc6-85c2-d8f7e1a091de",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyYzkxMzg1Mjc2MDE4YyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMzMxZjU2MTYyYWEyZjcifQ==",
          "items": [
            {
              "id": "xcore:personalized-offer:312de312095cda65",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
              "data": {
                "id": "xcore:personalized-offer:312de312095cda65",
                "format": "image/png",
                "language": [
                  "en-US"
                ],
                "deliveryURL": "https://image.jpeg"
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
| `items.id` | A ID da oferta proposta. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | O schema do conteúdo associado à oferta proposta. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | A ID da oferta proposta. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | O formato do conteúdo associado à oferta proposta. | `"format": "text/html"` |
| `language` | Uma matriz de idiomas associados ao conteúdo da oferta proposta. | `"language": [ "en-US" ]` |
| `content` | Conteúdo associado à oferta proposta no formato de uma string. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Conteúdo de imagem associado à oferta proposta no formato de um URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Características associadas à oferta proposta no formato de um objeto JSON. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |
