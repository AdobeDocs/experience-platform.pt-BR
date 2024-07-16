---
solution: Experience Platform
title: Guia da interface de segmentação de streaming
description: A segmentação por transmissão no Adobe Experience Platform permite fazer a segmentação em tempo quase real, concentrando-se na riqueza de dados. Com a segmentação por transmissão, a qualificação de segmentos agora acontece à medida que os dados chegam à Platform, reduzindo a necessidade de agendar e executar trabalhos de segmentação. Com esse recurso, a maioria das regras de segmento agora pode ser avaliada à medida que os dados são passados para a Platform, o que significa que a associação do segmento será mantida atualizada sem executar trabalhos de segmentação programados.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: c2f9bcd9aeb0073b8b26413ec29e2dff1ee5c80d
workflow-type: tm+mt
source-wordcount: '1537'
ht-degree: 0%

---

# Segmentação de transmissão

>[!NOTE]
>
>O documento a seguir declara como usar a segmentação por transmissão usando a interface do usuário. Para obter informações sobre como usar a segmentação por transmissão usando a API, leia o [guia da API de segmentação por transmissão](../api/streaming-segmentation.md).

A segmentação por transmissão no [!DNL Adobe Experience Platform] permite que os clientes façam a segmentação em tempo quase real, concentrando-se na riqueza de dados. Com a segmentação por transmissão, a qualificação de segmentos agora acontece à medida que os dados de transmissão chegam ao [!DNL Platform], diminuindo a necessidade de agendar e executar trabalhos de segmentação. Com esse recurso, a maioria das regras de segmento agora pode ser avaliada à medida que os dados são passados para [!DNL Platform], o que significa que a associação do segmento será mantida atualizada sem a execução de trabalhos de segmentação agendados.

>[!NOTE]
>
>A segmentação de streaming funciona em todos os dados que foram assimilados usando uma fonte de streaming. Os dados assimilados usando uma fonte baseada em lote serão avaliados à noite, mesmo que se qualifiquem para segmentação por transmissão.
>
>Além disso, os segmentos avaliados com segmentação por transmissão podem variar entre a associação ideal e real se a definição do segmento se basear em outra definição de segmento que é avaliada usando segmentação em lote. Por exemplo, se o Segmento A se basear no Segmento B, e o Segmento B for avaliado usando a segmentação em lote, já que o Segmento B é atualizado apenas a cada 24 horas, o Segmento A se afastará dos dados reais até ressincronizar com a atualização do Segmento B.

## Tipos de consulta de segmentação de transmissão {#query-types}

