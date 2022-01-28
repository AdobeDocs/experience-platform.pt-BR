---
keywords: Experience Platform; home; tópicos populares; segmentação; Segmentação; Serviço de segmentação; Segmentação de borda; Segmentação de borda; borda de fluxo;
solution: Experience Platform
title: 'Segmentação de borda usando a API '
topic-legacy: developer guide
description: Este documento contém exemplos de como usar a segmentação de borda com a API do serviço de segmentação do Adobe Experience Platform.
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: e52aa55adde532d838d5417feba36913ed03ce29
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 1%

---

# Segmentação de borda

>[!NOTE]
>
>O documento a seguir explica como executar a segmentação de borda usando a API . Para obter informações sobre como executar a segmentação de borda usando a interface do usuário, leia o [guia da interface do usuário de segmentação de borda](../ui/edge-segmentation.md).
>
>A segmentação de borda agora está disponível para todos os usuários da plataforma. Se você criou segmentos de borda durante o beta, esses segmentos continuarão operacionais.

A segmentação de borda é a capacidade de avaliar segmentos no Adobe Experience Platform instantaneamente na borda, permitindo casos de uso de personalização de página igual e próxima.

>[!IMPORTANT]
>
> Os dados de borda serão armazenados em um local de servidor de borda mais próximo de onde foram coletados e podem ser armazenados em um local diferente daquele designado como o data center (ou principal) da Adobe Experience Platform.
>
> Além disso, o mecanismo de segmentação de borda só atenderá às solicitações na borda em que houver **one** identidade primária marcada, que é consistente com identidades primárias não baseadas em borda.

## Introdução

Este guia do desenvolvedor requer uma compreensão funcional das várias [!DNL Adobe Experience Platform] serviços envolvidos com a segmentação de borda. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real, com base em dados agregados de várias fontes.
- [[!DNL Segmentation]](../home.md): Fornece a capacidade de criar segmentos e públicos-alvo a partir de [!DNL Real-time Customer Profile] dados.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): O quadro normalizado pelo qual [!DNL Platform] organiza os dados de experiência do cliente.

Para fazer chamadas com êxito para qualquer endpoint da API do Experience Platform, leia o guia em [introdução às APIs do Platform](../../landing/api-guide.md) para saber mais sobre os cabeçalhos necessários e como ler chamadas de API de exemplo.

## Tipos de query de segmentação de borda {#query-types}

Para que um segmento seja avaliado usando a segmentação de borda, a query deve estar em conformidade com as seguintes diretrizes:

