---
title: Personalização via Adobe Target
description: Saiba como usar a API do servidor para entregar e renderizar experiências personalizadas criadas no Adobe Target.
exl-id: c9e2f7ef-5022-4dc4-82b4-ecc210f27270
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 3%

---

# Personalização via Adobe Target

## Visão geral {#overview}

A API do Servidor de rede de borda pode fornecer e renderizar experiências personalizadas criadas no Adobe Target, com a ajuda do [Experience Composer baseado em formulário](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en).

>[!IMPORTANT]
>
>Experiências de personalização criadas com o [Visual Experience Composer (VEC) do Target](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=en) não são compatíveis com a API do servidor.

## Configurar o fluxo de dados {#configure-your-datastream}

Antes de usar a API do servidor em conjunto com o Adobe Target, é necessário habilitar a personalização do Adobe Target na configuração do conjunto de dados.

Consulte a [guia sobre como adicionar serviços a um armazenamento de dados](../edge/datastreams/overview.md#adobe-target-settings)para obter informações detalhadas sobre como ativar o Adobe Target.

Ao configurar seu armazenamento de dados, você pode (opcionalmente) fornecer valores para [!DNL Property Token], [!DNL Target Environment ID]e [!DNL Target Third Party ID Namespace].

![Imagem da interface do usuário mostrando a tela de configuração do serviço de armazenamento de dados, com Adobe Target selecionado](assets/target-datastream.png)

Você pode escolher entre as seguintes opções [!DNL Analytics Logging] opções:

* **[!DNL Server Side]**: Esta é a opção padrão para [[!DNL A4T]](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=pt-BR). Quando essa opção é selecionada, cada vez que o conteúdo de personalização é retornado pelo Target, a variável [!DNL A4T] Os dados do são enviados automaticamente para o Analytics, com base na resposta do mecanismo de personalização do Target.
* **[!DNL Client Side]**: Quando essa opção é selecionada, cada vez que o conteúdo de personalização é retornado pelo Target, a variável [!DNL A4T] Os dados são retornados ao aplicativo chamador. Se sua intenção é gravar esses dados no Analytics, é necessário garantir que eles sejam relatados em uma chamada subsequente para [!DNL Analytics].

   >[!IMPORTANT]
   >
   >Além da seleção de **[!UICONTROL Lado do cliente]** na configuração do Target, você também deve desativar o Analytics para que a rede de borda retorne a variável [!DNL A4T] informações de volta à resposta.


## Parâmetros personalizados {#custom-parameters}

A maioria dos campos na variável [!DNL XDM] parte de cada solicitação é serializada em notação de pontos e enviada para o Target como personalizada ou [!DNL mbox] parâmetros.


### Exemplo {#custom-parameters-example}

Dado o seguinte exemplo de XDM:

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

* `xdm.marketing.campaignGroup`
* `xdm.marketing.campaignName`
* `xdm.marketing.trackingCode`

## Atualizações de perfil do Target {#profile-update}

O [!DNL Server API] O permite atualizações no perfil do Target. Para atualizar um perfil do Target, verifique se os dados do perfil foram passados no `data` parte da solicitação no seguinte formato:

```json
"data":  {
    "__adobe.target": {
        "profile.eyeColor": "brown",
        "profile.hairColor": "brown"
    }
}
```

## Consulta de atividades do Target {#querying-target-activities}

### Schemas {#schemas}

A parte de consulta da solicitação determina qual conteúdo é retornado pelo Target. Em `personalization` objeto, `schemas` determina o tipo de conteúdo a ser retornado pelo Target.

Em situações em que não tem certeza de que tipo de oferta você recuperará, você deve incluir todos os quatro esquemas em seu query de personalização na Edge Network:

* **Ofertas baseadas em HTML:**
https://ns.adobe.com/personalization/html-content-item
* **Ofertas baseadas em JSON:**
https://ns.adobe.com/personalization/json-content-item
* **Ofertas de redirecionamento do Target**
https://ns.adobe.com/personalization/redirect-item
* **Ofertas de Manipulação de DOM do Target**
https://ns.adobe.com/personalization/dom-action

### Escopos de decisão {#decision-scopes}

Adobe Target [!DNL mbox] os nomes devem ser incluídos no `decisionScopes` para retornar o conteúdo apropriado.

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

Uma solicitação completa que inclui um objeto XDM completo, parâmetros do perfil, juntamente com a consulta do Target apropriada é descrita abaixo.

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

A Edge Network retornará uma resposta semelhante à abaixo.

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

Se o visitante se qualificar para uma atividade de personalização com base nos dados enviados para o Adobe Target, o conteúdo relevante da atividade será encontrado no `handle` objeto , onde o tipo é `personalization:decisions`.

Outro conteúdo às vezes será retornado em `handle` também. Outros tipos de conteúdo não são relevantes para a personalização do Target. Se o visitante se qualificar para várias atividades, cada atividade será uma `personalization` na matriz.

A tabela abaixo explica os elementos-chave dessa parte da resposta.

| Propriedade | Descrição | Exemplo |
|---|---|---|
| `scope` | O nome da mbox do Target que resultou nas ofertas propostas. | `"scope": "serverapimbox"` |
| `items[].schema` | O schema do conteúdo associado à oferta proposta. Isso estará relacionado ao tipo de atividade selecionado ao criar a atividade de personalização. | `"schema": "https://ns.adobe.com/personalization/json-content-item",` |
| `items[].meta.activity.id` | A ID exclusiva da atividade de oferta. Normalmente, é um número de 6 dígitos. | `"activity.id": "140281"` |
| `items[].meta.activity.name` | O nome da atividade de oferta especificada pelo usuário. Isso é fornecido durante a etapa de criação da atividade. | `"activity.name": "Server API Form"` |
| `items[].meta.experience.id` | A ID exclusiva da experiência de personalização. | `"experience.id": "0"` |
| `items[].meta.experience.name` | O nome exclusivo da experiência de personalização. | `"experience.name": "Experience A"` |
| `items[].data.id` | A ID da oferta proposta. | `"id": "282484"` |
| `items[].data.format` | O formato do conteúdo associado à oferta proposta. | `"format: "application/json` |
| `items[].data.content` | Conteúdo associado à oferta proposta. Ele será usado para personalização do conteúdo do aplicativo de chamada. | `"content": "<CONTENT CONFIGURED IN TARGET>"` |
