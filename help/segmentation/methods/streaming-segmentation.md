---
solution: Experience Platform
title: Guia de segmentação de streaming
description: Saiba mais sobre a segmentação por transmissão, incluindo o que é, como criar um público avaliado usando a segmentação por transmissão e como visualizar seus públicos criados usando a segmentação por transmissão.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: c009eb89331758c512abd8ff7ef185489063b48f
workflow-type: tm+mt
source-wordcount: '2051'
ht-degree: 3%

---

# Guia de segmentação de transmissão

>[!BEGINSHADEBOX]

>[!NOTE]
>
>Os critérios de qualificação de segmentação por transmissão foram atualizados em 20 de maio de 2025.

+++Atualizações de qualificação

>[!IMPORTANT]
>
>Todas as definições de segmento existentes que são avaliadas usando a segmentação de transmissão ou de borda continuarão funcionando como estão, a menos que sejam editadas ou atualizadas.

## Conjunto de regras {#ruleset}

Qualquer definição de segmento **nova ou editada** que corresponda aos conjuntos de regras a seguir **não será mais avaliada** usando streaming ou segmentação de borda. Em vez disso, eles serão avaliados usando a segmentação em lote.

- Um único evento com uma janela de tempo superior a 24 horas
   - Ative um público com todos os perfis que visualizaram uma página da Web nos últimos 3 dias.
- Um único evento sem janela de tempo
   - Ative um público com todos os perfis que visualizaram uma página da Web.

## Janela de tempo {#time-window}

Para avaliar um público com segmentação por transmissão, ele **deve** ser restrito em uma janela de tempo de 24 horas.

## Inclusão de dados em lote em públicos de transmissão {#include-batch-data}

>[!NOTE]
>
>Para manter a segmentação de transmissão precisa ao usar dados em lote, verifique se os dados em lote são **somente** mantidos dentro do público-alvo do lote e se são referenciados dentro do público-alvo de transmissão.

Antes dessa atualização, você poderia criar uma definição de público-alvo de transmissão que combinasse fontes de dados de lote e de transmissão. No entanto, com a atualização mais recente, a criação de um público-alvo com fontes de dados em lote e de transmissão será avaliada usando a segmentação em lote.

Se for necessário avaliar uma definição de segmento usando a segmentação de borda ou transmissão que corresponda ao conjunto de regras atualizado, será necessário criar explicitamente um lote e um conjunto de regras de transmissão e combiná-los usando o segmento de segmentos. Este conjunto de regras em lotes **deve** ser baseado em um esquema de perfil.

Por exemplo, digamos que você tenha dois públicos-alvo, com um público-alvo hospedando dados do esquema de perfil e o outro hospedando dados do esquema de evento de experiência:

| Público-alvo | Esquema | Tipo de Source | Definição de consulta | ID do público-alvo |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Residentes da Califórnia | Perfil | Lote | O endereço residencial é no estado da Califórnia | `e3be6d7f-1727-401f-a41e-c296b45f607a` |
| Check-outs recentes | Evento de experiência | Transmissão | Tem pelo menos um check-out nas últimas 24 horas | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

Se você quiser usar o componente de lote no público-alvo de transmissão, será necessário fazer uma referência ao público-alvo em lote usando o segmento de segmentos.

Assim, um conjunto de regras de exemplo que combinasse os dois públicos-alvo seria semelhante a:

```
inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and 
CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) 
WHEN(<= 24 hours before now)])
```

O público-alvo resultante *será avaliado* usando a segmentação por transmissão, pois ela aproveita a associação do público-alvo em lote referindo-se ao componente de público-alvo em lote.

No entanto, se você quiser combinar dois públicos-alvo com dados de evento, **não poderá** apenas combinar os dois eventos. Você precisará criar ambos os públicos e, em seguida, criar outro público que use o `inSegment` para se referir a esses dois públicos.

Por exemplo, digamos que você tenha dois públicos-alvo, com ambos os públicos-alvo abrigando dados do esquema do evento de experiência:

| Público-alvo | Esquema | Tipo de Source | Definição de consulta | ID do público-alvo |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Desistências recentes | Evento de experiência | Lote | Tem pelo menos um evento de abandono nas últimas 24 horas | `e3be6d7f-1727-401f-a41e-c296b45f607a` |
| Check-outs recentes | Evento de experiência | Transmissão | Tem pelo menos um check-out nas últimas 24 horas | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

Nessa situação, seria necessário criar um terceiro público-alvo da seguinte maneira:

```
inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and inSegment("9e1646bb-57ff-4309-ba59-17d6c5bab6a1")
```

