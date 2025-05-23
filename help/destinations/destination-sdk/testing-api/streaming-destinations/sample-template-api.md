---
description: Saiba como usar a API de teste de destino para gerar um modelo de transformação de mensagem de teste para seu destino.
title: Gerar um modelo de transformação de mensagem de amostra
exl-id: d18a06f7-0c3a-4b4d-a7d5-011690d00e2c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 2%

---


# Gerar um modelo de transformação de mensagem de amostra {#get-sample-template-api-operations}

>[!IMPORTANT]
>
>**Ponto de extremidade de API**: `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

Esta página lista e descreve todas as operações de API que você pode executar usando o ponto de extremidade de API `/authoring/testing/template/sample` para gerar um [modelo de transformação de mensagem](../../functionality/destination-server/message-format.md#using-templating) para o seu destino. Para obter uma descrição da funcionalidade com suporte neste ponto de extremidade, leia [criar modelo](create-template.md).

## Introdução às operações de amostra de API de modelo {#get-started}

Antes de continuar, consulte o [guia de introdução](../../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Obter modelo de amostra {#generate-sample-template}

Você pode obter um modelo de exemplo fazendo uma solicitação GET para o ponto de extremidade `authoring/testing/template/sample/` e fornecendo a ID de destino da configuração de destino com base na qual você está criando seu modelo.

>[!TIP]
>
>* A ID de destino que você deve usar aqui é o `instanceId` que corresponde a uma configuração de destino, criada usando o ponto de extremidade `/destinations`. Consulte [recuperar uma configuração de destino](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) para obter mais detalhes.

**Formato da API**

```http
GET authoring/testing/template/sample/{DESTINATION_ID}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{DESTINATION_ID}` | A ID da configuração de destino para a qual você está gerando um modelo de transformação de mensagem. |

**Solicitação**

A solicitação a seguir gera um novo modelo de amostra, configurado pelos parâmetros fornecidos na carga.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com um modelo de amostra que você pode editar para corresponder ao formato de dados esperado.

Se a ID de destino fornecida corresponder a uma configuração de destino com [agregação de melhor esforço](../../functionality/destination-configuration/aggregation-policy.md) e `maxUsersPerRequest=1` na política de agregação, a solicitação retornará um modelo de exemplo semelhante a este:

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

Se a ID de destino fornecida corresponder a um modelo de servidor de destino com [agregação configurável](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) ou [agregação de melhor esforço](../../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) com `maxUsersPerRequest` maior que um, a solicitação retornará um modelo de exemplo semelhante a este:

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

## Manipulação de erros de API {#api-error-handling}

Os endpoints da API do Destination SDK seguem os princípios gerais de mensagem de erro da API do Experience Platform. Consulte [códigos de status da API](../../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas do Experience Platform.

## Próximas etapas {#next-steps}

Depois de ler este documento, agora você sabe como gerar um modelo de transformação de mensagem usando o endpoint da API `/authoring/testing/template/sample`. Em seguida, você pode usar o [Renderizar ponto de extremidade de API do modelo](render-template-api.md) para gerar perfis exportados com base no modelo e compará-los com o formato de dados esperado do destino.