| Tipo de consulta | Detalhes | Exemplo |
| ---------- | ------- | ------- |
| Evento único | Qualquer definição de segmento que se refere a um único evento de entrada sem restrição de tempo. | Pessoas que adicionaram um item ao carrinho. |
| Evento único que se refere a um perfil | Qualquer definição de segmento que se refere a um ou mais atributos de perfil e um único evento de entrada sem restrição de tempo. | Pessoas que vivem nos EUA que visitaram a página inicial. |
| Evento único negado com um atributo de perfil | Qualquer definição de segmento que se refere a um evento de entrada único negado e um ou mais atributos de perfil | Pessoas que vivem nos EUA e têm **not** visitou a página inicial. |
| Evento único em uma janela de 24 horas | Qualquer definição de segmento que se refere a um único evento de entrada em 24 horas. | Pessoas que visitaram a página inicial nas últimas 24 horas. |
| Evento único com um atributo de perfil dentro de uma janela de tempo de 24 horas | Qualquer definição de segmento que se refere a um ou mais atributos de perfil e um evento de entrada único negado em 24 horas. | Pessoas que vivem nos EUA que visitaram a página inicial nas últimas 24 horas. |
| Evento único negado com um atributo de perfil dentro de uma janela de tempo de 24 horas | Qualquer definição de segmento que se refere a um ou mais atributos de perfil e um evento de entrada único negado em 24 horas. | Pessoas que vivem nos EUA e têm **not** visitou a página inicial nas últimas 24 horas. |
| Evento de frequência dentro de um período de 24 horas | Qualquer definição de segmento que se refere a um evento que ocorre um determinado número de vezes em uma janela de tempo de 24 horas. | Pessoas que visitaram a página inicial **pelo menos** cinco vezes nas últimas 24 horas. |
| Evento de frequência com um atributo de perfil dentro de uma janela de tempo de 24 horas | Qualquer definição de segmento que se refere a um ou mais atributos de perfil e um evento que ocorre um determinado número de vezes em uma janela de tempo de 24 horas. | Pessoas dos EUA que visitaram a página inicial **pelo menos** cinco vezes nas últimas 24 horas. |
| Evento de frequência negado com um perfil dentro de uma janela de tempo de 24 horas | Qualquer definição de segmento que se refere a um ou mais atributos de perfil e um evento negado que ocorre um determinado número de vezes em uma janela de tempo de 24 horas. | Pessoas que não visitaram a página inicial **more** mais de cinco vezes nas últimas 24 horas. |
| Várias ocorrências recebidas em um perfil de tempo de 24 horas | Qualquer definição de segmento que se refere a vários eventos que ocorrem dentro de uma janela de tempo de 24 horas. | Pessoas que visitaram a página inicial **ou** visitou a página de checkout nas últimas 24 horas. |
| Vários eventos com um perfil em uma janela de 24 horas | Qualquer definição de segmento que se refere a um ou mais atributos de perfil e vários eventos que ocorrem dentro de uma janela de tempo de 24 horas. | Pessoas dos EUA que visitaram a página inicial **e** visitou a página de checkout nas últimas 24 horas. |

Além disso, o segmento **must** estar vinculado a uma política de mesclagem ativa no Edge. Para obter mais informações sobre as políticas de mesclagem, leia o [guia de políticas de mesclagem](../../profile/api/merge-policies.md).

## Recuperar todos os segmentos ativados para a segmentação de borda

Você pode recuperar uma lista de todos os segmentos que são ativados para a segmentação de borda em sua Organização IMS fazendo uma solicitação de GET para a `/segment/definitions` endpoint .

**Formato da API**

Para recuperar segmentos ativados para segmentação de borda, você deve incluir o parâmetro de consulta `evaluationInfo.synchronous.enabled=true` no caminho da solicitação.

```http
GET /segment/definitions?evaluationInfo.synchronous.enabled=true
```

**Solicitação**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.synchronous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma matriz de segmentos na Organização IMS que são ativados para a segmentação de borda. Informações mais detalhadas sobre a definição de segmento retornada podem ser encontradas no [guia do endpoint de definições de segmento](./segment-definitions.md).

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
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
                    "enabled": false
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": true
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
            "imsOrgId": "{IMS_ORG_ID}",
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
                    "enabled": false
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": true
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

## Criar um segmento que esteja habilitado para a segmentação de borda

Você pode criar um segmento habilitado para a segmentação de borda, fazendo uma solicitação de POST para a `/segment/definitions` endpoint que corresponde a uma das [tipos de consulta de segmentação de borda listados acima](#query-types).

**Formato da API**

```http
POST /segment/definitions
```

**Solicitação**

>[!NOTE]
>
>O exemplo abaixo é uma solicitação padrão para criar um segmento. Para obter mais informações sobre como criar uma definição de segmento, leia o tutorial em [criação de um segmento](../tutorials/create-a-segment.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'  \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    }
}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da definição de segmento recém-criada que é habilitada para a segmentação de borda.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "chain(xEvent, timestamp, [X: WHAT(var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = "true")])"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": true
        }
    },
    "creationTime": 1572021085000,
    "updateEpoch": 1572021086000,
    "updateTime": 1572021086000
}
```

## Próximas etapas

Agora que você sabe como criar segmentos com segmentação de borda, pode usá-los para ativar casos de uso de personalização de mesma página e próxima página.

Para saber como executar ações semelhantes e trabalhar com segmentos usando a interface do usuário do Adobe Experience Platform, visite o [Guia do usuário do Construtor de segmentos](../ui/segment-builder.md).
