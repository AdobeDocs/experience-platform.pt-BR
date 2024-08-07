---
solution: Experience Platform
title: Segmentação do Edge usando a API
description: Este documento contém exemplos sobre como usar a segmentação de borda com a API de serviço de segmentação do Adobe Experience Platform.
role: Developer
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: 914174de797d7d5f6c47769d75380c0ce5685ee2
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 1%

---

# Segmentação de borda

>[!NOTE]
>
>O documento a seguir declara como executar a segmentação de borda usando a API. Para obter informações sobre como executar a segmentação de borda usando a interface, leia o [guia da interface de segmentação de borda](../ui/edge-segmentation.md).
>
>A segmentação do Edge agora está disponível para todos os usuários da Platform. Se você tiver criado definições de segmento de borda durante a versão beta, essas definições de segmento continuarão operacionais.

A segmentação do Edge é a capacidade de avaliar definições de segmento no Adobe Experience Platform instantaneamente na borda, permitindo casos de uso de personalização da mesma página e da próxima página.

>[!IMPORTANT]
>
> Os dados de borda serão armazenados em um local de servidor de borda mais próximo de onde foram coletados e podem ser armazenados em um local diferente daquele designado como data center do Adobe Experience Platform hub (ou principal).
>
> Além disso, o mecanismo de segmentação de borda só respeitará solicitações na borda em que há **uma** identidade principal marcada, que é consistente com identidades principais não baseadas em borda.

## Introdução

Este guia do desenvolvedor requer uma compreensão funcional dos vários serviços do [!DNL Adobe Experience Platform] envolvidos na segmentação de borda. Antes de iniciar este tutorial, revise a documentação dos seguintes serviços:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real, com base em dados agregados de múltiplas fontes.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): permite que você compile públicos a partir de dados de [!DNL Real-Time Customer Profile].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Platform] organiza os dados de experiência do cliente.

Para fazer chamadas com êxito para qualquer ponto de extremidade de API do Experience Platform, leia o manual sobre [introdução às APIs da plataforma](../../landing/api-guide.md) para saber mais sobre os cabeçalhos necessários e como ler chamadas de API de exemplo.

## Tipos de consulta de segmentação do Edge {#query-types}

Para que um segmento seja avaliado usando a segmentação de borda, a consulta deve estar em conformidade com as seguintes diretrizes:

| Tipo de consulta | Detalhes | Exemplo | Exemplo do PQL |
| ---------- | ------- | ------- | ----------- |
| Evento único | Qualquer definição de segmento que se refere a um único evento recebido sem restrição de tempo. | Pessoas que adicionaram um item ao carrinho. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| Perfil único | Qualquer definição de segmento que se refira a um único atributo somente de perfil | Pessoas que vivem nos EUA. | `homeAddress.countryCode = "US"` |
| Evento único que se refere a um perfil | Qualquer definição de segmento que se refira a um ou mais atributos de perfil e um único evento de entrada sem restrição de tempo. | Pessoas que moram nos EUA que visitaram a página inicial. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| Evento único negado com um atributo de perfil | Qualquer definição de segmento que se refira a um evento de entrada único negado e um ou mais atributos de perfil | Pessoas que vivem nos EUA e **não** visitaram a página inicial. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| Um único evento em uma janela de tempo | Qualquer definição de segmento que se refere a um único evento recebido em um período definido. | Pessoas que visitaram a página inicial nas últimas 24 horas. | `chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 24 hours before now)])` |
| Evento único com um atributo de perfil em uma janela de tempo relativa de menos de 24 horas | Qualquer definição de segmento que se refere a um único evento recebido, com um ou mais atributos de perfil, e ocorre em uma janela de tempo relativa de menos de 24 horas. | Pessoas que vivem nos EUA que visitaram a página inicial nas últimas 24 horas. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 24 hours before now)])` |
| Evento único negado com um atributo de perfil em uma janela de tempo | Qualquer definição de segmento que se refere a um ou mais atributos de perfil e um evento de entrada único negado em um período de tempo. | Pessoas que vivem nos EUA e **não** visitaram a página inicial nas últimas 24 horas. | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 24 hours before now)]))` |
| Evento de frequência em uma janela de tempo de 24 horas | Qualquer definição de segmento que se refere a um evento que ocorre um determinado número de vezes em uma janela de tempo de 24 horas. | Pessoas que visitaram a página inicial **pelo menos** cinco vezes nas últimas 24 horas. | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Evento de frequência com um atributo de perfil em uma janela de tempo de 24 horas | Qualquer definição de segmento que se refere a um ou mais atributos de perfil e um evento que ocorre um determinado número de vezes em uma janela de tempo de 24 horas. | Pessoas dos EUA que visitaram a página inicial **pelo menos** cinco vezes nas últimas 24 horas. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Evento de frequência negado com um perfil em uma janela de tempo de 24 horas | Qualquer definição de segmento que se refere a um ou mais atributos de perfil e um evento negado que ocorre um determinado número de vezes em uma janela de tempo de 24 horas. | Pessoas que não visitaram a página inicial **mais** do que cinco vezes nas últimas 24 horas. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| Várias ocorrências recebidas em um perfil de tempo de 24 horas | Qualquer definição de segmento que se refere a vários eventos que ocorrem em uma janela de tempo de 24 horas. | As pessoas que visitaram a página inicial **ou** visitaram a página de check-out nas últimas 24 horas. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Vários eventos com um perfil em uma janela de tempo de 24 horas | Qualquer definição de segmento que se refere a um ou mais atributos de perfil e vários eventos que ocorrem em uma janela de tempo de 24 horas. | Pessoas dos EUA que visitaram a página inicial **e** visitaram a página de check-out nas últimas 24 horas. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Segmento de segmentos | Qualquer definição de segmento que contenha um ou mais segmentos em lote ou de fluxo. | Pessoas que vivem nos EUA e estão no segmento &quot;segmento existente&quot;. | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| Consulta que se refere a um mapa | Qualquer definição de segmento que se refira a um mapa de propriedades. | Pessoas que foram adicionadas ao carrinho com base em dados de segmentos externos. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

