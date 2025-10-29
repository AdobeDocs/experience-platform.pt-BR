---
keywords: Experience Platform;página inicial;tópicos populares;serviço de consulta;serviço de consulta;consultas experienceevent;consulta experienceevent;consulta Experience Event;
title: Listar as exibições de página de um usuário
description: Saiba como gravar consultas que usam Eventos de experiência para criar uma lista das últimas 100 páginas que um usuário especificado usou.
exl-id: d831910d-d3a4-4a5a-b897-b09f0546dab0
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 1%

---

# Listar as exibições de página de um usuário

Este documento fornece um exemplo do SQL necessário para listar as exibições de página de um usuário especificado. Com o Serviço de Consulta da Adobe Experience Platform, você pode gravar consultas que usam o [!DNL Experience Events] para capturar uma variedade de casos de uso. Eventos de experiência são representados pela classe Experience Data Model (XDM) ExperienceEvent, que captura um instantâneo imutável e não agregado do sistema quando um usuário interage com um site ou serviço. Eventos de experiência podem até ser usados para análise de domínio de tempo. Consulte a [seção das próximas etapas](#next-steps) para obter mais casos de uso que envolvem [!DNL Experience Events] para gerar relatórios de visitantes.

Mais informações sobre o XDM e o [!DNL Experience Events] podem ser encontradas na [[!DNL XDM System] visão geral](../../xdm/home.md). Ao combinar o Serviço de consulta com o [!DNL Experience Events], é possível rastrear com eficiência as tendências comportamentais entre os usuários. Este documento fornece exemplos de consultas envolvendo [!DNL Experience Events].

## Objetivo

O exemplo a seguir lista as últimas 100 páginas que um usuário especificado visualizou.

```sql
SELECT 
timestamp, 
web.webReferrer.type as referrerType, 
web.webReferrer.URL as referrer, 
web.webPageDetails.name as pageName, 
_experience.analytics.event1to100.event1.value as A, 
_experience.analytics.event1to100.event2.value as B, 
_experience.analytics.event1to100.event3.value as C, 
web.webPageDetails.pageviews.value as pageViews
FROM your_analytics_table 
WHERE endUserIds._experience.aaid.id = '457C3510571E5930-69AA721C4CBF9339' 
ORDER BY timestamp 
LIMIT 100;
```

Os resultados dessa query podem ser vistos abaixo.

```console
      timestamp       |  referrerType  |                            referrer                                |                 pageName            |  A  |  B  |  C  | pageViews
|----------------------+----------------+--------------------------------------------------------------------+-------------------------------------+-----+-----+-----+--------------
2019-11-08 17:15:28.0 | typed_bookmark |                                                                    |                                     |     |     |     |
2019-11-08 17:53:05.0 | social         | http://www.reddit.com                                              | Home                                |     |     |     |          1.0
2019-11-08 17:53:45.0 | typed_bookmark |                                                                    | Kids                                |     |     |     |          1.0
2019-11-08 19:22:34.0 | typed_bookmark |                                                                    |                                     |     |     |     |          
2019-11-08 20:01:12.0 | search_engine  | http://www.google.com/search?ie=UTF-8&q=laundry parkas&cid=sem:115 | Home                                |     |     |     |          1.0 
2019-11-08 20:01:57.0 | typed_bookmark |                                                                    | Kids                                |     |     |     |          1.0
2019-11-08 20:03:36.0 | typed_bookmark |                                                                    | Search Results                      | 1.0 |     |     |          1.0
2019-11-08 20:04:30.0 | typed_bookmark |                                                                    | Product Details: Pemmican Power Bar |     |     |     |          1.0
2019-11-08 20:05:27.0 | typed_bookmark |                                                                    | Shopping Cart: Cart Details         |     |     |     |          1.0
2019-11-08 20:06:07.0 | typed_bookmark |                                                                    | Shopping Cart: Shipping Information |     |     |     |          1.0
2019-11-08 20:07:02.0 | typed_bookmark |                                                                    | Shopping Cart: Billing Information  |     |     | 1.0 |          1.0
2019-11-08 20:07:52.0 | typed_bookmark |                                                                    | Shopping Cart: Order Review         |     |     |     |          1.0
2019-11-08 20:08:45.0 | typed_bookmark |                                                                    | Order Confirmation                  |     |     |     |          1.0
2019-11-08 20:09:24.0 | typed_bookmark |                                                                    | Home                                |     |     |     |          1.0
2019-11-08 20:10:03.0 | typed_bookmark |                                                                    | Editorial Page: Camping Essentials  |     |     |     |          1.0
2019-11-08 20:11:01.0 | typed_bookmark |                                                                    | Account Registration|Form           |     |     |     |          1.0
2019-11-08 20:11:38.0 | typed_bookmark |                                                                    | Seasonal Sale                       |     |     |     |          1.0
2019-11-08 20:12:10.0 | typed_bookmark |                                                                    | Blog: Iris Sagan                    |     |     |     |          1.0
2019-11-08 20:13:09.0 | typed_bookmark |                                                                    | Product Details: UltraTech Socks    |     |     |     |          1.0
2019-11-08 20:14:05.0 | typed_bookmark |                                                                    | Seasonal Sale                       |     |     |     |          1.0
```

## Próximas etapas {#next-steps}

Ao ler este documento, você entende melhor como usar o Serviço de Consulta com [!DNL Experience Events] para listar as exibições de página como um usuário especificado.

Consulte os seguintes casos de uso para saber mais sobre outros casos de uso com base em visitantes:

- [Recupere uma lista de visitantes organizada por número de exibições de página.](./visitors-by-number-of-page-views.md)
- [Exibir um relatório de rollup de um visitante.](./roll-up-report-of-a-visitor.md)
- [Criar um relatório de tendências de eventos por dia.](./trended-report-of-events.md)
