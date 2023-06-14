---
keywords: Experience Platform;borda da mídia;tópicos populares;intervalo de datas
solution: Experience Platform
title: APIs do Media Edge
description: Visão geral das APIs do Media Edge.
source-git-commit: 9d535c8d6524d61612581fbf82986bc5c5cf52de
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 4%

---


# Visão geral da API do Media Edge

As APIs do Media Edge são criadas na Adobe Experience Platform (AEP) para fornecer dados de rastreamento de eventos de mídia dentro da estrutura do [Esquemas XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=en#:~:text=Experience%20Data%20Model%20(XDM)%2C,the%20power%20of%20digital%20experiences). Para clientes do Media Analytics, isso disponibiliza os seguintes recursos:

* Com [Customer Journey Analytics (CJA)](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=pt-BR)No, os clientes podem obter detalhes detalhados detalhados sobre duração, inícios e interrupções quase em tempo real para avaliar e combinar as métricas de mídia. Os clientes que migram do Adobe Analytics têm todas as métricas de relatórios disponíveis no CJA.

* Com [Adobe Real-time Customer Data Platform (CDP)](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=pt-BR), os clientes podem enriquecer seus perfis em tempo real com dados de consumo de mídia.

* Com [Adobe Journey Optimizer (AJO)](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=en), os clientes podem otimizar campanhas omnicanal e automatizar jornadas com sinais de consumo de mídia.


## Otimização dos fluxos de dados de rastreamento de mídia

Ambos [APIs da coleção de mídia](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-overview.html?lang=en&amp;media-tracking-data-flows) As APIs do Media Edge e do fornecem dados de rastreamento de mídia como serviços RESTful. Mas o uso do serviço Media Edge tem as seguintes vantagens:

* É a maneira mais fácil de incorporar esquemas XDM no fluxo de dados.

* As chamadas são direcionadas de um reprodutor de mídia diretamente para a [Rede da Experience Edge Platform](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=en).

* Ele rastreia os eventos de mídia com mais eficiência.

A tabela a seguir mostra um possível serviço de API de Adobe para vários casos de análise de mídia:

| Caso de uso | Serviço de API |
| -------- | ------ |
| Solução da AEP (CJA, RTDCP, AJO etc.) | Media Edge |
| CDP + CJA | Media Edge |
| Solução Adobe Analytics + AEP | Media Edge |
| Somente Adobe Analytics (já está rastreando) | Coleção de mídia |

>[!NOTE]
>
> O serviço da API Media Collection para Analytics ainda recebe dados XDM, mas não está otimizado para ele na medida em que o serviço Media Edge está. Dependendo dos dados enviados do Media Player, alguns dados somente do Analytics também podem ser roteados por meio do serviço da API Media Edge.

O gráfico a seguir mostra os fluxos de dados para os dois serviços de API:


![Fluxos de dados do Media Analytics](../assets/edge-api-dataflow.png)


Para obter mais informações sobre como usar as APIs do Media Edge, consulte a documentação Introdução.

Para obter mais informações sobre como trabalhar com o Platform Edge, consulte [Instalação do Media Analytics com o Experience Platform Edge](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/implementation-edge.html?lang=en).




