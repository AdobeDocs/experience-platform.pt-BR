---
title: Identificação do visitante via FPID
description: Saiba como identificar de forma consistente os visitantes por meio da API do Edge Network, usando o FPID
seo-description: Learn how to consistently identify visitors via the Edge Network API, by using the FPID
keywords: rede de borda;gateway;api;visitante;identificação;edge network;gateway;api;visitor;identification;fpid
exl-id: c61d2e7c-7b5e-4b14-bd52-13dde34e32e3
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Identificação do visitante via FPID

[!DNL First-party IDs] (`FPIDs`) são IDs de dispositivo geradas, gerenciadas e armazenadas por clientes. Isso dá aos clientes controle sobre a identificação de dispositivos de usuário. Ao enviar `FPIDs`, a Edge Network não gera um `ECID` totalmente novo para uma solicitação que não contém um.

O `FPID` pode ser incluído no corpo da solicitação de API como parte do `identityMap` ou pode ser enviado como um cookie.

Um `FPID` pode ser convertido deterministicamente em um `ECID` pela Edge Network, portanto, as identidades do `FPID` são totalmente compatíveis com as soluções da Experience Cloud. A obtenção de um `ECID` de um `FPID` específico sempre produz o mesmo resultado, portanto, os usuários terão uma experiência consistente.

O `ECID` obtido dessa maneira pode ser recuperado por meio de uma consulta `identity.fetch`:

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

Para solicitações que contêm tanto um `FPID` quanto um `ECID`, o `ECID` já presente na solicitação terá precedência sobre aquele que poderia ser gerado a partir de `FPID`. Em outras palavras, o Edge Network usa o `ECID` já fornecido e o `FPID` é ignorado. Um novo `ECID` só é gerado quando um `FPID` é fornecido sozinho.

Em termos de IDs de dispositivo, as sequências de dados de `server` devem usar `FPID` como ID de dispositivo. Outras identidades (ou seja, `EMAIL`) também podem ser fornecidas dentro do corpo da solicitação, mas o Edge Network exige que uma identidade primária seja fornecida explicitamente. A identidade principal é a identidade base na qual os dados do perfil serão armazenados.

>[!NOTE]
>
>As solicitações que não tiverem identidade, respectivamente, nenhuma identidade principal explicitamente definida no corpo da solicitação, falharão.

O seguinte grupo de campos `identityMap` está formado corretamente para uma solicitação de sequência de dados `server`:

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

O seguinte grupo de campos `identityMap` resultará em uma resposta de erro quando definido em uma solicitação de sequência de dados `server`:

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

A resposta de erro retornada pela Edge Network nesse caso é semelhante ao seguinte:

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

## Identificação de visitante com `FPID`

Para identificar usuários via `FPID`, verifique se o cookie `FPID` foi enviado antes de fazer qualquer solicitação à Edge Network. O `FPID` pode ser transmitido em um cookie ou como parte de `identityMap` no corpo da solicitação.

<!--

## Request with `FPID` passed as cookie header

```shell
curl -X POST 'https://edge.adobedc.net/v2/interact?dataStreamId={Data Stream ID}' \
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

## Solicitação com `FPID` aprovada como campo `identityMap`

O exemplo abaixo passa o [!DNL FPID] como um parâmetro `identityMap`.

```shell
curl -X POST "https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}"
-H "Authorization: Bearer {TOKEN}"
-H "x-gw-ims-org-id: {ORG_ID}"
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
