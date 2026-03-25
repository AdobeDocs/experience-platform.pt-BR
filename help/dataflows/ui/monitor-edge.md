---
title: Monitorar segmentação de borda
description: Saiba como usar o painel de monitoramento para observar a taxa de transferência de segmentação de borda.
source-git-commit: 809f80c721d6eedf5ee88dbb1cf4bf7e5a413614
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 3%

---


# Monitorar segmentação de borda

Você pode usar o painel de monitoramento na interface do usuário do Adobe Experience Platform para realizar o monitoramento em tempo real da segmentação de borda na organização. Use esse recurso para acessar uma transparência maior na taxa de transferência dos dados de borda.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Datastreams](../../datastreams/overview.md): as datastreams permitem conectar o Experience Platform Edge Network ao seu conjunto de dados.
* [Capacidades](../../landing/license-usage-and-guardrails/capacity.md): no Experience Platform, as capacidades informam se sua organização excedeu alguma das medidas de proteção e fornecem informações sobre como corrigir esses problemas.
* [Segmentação do Edge](../../segmentation/methods/edge-segmentation.md): a segmentação do Edge é a capacidade de avaliar definições de segmento no Adobe Experience Platform instantaneamente [na borda](../../landing/edge-and-hub-comparison.md), habilitando casos de uso de personalização da mesma página e da próxima página.

## Acesso {#access}

Para acessar o painel de monitoramento da taxa de transferência de segmentação de borda, selecione **[!UICONTROL Monitoring]** na seção **[!UICONTROL Data management]**, seguido de **[!UICONTROL Edge]**.

![O método para acessar o painel de segmentação de borda do monitor está realçado.](/help/dataflows/assets/ui/monitor-edge/access.png)

O painel de monitoramento é exibido. Isso mostra as métricas de monitoramento da taxa de transferência de transmissão da borda, um gráfico que exibe a taxa de transferência de transmissão da borda e uma visualização da sequência de dados. Essas métricas podem ser filtradas por serviço, por borda e por data.

![As opções de filtragem no painel de monitoramento estão realçadas.](/help/dataflows/assets/ui/monitor-edge/filtering.png)

>[!NOTE]
>
>Você poderá ver a exibição da sequência de dados **somente** se selecionar [!UICONTROL Edge segmentation throughput].

Se você filtrar por serviço, poderá escolher sobre qual serviço deseja exibir as informações de taxa de transferência. Isso inclui serviços como segmentação do Edge, coleta de dados, Target, Adobe Journey Optimizer, Offer Decisioning, destinos personalizados, encaminhamento de eventos, Adobe Analytics e Adobe Audience Manager.

Se você filtrar por borda, poderá escolher sobre qual borda deseja exibir as informações. As bordas suportadas incluem Costa Leste dos EUA, Costa Oeste dos EUA, Europa, Índia, Cingapura, Austrália, Japão e Suíça. É possível selecionar várias bordas para exibir de cada vez.

Se você filtrar por data, poderá escolher a escala de tempo para filtrar seus eventos. Essa escala de tempo pode ser configurada para até 30 dias. Como alternativa, você pode usar uma das seguintes escalas de tempo pré-configuradas: [!UICONTROL Last 6 hours], [!UICONTROL Last 12 hours], [!UICONTROL Last 24 hours], [!UICONTROL Last 7 days] e [!UICONTROL Last 30 days].

## Monitoramento de métricas para throughput de borda

A tabela de métricas fornece informações específicas sobre a taxa de transferência de borda do serviço selecionado. Consulte a tabela a seguir para obter mais detalhes sobre cada coluna.

| Métrica | Descrição |
| ------ | ----------- |
| Solicitações recebidas | O número de solicitações recebidas pelas bordas selecionadas dentro do período. |
| Taxa de transferência máxima | A taxa mais alta de solicitações recebidas pelas bordas selecionadas no período. |

{style="table-layout:auto"}

## Gráfico de monitoramento para taxa de transferência de segmentação de borda

O gráfico de monitoramento mostra os registros por segundo recebidos pelas bordas selecionadas dentro do período alocado, em comparação à capacidade máxima permitida.

![O gráfico de taxa de transferência da segmentação de borda é exibido.](/help/dataflows/assets/ui/monitor-edge/edge-segmentation-throughput.png)

## Exibição do fluxo de dados

>[!NOTE]
>
>A exibição da sequência de dados está **somente** disponível se você estiver filtrando a taxa de transferência de segmentação do Edge.

A seção de exibição da sequência de dados exibe uma lista das sequências de dados mais recentes que passaram pelas bordas da sandbox.

![A exibição da sequência de dados é exibida, mostrando informações sobre as sequências de dados listadas.](/help/dataflows/assets/ui/monitor-edge/datastream-view.png)

| Campo | Descrição |
| ----- | ----------- |
| Nome do fluxo de dados | O nome do fluxo de dados. |
| Conjuntos de dados | O nome dos conjuntos de dados aos quais o fluxo de dados pertence. |
| Serviço habilitado | Os nomes dos serviços para os quais a sequência de dados está habilitada. |
| Solicitações | O número de solicitações que passaram pela sequência de dados. |
| Taxa de transferência máxima | A taxa mais alta de solicitações que passaram pelo fluxo de dados. |
