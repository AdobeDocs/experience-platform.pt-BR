---
title: Identificação do visitante via FPID
description: Saiba como identificar visitantes de maneira consistente por meio da API do servidor, usando o FPID
seo-description: Learn how to consistently identify visitors via the Server API, by using the FPID
keywords: rede de borda;gateway;api;visitante;identificação;edge network;gateway;api;visitor;identification;fpid
exl-id: c61d2e7c-7b5e-4b14-bd52-13dde34e32e3
source-git-commit: 1ab1c269fd43368e059a76f96b3eb3ac4e7b8388
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# Identificação do visitante via FPID

[!DNL First-party IDs] (`FPIDs`) são IDs de dispositivo geradas, gerenciadas e armazenadas pelos clientes. Isso dá aos clientes controle sobre a identificação de dispositivos de usuário. Enviando `FPIDs`, a Edge Network não gera uma rede totalmente nova `ECID` para uma solicitação que não contém um.

A variável `FPID` pode ser incluído no corpo da solicitação de API como parte da variável `identityMap` ou ele pode ser enviado como um cookie.

Um `FPID` podem ser traduzidas deterministicamente em um `ECID` pela Rede de borda, portanto `FPID` as identidades são totalmente compatíveis com as soluções Experience Cloud. Obter uma `ECID` de um `FPID` O sempre produz o mesmo resultado, de modo que os usuários terão uma experiência consistente.

A variável `ECID` obtidos dessa forma podem ser recuperados por meio de um `identity.fetch` consulta:

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

Para solicitações que contêm um `FPID` e uma `ECID`, o `ECID` presente no pedido terá precedência sobre a que poderia ser gerada a partir da data `FPID`. Em outras palavras, a rede de borda usa a variável `ECID` já fornecidos e a `FPID` é ignorado. Um novo `ECID` é gerado somente quando um `FPID` é fornecido por conta própria.

Em termos de IDs de dispositivo, a variável `server` as sequências de dados devem usar `FPID` como ID do dispositivo. Outras identidades (por exemplo, `EMAIL`) também podem ser fornecidos no corpo da solicitação, mas a Rede de borda exige que uma identidade primária seja fornecida explicitamente. A identidade principal é a identidade base na qual os dados do perfil serão armazenados.

>[!NOTE]
>
>As solicitações que não tiverem identidade, respectivamente, nenhuma identidade principal explicitamente definida no corpo da solicitação, falharão.

As seguintes `identityMap` o grupo de campos está formado corretamente para um `server` solicitação de sequência de dados:

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

As seguintes `identityMap` grupo de campos resultará em uma resposta de erro quando definido em um `server` solicitação de sequência de dados:

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

A resposta de erro retornada pela Rede de borda nesse caso é semelhante ao seguinte:

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

Para identificar usuários via `FPID`, assegurar que a `FPID` cookie foi enviado antes de fazer qualquer solicitação à Rede de borda. A variável `FPID` pode ser transmitido em um cookie ou como parte da `identityMap` no corpo da solicitação.

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

## Solicitar com `FPID` passado como `identityMap` campo

O exemplo abaixo passa o [!DNL FPID] como um `identityMap` parâmetro.

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
