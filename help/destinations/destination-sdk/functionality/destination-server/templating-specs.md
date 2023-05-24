---
description: Saiba como formatar as solicitações HTTP enviadas para seu endpoint. Use o endpoint /authoring/destination-servers para configurar as especificações dos modelos de servidor de destino no Adobe Experience Platform Destination SDK.
title: Especificações de modelos para destinos criados com o Destination SDK
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 4%

---


# Especificações de modelo para destinos criados com o Destination SDK

Use a parte de especificação do modelo da configuração do servidor de destino para definir como formatar as solicitações HTTP enviadas para o seu destino.

Em uma especificação de modelo, é possível definir como transformar campos de atributo de perfil entre o esquema XDM e o formato compatível com sua plataforma.

As especificações do modelo fazem parte da configuração do servidor de destino para destinos em tempo real (transmissão).

Para entender onde esse componente se encaixa em uma integração criada com o Destination SDK, consulte o diagrama no [opções de configuração](../configuration-options.md) ou consulte o guia sobre como [usar o Destination SDK para configurar um destino de transmissão](../../guides/configure-destination-instructions.md#create-server-template-configuration).

Você pode configurar as especificações do modelo para seu destino por meio da `/authoring/destination-servers` terminal. Consulte as seguintes páginas de referência de API para obter exemplos detalhados de chamadas de API, onde é possível configurar os componentes mostrados nesta página.

* [Criar uma configuração do servidor de destino](../../authoring-api/destination-server/create-destination-server.md)
* [Atualizar uma configuração do servidor de destino](../../authoring-api/destination-server/update-destination-server.md)

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros compatíveis com o Destination SDK são **diferencia maiúsculas de minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações suportam a funcionalidade descrita nesta página.

| Tipo de integração | Suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Sim |
| Integrações baseadas em arquivo (lote) | Não |

## Configurar uma especificação de modelo {#configure-template-spec}

Adobe usa uma linguagem de modelo semelhante a [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) para transformar os campos do esquema XDM em um formato compatível com seu destino.

![Configuração de modelo realçada](../../assets/functionality/destination-server/template-configuration.png)

Para obter mais informações sobre a transformação, visite os links abaixo:

* [Formato de mensagem](message-format.md)
* [Uso de uma linguagem de modelo para as transformações de identidade, atributos e associação de segmento ](message-format.md#using-templating)

>[!TIP]
>
>Adobe oferece um [ferramenta de desenvolvedor](../../testing-api/streaming-destinations/create-template.md) que ajudam a criar e testar um template de transformação de mensagem.

Veja abaixo um exemplo de um modelo de solicitação HTTP, juntamente com descrições de cada parâmetro individual.

```json
{
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
| `httpMethod` | String | *Obrigatório.* O método que o Adobe usará nas chamadas para o servidor. Métodos compatíveis: `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `value` | String | *Obrigatório.* Essa string é a versão sem caracteres do modelo que formata as solicitações HTTP enviadas pela Platform no formato esperado pelo seu destino. <br> Para obter informações sobre como gravar o modelo, leia a seção sobre [uso de modelos](message-format.md#using-templating). <br> Para obter mais informações sobre o escape de caracteres, consulte o [RFC JSON padrão, seção sete](https://tools.ietf.org/html/rfc8259#section-7). <br> Para obter um exemplo de uma transformação simples, consulte [atributos de perfil](message-format.md#attributes) transformação. |
| `contentType` | String | *Obrigatório.* O tipo de conteúdo que seu servidor aceita. Dependendo do tipo de saída produzido pelo seu modelo de transformação, essa variável pode ser qualquer uma das [Tipos de conteúdo do aplicativo HTTP](https://www.iana.org/assignments/media-types/media-types.xhtml#application). Na maioria dos casos, esse valor deve ser definido como `application/json`. |

{style="table-layout:auto"}

## Próximas etapas {#next-steps}

Depois de ler este artigo, você terá que entender melhor o que é uma especificação de modelo e como configurá-la.

Para saber mais sobre os outros componentes do servidor de destino, consulte os seguintes artigos:

* [Especificações do servidor para destinos criados com o Destination SDK](server-specs.md)
* [Formato de mensagem](message-format.md)
* [Configuração da formatação de arquivo](file-formatting.md)