Além disso, o segmento **deve** estar vinculado a uma política de mesclagem que esteja ativa na borda. Para obter mais informações sobre políticas de mesclagem, leia o [guia de políticas de mesclagem](../../profile/api/merge-policies.md).

Uma definição de segmento **não** será habilitada para segmentação de borda nos seguintes cenários:

- A definição de segmento inclui uma combinação de um único evento e um evento `inSegment`.
   - No entanto, se o segmento contido no evento `inSegment` for somente perfil, a definição de segmento **será habilitada para segmentação de borda.**
- A definição do segmento usa &quot;Ignorar ano&quot; como parte de suas restrições de tempo.

## Recuperar todos os segmentos habilitados para segmentação de borda

Você pode recuperar uma lista de todos os segmentos que estão habilitados para segmentação de borda em sua organização fazendo uma solicitação GET para o ponto de extremidade `/segment/definitions`.

**Formato da API**

Para recuperar segmentos habilitados para segmentação de borda, você deve incluir o parâmetro de consulta `evaluationInfo.synchronous.enabled=true` no caminho da solicitação.

```http
GET /segment/definitions?evaluationInfo.synchronous.enabled=true
```

**Solicitação**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.synchronous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma matriz de segmentos em sua organização que estão habilitados para segmentação de borda. Informações mais detalhadas sobre a definição de segmento retornada podem ser encontradas no [manual de ponto de extremidade de definições de segmento](./segment-definitions.md).

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
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

## Criar um segmento habilitado para segmentação de borda

Você pode criar um segmento habilitado para segmentação de borda fazendo uma solicitação POST para o ponto de extremidade `/segment/definitions` que corresponda a um dos [tipos de consulta de segmentação de borda listados acima](#query-types).

**Formato da API**

```http
POST /segment/definitions
```

**Solicitação**

>[!NOTE]
>
>O exemplo abaixo é uma solicitação padrão para criar um segmento. Para obter mais informações sobre como criar uma definição de segmento, leia o tutorial em [criando um segmento](../tutorials/create-a-segment.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'  \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.profile"
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
    }
}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da definição de segmento recém-criada que está habilitada para segmentação de borda.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{ORG_ID}",
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

Agora que você sabe como criar segmentos habilitados para segmentação de borda, pode usá-los para habilitar casos de uso de personalização de mesma página e próxima página.

Para saber como executar ações semelhantes e trabalhar com segmentos usando a interface do usuário do Adobe Experience Platform, visite o [guia do usuário do Construtor de segmentos](../ui/segment-builder.md).

## Apêndice

A seção a seguir lista as perguntas frequentes sobre a segmentação de borda:

### Quanto tempo leva para um segmento ficar disponível no Edge Network?

Leva até uma hora para um segmento estar disponível no Edge Network.