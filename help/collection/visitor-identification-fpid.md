---
title: Identificação do visitante via FPID
description: Saiba como identificar de forma consistente visitantes por meio da API do servidor, usando o FPID
seo-description: Learn how to consistently identify visitors via the Server API, by using the FPID
keywords: rede de borda, gateway, api, visitante, identificação, fpid
source-git-commit: eaeab8fe96a9af399f8288b62b6ca9f31d949cfa
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---


# Identificação do visitante via FPID

## Visão geral

[!DNL First-party IDs] (`FPIDs`) são IDs de dispositivo geradas, gerenciadas e armazenadas por clientes. Isso dá aos clientes controle sobre a identificação de dispositivos do usuário. Ao enviar `FPIDs`, a Edge Network não gera uma novidade `ECID` para uma solicitação que não contém uma.

O `FPID` pode ser incluída no corpo da solicitação da API como parte do `identityMap` ou pode ser enviado como um cookie.

Um `FPID` pode ser convertido deterministicamente em um `ECID` pela Edge Network, assim `FPID` identidades são totalmente compatíveis com as soluções Experience Cloud. Obter um `ECID` de um `FPID` sempre gera o mesmo resultado, para que os usuários tenham uma experiência consistente.

O `ECID` obtido dessa forma pode ser recuperado por meio de um `identity.fetch` query:

```json
{
   "query":{
      "identity":{
         "fetch":[
            "ECID"
         ]
      }
   }
}
```

Para solicitações que contêm um `FPID` e um `ECID`, o `ECID` já presente na solicitação terá precedência sobre a que pode ser gerada pelo `FPID`. Portanto, a Edge Network usará a variável `ECID` já fornecido e não calculará um de `FPID`.

Em termos de IDs de dispositivo, a variável `server` os datastreams devem usar `FPID` como ID do dispositivo. Outras identidades (ou seja `EMAIL`) também pode ser fornecida no corpo da solicitação, mas a Rede de borda requer que uma identidade primária seja explicitamente fornecida. A identidade primária é a identidade base na qual os dados de perfil serão armazenados.

>[!NOTE]
>
>As solicitações que não têm identidade, respectivamente nenhuma identidade primária definida explicitamente no corpo da solicitação, falharão.

O seguinte `identityMap` grupo de campos é formado corretamente para um `server` solicitação do datastream:

```json
{
   "identityMap":{
      "FPID":[
         {
            "id":"123e4567-e89b-12d3-a456-426614174000",
            "authenticatedState":"ambiguous",
            "primary":true
         }
      ],
      "EMAIL":[
         {
            "id":"email@mail.com",
            "authenticatedState":"authenticated"
         }
      ]
   }
}
```

O seguinte `identityMap` grupo de campos resultará em uma resposta de erro ao definir um `server` solicitação do datastream:

```json
{
   "identityMap":{
      "FPID":[
         {
            "id":"123e4567-e89b-12d3-a456-426614174000",
            "authenticatedState":"ambiguous"
         }
      ],
      "EMAIL":[
         {
            "id":"email@mail.com",
            "authenticatedState":"authenticated"
         }
      ]
   }
}
```

Nesse caso, a resposta do erro retornada pela Edge Network é semelhante ao seguinte:

```json
{
   "type":"https://ns.adobe.com/aep/errors/EXEG-0306-400",
   "status":400,
   "title":"No primary identity set in request (event)",
   "detail":"No primary identity found in the input event. Update the request accordingly to your schema and try again.",
   "report":{
      "requestId":"{REQUEST_ID}",
      "configId":"{CONFIG_ID}",
      "orgId":"{ORG_ID}"
   }
}
```

## Identificação do visitante com `FPID`

Para identificar usuários via `FPID`, assegure que `FPID` O cookie foi enviado antes de fazer qualquer solicitação à Edge Network. O `FPID` pode ser passado em um cookie ou como parte do `identityMap` no corpo do pedido.

<!--

## Request with `FPID` passed as cookie header

```shell
curl -X POST 'https://edge.adobedc.net/ee/v2/interact?dataStreamId={Data Stream ID}' \
-H 'cookie: FPID=e98f38e6-6183-442d-8cd2-0e384f4c8aa8' \
-H 'Content-Type: application/json' \
-d '{
    "event": 
        {
            "xdm": {
                "web": {
                    "webPageDetails": {
                        "URL": "https://alloystore.dev"
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
                        "viewportWidth": 1907,
                        "viewportHeight": 545
                    }
                },
                "placeContext": {
                    "localTime": "2022-03-21T21:32:59.991-06:00",
                    "localTimezoneOffset": 360
                },
                "timestamp": "2022-03-22T03:32:59.992Z",
                "implementationDetails": {
                    "name": "https://ns.adobe.com/experience/alloy/reactor",
                    "version": "1.0",
                    "environment": "serverapi"
                }
            }
        },
    "query": {
        "identity": {
            "fetch": [
                "ECID"
            ]
        }
    },
    "meta":
        {
            "state":
            {
                "domain": "alloystore.dev",
                "cookiesEnabled": true
            }
        }
}'
```
-->

## Solicitação com `FPID` aprovado como `identityMap` campo

O exemplo abaixo passa a variável [!DNL FPID] como um `identityMap` parâmetro.

```shell
curl -X POST "https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}"
-H "Authorization: Bearer {TOKEN}"
-H "x-gw-ims-org-id: {IMS_ORG_ID}"
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "event": {
      "xdm": {
         "identityMap": {
            "FPID": [
               {
                  "id": "e98f38e6-6183-442d-8cd2-0e384f4c8aa8",
                  "authenticatedState": "ambiguous",
                  "primary": true
               }
            ]
         },
         "web": {
            "webPageDetails": {
               "URL": "https://alloystore.dev"
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
               "viewportWidth": 1907,
               "viewportHeight": 545
            }
         },
         "placeContext": {
            "localTime": "2022-03-21T21:32:59.991-06:00",
            "localTimezoneOffset": 360
         },
         "timestamp": "2022-03-22T03:32:59.992Z",
         "implementationDetails": {
            "name": "https://ns.adobe.com/experience/alloy/reactor",
            "version": "1.0",
            "environment": "serverapi"
         }
      }
   },
   "query": {
      "identity": {
         "fetch": [
            "ECID"
         ]
      }
   }
}'
```
