---
keywords: Experience Platform; home; tópicos populares; segmentação; Segmentação; Serviço de segmentação; Segmentação de borda; Segmentação de borda; borda de fluxo;
solution: Experience Platform
title: 'Segmentação de borda usando a API '
topic: guia do desenvolvedor
description: Este documento contém exemplos de como usar a segmentação de borda com a API do serviço de segmentação do Adobe Experience Platform.
exl-id: effce253-3d9b-43ab-b330-943fb196180f
translation-type: tm+mt
source-git-commit: 36169a42c7f6a73ca9cc165cd338d6a1cf245bfc
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 3%

---

# Segmentação de borda (beta)

>[!NOTE]
>
>O documento a seguir explica como executar a segmentação de borda usando a API . Para obter informações sobre como executar a segmentação de borda usando a interface do usuário, leia o [guia da interface do usuário de segmentação de borda](../ui/edge-segmentation.md). Além disso, a segmentação de borda está atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

A segmentação de borda é a capacidade de avaliar segmentos no Adobe Experience Platform instantaneamente na borda, permitindo casos de uso de personalização de página igual e próxima.

## Introdução

Este guia do desenvolvedor requer uma compreensão funcional dos vários serviços [!DNL Adobe Experience Platform] envolvidos com a segmentação de borda. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real, com base em dados agregados de várias fontes.
- [[!DNL Segmentation]](../home.md): Fornece a capacidade de criar segmentos e públicos-alvo a partir de seus  [!DNL Real-time Customer Profile] dados.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Platform] organiza os dados de experiência do cliente.

Para fazer chamadas com êxito para endpoints da API [!DNL Data Prep], leia o guia sobre a [introdução às APIs da plataforma](../../landing/api-guide.md) para saber mais sobre os cabeçalhos necessários e como ler chamadas de API de exemplo.

## Tipos de consulta de segmentação de borda {#query-types}

Para que um segmento seja avaliado usando a segmentação de borda, a query deve estar em conformidade com as seguintes diretrizes:

| Tipo de consulta | Detalhes |
| ---------- | ------- |
| Ocorrência de entrada | Qualquer definição de segmento que se refere a um único evento de entrada sem restrição de tempo. |
| Ocorrência recebida que se refere a um perfil | Qualquer definição de segmento que se refere a um único evento de entrada, sem restrição de tempo e um ou mais atributos de perfil. |
| Consulta de frequência | Qualquer definição de segmento que se refere a um evento que ocorre pelo menos um determinado número de vezes. |
| Consulta de frequência que se refere a um perfil | Qualquer definição de segmento que se refere a um evento que ocorre pelo menos um determinado número de vezes e tem um ou mais atributos de perfil. |

{style=&quot;table-layout:auto&quot;}

Os seguintes tipos de query são **não** suportados atualmente pela segmentação de borda:

| Tipo de consulta | Detalhes |
| ---------- | ------- |
| Janela de tempo relativo | Se uma consulta se refere a uma janela de tempo, ela não pode ser avaliada usando a segmentação de borda. |
| Negação | Se uma consulta tiver uma negação ou um evento `not`, ela não poderá ser avaliada usando a segmentação de borda. |
| Vários eventos | Se uma consulta contiver mais de um evento, ela não poderá ser avaliada usando a segmentação de borda. |

{style=&quot;table-layout:auto&quot;}

## Recuperar todos os segmentos ativados para a segmentação de borda

Você pode recuperar uma lista de todos os segmentos que são ativados para segmentação de borda na organização IMS fazendo uma solicitação de GET para o endpoint `/segment/definitions`.

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

Uma resposta bem-sucedida retorna uma matriz de segmentos na Organização IMS que são ativados para a segmentação de borda. Informações mais detalhadas sobre a definição de segmento retornada podem ser encontradas no [guia do ponto de extremidade das definições de segmento](./segment-definitions.md).

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

Você pode criar um segmento habilitado para a segmentação de borda, fazendo uma solicitação de POST para o endpoint `/segment/definitions`. Além de corresponder a um dos tipos de consulta de segmentação de borda [listados acima](#query-types), você deve definir o sinalizador `evaluationInfo.synchronous.enabled` no payload como true.

**Formato da API**

```http
POST /segment/definitions
```

**Solicitação**

>[!NOTE]
>
>O exemplo abaixo é uma solicitação padrão para criar um segmento. Para obter mais informações sobre como criar uma definição de segmento, leia o tutorial em [criar um segmento](../tutorials/create-a-segment.md).

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
    },
    "evaluationInfo": {
        "synchronous": {
            "enabled": true
        }
    }
}'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `evaluationInfo.synchronous.enabled` | O objeto `evaluationInfo` determina o tipo de avaliação pela qual a definição de segmento será submetida. Para usar a segmentação de borda, defina `evaluationInfo.synchronous.enabled` com um valor de `true`. |

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
```

## Próximas etapas

Agora que você sabe como criar segmentos com segmentação de borda, pode usá-los para ativar casos de uso de personalização de mesma página e próxima página.

Para saber como executar ações semelhantes e trabalhar com segmentos usando a interface do usuário do Adobe Experience Platform, visite o [Guia do usuário do Construtor de segmentos](../ui/segment-builder.md).
