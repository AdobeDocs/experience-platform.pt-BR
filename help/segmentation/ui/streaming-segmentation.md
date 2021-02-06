---
keywords: Experience Platform;home;popular topics;streaming segmentation;Segmentation;Serviço de segmentação;serviço de segmentação;guia ui;
solution: Experience Platform
title: Guia da interface de usuário de segmentação de fluxo
topic: ui guide
description: A segmentação contínua no Adobe Experience Platform permite que você faça a segmentação em tempo quase real, enquanto se concentra na riqueza de dados. Com a segmentação de fluxo contínuo, a qualificação de segmentos acontece à medida que os dados chegam à Plataforma, o que diminui a necessidade de programar e executar tarefas de segmentação. Com esse recurso, a maioria das regras de segmento pode ser avaliada à medida que os dados são passados para a Plataforma, o que significa que a associação de segmento será mantida atualizada sem executar trabalhos de segmentação programados.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 0%

---


# Segmentação em streaming

>[!NOTE]
>
>O documento a seguir indica como usar a segmentação de fluxo contínuo usando a interface do usuário. Para obter informações sobre como usar a segmentação de streaming usando a API, leia o [guia da API de segmentação de streaming](../api/streaming-segmentation.md).

A segmentação contínua em [!DNL Adobe Experience Platform] permite que os clientes façam a segmentação em tempo quase real, enquanto se concentram na riqueza de dados. Com a segmentação de fluxo contínuo, a qualificação de segmentos agora acontece à medida que os dados de streaming chegam [!DNL Platform], diminuindo a necessidade de programar e executar trabalhos de segmentação. Com esse recurso, a maioria das regras de segmento pode ser avaliada à medida que os dados são passados para [!DNL Platform], o que significa que a associação de segmento será mantida atualizada sem executar trabalhos de segmentação programados.

>[!NOTE]
>
>A segmentação de fluxo só pode ser usada para avaliar dados que são transmitidos para a Plataforma. Em outras palavras, os dados ingeridos por meio da ingestão em lote não serão avaliados por meio da segmentação em streaming e serão avaliados juntamente com o trabalho segmentado agendado à noite.

## Tipos de query de segmentação de transmissão

>[!NOTE]
>
>Para que a segmentação de fluxo funcione, será necessário ativar a segmentação programada para a organização. Para obter detalhes sobre como ativar a segmentação programada, consulte [a seção de segmentação de streaming no guia do usuário de Segmentação](./overview.md#scheduled-segmentation).

Um query será avaliado automaticamente com a segmentação de streaming se atender a qualquer um dos seguintes critérios:

| Tipo de query | Detalhes | Exemplo |
| ---------- | ------- | ------- |
| Ocorrência recebida | Qualquer definição de segmento que se refere a um único evento recebido sem nenhuma restrição de tempo. | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| Ocorrência recebida dentro de uma janela de tempo relativa | Qualquer definição de segmento que se refere a um único evento recebido. | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Somente perfil | Qualquer definição de segmento que se refere somente a um atributo de perfil. |  |
| Ocorrência recebida que se refere a um perfil | Qualquer definição de segmento que se refere a um único evento recebido, sem restrição de tempo, e um ou mais atributos de perfil. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| Ocorrência recebida que se refere a um perfil dentro de uma janela de tempo relativa | Qualquer definição de segmento que se refere a um único evento recebido e um ou mais atributos do perfil. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Vários eventos que se referem a um perfil | Qualquer definição de segmento que se refere a vários eventos **nas últimas 24 horas** e (opcionalmente) tem um ou mais atributos de perfil. | ![](../images/ui/streaming-segmentation/event-history-success.png) |

Uma definição de segmento **não** será ativada para a segmentação de streaming nos seguintes cenários:

- A definição do segmento inclui segmentos ou características do Adobe Audience Manager (AAM).
- A definição do segmento inclui várias entidades (query de várias entidades).

Além disso, algumas diretrizes se aplicam ao fazer a segmentação de streaming:

| Tipo de query | Orientação |
| ---------- | -------- |
| Query de evento único | Não há limites para a janela de pesquisa. |
| Query com histórico de eventos | <ul><li>A janela de pesquisa é limitada a **um dia**.</li><li>Há uma condição de ordem de tempo estrita **must** entre os eventos.</li><li>Query com pelo menos um evento negado são suportados. No entanto, todo o evento **não pode** ser uma negação.</li></ul> |

Se uma definição de segmento for modificada de modo que não atenda mais aos critérios para a segmentação de fluxo contínuo, a definição de segmento mudará automaticamente de &quot;Streaming&quot; para &quot;Lote&quot;.

## Detalhes do segmento de segmentação de transmissão

Depois de criar um segmento habilitado para streaming, você pode visualização os detalhes desse segmento.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

Especificamente, os detalhes sobre o **[!UICONTROL tamanho total de audiência qualificada]** são mostrados. O **[!UICONTROL Tamanho total da audiência qualificada]** mostra o número total de audiências qualificadas da última execução de tarefa de segmento concluída. Se um trabalho de segmento não tiver sido concluído nas últimas 24 horas, o número de audiências será obtido de uma estimativa.

Embaixo está um gráfico de linhas que mostra o número de segmentos que foram qualificados e desqualificados nas últimas 24 horas. A lista suspensa pode ser ajustada para mostrar as últimas 24 horas, semana passada ou últimos 30 dias.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Informações adicionais sobre a última avaliação do segmento podem ser encontradas selecionando a bolha de informações.

![](../images/ui/streaming-segmentation/info-bubble.png)

Para obter mais informações sobre definições de segmentos, leia a seção anterior sobre [detalhes de definição de segmentos](#segment-details).

## Demonstração de vídeo de segmentação contínua

O vídeo a seguir é destinado a suportar sua compreensão da segmentação de streaming. Ele mostra um exemplo de experiência do cliente seguido por um rápido tour dos principais recursos na interface [!DNL Platform].

>[!VIDEO](https://video.tv.adobe.com/v/36184?quality=12&learn=on)

## Próximas etapas

Este guia do usuário explica como as definições de segmentos ativados por streaming funcionam no Adobe Experience Platform e como monitorar os segmentos ativados por streaming.

Para saber mais sobre como usar a interface do usuário do Adobe Experience Platform, leia o [Guia do usuário de segmentação](./overview.md).