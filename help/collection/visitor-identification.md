---
title: Identificação do visitante
description: Saiba como a API do servidor Adobe Experience Platform Edge Network identifica visitantes
seo-description: Learn how Adobe Experience Platform Edge Network Server API identifies visitors
keywords: rede de borda;gateway;api;visitante;identificação;edge network;gateway;api;visitor;identification
exl-id: aa2f3b83-5cc8-4e02-9119-edfd5e212588
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 3%

---

# Identificação do visitante

A API do Servidor Edge Network oferece suporte à [identificação de visitantes por meio da ID de Primário ([!DNL FPID])](visitor-identification-fpid.md).

Todas as identidades de usuário devem ser fornecidas no grupo de campos `identityMap`. Este grupo de campos está incluído no mixin `ExperienceEvent` do SDK da Web da AEP.

```json
{
   "identityMap":{
      "FPID":[
         {
            "id":"55613368189701342632255821452918751312",
            "authenticatedState":"ambiguous"
         }
      ],
      "CRM":[
         {
            "id":"2394509340-30453470347",
            "authenticatedState":"authenticated"
         }
      ]
   }
}
```

## Identificadores de dispositivo {#identifiers}

Há várias maneiras pelas quais um dispositivo pode ser identificado dentro do Edge Network. Consulte a tabela abaixo para obter uma visão geral das IDs compatíveis.

| Namespace de ID | Gerenciado por | Descrição |
| --- | --- | --- |
| `FPID` | Cliente | `FPID` será automaticamente codificado em um `ECID` pelo Edge Network, portanto, as soluções que requerem `ECID` também funcionarão.  <br><br> Para identificação consistente do dispositivo, essas IDs devem ser mantidas no dispositivo e fornecidas em cada solicitação. Para interações na web, isso envolve armazená-las como cookies do navegador. |
| `IDFA`/`GAID` | Experience Platform | Pode identificar usuários entre aplicativos, de modo que essas IDs não sejam codificadas em `ECID` pelo Edge Network. |

<!--
| `ECID` | Adobe | `ECID` is required when leveraging and integrating with Adobe Analytics and Adobe Audience Manager. <br><br> For consistent device identification, these IDs must be persisted on the device and supplied on each request. For web interactions, this involves storing them as browser cookies. |
-->

<!--
## Edge Network Identity Protocol {#experience-edge-identity-protocol}

Device identities like `ECID` must be persisted on the client device and supplied on each request in the session and across sessions. Having stable device identities across multiple sessions improves the accuracy levels in your reports and allows delivering a consistent experience to the visitors.

For all non-server interactions, the Edge Network will automatically perform the following actions:

* Generate a new `ECID` when none is found on the request. This will automatically enhance the collected event with the new identity.
* Return a `state:store` instruction to the caller with the `kndctr_{$IMS_ORG_ID|url-safe}_identity` entry, which contains:
  * The [ID value](#ee-identity-format)
  * A `maxAge` value, in seconds, indicating how long the client persist the ID for

For example, let's consider the following request:

```json
{
   "events":[
      {
         "xdm":{
            "eventType":"web.webpagedetails.pageViews",
            "eventMergeId":"0772675a-1e24-44ea-a92b-0138c1d03a38",
            "web":{
               "webPageDetails":{
                  "URL":"https://alloystore.dev/",
                  "name":"home-demo-Home Page",
                  "pageViews":{
                     "value":1
                  }
               }
            },
            "device":{
               "screenHeight":1120,
               "screenWidth":1792,
               "screenOrientation":"landscape"
            },
            "environment":{
               "type":"browser",
               "browserDetails":{
                  "viewportWidth":1792,
                  "viewportHeight":481
               }
            },
            "timestamp":"2021-08-09T14:09:20.859Z"
         }
      }
   ]
}
```

The Edge Network response includes a `state:store` handle, which, in turn, includes an entry with the following name format: `kndctr_{$IMS_ORG_ID|url-safe}_identity`.

```json
{
   "requestId":"f5abf988-15d1-4463-a3b8-59aa0709a808",
   "handle":[
      {
         "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
         "value":"CiYzOTMyMzQ5NzU1MDY0MzIxNzc3NDEzMjY2NDA4OTIzOTExNDgyMlIRCIbghtqyLxABGAEqBElSTDHwAYbghtqyLw==",
         "maxAge":34128000
      }
   ],
   "type":"state:store"
}
```

>[!NOTE]
>
>The `kndctr_{$IMS_ORG_ID|url-safe}_` prefix is also used for other entries stored on the client device, and enables state isolation for complex integrations, which could involve multiple/different organizations. While the Edge Network will filter the entries which can be used for a given datastream, in order to minimize the payload, the caller (SDK) should ideally ensure that only the relevant entries are sent.

The caller must:

* Store this value on the client device
* Supply it on subsequent calls from that device in the request `meta.state.entries[]`, as shown below:

```json
{
   "meta":{
      "state":{
         "entries":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiYzOTMyMzQ5NzU1MDY0MzIxNzc3NDEzMjY2NDA4OTIzOTExNDgyMlIRCIbghtqyLxABGAEqBElSTDHwAYbghtqyLw=="
            }
         ]
      }
   }
}
```

## Identity Protocol via cookies (web)

When using first-party domain CNAMEs for interacting with the Edge Network, the client state can be managed automatically via first-party cookies.

The caller must explicitly activate this functionality via the `meta.state.cookiesEnabled` flag:

```json
{
   "meta":{
      "state":{
         "domain":"alloystore.dev",
         "cookiesEnabled":true
      }
   }
}
```

>[!NOTE]
>
>The `meta.state.domain` is an optional value which a caller could supply, specifying the exact domain on which the cookies should be stored. When this is missing, the Edge Network can automatically infer the top-level domain from the request. Automatic client state management via browser cookies **should never be used** in a `server` interaction.

-->
