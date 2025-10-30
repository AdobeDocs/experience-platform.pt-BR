---
description: Saiba como formatar as solicitações HTTP enviadas para seu endpoint. Use o endpoint /authoring/destination-servers para configurar as especificações dos modelos de servidor de destino no Adobe Experience Platform Destination SDK.
title: Especificações de modelos para destinos criados com o Destination SDK
exl-id: 066781c8-0af0-4958-b62f-194c6ba13f3a
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 2%

---

# Especificações de modelo para destinos criados com o Destination SDK

Use a parte de especificação do modelo da configuração do servidor de destino para definir como formatar as solicitações HTTP enviadas para o seu destino.

Em uma especificação de modelo, é possível definir como transformar campos de atributo de perfil entre o esquema XDM e o formato compatível com sua plataforma.

As especificações do modelo fazem parte da configuração do servidor de destino para destinos em tempo real (transmissão).

Para entender onde esse componente se encaixa em uma integração criada com o Destination SDK, consulte o diagrama na documentação de [opções de configuração](../configuration-options.md) ou consulte o guia sobre como [usar o Destination SDK para configurar um destino de streaming](../../guides/configure-destination-instructions.md#create-server-template-configuration).

Você pode configurar as especificações do modelo para o seu destino por meio do ponto de extremidade `/authoring/destination-servers`. Consulte as seguintes páginas de referência de API para obter exemplos detalhados de chamadas de API, onde é possível configurar os componentes mostrados nesta página.

* [Criar uma configuração do servidor de destino](../../authoring-api/destination-server/create-destination-server.md)
* [Atualizar uma configuração do servidor de destino](../../authoring-api/destination-server/update-destination-server.md)

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros com suporte do Destination SDK diferenciam maiúsculas de minúsculas **1}.** Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações suportam a funcionalidade descrita nesta página.

| Tipo de integração | Suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Sim |
| Integrações baseadas em arquivo (lote) | Não |

## Configurar uma especificação de modelo {#configure-template-spec}

O Adobe usa uma linguagem de modelo semelhante a [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) para transformar os campos do esquema XDM em um formato compatível com seu destino.

![Configuração do modelo realçada](../../assets/functionality/destination-server/template-configuration.png)

Para obter mais informações sobre a transformação, visite os links abaixo:

* [Formato da mensagem](message-format.md)
* [Uso de uma linguagem de modelo para as transformações de identidade, atributos e associação de público](message-format.md#using-templating)

>[!TIP]
>
>O Adobe oferece uma [ferramenta de desenvolvedor](../../testing-api/streaming-destinations/create-template.md) que ajuda você a criar e testar um modelo de transformação de mensagem.

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
| `httpMethod` | String | *Obrigatório.* O método que o Adobe usará nas chamadas para o servidor. Métodos com suporte: `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `value` | String | *Obrigatório.* Esta cadeia de caracteres é a versão sem caracteres do modelo que formata as solicitações HTTP enviadas pelo Experience Platform no formato esperado pelo seu destino. <br> Para obter informações sobre como gravar o modelo, leia a seção sobre [usando o modelo](message-format.md#using-templating). <br> Para obter mais informações sobre o escape de caracteres, consulte o [padrão RFC JSON, seção sete](https://tools.ietf.org/html/rfc8259#section-7). <br> Para obter um exemplo de uma transformação simples, consulte a transformação [atributos de perfil](message-format.md#attributes). |
| `contentType` | String | *Obrigatório.* O tipo de conteúdo que seu servidor aceita. Dependendo do tipo de saída produzido pelo seu modelo de transformação, pode ser qualquer um dos [tipos de conteúdo de aplicativo HTTP](https://www.iana.org/assignments/media-types/media-types.xhtml#application) com suporte. Na maioria dos casos, esse valor deve ser definido como `application/json`. |

{style="table-layout:auto"}

## Próximas etapas {#next-steps}

Depois de ler este artigo, você terá que entender melhor o que é uma especificação de modelo e como configurá-la.

Para saber mais sobre os outros componentes do servidor de destino, consulte os seguintes artigos:

* [Especificações do servidor para destinos criados com o Destination SDK](server-specs.md)
* [Formato da mensagem](message-format.md)
* [Configuração da formatação de arquivo](file-formatting.md)
