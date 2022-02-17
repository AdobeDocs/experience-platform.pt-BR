---
keywords: Experience Platform, home, tópicos populares, segmentação de borda, Segmentação, Serviço de segmentação, serviço de segmentação, guia da interface do usuário, borda de fluxo;
solution: Experience Platform
title: Guia da interface do usuário de segmentação de borda
topic-legacy: ui guide
description: A segmentação de borda é a capacidade de avaliar segmentos na Platform instantaneamente na borda, permitindo casos de uso de personalização de página da mesma página e da próxima página.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 0173fbd36791f837e0d0336f9fa7bcc84e64909f
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# Guia da interface do usuário de segmentação de borda

>[!NOTE]
>
>A segmentação de borda agora está disponível para todos os usuários da plataforma. Se você criou segmentos de borda durante o beta, esses segmentos continuarão operacionais.

A segmentação de borda é a capacidade de avaliar segmentos no Adobe Experience Platform instantaneamente [na borda](../../edge/home.md), ativando casos de uso de personalização de página e página seguinte.

>[!IMPORTANT]
>
> Os dados de borda serão armazenados em um local de servidor de borda mais próximo de onde foram coletados e podem ser armazenados em um local diferente daquele designado como o data center (ou principal) da Adobe Experience Platform.
>
> Além disso, o mecanismo de segmentação de borda só atenderá às solicitações na borda em que houver **one** identidade primária marcada, que é consistente com identidades primárias não baseadas em borda.

## Tipos de query de segmentação de borda

Atualmente, somente os tipos de consulta selecionados podem ser avaliados com a segmentação de borda. As seções a seguir fornecem uma lista de tipos de query que podem ser avaliados com a segmentação de borda e aqueles que não são compatíveis no momento.

### Tipos de consulta compatíveis

Um query pode ser avaliado com segmentação de borda se atender a qualquer um dos critérios descritos na tabela a seguir.

>[!NOTE]
>
>Se a query corresponder a qualquer um dos tipos de query na tabela a seguir, ela será avaliada automaticamente usando a segmentação de borda. O sistema determina essa capacidade automaticamente com base na expressão de consulta.

| Tipo de consulta | Detalhes | Exemplo |
| ---------- | ------- | ------- |
| Evento único | Qualquer definição de segmento que se refere a um único evento de entrada sem restrição de tempo. | Pessoas que adicionaram um item ao carrinho. |
| Evento único que se refere a um perfil | Qualquer definição de segmento que se refere a um ou mais atributos de perfil e um único evento de entrada sem restrição de tempo. | Pessoas que vivem nos EUA que visitaram a página inicial. |
| Evento único negado com um atributo de perfil | Qualquer definição de segmento que se refere a um evento de entrada único negado e um ou mais atributos de perfil | Pessoas que vivem nos EUA e têm **not** visitou a página inicial. |
| Evento único em uma janela de 24 horas | Qualquer definição de segmento que se refere a um único evento de entrada em 24 horas. | Pessoas que visitaram a página inicial nas últimas 24 horas. |
| Evento único com um atributo de perfil dentro de uma janela de tempo de 24 horas | Qualquer definição de segmento que se refere a um ou mais atributos de perfil e um único evento de entrada em 24 horas. | Pessoas que vivem nos EUA que visitaram a página inicial nas últimas 24 horas. |
| Evento único negado com um atributo de perfil dentro de uma janela de tempo de 24 horas | Qualquer definição de segmento que se refere a um ou mais atributos de perfil e um evento de entrada único negado em 24 horas. | Pessoas que vivem nos EUA e têm **not** visitou a página inicial nas últimas 24 horas. |
| Evento de frequência dentro de um período de 24 horas | Qualquer definição de segmento que se refere a um evento que ocorre um determinado número de vezes em uma janela de tempo de 24 horas. | Pessoas que visitaram a página inicial **pelo menos** cinco vezes nas últimas 24 horas. |
| Evento de frequência com um atributo de perfil dentro de uma janela de tempo de 24 horas | Qualquer definição de segmento que se refere a um ou mais atributos de perfil e um evento que ocorre um determinado número de vezes em uma janela de tempo de 24 horas. | Pessoas dos EUA que visitaram a página inicial **pelo menos** cinco vezes nas últimas 24 horas. |
| Evento de frequência negado com um perfil dentro de uma janela de tempo de 24 horas | Qualquer definição de segmento que se refere a um ou mais atributos de perfil e um evento negado que ocorre um determinado número de vezes em uma janela de tempo de 24 horas. | Pessoas que não visitaram a página inicial **more** mais de cinco vezes nas últimas 24 horas. |
| Várias ocorrências recebidas em um perfil de tempo de 24 horas | Qualquer definição de segmento que se refere a vários eventos que ocorrem dentro de uma janela de tempo de 24 horas. | Pessoas que visitaram a página inicial **ou** visitou a página de checkout nas últimas 24 horas. |
| Vários eventos com um perfil em uma janela de 24 horas | Qualquer definição de segmento que se refere a um ou mais atributos de perfil e vários eventos que ocorrem dentro de uma janela de tempo de 24 horas. | Pessoas dos EUA que visitaram a página inicial **e** visitou a página de checkout nas últimas 24 horas. |

## Próximas etapas

Este guia explica como avaliar segmentos com segmentação de borda no Adobe Experience Platform. Para saber mais sobre como usar a interface do usuário do Experience Platform, leia o [Guia do usuário de segmentação](./overview.md). Para saber como executar ações semelhantes e trabalhar com segmentos usando APIs do Experience Platform, visite o [guia da API de segmentação de borda](../api/edge-segmentation.md).
