---
title: Monitorar uso de licença de consulta em lote
description: A interface do usuário do Adobe Experience Platform fornece um painel por meio do qual você pode visualizar informações importantes sobre o uso da licença do Data Distiller da sua organização.
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
source-git-commit: a1c5b687108a9fc8729008e2b0e39ec6b1842f54
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# (Alfa) Monitorar o uso de licença de consulta em lote {#monitor-license-usage}

>[!IMPORTANT]
>
>A capacidade de monitorar o uso de licença de consulta em lote por meio da interface ainda não está disponível para todos os usuários. Esse recurso está em alfa e ainda está sendo testado. Este documento está sujeito a alterações.

A interface do usuário (UI) do Adobe Experience Platform fornece um painel por meio do qual você pode exibir informações importantes sobre o uso da licença do Serviço de consulta da sua organização.

Para obter instruções detalhadas sobre como acessar e interagir com o painel de uso de licença na interface do usuário, bem como para saber mais sobre as métricas disponíveis exibidas no painel, visite o [guia do painel de uso da licença](../../dashboards/guides/license-usage.md).

Leia as [visão geral dos painéis](../../dashboards/home.md) para obter um resumo de todos os recursos do painel dentro do Experience Platform.

## Widgets {#widgets}

O painel de uso de licença é composto por widgets, que exibem métricas somente leitura que fornecem informações importantes sobre o uso de licença da sua organização. As métricas visíveis dependem do licenciamento específico da sua organização.

Selecione um botão de opção para escolher uma sandbox para análise e use a lista suspensa para selecionar um período para a análise. As opções disponíveis são um período de 30 dias, 90 dias, 12 meses, o último ano, o período completo do contrato ou uma data personalizada.

## Computar horas {#compute-hours}

A variável [!UICONTROL Computar horas] O widget usa um gráfico de linhas para visualizar o tempo de processamento de consultas em lote de sua organização a cada dia. O widget exibe três métricas indicadas por um número na parte superior esquerda do widget. São eles

- [!UICONTROL Efetivo]: o número total de horas computacionais do período escolhido na lista suspensa visão geral. Essa métrica também é indicada no gráfico por uma linha sólida.
- [!UICONTROL Licenciado]: o número total de horas computacionais permitido pelo contrato de licença de sua organização. Essa métrica também é indicada no gráfico por uma linha pontilhada.
- [!UICONTROL Uso]: essa é a porcentagem de seu uso em relação às horas computacionais máximas acordadas por sua licença.

>[!IMPORTANT]
>
>A variável [!UICONTROL Computar horas] O widget só é aplicável a clientes com a licença do Data Distiller para consultas em lote.

![O painel de uso da licença com o widget de horas de computação destacado.](../images/data-distiller/compute-hours.png)
