---
description: As especificações do servidor e do modelo podem ser configuradas no SDK de destino do Adobe Experience Platform por meio do endpoint comum `/authoring/destination-servers`.
title: Opções de configuração para especificações do servidor e do modelo no SDK de destino
source-git-commit: d2452bf0e59866d3deca57090001c4c5a0935525
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 7%

---

# Opções de configuração para especificações do servidor e do modelo

## Visão geral {#overview}

As especificações do servidor e do modelo podem ser configuradas no SDK de Destino do Adobe Experience Platform por meio do endpoint comum `/authoring/destination-servers`. Leia [Operações de ponto de extremidade da API de Destinos](./destination-server-api.md) para obter uma lista completa de operações que podem ser executadas no ponto de extremidade.

## Exemplo de configuração {#example-configuration}

```json
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{endpoint.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

## Especificações do servidor {#server-specs}

![Configuração do servidor realçada](./assets/server-configuration.png)

Os clientes poderão ativar os dados do Adobe Experience Platform para o seu destino por meio de exportações HTTP. A configuração do servidor contém informações sobre o servidor que recebe as mensagens (o servidor no seu lado).

Esse processo fornece dados do usuário como uma série de mensagens HTTP para sua plataforma de destino. Os parâmetros abaixo formam o modelo de especificações do servidor HTTP.

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `name` | String | Representa um nome amigável do seu servidor, visível somente para o Adobe. Este nome não está visível para parceiros ou clientes. Exemplo `Moviestar destination server`. |
| `destinationServerType` | String | `URL_BASED` no momento, é a única opção disponível. |
| `templatingStrategy` | String | <ul><li>Use `PEBBLE_V1` se o Adobe precisar transformar o URL no campo `value` abaixo. Use essa opção se você tiver um terminal como: `https://api.moviestar.com/data/{{endpoint.region}}/items` </li><li> Use `NONE` se nenhuma transformação for necessária no lado do Adobe, por exemplo, se você tiver um terminal como: `https://api.moviestar.com/data/items` </li></ul> |
| `value` | String | Preencha o endereço do ponto de extremidade da API ao qual o Experience Platform deve se conectar. |

{style=&quot;table-layout:auto&quot;}

<!--

|Parameter | Type | Description|
|---------|----------|------|
|`hostname` | String | This is the hostname of your server. Example `https://data-in.acmecompany.net`.  |
|`port` | integer | The server port of your destination, for example `443`, `80`. |
|`maxUsersPerRequest` | integer | Specifies the maximum number of users per request allowed for your server. |
|`path` | String | This represents the url path and parameters of your server. Example:  `/path/to/import` |
|`httpMethod` | String | The method that Adobe will use in calls to your server. Options are `GET`, `PUT`, `POST`, `DELETE`, `PATCH`, `OPTIONS`, `HEAD`. |
|`contentType` | String | Defines how to structure the content sent to your servers. Supported options are JSON and XML. |

-->

## Especificações do modelo {#template-specs}

![Configuração do modelo realçada](./assets/template-configuration.png)

A especificação do modelo permite configurar como formatar a mensagem exportada para o destino. O Adobe usa uma linguagem de modelo semelhante a [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) para transformar os campos do esquema XDM em um formato compatível com seu destino. Para obter mais informações sobre a transformação, visite os links abaixo:

* [Formato de mensagem](./message-format.md)
* [Uso de uma linguagem de modelo para as transformações de identidade, atributos e associação de segmento ](./message-format.md#using-templating)

>[!TIP]
>
>O Adobe oferece uma [ferramenta de desenvolvedor](./create-template.md) que ajuda a criar e testar um modelo de transformação de mensagem.

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `httpMethod` | String | O método que o Adobe usará nas chamadas para o seu servidor. As opções são `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | String | Use  `PEBBLE_V1`. |
| `value` | String | Essa é a versão sem caracteres que transforma os dados dos clientes da Platform no formato que seu serviço espera. <br> Para obter informações sobre como gravar o modelo, leia a seção  [Uso do modelo](./message-format.md#using-templating) . <br> Para obter mais informações sobre o escape de caracteres, consulte o padrão JSON  [RFC, seção 7](https://tools.ietf.org/html/rfc8259#section-7). <br> Para obter um exemplo de uma transformação simples, consulte a transformação  [dos atributos ](./message-format.md#attributes) de perfil . |
| `contentType` | String | O tipo de conteúdo que seu servidor aceita. Esse valor provavelmente é `application/json`. |

{style=&quot;table-layout:auto&quot;}

<!--

|`requestBody` | String | The request body contains the data exported from Real-time CDP, activated to your destination. <br> We need to know which data format macros your destination should support. See [Outbound Template Macros](https://docs.adobe.com/content./en/audience-manager/user-guide/implementation-integration-guides/receiving-audience-data/batch-outbound-data-transfers/outbound-template-macros.html) and [Outbound Macro Examples](https://docs.adobe.com/content./en/audience-manager/user-guide/implementation-integration-guides/receiving-audience-data/batch-outbound-data-transfers/outbound-macro-examples.html) for examples from Adobe's DMP, Audience Manager. <br> See also, [Message format](#message-format) for further information.  |
|`queryParameters` | String | Request parameters defined as macros. See above.|



<br>&nbsp;

#### Example

A valid HTTP specs template could look like below:

```

{
  "name": "ACME company HTTP template",
  "type": "HTTP", 
  "httpTemplate": {
    "httpMethod": "POST",
    "requestBody": "{"AdvertiserId":"12345", "DataCenterId": 2, "SegmentID":"dfd215e4-8d6b-4fdb-90b9-fab4456f2c9d","Data":[{"Name":"4321"}]}",
    "queryParameters": "{"AdvertiserId":"12345", "DataCenterId": 2, "SegmentID":"dfd215e4-8d6b-4fdb-90b9-fab4456f2c9d","Data":[{"Name":"4321"}]}",
    "contentType": "JSON"
  }
}

```

// commenting out this part as these types of destination specs are not supported in phase one

### File specifications

File-based destinations deliver file exports containing segment qualifications and profile attributes to your preferred storage location. If you want to set up a batch file-based destination, the template we'll use will be as below:

## Server specs

The server configuration contains information about the server receiving the messages (the server on your side). 
Adobe Real-time CDP currently supports three types of server configurations:
* URL
* File-based SFTP
* File-based S3

For URL destinations, you would provide us your server's information, for File-based SFTP and File-based S3 you would provide information as to the storage locations where files should be delivered.
Provide us the necessary information about your server or storage locations, as shown in the sections below.


**urlBasedDestination**

|Parameter | Type | Description|
|---------|----------|------|
|`hostname` | String | This is the hostname of your server. Example `https://data-in.acmecompany.net`.  |
|`port` | integer | The server port of your destination, for example `443`, `80`. |
|`maxUsersPerRequest` | integer | Specifies the maximum number of users per request allowed for your server. |
|`path` | String | This represents the url path and parameters of your server. Example:  `/path/to/import` |


// commenting out this part as these types of destination specs are not supported in phase one

**SFTP Destinations**

For FTP destinations, we need the protocol details below:

Parameter | Type | 
---------|----------|
 hostname | String | 
 port | integer | 
 rootDirectory | String | 
 moveToWhenCompleted | integer | 
 tmpFileRename | integer | 
 encryptionMode | String |
 filenameSuffix | String | 

**Amazon S3 Destinations**

For Amazon S3 destinations, we need the protocol details below:

Parameter | Description | 
---------|----------|
 bucket | Your Amazon S3 bucket name | 
 path | Your Amazon S3 bucket path | 

-->
