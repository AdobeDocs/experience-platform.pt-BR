---
keywords: Experience Platform;página inicial;tópicos populares;serviço de consulta;serviço de consulta;consultas experienceevent;consulta experienceevent;consulta Experience Event;
title: Exibir um relatório de rollup para um visitante específico
description: O documento a seguir fornece exemplos de consultas envolvendo eventos de experiência no serviço de consulta da Adobe Experience Platform.
exl-id: 1348503f-65c1-41f9-b111-1284a49449a1
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 1%

---

# Exibir um relatório de rollup para um visitante específico

Este documento fornece um exemplo de SQL para agregar dados de várias propriedades de análise para um usuário específico e ver esses dados juntos em um relatório. Com o Serviço de Consulta da Adobe Experience Platform, você pode gravar consultas que usam o [!DNL Experience Events] para capturar uma variedade de casos de uso. Eventos de experiência são representados pela classe Experience Data Model (XDM) ExperienceEvent, que captura um instantâneo imutável e não agregado do sistema quando um usuário interage com um site ou serviço. Eventos de experiência podem até ser usados para análise de domínio de tempo. Consulte a [seção das próximas etapas](#next-steps) para obter mais casos de uso que envolvem [!DNL Experience Events] para gerar relatórios de visitantes.

Mais informações sobre o XDM e o [!DNL Experience Events] podem ser encontradas na [[!DNL XDM System] visão geral](../../xdm/home.md). Ao combinar o Serviço de consulta com o [!DNL Experience Events], é possível rastrear com eficiência as tendências comportamentais entre os usuários. Este documento fornece exemplos de consultas envolvendo [!DNL Experience Events].

## Objetivo

O exemplo SQL a seguir mostra como exibir um relatório agregado de vários valores de análise para um usuário especificado.

```sql
SELECT 
endUserIds._experience.aaid.id, 
SUM(web.webPageDetails.pageviews.value) as pageViews, 
SUM(_experience.analytics.event1to100.event1.value) as A, 
SUM(_experience.analytics.event1to100.event2.value) as B, 
SUM(_experience.analytics.event1to100.event3.value) as C,
SUM(
    CASE 
    WHEN _experience.analytics.customDimensions.evars.evar1 = 'parkas' 
    THEN 1 
    ELSE 0 
    END) as viewedParkas
FROM your_analytics_table 
WHERE endUserIds._experience.aaid.id = '457C3510571E5930-69AA721C4CBF9339' 
GROUP BY endUserIds._experience.aaid.id
ORDER BY pageViews DESC;
```

Os resultados da query são exibidos na tabela abaixo.

```console
               id                 | pageViews |   A   |   B   |   C   | viewedParkas
|----------------------------------+-----------+-------+-------+-------+--------------
457C3510571E5930-69AA721C4CBF9339 |     706.0 | 83.0  |  7.0  | 38.0  |          22
```

## Próximas etapas {#next-steps}

Ao ler este documento, você compreenderá melhor como usar o Serviço de Consulta com [!DNL Experience Events] para exibir um relatório agregado de valores de análise para um usuário especificado.

Consulte os seguintes casos de uso para saber mais sobre outros casos de uso com base em visitantes:

- [Recupere uma lista de visitantes organizada por número de exibições de página.](./visitors-by-number-of-page-views.md)
- [Liste as sessões anteriores de um visitante.](./list-visitor-sessions.md)
- [Criar um relatório de tendências de eventos por dia.](./trended-report-of-events.md)
