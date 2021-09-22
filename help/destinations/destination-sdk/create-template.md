---
description: Como parte do SDK de destino, o Adobe fornece ferramentas de desenvolvedor para ajudá-lo a configurar e testar seu destino. Esta página descreve como criar e testar um template de transformação de mensagem.
title: Criar e testar um modelo de transformação de mensagem
exl-id: 15e7f436-4d33-4172-bd14-ad8dfbd5e4a8
source-git-commit: 2ed132cd16db64b5921c5632445956f750fead56
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 0%

---

# Criar e testar um modelo de transformação de mensagem {#create-template}

## Visão geral {#overview}

Como parte do SDK de destino, o Adobe fornece ferramentas de desenvolvedor para ajudá-lo a configurar e testar seu destino. Esta página descreve como criar e testar um template de transformação de mensagem. Para obter informações sobre como testar seu destino, leia [Testar sua configuração de destino](./test-destination.md).

Para **criar e testar um template de transformação de mensagem** entre o schema de destino no Adobe Experience Platform e o formato de mensagem compatível com seu destino, use a *Ferramenta de criação de modelo* descrita mais abaixo.  Leia mais sobre a transformação de dados entre o schema de origem e de destino no [documento de formato de mensagem](./message-format.md#using-templating).

A ilustração abaixo mostra como criar e testar um modelo de transformação de mensagem se encaixa no [fluxo de trabalho de configuração de destino](./configure-destination-instructions.md) no SDK de destino:

![Gráfico de onde a etapa criar modelo se encaixa no fluxo de trabalho de configuração de destino](./assets/create-template-step.png)

## Por que você precisa criar e testar um template de transformação de mensagem {#why-create-message-transformation-template}

Uma das primeiras etapas ao criar seu destino no SDK de destino é pensar em como o formato de dados para associação de segmento, identidades e atributos de perfil é transformado quando exportado do Adobe Experience Platform para seu destino. Encontre informações sobre a transformação entre o esquema Adobe XDM e o esquema de destino no [documento de formato de mensagem](./message-format.md#using-templating).

Para que a transformação seja bem-sucedida, é necessário fornecer um template de transformação, semelhante ao deste exemplo: [Crie um modelo que envie segmentos, identidades e atributos de perfil](./message-format.md#segments-identities-attributes).

O Adobe fornece uma ferramenta de modelo que permite criar e testar o modelo de mensagem que transforma dados do formato Adobe XDM no formato compatível com seu destino. A ferramenta tem dois pontos de extremidade de API que podem ser usados:
* Use a *API de modelo de amostra* para obter um modelo de amostra.
* Use a *API do modelo de renderização* para renderizar o modelo de amostra e comparar o resultado com o formato de dados esperado do seu destino. Depois de comparar os dados exportados com o formato de dados esperado pelo seu destino, você pode editar o modelo. Dessa forma, os dados exportados gerados correspondem ao formato de dados esperado pelo destino.

## Como usar a API de modelo de amostra e a API de modelo de renderização para criar um modelo para o seu destino {#iterative-process}

O processo para obter e testar o modelo é iterativo. Repita as etapas abaixo até que os perfis exportados correspondam ao formato de dados esperado do seu destino.

1. Primeiro, [obtenha um modelo de amostra](./create-template.md#sample-template-api).
2. Use o modelo de amostra como ponto de partida para criar um rascunho próprio.
3. Chame o [ponto de extremidade da API do modelo de renderização](./create-template.md#render-template-api) com seu próprio modelo. O Adobe gera perfis de amostra com base no esquema e retorna o resultado ou qualquer erro encontrado.
4. Compare os dados exportados com o formato de dados esperado pelo seu destino. Se necessário, edite o modelo .
5. Repita esse processo até que os perfis exportados correspondam ao formato de dados esperado do destino.

## Etapas a serem concluídas antes de criar o modelo {#prerequisites}

Antes de estar pronto para criar o template, complete as etapas abaixo:

1. [Crie uma configuração](./destination-server-api.md) de servidor de destino. O modelo que você gerará será diferente, com base no valor fornecido para o parâmetro `maxUsersPerRequest`.
   * Use `maxUsersPerRequest=1` se quiser que uma chamada de API para seu destino inclua um único perfil, juntamente com suas qualificações de segmento, identidades e atributos de perfil.
   * Use `maxUsersPerRequest` com um valor maior que um se quiser que uma chamada de API para seu destino inclua vários perfis, juntamente com suas qualificações de segmento, identidades e atributos de perfil.
2. [Crie uma ](./destination-configuration-api.md#create) configuração de destino e adicione a ID da configuração do servidor de destino em  `destinationDelivery.destinationServerId`.
3. [Obtenha a ID da ](./destination-configuration-api.md#retrieve-list) configuração de destino que você acabou de criar para poder usá-la na ferramenta de criação de modelo.

## Obter um modelo de amostra usando a API do modelo de amostra {#sample-template-api}

>[!NOTE]
>
>Para obter a documentação completa de referência da API, leia [Obter operações da API do modelo de amostra](./sample-template-api.md).

Adicione uma ID de destino à chamada, conforme mostrado abaixo, e a resposta retornará um exemplo de modelo correspondente à ID de destino.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

Se a ID de destino fornecida corresponder a uma configuração de destino com [melhor agregação de esforço](./destination-configuration.md#best-effort-aggregation) e `maxUsersPerRequest=1` na política de agregação, a solicitação retornará um modelo de amostra semelhante a este:

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
        {#- Alternative syntax for filtering segments by status: -#}
        {% for segment in removedSegments(input.profile.segmentMembership.ups) %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ]
    }
}
```

Se a ID de destino fornecida corresponder a um modelo de servidor de destino com [agregação configurável](./destination-configuration.md#configurable-aggregation) ou [melhor agregação de esforço](./destination-configuration.md#best-effort-aggregation) com `maxUsersPerRequest` maior que um, a solicitação retornará um modelo de amostra semelhante a este:

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
                {#- Alternative syntax for filtering segments by status: -#}
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

## Esqueça o modelo {#character-escape-template}

Antes de usar o modelo para renderizar perfis que correspondam ao formato esperado do seu destino, você deve usar o caractere escape do modelo, como mostrado na gravação de tela abaixo.

![Vídeo que mostra como evitar caracteres em um modelo usando uma ferramenta de escape de caractere online](./assets/escape-characters.gif)

Você pode usar uma ferramenta de escape de caracteres online. A demonstração acima usa o [JSON Escape formatter](https://jsonformatter.org/json-escape).

## API do modelo de renderização {#render-template-api}

Depois de criar um template de transformação de mensagem usando a [API de modelo de amostra](./create-template.md#sample-template-api), você pode [renderizar o template](./render-template-api.md) para gerar dados exportados com base nele. Isso permite verificar se os perfis que o Adobe Experience Platform exportaria para o seu destino correspondem ao formato esperado do seu destino.

Consulte a referência da API para obter exemplos de chamadas que você pode fazer:

* [Renderizar um modelo sem perfis enviados no corpo](./render-template-api.md#multiple-profiles-no-body)
* [Renderizar um modelo com perfis enviados no corpo](./render-template-api.md#multiple-profiles-with-body)

Edite o modelo e faça chamadas para o endpoint da API do modelo de renderização até que os perfis exportados correspondam ao formato de dados esperado do seu destino.

## Adicionar seu modelo de escape de caractere à configuração do servidor de destino

Quando estiver satisfeito com seu template de transformação de mensagem, adicione-o à [configuração do servidor de destino](./server-and-template-configuration.md), em `httpTemplate.requestBody.value`.
