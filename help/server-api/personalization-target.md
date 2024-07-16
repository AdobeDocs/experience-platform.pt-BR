---
title: Personalization via Adobe Target
description: Saiba como usar a API do servidor para fornecer e renderizar experiências personalizadas criadas no Adobe Target.
exl-id: c9e2f7ef-5022-4dc4-82b4-ecc210f27270
source-git-commit: ddffe9bf30741b457f7de1099b50ac1624fca927
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 1%

---

# Personalization via Adobe Target

## Visão geral {#overview}

A API do servidor Edge Network pode fornecer e renderizar experiências personalizadas criadas no Adobe Target, com a ajuda do [Experience Composer baseado em formulário](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html).

>[!IMPORTANT]
>
>As experiências do Personalization criadas por meio do [Target Visual Experience Composer (VEC)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) não são totalmente compatíveis com a API do servidor. A API do Servidor pode **recuperar** atividades criadas pelo VEC, mas a API do Servidor não pode **renderizar** atividades criadas pelo VEC. Se você quiser renderizar atividades criadas pelo VEC, implemente a [personalização híbrida](../web-sdk/personalization/hybrid-personalization.md) usando o SDK da Web e a API do servidor Edge Network.

## Configurar o fluxo de dados {#configure-your-datastream}

Antes de usar a API do servidor em conjunto com o Adobe Target, é necessário habilitar a personalização do Adobe Target na configuração do fluxo de dados.

