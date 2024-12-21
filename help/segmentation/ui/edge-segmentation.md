---
solution: Experience Platform
title: Guia da interface de segmentação do Edge
description: Saiba como usar a segmentação de borda para avaliar definições de segmento na Platform instantaneamente na borda, permitindo casos de uso de personalização da mesma página e da próxima página.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 828a586f0264147676da5c43c73d3b3b9d50b9c2
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---

# Guia da interface de segmentação de borda

>[!NOTE]
>
>A segmentação do Edge agora está disponível para todos os usuários da Platform. Se você tiver criado definições de segmento de borda durante a versão beta, essas definições de segmento continuarão operacionais.

A segmentação do Edge é a capacidade de avaliar segmentos no Adobe Experience Platform instantaneamente [na borda](../../web-sdk/home.md), permitindo casos de uso de personalização da mesma página e da próxima página.

>[!IMPORTANT]
>
> Os dados de borda serão armazenados em um local de servidor de borda mais próximo de onde foram coletados e podem ser armazenados em um local diferente daquele designado como data center do Adobe Experience Platform hub (ou principal).
>
> Além disso, o mecanismo de segmentação de borda só respeitará solicitações na borda em que há **uma** identidade principal marcada, que é consistente com identidades principais não baseadas em borda.

## Tipos de consulta de segmentação do Edge {#query-types}

Atualmente, somente os tipos de consulta selecionados podem ser avaliados com a segmentação de borda. As seções a seguir fornecem uma lista de tipos de consulta que podem ser avaliados com a segmentação de borda e aqueles que não são compatíveis no momento.

Uma consulta pode ser avaliada com segmentação de borda se atender a qualquer um dos critérios descritos na tabela a seguir.

>[!NOTE]
>
>Se a consulta corresponder a qualquer um dos tipos de consulta na tabela a seguir, ela será avaliada automaticamente usando a segmentação de borda. O sistema determina essa capacidade automaticamente com base na expressão de consulta.

| Tipo de consulta | Detalhes |
| ---------- | ------- |
| Evento único | Qualquer definição de segmento que se refere a um único evento recebido sem restrição de tempo. |
| Evento único em uma janela de tempo relativa | Qualquer definição de segmento que se refere a um único evento de entrada. |
| Evento único com uma janela de tempo | Qualquer definição de segmento que se refere a um único evento recebido com uma janela de tempo. |
| Somente perfil | Qualquer definição de segmento que se refere apenas a um atributo de perfil. |
| Evento único com um atributo de perfil em uma janela de tempo relativa de menos de 24 horas | Qualquer definição de segmento que se refere a um único evento recebido, com um ou mais atributos de perfil, e ocorre em uma janela de tempo relativa de menos de 24 horas. |
| Segmento de segmentos | Qualquer definição de segmento que contenha uma ou mais definições de segmento de lote ou transmissão. **Observação:** se o segmento de segmentos for usado com definições de segmento do **lote**, a desqualificação de perfil poderá levar **até 24 horas** para ocorrer. Se o segmento de segmentos for usado com **streaming** definições de segmento, a desqualificação de perfil ocorrerá de maneira streaming. |
| Vários eventos com um atributo de perfil | Qualquer definição de segmento que se refere a vários eventos não sequenciais **nas últimas 24 horas** e (opcionalmente) tem um ou mais atributos de perfil. |

Uma definição de segmento **não** será habilitada para segmentação de borda no seguinte cenário:

- A definição de segmento inclui uma combinação de um único evento e um evento `inSegment`.
   - No entanto, se a definição de segmento contida no evento `inSegment` for somente perfil, a definição de segmento **será habilitada para segmentação de borda.**
- A definição do segmento usa &quot;Ignorar ano&quot; como parte de suas restrições de tempo.

## Próximas etapas

Este guia explica como avaliar definições de segmento com segmentação de borda no Adobe Experience Platform. Para saber mais sobre como usar a interface do usuário do Experience Platform, leia o [Guia do usuário de segmentação](./overview.md). Para saber como executar ações semelhantes e trabalhar com definições de segmento usando APIs de Experience Platform, visite o [guia da API de segmentação de borda](../api/edge-segmentation.md).

## Apêndice

A seção a seguir lista as perguntas frequentes sobre a segmentação de borda:

### Quanto tempo leva para uma definição de segmento ficar disponível no Edge Network?

Leva até uma hora para uma definição de segmento estar disponível no Edge Network.
