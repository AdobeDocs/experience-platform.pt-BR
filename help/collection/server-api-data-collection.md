---
title: Coleta de dados
description: Saiba como a API do servidor de rede de borda do Adobe Experience Platform estrutura os dados coletados
seo-description: Learn how the Adobe Experience Platform Edge Network Server API structures the collected data
keywords: coleta de dados, coleta, Adobe Experience Platform Edge Network, api, estrutura
source-git-commit: 92b3a7bff576f72edc8628a850a2cdb9b43cb1c4
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 4%

---


# Coleta de dados

O [!DNL Server API] O oferece dois tipos de endpoints de coleta de dados:

* [Pontos finais de coleta de dados interativos](interactive-data-collection.md), usado quando o cliente espera que uma resposta seja retornada pelo servidor. Esses endpoints também podem retornar conteúdo de outros serviços de rede de borda, enquanto realizam a coleta de dados.
* [Coleta de dados de eventos não interativos](non-interactive-data-collection.md), usado quando nenhuma resposta é esperada do servidor. Esses endpoints são usados somente para coleta de dados.

## `Event` objeto {#event-object}

Dados coletados pela [!DNL Server API] está estruturado na variável `Event` objeto. A estrutura desse objeto é descrita abaixo.

```json
{
   "xdm":{
      "identityMap":{
         "Email_LC_SHA256":[
            {
               "id":"0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
               "primary":true
            }
         ]
      },
      "eventType":"web.webpagedetails.pageViews",
      "web":{
         "webPageDetails":{
            "URL":"https://alloystore.dev/",
            "name":"home-demo-Home Page",
            "pageViews":{
               "value":1
            }
         }
      },
      "placeContext":{
         "localTime":"2021-08-09T17:09:20.859+03:00",
         "localTimezoneOffset":-180
      },
      "timestamp":"2021-08-09T14:09:20.859Z"
   },
   "data":{
      "prop1":"custom value",
      "var10":"search (organic)"
   }
}
```

| Atributo | Tipo | Descrição |
| --- | --- | --- |
| `xdm` | Objeto | *Obrigatório*. Objeto JSON contendo dados no formato XDM, correspondente ao esquema do conjunto de dados. |
| `data` | Objeto | *Opcional*. Objeto JSON contendo dados de forma livre, que pode ser mapeado para XDM pela Edge Network. |