Consulte o [guia sobre como adicionar serviços a uma sequência de dados](../datastreams/overview.md#adobe-target-settings), para obter informações detalhadas sobre como habilitar o Adobe Target.

Ao configurar sua sequência de dados, você pode (opcionalmente) fornecer valores para [!DNL Property Token], [!DNL Target Environment ID] e [!DNL Target Third Party ID Namespace].

![Imagem da interface mostrando a tela de configuração do serviço de sequência de dados, com o Adobe Target selecionado](assets/target-datastream.png)

## Parâmetros personalizados {#custom-parameters}

A maioria dos campos na parte [!DNL XDM] de cada solicitação são serializados em notação de pontos e depois enviados para o Target como parâmetros personalizados ou [!DNL mbox].


### Exemplo {#custom-parameters-example}

Dada a seguinte amostra XDM:

```json
"xdm":{
   "marketing":{
      "campaignGroup":"winter22",
      "campaignName":"homeOwnerPromo22",
      "trackingCode":"hop22"
   }
}
```

Ao criar públicos no Target, os seguintes valores estarão disponíveis como parâmetros personalizados:

* `marketing.campaignGroup`
* `marketing.campaignName`
* `marketing.trackingCode`

## Atualizações do perfil do Target {#profile-update}

O [!DNL Server API] permite atualizações no perfil do Target. Para atualizar um perfil do Target, verifique se os dados do perfil foram passados na parte `data` da solicitação no seguinte formato:

```json
"data":  {
    "__adobe.target": {
        "profile.eyeColor": "brown",
        "profile.hairColor": "brown"
    }
}
```

## Consulta a atividades do Target {#querying-target-activities}

### Esquemas {#schemas}

A parte de consulta da solicitação determina qual conteúdo é retornado pelo Target. Sob o objeto `personalization`, `schemas` determina o tipo de conteúdo a ser retornado pelo Target.

Em situações em que você não tem certeza do tipo de ofertas que recuperará, inclua todos os quatro esquemas em sua consulta de personalização ao Edge Network:

* **Ofertas baseadas em HTML:**
https://ns.adobe.com/personalization/html-content-item
* **Ofertas baseadas em JSON:**
https://ns.adobe.com/personalization/json-content-item
* **Ofertas de redirecionamento do Target**
https://ns.adobe.com/personalization/redirect-item
* **Ofertas de Manipulação de DOM de Destino**
https://ns.adobe.com/personalization/dom-action

### Escopos de decisão {#decision-scopes}

Os nomes do Adobe Target [!DNL mbox] devem ser incluídos na matriz `decisionScopes` para retornar o conteúdo apropriado.

#### Exemplo {#decision-scopes-example}

No exemplo abaixo, todos os quatro tipos de ofertas são solicitados juntamente com uma atividade do Target chamada `serverapimbox`.

```json
"query":{
   "personalization":{
      "schemas":[
         "https://ns.adobe.com/personalization/html-content-item",
         "https://ns.adobe.com/personalization/json-content-item",
         "https://ns.adobe.com/personalization/redirect-item",
         "https://ns.adobe.com/personalization/dom-action"
      ],
      "decisionScopes":[
         "serverapimbox"
      ]
   }
}
```

## Exemplo de chamada de API {#api-example}

**Formato da API**

```http
POST /ee/v2/interact
```

### Solicitação {#request}

Uma solicitação completa que inclui um objeto XDM completo, parâmetros do perfil e a consulta do Target apropriada é descrita abaixo.

```shell
curl -X POST 'https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org: {ORG_ID}' \
--header 'Authorization: Bearer {TOKEN}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "event": {
        "xdm": {
            "eventType": "web.webpagedetails.pageViews",
            "identityMap": {
                "ECID": [
                    {
                        "id": "05907638112924484241029082405297151763",
                        "authenticatedState": "ambiguous",
                        "primary": true
                    }
                ]
            },
            "web": {
                "webPageDetails": {
                    "URL": "https://alloystore.dev",
                    "name": "Home Page"
                },
                "webReferrer": {
                    "URL": ""
                }
            },
            "device": {
                "screenHeight": 1440,
                "screenWidth": 3440,
                "screenOrientation": "landscape"
            },
            "environment": {
                "type": "browser",
                "browserDetails": {
                    "viewportWidth": 3440,
                    "viewportHeight": 1440
                }
            },
            "placeContext": {
                "localTime": "2022-03-22T22:45:21.193-06:00",
                "localTimezoneOffset": 360
            },
            "timestamp": "2022-03-23T04:45:21.193Z",
            "implementationDetails": {
                "name": "https://ns.adobe.com/experience/alloy/reactor",
                "version": "1.0",
                "environment": "serverapi"
            },
            "data": {
                "__adobe": {
                    "target": {
                        "profile.eyeColor": "brown",
                        "profile.hairColor": "brown",
                        "profile.shoeColor": "black"
                    }
                }
            }
        }
    },
    "query": {
        "personalization": {
            "schemas": [
                "https://ns.adobe.com/personalization/html-content-item",
                "https://ns.adobe.com/personalization/json-content-item",
                "https://ns.adobe.com/personalization/redirect-item",
                "https://ns.adobe.com/personalization/dom-action"
            ],
            "decisionScopes": [
                "serverapimbox"
            ]
        }
    }
}'
```

### Resposta {#response}

O Edge Network retornará uma resposta semelhante à mostrada abaixo.

```json
{
   "requestId":"10959bbf-f83d-40e1-9521-d9145f19cdc5",
   "handle":[
      {
         "payload":[
            {
               "id":"AT:eyJhY3Rpdml0eUlkIjoiMTQwMjgxIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
               "scope":"serverapimbox",
               "scopeDetails":{
                  "decisionProvider":"TGT",
                  "activity":{
                     "id":"140281"
                  },
                  "experience":{
                     "id":"0"
                  },
                  "strategies":[
                     {
                        "algorithmID":"0",
                        "trafficType":"0"
                     }
                  ],
                  "characteristics":{
                     "eventToken":"xycjBJlZhwVV5MN0kMkmoGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw=="
                  }
               },
               "items":[
                  {
                     "id":"282484",
                     "schema":"https://ns.adobe.com/personalization/json-content-item",
                     "meta":{
                        "offer.name":"/server_apiform/experiences/0/pages/0/zones/0/1648103551041",
                        "experience.id":"0",
                        "activity.name":"Server API Form",
                        "activity.id":"140281",
                        "experience.name":"Experience A",
                        "option.id":"2",
                        "offer.id":"282484"
                     },
                     "data":{
                        "id":"282484",
                        "format":"application/json",
                        "content":{
                           "value":"a/b json experience a",
                           "platform":"server"
                        }
                     }
                  }
               ]
            }
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      },
      {
         "payload":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiYwNTkwNzYzODExMjkyNDQ4NDI0MTAyOTA4MjQwNTI5NzE1MTc2M1IOCL-pwpv9LxgBKgNPUjLwAb-pwpv9Lw==",
               "maxAge":34128000
            }
         ],
         "type":"state:store"
      }
   ]
}
```

Se o visitante se qualificar para uma atividade de personalização com base nos dados enviados para o Adobe Target, o conteúdo relevante da atividade será encontrado no objeto `handle`, onde o tipo é `personalization:decisions`.

Às vezes, outros conteúdos também serão retornados em `handle`. Outros tipos de conteúdo não são relevantes para a personalização do Target. Se o visitante se qualificar para várias atividades, cada atividade será um objeto `personalization` separado na matriz.

A tabela abaixo explica os principais elementos dessa parte da resposta.

| Propriedade | Descrição | Exemplo |
|---|---|---|
| `scope` | O nome da mbox do Target que resultou nas ofertas propostas. | `"scope": "serverapimbox"` |
| `items[].schema` | O schema do conteúdo associado à oferta proposta. Isso será relacionado ao tipo de atividade selecionado ao criar a atividade de personalização. | `"schema": "https://ns.adobe.com/personalization/json-content-item",` |
| `items[].meta.activity.id` | O identificador exclusivo da atividade de oferta. Normalmente, um número de 6 dígitos. | `"activity.id": "140281"` |
| `items[].meta.activity.name` | O nome da atividade de oferta especificada pelo usuário. Isso é fornecido durante a etapa de criação da atividade. | `"activity.name": "Server API Form"` |
| `items[].meta.experience.id` | O identificador exclusivo da experiência de personalização. | `"experience.id": "0"` |
| `items[].meta.experience.name` | O nome exclusivo da experiência de personalização. | `"experience.name": "Experience A"` |
| `items[].data.id` | A ID da oferta proposta. | `"id": "282484"` |
| `items[].data.format` | O formato do conteúdo associado à oferta proposta. | `"format: "application/json` |
| `items[].data.content` | Conteúdo associado à oferta proposta. Ele será usado para personalização do conteúdo do aplicativo de chamada. | `"content": "<CONTENT CONFIGURED IN TARGET>"` |

## Aplicativo de amostra de personalização do lado do servidor {#sample}

O aplicativo de exemplo encontrado em [esta URL](https://github.com/adobe/alloy-samples/tree/main/target/personalization-server-side) demonstra o uso do Adobe Experience Platform para obter conteúdo de personalização do Adobe Target. A página da Web muda com base no conteúdo de personalização retornado.

Este exemplo _não_ depende de bibliotecas do lado do cliente como o [!DNL Web SDK] para obter conteúdo de personalização. Em vez disso, ele usa as APIs do Adobe Experience Platform para buscar conteúdo de personalização. Em seguida, a implementação gera o lado do servidor do HTML com base no conteúdo de personalização retornado.