>[!NOTE]
>
>Para que a segmentação por transmissão funcione, é necessário habilitar a segmentação agendada para a organização. Para obter detalhes sobre como habilitar a segmentação agendada, consulte [a visão geral do Portal de público-alvo](./audience-portal.md#scheduled-segmentation).

Uma consulta será avaliada automaticamente com a segmentação por transmissão se atender a qualquer um dos seguintes critérios:

| Tipo de consulta | Detalhes | Exemplo |
| ---------- | ------- | ------- |
| Evento único | Qualquer definição de segmento que se refere a um único evento recebido sem restrição de tempo. | ![Um exemplo de um único evento é mostrado.](../images/ui/streaming-segmentation/incoming-hit.png) |
| Evento único em uma janela de tempo relativa | Qualquer definição de segmento que se refere a um único evento de entrada. | ![Um exemplo de um único evento em uma janela de tempo relativa é mostrado.](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Evento único com uma janela de tempo | Qualquer definição de segmento que se refere a um único evento recebido com uma janela de tempo. | ![Um exemplo de um único evento com uma janela de tempo é mostrado.](../images/ui/streaming-segmentation/historic-time-window.png) |
| Somente perfil | Qualquer definição de segmento que se refere apenas a um atributo de perfil. | |
| Evento único com um atributo de perfil em uma janela de tempo relativa de menos de 24 horas | Qualquer definição de segmento que se refere a um único evento recebido, com um ou mais atributos de perfil, e ocorre em uma janela de tempo relativa de menos de 24 horas. | ![Um exemplo de um único evento com um atributo de perfil em uma janela de tempo relativa é mostrado.](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Segmento de segmentos | Qualquer definição de segmento que contenha um ou mais segmentos em lote ou de fluxo. **Observação:** se um segmento de segmentos for usado, a desqualificação de perfis ocorrerá **a cada 24 horas**. | ![Um exemplo de segmento de segmentos é mostrado.](../images/ui/streaming-segmentation/two-batches.png) |
| Vários eventos com um atributo de perfil | Qualquer definição de segmento que se refere a vários eventos **nas últimas 24 horas** e (opcionalmente) tem um ou mais atributos de perfil. | ![Um exemplo de vários eventos com um atributo de perfil é mostrado.](../images/ui/streaming-segmentation/event-history-success.png) |

Uma definição de segmento **não** será habilitada para segmentação por transmissão nos seguintes cenários:

- A definição do segmento inclui segmentos ou características do Adobe Audience Manager (AAM).
- A definição do segmento inclui várias entidades (consultas de várias entidades).
- A definição de segmento inclui uma combinação de um único evento e um evento `inSegment`.
   - No entanto, se a definição de segmento contida no evento `inSegment` for somente perfil, a definição de segmento **será** habilitada para segmentação por transmissão.
- A definição do segmento usa &quot;Ignorar ano&quot; como parte de suas restrições de tempo.

Observe que as seguintes diretrizes se aplicam ao fazer a segmentação por transmissão:

| Tipo de consulta | Orientação |
| ---------- | -------- |
| Consulta de evento único | Não há limites para a janela de retrospectiva. |
| Consulta com histórico de eventos | <ul><li>A janela de pesquisa é limitada a **um dia**.</li><li>Uma condição estrita de ordenação de tempo **deve** existe entre os eventos.</li><li>Há suporte para consultas com pelo menos um evento negado. No entanto, o evento inteiro **não pode** ser uma negação.</li></ul> |

Se uma definição de segmento for modificada para não atender mais aos critérios de segmentação por transmissão, a definição de segmento mudará automaticamente de &quot;Transmissão&quot; para &quot;Lote&quot;.

Além disso, a desqualificação de segmentos, semelhante à qualificação de segmentos, acontece em tempo real. Como resultado, se um público-alvo não se qualificar mais para um segmento, ele será imediatamente desqualificado. Por exemplo, se a definição do segmento solicitar &quot;Todos os usuários que compraram sapatos vermelhos nas últimas três horas&quot;, após três horas, todos os perfis que se qualificaram inicialmente para a definição do segmento serão desqualificados.

## Detalhes de definição do segmento de segmentação de transmissão

Depois de criar um segmento ativado para transmissão, você pode visualizar os detalhes desse segmento.

![A página de detalhes da definição de segmento é exibida.](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

Especificamente, a métrica **[!UICONTROL Total qualificado]** é exibida, o que mostra o número total de públicos qualificados, com base nas avaliações em lote e de transmissão deste segmento.

Abaixo está um gráfico de linhas que mostra o número de novos públicos-alvo que foram atualizados nas últimas 24 horas usando o método de avaliação de transmissão contínua. A lista suspensa pode ser ajustada para mostrar as últimas 24 horas, a última semana ou os últimos 30 dias. A métrica **[!UICONTROL Novo público atualizado]** é baseada na alteração no tamanho do público durante o intervalo de tempo selecionado, conforme avaliado pela segmentação por transmissão. Essa métrica não inclui o público qualificado total da avaliação diária do lote de segmentos.

>[!NOTE]
>
>Uma definição de segmento é considerada qualificada se passar de sem status para realizado ou se passar de encerrado para realizado. Uma definição de segmento é considerada não qualificada se for da realização à saída.
>
>Mais informações sobre esses status podem ser encontradas na tabela de status na [Visão geral do Portal de público-alvo](./audience-portal.md#customize).

![O cartão Perfis ao longo do tempo está realçado, mostrando um gráfico de linhas dos perfis ao longo do tempo.](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Para obter informações adicionais sobre a última avaliação de segmento, selecione a bolha de informações ao lado de **[!UICONTROL Total qualificado]**.

![A bolha de informações para o Total de perfis qualificados foi selecionada. Isso exibe informações sobre o último horário de avaliação do segmento.](../images/ui/streaming-segmentation/info-bubble.png)

Para obter mais informações sobre definições de segmento, leia a seção anterior em [detalhes de definição de segmento](#segment-details).

## Próximas etapas

Este guia do usuário explica como as definições de segmento habilitado para streaming funcionam no Adobe Experience Platform e como monitorar segmentos habilitados para streaming.

Para saber mais sobre como usar a interface do usuário do Adobe Experience Platform, leia o [Guia do usuário de segmentação](./overview.md).

## Apêndice

A seção a seguir lista as perguntas frequentes relacionadas à segmentação de transmissão:

### A &quot;desqualificação&quot; da segmentação por transmissão também ocorre em tempo real?

Para a maioria das instâncias, a desqualificação da segmentação por transmissão ocorre em tempo real. No entanto, os segmentos de transmissão que usam segmentos de segmentos **não** não se qualificam em tempo real, em vez disso, se desqualificam após 24 horas.

### Em quais dados a segmentação por transmissão funciona?

A segmentação de streaming funciona em todos os dados que foram assimilados usando uma fonte de streaming. Os segmentos assimilados usando uma origem em lote serão avaliados à noite, mesmo que se qualifiquem para segmentação por transmissão. Os eventos transmitidos para o sistema com um carimbo de data e hora com mais de 24 horas serão processados na tarefa em lote subsequente.

### Como os segmentos são definidos como segmentação em lote ou por transmissão?

Uma definição de segmento é definida como segmentação de lote, fluxo ou borda com base em uma combinação de tipo de consulta e duração do histórico de eventos. Uma lista de quais segmentos serão avaliados como uma definição de segmento de streaming pode ser encontrada na [seção de tipos de consulta de segmentação de streaming](#query-types).

Observe que se uma definição de segmento contiver **ambos** uma expressão `inSegment` e uma cadeia direta de evento único, ela não poderá se qualificar para segmentação de transmissão. Se você quiser que essa definição de segmento se qualifique para a segmentação por transmissão, transforme a cadeia direta de evento único em seu próprio segmento.

### Por que o número de segmentos &quot;total qualificado&quot; continua aumentando, enquanto o número em &quot;Últimos X dias&quot; permanece em zero na seção de detalhes de definição do segmento?

O número total de segmentos qualificados é retirado do trabalho diário de segmentação, que inclui públicos qualificados para segmentos em lote e de fluxo. Esse valor é mostrado para segmentos em lote e de transmissão.

O número nos &quot;Últimos X dias&quot; **somente** inclui públicos qualificados na segmentação por transmissão e **somente** aumenta se você tiver transmitido dados para o sistema e se contar para essa definição de transmissão. Este valor é **somente** exibido para segmentos de streaming. Como resultado, o valor **maio** é exibido como 0 para segmentos em lote.

Como resultado, se você vir que o número em &quot;Últimos X dias&quot; é zero e o gráfico de linha também está relatando zero, você **não** transmitiu qualquer perfil no sistema que se qualificaria para esse segmento.

### Quanto tempo leva para uma definição de segmento ficar disponível?

Leva até uma hora para uma definição de segmento estar disponível.

### Existem limitações para os dados que estão sendo transmitidos?

Para que os dados transmitidos sejam usados na segmentação por transmissão, **deve** haver um espaçamento entre os eventos transmitidos. Se muitos eventos forem transmitidos no mesmo segundo, a Platform tratará esses eventos como dados gerados pelo bot e eles serão descartados. Como prática recomendada, você deve ter **pelo menos** cinco segundos entre os dados do evento para garantir que os dados sejam usados corretamente.