>[!IMPORTANT]
>
>Todas as definições de segmento existentes que correspondem aos conjuntos de regras permanecerão avaliadas usando a segmentação de transmissão ou de borda até serem editadas.
>
>Além disso, todas as definições de segmento existentes que atualmente atendem aos outros critérios de avaliação de transmissão ou segmentação de borda permanecerão avaliadas com a transmissão ou segmentação de borda.

## Política de mesclagem {#merge-policy}

Todas as definições de segmento **novas ou editadas** qualificadas para streaming ou segmentação de borda **devem** estar na política de mesclagem &quot;Ativo no Edge&quot;.

Se não houver uma política de mesclagem ativa definida, você precisará [configurar sua política de mesclagem](../../profile/merge-policies/ui-guide.md#configure) e configurá-la para estar ativa na borda.


+++

>[!ENDSHADEBOX]

A segmentação de transmissão é a capacidade de avaliar públicos-alvo no Adobe Experience Platform em tempo quase real, concentrando-se na riqueza de dados.

Com a segmentação por transmissão, a qualificação de público-alvo agora acontece à medida que os dados de transmissão chegam ao Experience Platform, reduzindo a necessidade de agendar e executar trabalhos de segmentação. Isso permite avaliar os dados conforme eles são transmitidos para o Experience Platform, permitindo que a associação do público-alvo seja mantida atualizada automaticamente.

## Conjuntos de regras elegíveis {#rulesets}

>[!IMPORTANT]
>
>Para usar a segmentação por transmissão, você **deve** usar uma política de mesclagem que esteja &quot;Ativa no Edge&quot;. Para obter mais informações sobre políticas de mesclagem, leia a [visão geral das políticas de mesclagem](../../profile/merge-policies/overview.md).

Um conjunto de regras será elegível para segmentação por transmissão se atender a qualquer um dos critérios descritos na tabela a seguir.

>[!NOTE]
>
>Para que a segmentação por transmissão funcione, é necessário habilitar a segmentação agendada para a organização. Para obter detalhes sobre como habilitar a segmentação agendada, consulte [a visão geral do Portal de público-alvo](../ui/audience-portal.md#scheduled-segmentation).

| Tipo de consulta | Detalhes | Consulta | Exemplo |
| ---------- | ------- | ----- | ------- |
| Evento único em uma janela de tempo de menos de 24 horas | Qualquer definição de segmento que se refira a um único evento recebido em uma janela de tempo de menos de 24 horas. | `CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![Um exemplo de um único evento em uma janela de tempo relativa é mostrado.](../images/methods/streaming/single-event.png) |
| Somente perfil | Qualquer definição de segmento que se refere apenas a um atributo de perfil. | `homeAddress.country.equals("US", false)` | ![Um exemplo de um atributo de perfil mostrado.](../images/methods/streaming/profile-attribute.png) |
| Evento único com um atributo de perfil em uma janela de tempo relativa de menos de 24 horas | Qualquer definição de segmento que se refere a um único evento recebido, com um ou mais atributos de perfil, e ocorre em uma janela de tempo relativa de menos de 24 horas. | `workAddress.country.equals("US", false) and CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![Um exemplo de um único evento com um atributo de perfil em uma janela de tempo relativa é mostrado.](../images/methods/streaming/single-event-with-profile-attribute.png) |
| Vários eventos em uma janela de tempo relativa de 24 horas | Qualquer definição de segmento que se refere a vários eventos **nas últimas 24 horas** e (opcionalmente) tem um ou mais atributos de perfil. | `workAddress.country.equals("US", false) and CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("directMarketing.emailClicked", false)) WHEN(today), C1: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![Um exemplo de vários eventos com um atributo de perfil é mostrado.](../images/methods/streaming/multiple-events-with-profile-attribute.png) |

Uma definição de segmento **não** estará qualificada para segmentação por transmissão nos seguintes cenários:

- A definição do segmento inclui segmentos ou características do Adobe Audience Manager (AAM).
- A definição do segmento inclui várias entidades (consultas de várias entidades).
- A definição de segmento inclui uma combinação de um único evento e um evento `inSegment`.
   - Por exemplo, encadear o seguinte em um único conjunto de regras: `inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and  CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false))  WHEN(<= 24 hours before now)])`.
- A definição do segmento usa &quot;Ignorar ano&quot; como parte de suas restrições de tempo.

Observe as diretrizes a seguir que se aplicam às consultas de segmentação por transmissão:

| Tipo de consulta | Diretriz |
| ---------- | -------- |
| Conjunto de regras de evento único | A janela de pesquisa é limitada a **um dia**. |
| Consulta com histórico de eventos | <ul><li>A janela de pesquisa é limitada a **um dia**.</li><li>Uma condição estrita de ordenação de tempo **deve** existe entre os eventos.</li><li>Há suporte para consultas com pelo menos um evento negado. No entanto, o evento inteiro **não pode** ser uma negação.</li></ul> |

Se uma definição de segmento for modificada para não atender mais aos critérios de segmentação por transmissão, a definição de segmento mudará automaticamente de &quot;Transmissão&quot; para &quot;Lote&quot;.

Além disso, a desqualificação de segmentos, semelhante à qualificação de segmentos, acontece em tempo real. Como resultado, se um público-alvo não se qualificar mais para um segmento, ele será imediatamente desqualificado. Por exemplo, se a definição do segmento solicitar &quot;Todos os usuários que compraram sapatos vermelhos nas últimas três horas&quot;, após três horas, todos os perfis que se qualificaram inicialmente para a definição do segmento serão desqualificados.

### Combinar públicos {#combine-audiences}

Para combinar dados de fontes de lote e de transmissão, será necessário separar os componentes de lote e transmissão em públicos separados.

### Atributo de perfil e evento de experiência {#profile-and-event}

Por exemplo, vamos considerar os dois seguintes públicos-alvo de amostra:

| Público-alvo | Esquema | Tipo de Source | Definição de consulta | ID do público-alvo |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Residentes da Califórnia | Perfil | Lote | O endereço residencial é no estado da Califórnia | `e3be6d7f-1727-401f-a41e-c296b45f607a` |
| Check-outs recentes | Evento de experiência | Transmissão | Tem pelo menos um check-out nas últimas 24 horas | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

Se você quiser usar o componente de lote no público-alvo de transmissão, será necessário fazer uma referência ao público-alvo em lote usando o segmento de segmentos.

Assim, um conjunto de regras de exemplo que combinasse os dois públicos-alvo seria semelhante a:

```
inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and 
CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) 
WHEN(<= 24 hours before now)])
```

O público-alvo resultante *será avaliado* usando a segmentação por transmissão, pois ela aproveita a associação do público-alvo em lote referindo-se ao componente de público-alvo em lote.

### Vários eventos de experiência {#two-events}

Se você deseja combinar vários públicos com dados do evento, **não pode** apenas combinar os eventos. Você precisará criar um público-alvo para cada evento e, em seguida, criar outro público-alvo que use `inSegment` para fazer referência a todos os públicos-alvo.

Por exemplo, digamos que você tenha dois públicos-alvo, com ambos os públicos-alvo abrigando dados do esquema do evento de experiência:

| Público-alvo | Esquema | Tipo de Source | Definição de consulta | ID do público-alvo |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Desistências recentes | Evento de experiência | Lote | Tem pelo menos um evento de abandono nas últimas 48 horas | `7deb246a-49b4-4687-95f9-6316df049948` |
| Check-outs recentes | Evento de experiência | Transmissão | Tem pelo menos um check-out nas últimas 24 horas | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

Nessa situação, seria necessário criar um terceiro público-alvo da seguinte maneira:

```
inSegment("7deb246a-49b4-4687-95f9-6316df049948) and inSegment("9e1646bb-57ff-4309-ba59-17d6c5bab6a1")
```

## Criar público-alvo {#create-audience}

Você pode criar um público-alvo que seja avaliado usando a segmentação por transmissão usando a API do Serviço de segmentação ou o Audience Portal na interface.

Uma definição de segmento pode ser habilitada para streaming se corresponder a um dos [conjuntos de regras qualificados](#eligible-rulesets).

>[!BEGINTABS]

>[!TAB API do serviço de segmentação]

**Formato da API**

```http
POST /segment/definitions
```

**Solicitação**

+++ Um exemplo de solicitação para criar uma definição de segmento habilitada para segmentação por transmissão

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
                "enabled": false
            },
            "continuous": {
                "enabled": true
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

+++Um exemplo de resposta ao criar uma definição de segmento.

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
            "enabled": false
        },
        "continuous": {
            "enabled": true
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

![O botão Criar público-alvo está realçado no Portal de Público-Alvo.](../images/methods/streaming/select-create-audience.png)

Um popover é exibido. Selecione **[!UICONTROL Regras de compilação]** para entrar no Construtor de segmentos.

![O botão Criar regras está realçado no popover Criar público-alvo.](../images/methods/streaming/select-build-rules.png)

No Construtor de segmentos, crie uma definição de segmento que corresponda a um dos [conjuntos de regras qualificados](#eligible-rulesets). Se a definição do segmento se qualificar para segmentação por transmissão, você poderá selecionar **[!UICONTROL Streaming]** como o **[!UICONTROL Método de avaliação]**.

![A definição de segmento é exibida. O tipo de avaliação está realçado, mostrando que a definição de segmento pode ser avaliada usando a segmentação por transmissão.](../images/methods/streaming/streaming-evaluation-method.png)

Para saber mais sobre como criar definições de segmento, leia o [Guia do Construtor de segmentos](../ui/segment-builder.md)

>[!ENDTABS]

## Recuperar públicos-alvo {#retrieve-audiences}

Você pode recuperar todos os públicos-alvo avaliados por meio da segmentação por transmissão usando a API do serviço de segmentação ou o Audience Portal na interface do usuário.

>[!BEGINTABS]

>[!TAB API do serviço de segmentação]

Recupere uma lista de todas as definições de segmento que são avaliadas usando a segmentação por transmissão na organização fazendo uma solicitação GET para o ponto de extremidade `/segment/definitions`.

**Formato da API**

Você deve incluir o parâmetro de consulta `evaluationInfo.synchronous.enabled=true` no caminho da solicitação para recuperar definições de segmento avaliadas usando a segmentação de transmissão.

```http
GET /segment/definitions?evaluationInfo.continuous.enabled=true
```

**Solicitação**

+++ Um exemplo de solicitação para listar todas as definições de segmento habilitadas para streaming

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.continuous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma matriz de definições de segmento na organização que estão habilitadas para segmentação por transmissão.

+++Um exemplo de resposta que contém uma lista de todas as definições de segmento habilitadas para segmentação por transmissão na organização

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
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
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

Você pode recuperar todos os públicos-alvo que estão ativados para segmentação por transmissão na organização usando filtros no Portal de público-alvo. Selecione o ícone ![filtro](../../images/icons/filter.png) para exibir a lista de filtros.

![O ícone de filtro está realçado no Audience Portal.](../images/methods/filter-audiences.png)

Nos filtros disponíveis, vá para **[!UICONTROL Atualizar frequência]** e selecione &quot;[!UICONTROL Streaming]&quot;. Usar esse filtro exibe todos os públicos-alvo em sua organização que são avaliados usando a segmentação por transmissão.

![A frequência de atualização de streaming está selecionada, exibindo todos os públicos-alvo na organização que são avaliados por meio da segmentação de streaming.](../images/methods/streaming/filter-streaming.png)

Para saber mais sobre como exibir públicos-alvo no Experience Platform, leia o [Guia do Portal de Público-Alvo](../ui/audience-portal.md).

>[!ENDTABS]

## Detalhes do público-alvo {#audience-details}

Você pode exibir detalhes de um público-alvo específico avaliado usando a segmentação por transmissão ao selecioná-lo no Portal de público-alvo.

Depois de selecionar um público no Audience Portal, a página de detalhes do público é exibida. Isso exibe informações sobre o público-alvo, incluindo um resumo dos detalhes do público-alvo, a quantidade de perfis qualificados ao longo do tempo, bem como os destinos para os quais o público-alvo foi ativado.

![A página de detalhes do público-alvo é exibida para um público avaliado por meio da segmentação por transmissão.](../images/methods/streaming/audience-details.png)

Para públicos habilitados para transmissão, o cartão **[!UICONTROL Perfis ao longo do tempo]** é exibido, mostrando o total de métricas qualificadas e o novo público atualizado.

A métrica **[!UICONTROL Total qualificado]** representa o número total de públicos qualificados, com base nas avaliações em lote e de fluxo para esse público.

A métrica **[!UICONTROL Novo público atualizado]** é representada por um gráfico de linha que mostra a alteração no tamanho do público-alvo por meio da segmentação por transmissão. Você pode ajustar a lista suspensa para mostrar as últimas 24 horas, a última semana ou os últimos 30 dias.

![Os perfis no cartão de ponto estão realçados.](../images/methods/streaming/profiles-over-time.png)

Para obter mais detalhes sobre detalhes do público-alvo, leia a [Visão geral do Portal de público-alvo](../ui/audience-portal.md#audience-details).

## Próximas etapas

Este guia explica como as definições de segmento habilitadas para streaming funcionam no Adobe Experience Platform e como monitorar definições de segmento habilitadas para streaming.

Para saber mais sobre como usar a interface do usuário do Adobe Experience Platform, leia o [Guia do usuário de segmentação](./overview.md).

Para perguntas frequentes sobre a segmentação por transmissão, leia a [seção segmentação por transmissão das Perguntas frequentes](../faq.md#streaming-segmentation).
