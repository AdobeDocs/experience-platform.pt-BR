---
title: Coleção de dados
description: Saiba como a API do Adobe Experience Platform Edge Network Server estrutura os dados coletados.
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 6%

---


# Coleção de dados

O [!DNL Server API] oferece dois tipos de pontos de extremidade de coleta de dados:

* [Pontos de extremidade de coleção de dados interativos](interactive-data-collection.md), usados quando o cliente espera que uma resposta seja retornada pelo servidor. Esses endpoints também podem retornar conteúdo de outros serviços Edge Network enquanto executam a coleta de dados.
* [Coleção de dados de evento não interativa](non-interactive-data-collection.md), usada quando nenhuma resposta é esperada do servidor. Esses endpoints são usados somente para a coleta de dados do.

## objeto `Event` {#event-object}

Os dados coletados por [!DNL Server API] são estruturados no objeto `Event`. A estrutura desse objeto é descrita abaixo.

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
| `xdm` | Objeto | *Obrigatório*. Objeto JSON que contém dados no formato XDM, correspondentes ao esquema do conjunto de dados. |
| `data` | Objeto | *Opcional*. Objeto JSON que contém dados de forma livre, que podem ser mapeados para o XDM pelo Edge Network. |

