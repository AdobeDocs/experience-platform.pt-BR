---
description: Saiba como formatar as solicitações HTTP enviadas para o terminal. Use o endpoint /authoring/destination-servers para configurar as especificações de modelos do servidor de destino no Adobe Experience Platform Destination SDK.
title: Especificações de modelo para destinos criados com o Destination SDK
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 4%

---


# Especificações de modelo para destinos criados com o Destination SDK

Use a parte de especificação do modelo da configuração do servidor de destino para configurar como formatar as solicitações HTTP enviadas para seu destino.

Em uma especificação de modelo, você pode definir como transformar campos de atributo de perfil entre o esquema XDM e o formato compatível com a plataforma.

As especificações do modelo são parte da configuração do servidor de destino para destinos em tempo real (streaming).

Para entender onde esse componente se encaixa em uma integração criada com o Destination SDK, consulte o diagrama no [opções de configuração](../configuration-options.md) ou consulte o guia sobre como [use o Destination SDK para configurar um destino de transmissão](../../guides/configure-destination-instructions.md#create-server-template-configuration).

Você pode configurar as especificações do modelo para seu destino por meio da variável `/authoring/destination-servers` endpoint . Consulte as páginas de referência da API a seguir para obter exemplos detalhados de chamadas de API, onde é possível configurar os componentes mostrados nesta página.

* [Criar uma configuração de servidor de destino](../../authoring-api/destination-server/create-destination-server.md)
* [Atualizar uma configuração de servidor de destino](../../authoring-api/destination-server/update-destination-server.md)

>[!IMPORTANT]
>
>Todos os nomes de parâmetros e valores suportados pelo Destination SDK são **distinção entre maiúsculas e minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações oferecem suporte à funcionalidade descrita nesta página.

| Tipo de integração | Oferece suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Sim |
| Integrações baseadas em arquivo (em lote) | Não |

## Configurar uma especificação de modelo {#configure-template-spec}

O Adobe usa uma linguagem de modelo semelhante a [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) para transformar os campos do esquema XDM em um formato compatível com seu destino.

![Configuração do modelo realçada](../../assets/functionality/destination-server/template-configuration.png)

Para obter mais informações sobre a transformação, visite os links abaixo:

* [Formato de mensagem](message-format.md)
* [Uso de uma linguagem de modelo para as transformações de identidade, atributos e associação de segmento ](message-format.md#using-templating)

>[!TIP]
>
>O Adobe oferece um [ferramenta desenvolvedor](../../testing-api/streaming-destinations/create-template.md) isso ajuda a criar e testar um template de transformação de mensagem.

Veja abaixo um exemplo de um template de solicitação HTTP, juntamente com descrições de cada parâmetro individual.

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
| `httpMethod` | String | *Obrigatório.* O método que o Adobe usará nas chamadas para o seu servidor. Métodos suportados: `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `value` | String | *Obrigatório.* Essa é a versão do modelo com escape de caracteres que formata as solicitações HTTP enviadas pela Platform no formato esperado pelo seu destino. <br> Para obter informações sobre como gravar o modelo, leia a seção em [uso de modelos](message-format.md#using-templating). <br> Para obter mais informações sobre o escape de caracteres, consulte [Padrão RFC JSON, seção sete](https://tools.ietf.org/html/rfc8259#section-7). <br> Para obter um exemplo de transformação simples, consulte [atributos do perfil](message-format.md#attributes) transformação. |
| `contentType` | String | *Obrigatório.* O tipo de conteúdo que seu servidor aceita. Dependendo do tipo de saída produzido pelo modelo de transformação, isso pode ser qualquer um dos [Tipos de conteúdo do aplicativo HTTP](https://www.iana.org/assignments/media-types/media-types.xhtml#application). Na maioria dos casos, esse valor deve ser definido como `application/json`. |

{style="table-layout:auto"}

## Próximas etapas {#next-steps}

Após ler este artigo, você deve ter uma melhor compreensão do que é uma especificação de modelo e como configurá-la.

Para saber mais sobre os outros componentes do servidor de destino, consulte os seguintes artigos:

* [Especificações do servidor para destinos criados com o Destination SDK](server-specs.md)
* [Formato de mensagem](message-format.md)
* [Configuração de formatação de arquivo](file-formatting.md)