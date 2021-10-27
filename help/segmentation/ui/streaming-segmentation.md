---
keywords: Experience Platform; home; tópicos populares; segmentação de fluxo; Segmentação; Serviço de segmentação; serviço de segmentação; guia da interface do usuário;
solution: Experience Platform
title: Guia da interface do usuário de segmentação de fluxo
topic-legacy: ui guide
description: A segmentação por streaming no Adobe Experience Platform permite fazer a segmentação quase em tempo real, ao mesmo tempo em que se concentra na riqueza de dados. Com a segmentação de fluxo, a qualificação de segmento agora acontece à medida que os dados chegam ao Platform, o que diminui a necessidade de agendar e executar tarefas de segmentação. Com esse recurso, a maioria das regras de segmento agora pode ser avaliada à medida que os dados são passados para a Plataforma, o que significa que a associação de segmento será mantida atualizada sem executar tarefas de segmentação programadas.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: bb5a56557ce162395511ca9a3a2b98726ce6c190
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# Segmentação de streaming

>[!NOTE]
>
>O documento a seguir explica como usar a segmentação de transmissão usando a interface do usuário do . Para obter informações sobre como usar a segmentação de transmissão usando a API, leia o [guia da API de segmentação de fluxo](../api/streaming-segmentation.md).

Transmitir a segmentação em [!DNL Adobe Experience Platform] O permite que os clientes façam segmentação quase em tempo real, concentrando-se na riqueza de dados. Com a segmentação por streaming, a qualificação de segmento agora acontece à medida que os dados de streaming chegam [!DNL Platform], aliviando a necessidade de agendar e executar tarefas de segmentação. Com esse recurso, a maioria das regras de segmento agora pode ser avaliada à medida que os dados são passados para [!DNL Platform], o que significa que a associação de segmento será mantida atualizada sem executar tarefas de segmentação programadas.

>[!NOTE]
>
>A segmentação de fluxo só pode ser usada para avaliar dados transmitidos para a Plataforma. Em outras palavras, os dados assimilados por meio da assimilação em lote não serão avaliados por meio da segmentação de fluxo, e serão avaliados junto com o trabalho de segmento agendado à noite.
>
>Além disso, os segmentos avaliados com a segmentação de fluxo podem oscilar entre a associação ideal e real se o segmento for baseado em outro segmento avaliado por meio da segmentação em lote. Por exemplo, se o Segmento A for baseado no Segmento B e o Segmento B for avaliado usando a segmentação em lote, já que o Segmento B só é atualizado a cada 24 horas, o Segmento A se afastará dos dados reais até que seja ressincronizado com a atualização do Segmento B.

## Tipos de consulta de segmentação de fluxo

>[!NOTE]
>
>Para que a segmentação de transmissão funcione, é necessário ativar a segmentação agendada para a organização. Para obter detalhes sobre como ativar a segmentação agendada, consulte [a seção de segmentação de fluxo no guia do usuário de Segmentação](./overview.md#scheduled-segmentation).

Um query será avaliado automaticamente com a segmentação de transmissão se atender a qualquer um dos seguintes critérios:

| Tipo de consulta | Detalhes | Exemplo |
| ---------- | ------- | ------- |
| Evento único | Qualquer definição de segmento que se refere a um único evento de entrada sem restrição de tempo. | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| Evento único em uma janela de tempo relativa | Qualquer definição de segmento que se refere a um único evento de entrada. | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Evento único com janela de tempo | Qualquer definição de segmento que se refere a um único evento de entrada com uma janela de tempo. | ![](../images/ui/streaming-segmentation/historic-time-window.png) |
| Somente perfil | Qualquer definição de segmento que se refere somente a um atributo de perfil. |  |
| Evento único com um atributo de perfil | Qualquer definição de segmento que se refere a um único evento de entrada, sem restrição de tempo e um ou mais atributos de perfil. **Observação:** O query é avaliado imediatamente quando o evento ocorre. No entanto, no caso de um evento de perfil, ele deve aguardar 24 horas para ser incorporado. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| Evento único com um atributo de perfil dentro de uma janela de tempo relativa | Qualquer definição de segmento que se refere a um único evento de entrada e um ou mais atributos de perfil. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Segmento de segmentos | Qualquer definição de segmento que contenha um ou mais segmentos em lote ou em fluxo. **Observação:** Se um segmento de segmentos for usado, a desativação do perfil ocorrerá **a cada 24 horas**. | ![](../images/ui/streaming-segmentation/two-batches.png) |
| Vários eventos com um atributo de perfil | Qualquer definição de segmento que se refere a vários eventos **nas últimas 24 horas** e (opcionalmente) tem um ou mais atributos de perfil. | ![](../images/ui/streaming-segmentation/event-history-success.png) |

Uma definição de segmento **not** ser habilitado para segmentação de transmissão nos seguintes cenários:

- A definição de segmento inclui segmentos ou características do Adobe Audience Manager (AAM).
- A definição de segmento inclui várias entidades (consultas de várias entidades).

Além disso, algumas diretrizes se aplicam ao fazer a segmentação de fluxo:

| Tipo de consulta | Orientação |
| ---------- | -------- |
| Query de evento único | Não há limites para a janela de retrospectiva. |
| Consulta com histórico de eventos | <ul><li>A janela de retrospectiva está limitada a **um dia**.</li><li>Uma condição de ordem de tempo estrita **must** existir entre os eventos.</li><li>Consultas com pelo menos um evento negado são suportadas. No entanto, o evento inteiro **cannot** ser uma negação.</li></ul> |

Se uma definição de segmento for modificada para que não atenda mais aos critérios para a segmentação de transmissão, a definição de segmento mudará automaticamente de &quot;Streaming&quot; para &quot;Lote&quot;.

## Detalhes do segmento de segmentação de fluxo

Após criar um segmento habilitado para transmissão, você pode visualizar os detalhes desse segmento.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

Especificamente, detalhes sobre o **[!UICONTROL tamanho total do público qualificado]** são mostradas. O **[!UICONTROL Tamanho total do público-alvo qualificado]** mostra o número total de públicos-alvo qualificados da última execução de tarefa de segmento concluída. Se um trabalho de segmento não tiver sido concluído nas últimas 24 horas, o número de públicos-alvo será obtido de uma estimativa.

Embaixo está um gráfico de linhas que mostra o número de segmentos que foram qualificados e desqualificados nas últimas 24 horas. A lista suspensa pode ser ajustada para mostrar as últimas 24 horas, semana passada ou últimos 30 dias.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Informações adicionais sobre a última avaliação de segmento podem ser encontradas selecionando a bolha de informações.

![](../images/ui/streaming-segmentation/info-bubble.png)

Para obter mais informações sobre definições de segmentos, leia a seção anterior em [detalhes da definição de segmento](#segment-details).

## Próximas etapas

Este guia do usuário explica como as definições de segmentos ativadas para transmissão funcionam no Adobe Experience Platform e como monitorar os segmentos ativados para transmissão.

Para saber mais sobre como usar a interface do usuário do Adobe Experience Platform, leia o [Guia do usuário de segmentação](./overview.md).
