---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, consultas de evento de experiência, consulta de evento de experiência, consulta de evento de experiência, consulta de evento de experiência;
title: Listar as exibições de página de um usuário
description: Saiba como gravar consultas que usam Eventos de experiência para criar uma lista das últimas 100 páginas que um usuário especificado usou.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 1%

---

# Listar as exibições de página de um usuário

Este documento fornece um exemplo do SQL necessário para listar as exibições de página de um usuário especificado. Com o Adobe Experience Platform Query Service, você pode gravar consultas que usam [!DNL Experience Events] para capturar uma variedade de casos de uso. Os Eventos de experiência são representados pela classe ExperienceEvent do Experience Data Model (XDM), que captura um instantâneo imutável e não agregado do sistema quando um usuário interage com um site ou serviço. Os Eventos de experiência podem ser usados para análise de domínio de tempo. Consulte a [seção próximas etapas](#next-steps) para mais casos de uso que envolvam [!DNL Experience Events] para gerar relatórios de visitante.

Mais informações sobre o XDM e [!DNL Experience Events] podem ser encontradas no [[!DNL XDM System] visão geral](../../xdm/home.md). Ao combinar o Serviço de query com [!DNL Experience Events], você pode efetivamente rastrear tendências comportamentais entre seus usuários. O documento a seguir fornece exemplos de consultas envolvendo [!DNL Experience Events].

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

Os resultados desta consulta podem ser vistos abaixo.

```console
      timestamp       |  referrerType  |                            referrer                                |                 pageName            |  A  |  B  |  C  | pageViews
----------------------+----------------+--------------------------------------------------------------------+-------------------------------------+-----+-----+-----+--------------
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

Ao ler este documento, você tem uma melhor compreensão de como usar o Serviço de query com [!DNL Experience Events] para listar as exibições de página como um usuário especificado.

Consulte os seguintes casos de uso para saber mais sobre outros casos de uso baseados em visitantes:

- [Recupere uma lista de visitantes organizados pelo número de exibições da página.](./visitors-by-number-of-page-views.md)
- [Exibir um relatório de roll-up de um visitante.](./roll-up-report-of-a-visitor.md)
- [Crie um relatório de tendências de eventos por dia.](./trended-report-of-events.md)
