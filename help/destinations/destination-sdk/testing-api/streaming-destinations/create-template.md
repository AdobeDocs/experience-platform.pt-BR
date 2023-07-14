---
description: Saiba como usar a API de teste de destino para testar seu modelo de transformação de mensagem de destino de transmissão antes de publicar o destino.
title: Criar e testar um modelo de transformação de mensagem
exl-id: 15e7f436-4d33-4172-bd14-ad8dfbd5e4a8
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 0%

---


# Criar e testar um modelo de transformação de mensagem {#create-template}

## Visão geral {#overview}

Como parte do Destination SDK, o Adobe fornece ferramentas de desenvolvedor para ajudá-lo a configurar e testar seu destino. Esta página descreve como criar e testar um modelo de transformação de mensagem. Para obter informações sobre como testar o destino, leia [Testar a configuração de destino](streaming-destination-testing-overview.md).

Para **criar e testar um modelo de transformação de mensagem** entre o schema de destino no Adobe Experience Platform e o formato de mensagem compatível com seu destino, use o *Ferramenta de criação de modelos* descrito mais adiante.  Leia mais sobre a transformação de dados entre o esquema de origem e de destino na [documento de formato de mensagem](../../functionality/destination-server/message-format.md#using-templating).

Veja abaixo como criar e testar um modelo de transformação de mensagem se encaixa nas [fluxo de trabalho de configuração de destino](../../guides/configure-destination-instructions.md) em Destination SDK:

![Gráfico de onde a etapa criar modelo se encaixa no fluxo de trabalho de configuração de destino](../../assets/testing-api/create-template-step.png)

## Por que você precisa criar e testar um template de transformação de mensagem {#why-create-message-transformation-template}

Uma das primeiras etapas na criação do seu destino no Destination SDK é pensar em como o formato de dados para associação de público-alvo, identidades e atributos de perfil é transformado quando exportado do Adobe Experience Platform para o seu destino. Encontre informações sobre a transformação entre o esquema XDM do Adobe e o esquema de destino na [documento de formato de mensagem](../../functionality/destination-server/message-format.md#using-templating).

Para que a transformação seja bem-sucedida, você deve fornecer um template de transformação, semelhante a este exemplo: [Criar um modelo que envia segmentos, identidades e atributos de perfil](../../functionality/destination-server/message-format.md#segments-identities-attributes).

O Adobe fornece uma ferramenta de modelo que permite criar e testar o modelo de mensagem que transforma os dados do formato XDM do Adobe no formato compatível com seu destino. A ferramenta tem dois endpoints de API que podem ser usados:

* Use o *exemplo de API de modelo* para obter um modelo de amostra.
* Use o *API de modelo de renderização* para renderizar o modelo de amostra para comparar o resultado com o formato de dados esperado do seu destino. Depois de comparar os dados exportados com o formato de dados esperado pelo seu destino, você pode editar o template. Dessa forma, os dados exportados gerados correspondem ao formato de dados esperado pelo destino.

## Etapas a serem concluídas antes de criar o modelo {#prerequisites}

Antes de estar pronto para criar o template, conclua as etapas abaixo:

1. [Criar uma configuração do servidor de destino](../../authoring-api/destination-server/create-destination-server.md). O template gerado é diferente com base no valor fornecido para o `maxUsersPerRequest` parâmetro.
   * Uso `maxUsersPerRequest=1` se você quiser que uma chamada de API para o seu destino inclua um único perfil, juntamente com suas qualificações de público-alvo, identidades e atributos de perfil.
   * Uso `maxUsersPerRequest` com um valor maior que um se você quiser que uma chamada de API para o seu destino inclua vários perfis, juntamente com suas qualificações de público-alvo, identidades e atributos de perfil.
2. [Criar uma configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md) e adicione a ID da configuração do servidor de destino em `destinationDelivery.destinationServerId`.
3. [Obter a ID da configuração de destino](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) que você acabou de criar, para que possa usá-lo na ferramenta de criação de template.
4. Compreender [quais funções e filtros você pode usar](../../functionality/destination-server/supported-functions.md) no template de transformação de mensagem.

## Como usar a API de modelo de amostra e a API de modelo de renderização para criar um modelo para o seu destino {#iterative-process}

>[!TIP]
>
>Antes de criar e editar o modelo de transformação de mensagem, você pode começar chamando o [ponto de extremidade da API do modelo de renderização](../../testing-api/streaming-destinations/render-template-api.md#render-exported-data) com um modelo simples que exporta seus perfis brutos sem aplicar transformações. A sintaxe do modelo simples é: <br> `"template": "{% for profile in input.profiles %}{{profile|raw}}{% endfor %}}"`

O processo para obter e testar o modelo é iterativo. Repita as etapas abaixo até que os perfis exportados correspondam ao formato de dados esperado do seu destino.

1. Primeiro, [obtenha um modelo de amostra](../../testing-api/streaming-destinations/create-template.md#sample-template-api).
2. Use o modelo de amostra como ponto de partida para criar seu próprio rascunho.
3. Chame o [ponto de extremidade da API do modelo de renderização](../../testing-api/streaming-destinations/create-template.md#render-template-api) com seu próprio modelo. O Adobe gera perfis de amostra com base no esquema e retorna o resultado ou quaisquer erros encontrados.
4. Compare os dados exportados com o formato de dados esperado pelo seu destino. Se necessário, edite o template.
5. Repita esse processo até que os perfis exportados correspondam ao formato de dados esperado do destino.

## Obter um modelo de amostra usando a API de modelo de amostra {#sample-template-api}

>[!NOTE]
>
>Para obter a documentação de referência completa da API, leia [Obter operações de API de modelo de amostra](../../testing-api/streaming-destinations/sample-template-api.md).

Adicione uma ID de destino à chamada, como mostrado abaixo, e a resposta retornará um exemplo de modelo correspondente à ID de destino.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

Se a ID de destino fornecida corresponder a uma configuração de destino com [agregação de melhor esforço](../../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) e `maxUsersPerRequest=1` na política de agregação, a solicitação retorna um template de amostra semelhante a este:

```python
{#- THIS is an example template for a single profile -#}
{#- A '-' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}
{
    "identities": [
    {%- for idMapEntry in input.profile.identityMap -%}
    {%- set namespace = idMapEntry.key -%}
        {%- for identity in idMapEntry.value %}
        {
            "type": "{{ namespace }}",
            "id": "{{ identity.id }}"
        }{%- if not loop.last -%},{%- endif -%}
        {%- endfor -%}{%- if not loop.last -%},{%- endif -%}
    {% endfor %}
    ],
    "AdobeExperiencePlatformSegments": {
        "add": [
        {%- for segment in input.profile.segmentMembership.ups | added %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ],
        "remove": [
        {#- Alternative syntax for filtering audiences by status: -#}
        {% for segment in removedSegments(input.profile.segmentMembership.ups) %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ]
    }
}
```

Se a ID de destino fornecida corresponder a um modelo de servidor de destino com [agregação configurável](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) ou [agregação de melhor esforço](../../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) com `maxUsersPerRequest` maior que um, a solicitação retorna um modelo de amostra semelhante a este:

```python
{#- THIS is an example template for multiple profiles -#}
{#- A '-' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}
{
    "profiles": [
    {%- for profile in input.profiles %}
        {
            "identities": [
            {%- for idMapEntry in profile.identityMap -%}
            {%- set namespace = idMapEntry.key -%}
                {%- for identity in idMapEntry.value %}
                {
                    "type": "{{ namespace }}",
                    "id": "{{ identity.id }}"
                }{%- if not loop.last -%},{%- endif -%}
                {%- endfor -%}{%- if not loop.last -%},{%- endif -%}
            {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                {%- for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
                {% endfor %}
                ],
                "remove": [
                {#- Alternative syntax for filtering audiences by status: -#}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
                {% endfor %}
                ]
            }
        }{%- if not loop.last -%},{%- endif -%}
    {% endfor %}
    ]
}
```

## Caractere de escape em seu modelo {#character-escape-template}

Antes de usar o modelo para renderizar perfis que correspondam ao formato esperado do destino, você deve usar o recurso de escape de caractere no modelo, conforme mostrado na gravação de tela abaixo.

![Vídeo que mostra como usar o recurso de escape de caracteres em um modelo usando uma ferramenta de escape de caracteres online](../../assets/testing-api/escape-characters.gif)

Você pode usar uma ferramenta de escape de caracteres online. A demonstração acima usa a variável [Formatador JSON Escape](https://jsonformatter.org/json-escape).

## API de modelo de renderização {#render-template-api}

Após criar um template de transformação de mensagem usando o [exemplo de API de modelo](create-template.md#sample-template-api), você pode [renderizar o modelo](render-template-api.md) para gerar dados exportados com base neles. Isso permite verificar se os perfis que o Adobe Experience Platform exportaria para seu destino correspondem ao formato esperado do destino.

Consulte a referência da API para obter exemplos de chamadas que você pode fazer:

* [Renderizar um modelo sem perfis enviados no corpo](render-template-api.md#multiple-profiles-no-body)
* [Renderizar um modelo com perfis enviados no corpo](render-template-api.md#multiple-profiles-with-body)

Edite o modelo e faça chamadas para o endpoint da API do modelo de renderização até que os perfis exportados correspondam ao formato de dados esperado do destino.

## Adicionar seu modelo com caractere de escape à configuração do servidor de destino

Quando estiver satisfeito com o modelo de transformação de mensagem, adicione-o ao [configuração do servidor de destino](../../authoring-api/destination-server/create-destination-server.md), em `httpTemplate.requestBody.value`.
