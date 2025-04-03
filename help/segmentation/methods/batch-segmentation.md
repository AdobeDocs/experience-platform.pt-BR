---
title: Guia de segmentação em lote
description: Saiba mais sobre a segmentação em lote, incluindo o que é, como criar um público-alvo avaliado usando a segmentação em lote e como visualizar os públicos-alvo criados usando a segmentação em lote.
exl-id: b6fba2fb-8eec-4429-92fd-ece5c79d379d
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 2%

---

# Guia de segmentação em lote

A segmentação em lote é um método de avaliação de segmentação que permite mover os dados do perfil de uma só vez para criar públicos correspondentes.

Com a segmentação em lote, você pode criar públicos-alvo detalhados e avançados e executar trabalhos de segmentação para determinar quando deseja que esses dados sejam propagados para serviços downstream.

## Tipos de consulta elegíveis {#query-types}

Todas as consultas são qualificadas para segmentação em lote.

## Criar público-alvo {#create-audience}

Você pode criar um público-alvo que seja avaliado usando a segmentação em lote, com a API do Serviço de segmentação ou por meio do Portal de público-alvo na interface.

>[!BEGINTABS]

>[!TAB API do serviço de segmentação]

**Formato da API**

```http
POST /segment/definitions
```

**Solicitação**

+++ Um exemplo de solicitação para criar uma definição de segmento que esteja ativada para segmentação em lote

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People in the USA",
        "description: "An audience that looks for people who live in the USA",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "homeAddress.country = \"US\""
        },
        "evaluationInfo": {
            "batch": {
                "enabled": true
            },
            "continuous": {
                "enabled": false
            },
            "synchronous": {
                "enabled": false
            }
        },
        "schema": {
            "name": "_xdm.context.profile"
        }
     }'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da definição de segmento recém-criada.

+++Uma resposta de amostra ao criar uma definição de segmento.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People in the USA",
    "description": "An audience that looks for people who live in the USA",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "homeAddress.country = \"US\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

+++

Mais informações sobre como usar este ponto de extremidade podem ser encontradas no [manual do ponto de extremidade de definição de segmento](../api/segment-definitions.md).

>[!TAB Portal de público-alvo]

No Portal de Público, selecione **[!UICONTROL Criar público-alvo]**.

![O botão Criar público-alvo está realçado no Portal de Público-Alvo.](../images/methods/batch/select-create-audience.png)

Um popover é exibido. Selecione **[!UICONTROL Regras de compilação]** para entrar no Construtor de segmentos.

![O botão Criar regras está realçado no popover Criar público-alvo.](../images/methods/batch/select-build-rules.png)

Depois de criar a definição de segmento, selecione **[!UICONTROL Lote]** como o **[!UICONTROL Método de avaliação]**.

![A definição de segmento é exibida. O tipo de avaliação está realçado, mostrando que a definição de segmento pode ser avaliada usando a segmentação por transmissão.](../images/methods/batch/batch-evaluation-method.png)

Para saber mais sobre como criar definições de segmento, leia o [Guia do Construtor de segmentos](../ui/segment-builder.md)

>[!ENDTABS]

## Recuperar públicos-alvo {#retrieve-audiences}

Você pode recuperar todos os públicos-alvo avaliados por meio da segmentação em lote, usando a API do serviço de segmentação ou o Audience Portal na interface do usuário.

>[!BEGINTABS]

>[!TAB API do serviço de segmentação]

Recupere uma lista de todas as definições de segmento que são avaliadas usando a segmentação em lote em sua organização fazendo uma solicitação GET para o ponto de extremidade `/segment/definitions`.

**Formato da API**

Você deve incluir o parâmetro de consulta `evaluationInfo.batch.enabled=true` no caminho da solicitação para recuperar definições de segmento avaliadas usando a segmentação em lote.

```http
GET /segment/definitions?evaluationInfo.batch.enabled=true
```

**Solicitação**

+++ Um exemplo de solicitação para listar todas as definições de segmento habilitadas para lote

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.batch.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma matriz de definições de segmento na organização que são avaliadas usando a segmentação em lote.

+++Uma resposta de amostra que contém uma lista de todas as definições de segmento avaliadas por segmentação em lote em sua organização

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": " People who are NOT on their homepage ",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = false"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572029711000,
            "updateEpoch": 1572029712000,
            "updateTime": 1572029712000
        },
        {
            "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "Homepage_continuous",
            "description": "People who are on their homepage - continuous",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572021085000,
            "updateEpoch": 1572021086000,
            "updateTime": 1572021086000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

Informações mais detalhadas sobre a definição de segmento retornada podem ser encontradas no [manual de ponto de extremidade de definições de segmento](../api/segment-definitions.md).

+++

>[!TAB Portal de público-alvo]

Você pode recuperar todos os públicos-alvo que estão ativados para segmentação em lote em sua organização usando filtros no Portal de público-alvo. Selecione o ícone ![filtro](../../images/icons/filter.png) para exibir a lista de filtros.

![O ícone de filtro está realçado no Audience Portal.](../images/methods/filter-audiences.png)

Nos filtros disponíveis, vá para **[!UICONTROL Atualizar frequência]** e selecione &quot;[!UICONTROL Lote]&quot;. O uso desse filtro exibe todos os públicos-alvo na organização que são avaliados usando a segmentação em lote.

![A frequência de atualização em lote está selecionada, exibindo todos os públicos-alvo na organização que são avaliados usando a segmentação em lote.](../images/methods/batch/filter-batch.png)

Para saber mais sobre como exibir públicos-alvo no Experience Platform, leia o [Guia do Portal de Público-Alvo](../ui/audience-portal.md).

>[!ENDTABS]

## Próximas etapas

Este guia explica como criar uma definição de segmento que possa ser avaliada usando a segmentação em lote no Adobe Experience Platform.

Para saber mais sobre como usar a interface do usuário do Experience Platform, leia o [Guia do usuário de segmentação](../ui/overview.md).

Para perguntas frequentes sobre a segmentação em lote, leia a [seção segmentação em lote das Perguntas frequentes](../faq.md#batch-segmentation).
