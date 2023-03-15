---
description: As especificações do servidor e do modelo podem ser configuradas no Adobe Experience Platform Destination SDK por meio do endpoint comum `/authoring/destination-servers`.
title: Opções de configuração para especificações de servidor e modelo no Destination SDK
exl-id: cf493ed5-0bdb-4b90-b84d-73926a566a2a
source-git-commit: a08201c4bc71b0e37202133836e9347ed4d3cd6b
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 7%

---

# Opções de configuração para servidor de destinos de transmissão e especificações do modelo

## Visão geral {#overview}

As especificações do servidor e do modelo podem ser configuradas no Adobe Experience Platform Destination SDK por meio do endpoint comum `/authoring/destination-servers`. Ler [Operações de endpoint da API de destinos](./destination-server-api.md) para obter uma lista completa de operações que podem ser executadas no endpoint.

## Especificações do servidor {#server-specs}

![Configuração do servidor realçada](./assets/server-configuration.png)

Os clientes poderão ativar dados do Adobe Experience Platform para o seu destino por meio de exportações HTTP. A configuração do servidor contém informações sobre o servidor que recebe as mensagens (o servidor do seu lado).

Esse processo fornece dados do usuário como uma série de mensagens HTTP para a plataforma de destino. Os parâmetros abaixo formam o modelo de especificações do servidor HTTP.

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `name` | String | *Obrigatório.* Representa um nome amigável do servidor, visível somente para o Adobe. Este nome não está visível para parceiros ou clientes. Exemplo `Moviestar destination server`. |
| `destinationServerType` | String | *Obrigatório.* Defina como `URL_BASED` para destinos de transmissão. |
| `templatingStrategy` | String | *Obrigatório.* <ul><li>Uso `PEBBLE_V1` se estiver usando uma macro em vez de um valor fixo na variável `value` campo. Use essa opção se você tiver um terminal como: `https://api.moviestar.com/data/{{customerData.region}}/items` </li><li> Uso `NONE` se nenhuma transformação for necessária no lado do Adobe, por exemplo, se você tiver um terminal como: `https://api.moviestar.com/data/items` </li></ul> |
| `value` | String | *Obrigatório.* Preencha o endereço do endpoint da API ao qual o Experience Platform deve se conectar. |

{style="table-layout:auto"}

## Especificações do modelo {#template-specs}

![Configuração de modelo realçada](./assets/template-configuration.png)

A especificação do modelo permite configurar como formatar a mensagem exportada para o seu destino. Adobe usa uma linguagem de modelo semelhante a [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) para transformar os campos do esquema XDM em um formato compatível com seu destino. Para obter mais informações sobre a transformação, visite os links abaixo:

* [Formato de mensagem](./message-format.md)
* [Uso de uma linguagem de modelo para as transformações de identidade, atributos e associação de segmento ](./message-format.md#using-templating)

>[!TIP]
>
>Adobe oferece um [ferramenta de desenvolvedor](./create-template.md) que ajudam a criar e testar um template de transformação de mensagem.

## Configuração de exemplo de destino de streaming  {#example-configuration}

```json
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.endpointRegion}}/items"
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

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `httpMethod` | String | *Obrigatório.* O método que o Adobe usará nas chamadas para o servidor. As opções são `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `value` | String | *Obrigatório.* Essa cadeia de caracteres é a versão com escape de caracteres que transforma os dados dos clientes da Platform no formato esperado pelo serviço. <br> Para obter informações sobre como gravar o template, leia o [Uso da seção de modelos](./message-format.md#using-templating). <br> Para obter mais informações sobre o escape de caracteres, consulte o [RFC JSON padrão, seção sete](https://tools.ietf.org/html/rfc8259#section-7). <br> Para obter um exemplo de uma transformação simples, consulte [Atributos do perfil](./message-format.md#attributes) transformação. |
| `contentType` | String | *Obrigatório.* O tipo de conteúdo que seu servidor aceita. Este valor é mais provável `application/json`. |

{style="table-layout:auto"}