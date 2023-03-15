---
title: Coleta de dados
description: Saiba como a API do servidor de rede de borda da Adobe Experience Platform estrutura os dados coletados.
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 6%

---


# Coleta de dados

A variável [!DNL Server API] O oferece dois tipos de endpoints de coleta de dados:

* [Pontos de extremidade de coleta de dados interativos](interactive-data-collection.md), usado quando o cliente espera que uma resposta seja retornada pelo servidor. Esses endpoints também podem retornar conteúdo de outros serviços da rede de borda ao realizar a coleta de dados.
* [Coleta de dados de evento não interativa](non-interactive-data-collection.md), usado quando nenhuma resposta é esperada do servidor. Esses endpoints são usados somente para a coleta de dados do.

## `Event` objeto {#event-object}

Dados coletados pelo [!DNL Server API] está estruturado no `Event` objeto. A estrutura desse objeto é descrita abaixo.

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
| `data` | Objeto | *Opcional*. Objeto JSON que contém dados de forma livre, que podem ser mapeados para XDM pela Rede de borda. |

