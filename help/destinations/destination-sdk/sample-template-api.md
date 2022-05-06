---
description: Esta página lista e descreve todas as operações da API que podem ser realizadas usando o endpoint da API `/authoring/testing/template/sample`, para obter um template de transformação de mensagem de teste para o seu destino.
title: Obter exemplos de operações da API de modelo
exl-id: d18a06f7-0c3a-4b4d-a7d5-011690d00e2c
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 2%

---

# Obter exemplos de operações da API de modelo {#get=sample-template-api-operations}

>[!IMPORTANT]
>
>**Ponto de extremidade da API**: `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

Esta página lista e descreve todas as operações de API que você pode executar usando o `/authoring/testing/template/sample` endpoint da API, para gerar um [modelo de transformação de mensagem](./message-format.md#using-templating) para o seu destino. Para obter uma descrição da funcionalidade suportada por este ponto de extremidade, leia [criar modelo](./create-template.md).

## Introdução às operações da API do modelo de amostra {#get-started}

Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com sucesso, incluindo como obter a permissão de criação de destino necessária e os cabeçalhos necessários.

## Obter modelo de amostra {#generate-sample-template}

Você pode obter um modelo de amostra fazendo uma solicitação do GET para a variável `authoring/testing/template/sample/` endpoint e fornecer a ID de destino da configuração de destino com base na qual você está criando o modelo.

>[!TIP]
>
>* A ID de destino que você deve usar aqui é a variável `instanceId` que corresponde a uma configuração de destino, criada usando o `/destinations` endpoint . Consulte a [referência da API de configuração de destino](./destination-configuration-api.md#retrieve-list).


**Formato da API**


```http
GET authoring/testing/template/sample/{DESTINATION_ID}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{DESTINATION_ID}` | A ID da configuração de destino para a qual você está gerando um template de transformação de mensagem. |

**Solicitação**

A solicitação a seguir gera um novo modelo de amostra, configurado pelos parâmetros fornecidos no payload.

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

Uma resposta bem-sucedida retorna o status HTTP 200 com um modelo de amostra que pode ser editado para corresponder ao formato de dados esperado.

Se a ID de destino fornecida corresponder a uma configuração de destino com [melhor agregação de esforço](./destination-configuration.md#best-effort-aggregation) e `maxUsersPerRequest=1` na política de agregação, a solicitação retorna um template de amostra semelhante a este:

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

Se a ID de destino fornecida corresponder a um modelo de servidor de destino com [agregação configurável](./destination-configuration.md#configurable-aggregation) ou [melhor agregação de esforço](./destination-configuration.md#best-effort-aggregation) com `maxUsersPerRequest` maior que um, a solicitação retorna um template de amostra semelhante a este:

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

## Tratamento de erros da API {#api-error-handling}

Os pontos de extremidade da API do Destination SDK seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](../../landing/troubleshooting.md#api-status-codes) e [erros do cabeçalho da solicitação](../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas {#next-steps}

Depois de ler este documento, você agora sabe gerar um template de transformação de mensagem usando o `/authoring/testing/template/sample` Ponto de extremidade da API. Em seguida, você pode usar o [Ponto de extremidade da API do modelo de renderização](./render-template-api.md) para gerar perfis exportados com base no modelo e compará-los com o formato de dados esperado do destino.
