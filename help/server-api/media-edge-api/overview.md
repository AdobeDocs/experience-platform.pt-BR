---
solution: Experience Platform
title: APIs do Media Edge
description: Visão geral das APIs do Media Edge
exl-id: 55c952de-caab-4301-acf2-f7b64cebbb1c
source-git-commit: ba5a539603da656117c95d19c9e989ef0e252f82
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 5%

---

# Visão geral da API do Media Edge

As APIs do Media Edge são criadas no Adobe Experience Platform para fornecer dados de rastreamento de eventos de mídia dentro da estrutura do [Esquemas XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=en#:~:text=Experience%20Data%20Model%20(XDM)%2C,the%20power%20of%20digital%20experiences). Para clientes do Media Analytics, isso disponibiliza os seguintes recursos:

* Com [Adobe Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=pt-BR)No, os clientes podem obter detalhes detalhados detalhados sobre duração, inícios e interrupções quase em tempo real para avaliar e combinar as métricas de mídia. Os clientes que migram do Adobe Analytics têm todas as métricas de relatórios disponíveis no Adobe Customer Journey Analytics.

* Com [Adobe Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=pt-BR), os clientes podem enriquecer seus perfis em tempo real com dados de consumo de mídia.

* Com [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=en), os clientes podem otimizar campanhas omnicanal e automatizar jornadas com sinais de consumo de mídia.


## Otimização dos fluxos de dados de rastreamento de mídia

Ambos [APIs da coleção de mídia](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-overview.html?lang=en&amp;media-tracking-data-flows) As APIs do Media Edge e do fornecem dados de rastreamento de mídia como serviços RESTful. Mas o uso do serviço Media Edge tem as seguintes vantagens:

* É a maneira mais fácil de incorporar esquemas XDM no fluxo de dados.

* As chamadas são direcionadas de um reprodutor de mídia diretamente para a [Rede de borda Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=en).

* Ele rastreia eventos de mídia com eficiência, com um mínimo de chamadas entre servidores.

A tabela a seguir mostra um possível serviço de API de Adobe para vários casos de análise de mídia:

| Caso de uso | Serviço de API |
| -------- | ----------- |
| Solução da Adobe Experience Platform | Media Edge |
| REAL-TIME CDP + CUSTOMER JOURNEY ANALYTICS | Media Edge |
| Solução Adobe Analytics + Adobe Experience Platform | Media Edge |
| Somente Adobe Analytics (já está rastreando) | Coleção de mídia |

>[!NOTE]
>
> O serviço da API Media Collection para Analytics ainda recebe dados XDM, mas não está otimizado para ele na medida em que o serviço Media Edge está. Dependendo dos dados enviados do Media Player, alguns dados somente do Analytics também podem ser roteados por meio do serviço da API Media Edge.

O gráfico a seguir mostra os fluxos de dados para os dois serviços de API:

![Fluxos de dados do Media Analytics](../assets/edge-api-dataflow.png)

## Próximas etapas

* Para obter mais informações sobre como usar as APIs do Media Edge, consulte a [Documentação de introdução](getting-started.md).

* Para obter mais informações sobre como trabalhar com o Platform Edge, consulte [Instalação do Media Analytics com o Experience Platform Edge](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/implementation-edge.html?lang=en).
