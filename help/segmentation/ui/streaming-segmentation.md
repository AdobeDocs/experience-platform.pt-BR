---
keywords: Experience Platform; home; tópicos populares; segmentação de fluxo; Segmentação; Serviço de segmentação; serviço de segmentação; guia da interface do usuário;
solution: Experience Platform
title: Guia da interface do usuário de segmentação de fluxo
topic-legacy: ui guide
description: A segmentação por streaming no Adobe Experience Platform permite fazer a segmentação quase em tempo real, ao mesmo tempo em que se concentra na riqueza de dados. Com a segmentação de fluxo, a qualificação de segmento agora acontece à medida que os dados chegam ao Platform, o que diminui a necessidade de agendar e executar tarefas de segmentação. Com esse recurso, a maioria das regras de segmento agora pode ser avaliada à medida que os dados são passados para a Plataforma, o que significa que a associação de segmento será mantida atualizada sem executar tarefas de segmentação programadas.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: 1fa7663cc8bebca98f284593e98163315acda478
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 0%

---

# Segmentação de streaming

>[!NOTE]
>
>O documento a seguir explica como usar a segmentação de transmissão usando a interface do usuário do . Para obter informações sobre como usar a segmentação de transmissão usando a API, leia o [guia da API de segmentação de fluxo](../api/streaming-segmentation.md).

Transmitir a segmentação em [!DNL Adobe Experience Platform] O permite que os clientes façam segmentação quase em tempo real, concentrando-se na riqueza de dados. Com a segmentação por streaming, a qualificação de segmento agora acontece à medida que os dados de streaming chegam [!DNL Platform], aliviando a necessidade de agendar e executar tarefas de segmentação. Com esse recurso, a maioria das regras de segmento agora pode ser avaliada à medida que os dados são passados para [!DNL Platform], o que significa que a associação de segmento será mantida atualizada sem executar tarefas de segmentação programadas.

>[!NOTE]
>
>
>Os segmentos avaliados com a segmentação de transmissão podem oscilar entre a associação ideal e real se o segmento for baseado em outro segmento avaliado por meio da segmentação em lote. Por exemplo, se o Segmento A for baseado no Segmento B e o Segmento B for avaliado usando a segmentação em lote, já que o Segmento B só é atualizado a cada 24 horas, o Segmento A se afastará dos dados reais até que seja ressincronizado com a atualização do Segmento B.

## Tipos de consulta de segmentação de fluxo {#query-types}

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

Observe que as seguintes diretrizes se aplicam ao fazer a segmentação de fluxo:

| Tipo de consulta | Orientação |
| ---------- | -------- |
| Query de evento único | Não há limites para a janela de retrospectiva. |
| Consulta com histórico de eventos | <ul><li>A janela de retrospectiva está limitada a **um dia**.</li><li>Uma condição de ordem de tempo estrita **must** existir entre os eventos.</li><li>Consultas com pelo menos um evento negado são suportadas. No entanto, o evento inteiro **cannot** ser uma negação.</li></ul> |

Se uma definição de segmento for modificada para que não atenda mais aos critérios para a segmentação de transmissão, a definição de segmento mudará automaticamente de &quot;Streaming&quot; para &quot;Lote&quot;.

Além disso, a inqualificação de segmentos, de forma semelhante à qualificação de segmentos, ocorre em tempo real. Como resultado, se um público-alvo não se qualificar mais para um segmento, ele será imediatamente desqualificado. Por exemplo, se a definição de segmento solicitar &quot;Todos os usuários que compraram sapatos vermelhos nas últimas três horas&quot;, após três horas, todos os perfis que inicialmente se qualificaram para a definição do segmento serão não qualificados.

## Detalhes do segmento de segmentação de fluxo

Após criar um segmento habilitado para transmissão, você pode visualizar os detalhes desse segmento.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

Especificamente, detalhes sobre o **[!UICONTROL tamanho total do público qualificado]** são mostradas. O **[!UICONTROL Tamanho total do público-alvo qualificado]** mostra o número total de públicos-alvo qualificados da última execução de tarefa de segmento concluída. Se um trabalho de segmento não tiver sido concluído nas últimas 24 horas, o número de públicos-alvo será obtido de uma estimativa.

Embaixo está um gráfico de linhas que mostra o número de segmentos que foram qualificados e desqualificados nas últimas 24 horas. A lista suspensa pode ser ajustada para mostrar as últimas 24 horas, semana passada ou últimos 30 dias.

>[!NOTE]
>
>Um segmento é considerado qualificado se passar de sem status para realizado ou se passar de fechado para realizado. Um segmento é considerado não qualificado se passar de realizado para fechado ou de existente para fechado.
>
>Mais informações sobre esses status podem ser encontradas na tabela de status na seção [visão geral da segmentação](./overview.md#browse).

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Informações adicionais sobre a última avaliação de segmento podem ser encontradas selecionando a bolha de informações.

![](../images/ui/streaming-segmentation/info-bubble.png)

Para obter mais informações sobre definições de segmentos, leia a seção anterior em [detalhes da definição de segmento](#segment-details).

## Próximas etapas

Este guia do usuário explica como as definições de segmentos ativadas para transmissão funcionam no Adobe Experience Platform e como monitorar os segmentos ativados para transmissão.

Para saber mais sobre como usar a interface do usuário do Adobe Experience Platform, leia o [Guia do usuário de segmentação](./overview.md).

## Apêndice

A seção a seguir lista as perguntas mais frequentes sobre a segmentação de fluxo:

### A &quot;inqualificação&quot; da segmentação por streaming também ocorre em tempo real?

Para a maioria das instâncias, a inqualificação da segmentação de streaming ocorre em tempo real. No entanto, os segmentos de fluxo que usam segmentos de segmentos **not** não se qualificam em tempo real, em vez disso, não se qualificam após 24 horas.

### Em quais dados a segmentação de fluxo funciona?

A segmentação de transmissão funciona em todos os dados assimilados por meio de uma fonte de transmissão. Os segmentos assimilados usando uma fonte baseada em lote serão avaliados à noite, mesmo que se qualifiquem para a segmentação de transmissão.

### Como os segmentos são definidos como segmentação em lote ou streaming?

Um segmento é definido como segmentação em lote ou em fluxo com base em uma combinação de tipo de query e duração do histórico do evento. Uma lista de quais segmentos serão avaliados como um segmento de transmissão pode ser encontrada no [seção de tipos de consulta de segmentação de fluxo](#query-types).

### Um usuário pode definir um segmento como segmentação em lote ou em fluxo?

No momento, o usuário não pode definir se um segmento é avaliado por meio da assimilação em lote ou streaming, pois o sistema determinará automaticamente com qual método o segmento será avaliado.

### Por que o número de segmentos &quot;qualificados totais&quot; continua aumentando enquanto o número em &quot;Últimos X dias&quot; permanece em zero na seção de detalhes do segmento?

O número total de segmentos qualificados é obtido do trabalho de segmentação diário, que inclui públicos-alvo qualificados para segmentos em lote e em fluxo. Esse valor é mostrado para segmentos em lote e streaming.

O número em &quot;Últimos X dias&quot; **only** inclui públicos-alvo qualificados na segmentação de transmissão, e **only** O aumenta se você tiver transmitido dados para o sistema e isso contar para essa definição de transmissão. Este valor é **only** exibido para segmentos de transmissão. Como resultado, esse valor **pode** exibir como 0 para segmentos em lote.

Como resultado, se você perceber que o número em &quot;Últimos X dias&quot; é zero, e o gráfico de linha também está relatando zero, você terá que **not** os perfis eram transmitidos no sistema e se qualificavam para esse segmento.