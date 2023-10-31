---
solution: Experience Platform
title: Guia da interface de segmentação de borda
description: Saiba como usar a segmentação de borda para avaliar definições de segmento na Platform instantaneamente na borda, permitindo casos de uso de personalização da mesma página e da próxima página.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 9f586b336f5cc232ac9b04a74846b7cfc2b46a71
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 0%

---

# Guia da interface de segmentação de borda

>[!NOTE]
>
>A segmentação de borda agora está disponível para todos os usuários da Platform. Se você tiver criado definições de segmento de borda durante a versão beta, essas definições de segmento continuarão operacionais.

A segmentação de borda é a capacidade de avaliar segmentos no Adobe Experience Platform instantaneamente [na borda](../../edge/home.md), permitindo casos de uso de personalização da mesma página e da próxima página.

>[!IMPORTANT]
>
> Os dados de borda serão armazenados em um local de servidor de borda mais próximo de onde foram coletados e podem ser armazenados em um local diferente daquele designado como data center do Adobe Experience Platform hub (ou principal).
>
> Além disso, o mecanismo de segmentação de borda somente respeitará as solicitações na borda em que há **um** identidade primária marcada, que é consistente com identidades primárias não baseadas em borda.

## Tipos de consulta de segmentação de borda {#query-types}

Atualmente, somente os tipos de consulta selecionados podem ser avaliados com a segmentação de borda. As seções a seguir fornecem uma lista de tipos de consulta que podem ser avaliados com a segmentação de borda e aqueles que não são compatíveis no momento.

Uma consulta pode ser avaliada com segmentação de borda se atender a qualquer um dos critérios descritos na tabela a seguir.

>[!NOTE]
>
>Se a consulta corresponder a qualquer um dos tipos de consulta na tabela a seguir, ela será avaliada automaticamente usando a segmentação de borda. O sistema determina essa capacidade automaticamente com base na expressão de consulta.

| Tipo de consulta | Detalhes | Exemplo | Exemplo de PQL |
| ---------- | ------- | ------- | ----------- |
| Evento único | Qualquer definição de segmento que se refere a um único evento recebido sem restrição de tempo. | Pessoas que adicionaram um item ao carrinho. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| Perfil único | Qualquer definição de segmento que se refira a um único atributo somente de perfil | Pessoas que vivem nos EUA. | `homeAddress.countryCode = "US"` |
| Evento único que se refere a um perfil | Qualquer definição de segmento que se refira a um ou mais atributos de perfil e um único evento de entrada sem restrição de tempo. | Pessoas que moram nos EUA que visitaram a página inicial. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")])` |
| Evento único negado com um atributo de perfil | Qualquer definição de segmento que se refira a um evento de entrada único negado e um ou mais atributos de perfil | As pessoas que vivem nos EUA e têm **não** visitou a página inicial. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| Um único evento em uma janela de tempo | Qualquer definição de segmento que se refere a um único evento recebido em um período definido. | Pessoas que visitaram a página inicial nas últimas 24 horas. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)])` |
| Evento único com um atributo de perfil em uma janela de tempo relativa de menos de 24 horas | Qualquer definição de segmento que se refere a um único evento recebido, com um ou mais atributos de perfil, e ocorre em uma janela de tempo relativa de menos de 24 horas. | Pessoas que vivem nos EUA que visitaram a página inicial nas últimas 24 horas. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)])` |
| Evento único negado com um atributo de perfil em uma janela de tempo | Qualquer definição de segmento que se refere a um ou mais atributos de perfil e um evento de entrada único negado em um período de tempo. | As pessoas que vivem nos EUA e têm **não** visitou a página inicial nas últimas 24 horas. | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)]))` |
| Evento de frequência em uma janela de tempo de 24 horas | Qualquer definição de segmento que se refere a um evento que ocorre um determinado número de vezes em uma janela de tempo de 24 horas. | Pessoas que visitaram a página inicial **pelo menos** cinco vezes nas últimas 24 horas. | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Evento de frequência com um atributo de perfil em uma janela de tempo de 24 horas | Qualquer definição de segmento que se refere a um ou mais atributos de perfil e um evento que ocorre um determinado número de vezes em uma janela de tempo de 24 horas. | Pessoas dos EUA que visitaram a página inicial **pelo menos** cinco vezes nas últimas 24 horas. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Evento de frequência negado com um perfil em uma janela de tempo de 24 horas | Qualquer definição de segmento que se refere a um ou mais atributos de perfil e um evento negado que ocorre um determinado número de vezes em uma janela de tempo de 24 horas. | Pessoas que não visitaram a página inicial **mais** cinco vezes nas últimas 24 horas. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| Várias ocorrências recebidas em um perfil de tempo de 24 horas | Qualquer definição de segmento que se refere a vários eventos que ocorrem em uma janela de tempo de 24 horas. | Pessoas que visitaram a página inicial **ou** visitou a página de check-out nas últimas 24 horas. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Vários eventos com um perfil em uma janela de tempo de 24 horas | Qualquer definição de segmento que se refere a um ou mais atributos de perfil e vários eventos que ocorrem em uma janela de tempo de 24 horas. | Pessoas dos EUA que visitaram a página inicial **e** visitou a página de check-out nas últimas 24 horas. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Segmento de segmentos | Qualquer definição de segmento que contenha um ou mais segmentos em lote ou de fluxo. | Pessoas que vivem nos EUA e estão no segmento &quot;segmento existente&quot;. | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| Consulta que se refere a um mapa | Qualquer definição de segmento que se refira a um mapa de propriedades. | Pessoas que foram adicionadas ao carrinho com base em dados de segmentos externos. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

Uma definição de segmento **não** ser ativado para segmentação de borda no seguinte cenário:

- A definição de segmento inclui uma combinação de um único evento e uma `inSegment` evento.
   - No entanto, se a definição de segmento contida na variável `inSegment` evento é somente perfil, a definição do segmento **irá** ser ativado para segmentação de borda.

## Próximas etapas

Este guia explica como avaliar definições de segmento com segmentação de borda no Adobe Experience Platform. Para saber mais sobre como usar a interface do usuário do Experience Platform, leia o [Guia do usuário de segmentação](./overview.md). Para saber como executar ações semelhantes e trabalhar com definições de segmento usando APIs Experience Platform, visite o [guia da API de segmentação de borda](../api/edge-segmentation.md).

## Apêndice

A seção a seguir lista as perguntas frequentes sobre a segmentação de borda:

### Quanto tempo leva para uma definição de segmento ficar disponível na Rede de borda?

Demora até uma hora para uma definição de segmento estar disponível na rede de borda.
