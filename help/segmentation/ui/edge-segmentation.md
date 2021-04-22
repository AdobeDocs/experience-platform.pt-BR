---
keywords: Experience Platform, home, tópicos populares, segmentação de borda, Segmentação, Serviço de segmentação, serviço de segmentação, guia da interface do usuário, borda de fluxo;
solution: Experience Platform
title: Guia da interface do usuário de segmentação de borda
topic-legacy: ui guide
description: A segmentação de borda é a capacidade de avaliar segmentos na Platform instantaneamente na borda, permitindo casos de uso de personalização de página da mesma página e da próxima página.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
translation-type: tm+mt
source-git-commit: 5256c2a13fc75f7d46911f2ad368188d9e818921
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 4%

---

# Guia da interface de usuário de segmentação de borda (beta)

>[!NOTE]
>
>A segmentação de borda está atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

A segmentação de borda é a capacidade de avaliar segmentos no Adobe Experience Platform instantaneamente na borda, permitindo casos de uso de personalização de página igual e próxima.

## Tipos de query de segmentação de borda

Um query pode ser avaliado com segmentação de borda se atender a qualquer um dos seguintes critérios:

| Tipo de consulta | Detalhes | Exemplo |
| ---------- | ------- | ------- |
| Ocorrência de entrada | Qualquer definição de segmento que se refere a um único evento de entrada sem restrição de tempo. | ![](../images/ui/edge-segmentation/incoming-hit.png) |
| Ocorrência recebida que se refere a um perfil | Qualquer definição de segmento que se refere a um único evento de entrada, sem restrição de tempo e um ou mais atributos de perfil. | ![](../images/ui/edge-segmentation/profile-hit.png) |
| Consulta de frequência | Qualquer definição de segmento que se refere a um evento que ocorre pelo menos um determinado número de vezes. |  |
| Consulta de frequência que se refere a um perfil | Qualquer definição de segmento que se refere a um evento que ocorre pelo menos um determinado número de vezes e tem um ou mais atributos de perfil. |  |

Se a consulta corresponder a qualquer um dos tipos de consulta acima, você poderá ativá-la para segmentação de borda ativando o **[!UICONTROL Evaluate as streaming segment on the edge]**.

![](../images/ui/edge-segmentation/mark-on-edge.png)

Os seguintes tipos de query são **não** compatíveis atualmente com a segmentação de borda:

| Tipo de consulta | Detalhes |
| ---------- | ------- |
| Janela de tempo relativo | Se uma consulta se refere a uma janela de tempo, ela não pode ser avaliada usando a segmentação de borda. |
| Negação | Se uma consulta tiver uma negação ou um evento `not`, ela não poderá ser avaliada usando a segmentação de borda. |
| Vários eventos | Se uma consulta contiver mais de um evento, ela não poderá ser avaliada usando a segmentação de borda. |

## Próximas etapas

Este guia do usuário explica como avaliar segmentos com segmentação de borda no Adobe Experience Platform.

Para saber mais sobre como usar a interface do usuário do Adobe Experience Platform, leia o [Guia do usuário de segmentação](./overview.md). Para saber como executar ações semelhantes e trabalhar com segmentos usando a interface do usuário do Adobe Experience Platform, visite o [guia da API de segmentação de borda](../api/edge-segmentation.md).
