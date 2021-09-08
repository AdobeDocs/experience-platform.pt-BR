---
description: Esta página lista e descreve todas as operações da API que podem ser realizadas usando o endpoint da API `/authoring/testing/template/sample`, para obter um template de transformação de mensagem de teste para o seu destino.
title: Obter exemplos de operações da API de modelo
source-git-commit: 19307fba8f722babe5b6d57e80735ffde00fc851
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 2%

---

# Obter exemplo de operações da API de modelo {#get=sample-template-api-operations}

>[!IMPORTANT]
>
>**Ponto de extremidade** da API:  `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

Esta página lista e descreve todas as operações de API que você pode executar usando o endpoint da API `/authoring/testing/template/sample` para gerar um [template de transformação de mensagem](./message-format.md#using-templating) para o seu destino. Para obter uma descrição da funcionalidade suportada por este ponto de extremidade, leia [criar modelo](./create-template.md).

## Introdução às operações da API do modelo de amostra {#get-started}

Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com êxito, incluindo como obter a permissão de criação de destino necessária e os cabeçalhos necessários.

## Obter modelo de amostra {#generate-sample-template}

Você pode obter um modelo de amostra fazendo uma solicitação GET ao endpoint `authoring/testing/template/sample/` e fornecendo a ID de destino da configuração de destino com base na qual você está criando seu modelo.

>[!TIP]
>
>* A ID de destino que você deve usar aqui é a `instanceId` que corresponde a uma configuração de destino, criada usando o ponto de extremidade `/destinations`. Consulte a [referência da API de configuração de destino](./destination-configuration-api.md#retrieve-list).


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
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com um modelo de amostra que pode ser editado para corresponder ao formato de dados esperado.

Se a ID de destino fornecida corresponder a um modelo de servidor de destino com `maxUsersPerRequest=1`, a solicitação retornará um modelo de amostra semelhante a este:

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

Se a ID de destino fornecida corresponder a um modelo de servidor de destino com `maxUsersPerRequest` maior que um, a solicitação retornará um modelo de amostra semelhante a este:

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

Os pontos de extremidade da API do SDK de destino seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) e [erros do cabeçalho da solicitação](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas {#next-steps}

Depois de ler este documento, você agora sabe como gerar um template de transformação de mensagem usando o endpoint da API `/authoring/testing/template/sample`. Em seguida, você pode usar o [Renderizar ponto de extremidade da API de modelo](./render-template-api.md) para gerar perfis exportados com base no modelo e compará-los ao formato de dados esperado do destino.