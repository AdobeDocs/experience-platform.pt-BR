---
keywords: Experience Platform;home;popular topics;segment evaluation
solution: Experience Platform
title: Segmentação em streaming
topic: ui guide
description: A segmentação contínua no Adobe Experience Platform permite que você faça a segmentação em tempo quase real, enquanto se concentra na riqueza de dados. Com a segmentação de fluxo contínuo, a qualificação de segmentos acontece à medida que os dados chegam à Plataforma, o que diminui a necessidade de programar e executar tarefas de segmentação. Com esse recurso, a maioria das regras de segmento pode ser avaliada à medida que os dados são passados para a Plataforma, o que significa que a associação de segmento será mantida atualizada sem executar trabalhos de segmentação programados.
translation-type: tm+mt
source-git-commit: 23516c66a67ae5663dcf90a40ccba98bfd266ab0
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 0%

---


# Segmentação em streaming

>[!NOTE]
>
>O documento a seguir indica como usar a segmentação de fluxo contínuo usando a interface do usuário. Para obter informações sobre como usar a segmentação de streaming usando a API, leia o guia [da API de segmentação de](../api/streaming-segmentation.md)streaming.

A segmentação contínua permite [!DNL Adobe Experience Platform] que os clientes façam a segmentação em tempo quase real, concentrando-se na riqueza de dados. Com a segmentação de fluxo contínuo, a qualificação de segmentos acontece à medida que os dados chegam, o que diminui a necessidade de programar e executar tarefas de segmentação. [!DNL Platform] Com esse recurso, a maioria das regras de segmento agora pode ser avaliada à medida que os dados são passados para [!DNL Platform], o que significa que a associação de segmento será mantida atualizada sem executar trabalhos de segmentação programados.

## Tipos de query de segmentação de transmissão

>[!NOTE]
>
>Para que a segmentação de fluxo funcione, será necessário ativar a segmentação programada para a organização. Para obter detalhes sobre como ativar a segmentação programada, consulte [a seção de segmentação de streaming no guia](./overview.md#scheduled-segmentation)do usuário de Segmentação.

Um query será avaliado automaticamente com a segmentação de streaming se atender a qualquer um dos seguintes critérios:

| Tipo de query | Detalhes | Exemplo |
| ---------- | ------- | ------- |
| Ocorrência recebida | Qualquer definição de segmento que se refere a um único evento recebido sem nenhuma restrição de tempo. | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| Ocorrência recebida dentro de uma janela de tempo relativa | Qualquer definição de segmento que se refere a um único evento recebido **nos últimos sete dias**. | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Somente perfil | Qualquer definição de segmento que se refere somente a um atributo de perfil. |  |
| Ocorrência recebida que se refere a um perfil | Qualquer definição de segmento que se refere a um único evento recebido, sem restrição de tempo, e um ou mais atributos de perfil. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| Ocorrência recebida que se refere a um perfil dentro de uma janela de tempo relativa | Qualquer definição de segmento que se refere a um único evento recebido e um ou mais atributos do perfil, **nos últimos sete dias**. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Vários eventos que se referem a um perfil | Qualquer definição de segmento que se refere a vários eventos **nas últimas 24 horas** e (opcionalmente) tem um ou mais atributos de perfil. | ![](../images/ui/streaming-segmentation/event-history-success.png) |

A seção a seguir lista exemplos de definição de segmento que **não** serão ativados para a segmentação de streaming.

| Tipo de query | Detalhes | Exemplo |
| ---------- | ------- | ------- |
| Ocorrência recebida dentro de uma janela de tempo relativa | Se a definição do segmento se refere a um evento recebido **não** dentro do **último período** de sete dias. Por exemplo, nas **últimas duas semanas**. | ![](../images/ui/streaming-segmentation/relative-hit-failure.png) |
| Ocorrência recebida que se refere a um perfil em uma janela relativa | As seguintes opções **não** suportam a segmentação de streaming:<ul><li>Um evento recebido **não** dentro dos **últimos sete dias**.</li><li>Uma definição de segmento que inclui [!DNL Adobe Audience Manager (AAM)] segmentos ou características.</li></ul> | ![](../images/ui/streaming-segmentation/profile-relative-failure.png) |
| Vários eventos que se referem a um perfil | As seguintes opções **não** suportam a segmentação de streaming:<ul><li>Um evento que **não** ocorre dentro **das últimas 24 horas**.</li><li>Uma definição de segmento que inclui segmentos ou características do Adobe Audience Manager (AAM).</li></ul> | ![](../images/ui/streaming-segmentation/event-history-failure.png) |
| Query de várias entidades | Os query de várias entidades **não** são suportados pela segmentação de streaming. |  |

Além disso, algumas diretrizes se aplicam ao fazer a segmentação de streaming:

| Tipo de query | Orientação |
| ---------- | -------- |
| Query de evento único | A janela de retrospectiva é limitada a **sete dias**. |
| Query com histórico de eventos | <ul><li>A janela de retrospectiva é limitada a **um dia**.</li><li>Uma condição de pedido de tempo estrita **deve** existir entre os eventos.</li><li>Somente pedidos de tempo simples (antes e depois) entre os eventos são permitidos.</li><li>Os eventos individuais **não podem** ser negados. Entretanto, todo o query **pode** ser negado.</li></ul> |

## Detalhes do segmento de segmentação de transmissão

Depois de criar um segmento habilitado para streaming, você pode visualização os detalhes desse segmento.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

Especificamente, os detalhes sobre o tamanho **** total da audiência qualificada são mostrados. Se um trabalho tiver sido executado nas últimas 24 horas, o tamanho **[!UICONTROL de audiência qualificado]** total do trabalho será mostrado, além de um gráfico de linha para a audiência adicionada. Caso contrário, o tamanho **[!UICONTROL de audiência estimado]** total será mostrado, além de uma linha de tendência de visualização.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Informações adicionais sobre a última avaliação do segmento podem ser encontradas selecionando a bolha de informações.

![](../images/ui/streaming-segmentation/info-bubble.png)

Para obter mais informações sobre definições de segmentos, leia a seção anterior sobre detalhes [de definição de](#segment-details)segmentos.

## Demonstração de vídeo de segmentação contínua

O vídeo a seguir é destinado a suportar sua compreensão da segmentação de streaming. Mostra um exemplo de experiência do cliente seguido de um rápido tour dos principais recursos na [!DNL Platform] interface.

>[!VIDEO](https://video.tv.adobe.com/v/36184?quality=12&learn=on)

## Próximas etapas

Este guia do usuário explica como as definições de segmentos ativados por streaming funcionam no Adobe Experience Platform e como monitorar os segmentos ativados por streaming.

Para saber mais sobre como usar a interface do usuário do Adobe Experience Platform, leia o guia [do usuário de](./overview.md)Segmentação.