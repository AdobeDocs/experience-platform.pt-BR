---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, consultas de evento de experiência, consulta de evento de experiência, consulta de evento de experiência, consulta de evento de experiência;
title: Exibir um relatório de roll-up de um visitante específico
description: O documento a seguir fornece exemplos de consultas envolvendo Eventos de experiência no Adobe Experience Platform Query Service.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 1%

---

# Exibir um relatório de roll-up de um visitante específico

Este documento fornece um exemplo SQL para agregar dados de várias propriedades de análise de um usuário específico e ver esses dados juntos em um relatório. Com o Adobe Experience Platform Query Service, você pode gravar consultas que usam [!DNL Experience Events] para capturar uma variedade de casos de uso. Os Eventos de experiência são representados pela classe ExperienceEvent do Experience Data Model (XDM), que captura um instantâneo imutável e não agregado do sistema quando um usuário interage com um site ou serviço. Os Eventos de experiência podem ser usados para análise de domínio de tempo. Consulte a [seção próximas etapas](#next-steps) para mais casos de uso que envolvam [!DNL Experience Events] para gerar relatórios de visitante.

Mais informações sobre o XDM e [!DNL Experience Events] podem ser encontradas no [[!DNL XDM System] visão geral](../../xdm/home.md). Ao combinar o Serviço de query com [!DNL Experience Events], você pode efetivamente rastrear tendências comportamentais entre seus usuários. O documento a seguir fornece exemplos de consultas envolvendo [!DNL Experience Events].

## Objetivo

O exemplo SQL a seguir mostra como visualizar um relatório agregado de vários valores de análise de um usuário especificado.

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

Os resultados da consulta são exibidos na tabela abaixo.

```console
               id                 | pageViews |   A   |   B   |   C   | viewedParkas
----------------------------------+-----------+-------+-------+-------+--------------
457C3510571E5930-69AA721C4CBF9339 |     706.0 | 83.0  |  7.0  | 38.0  |          22
```

## Próximas etapas {#next-steps}

Ao ler este documento, você tem uma melhor compreensão de como usar o Serviço de query com [!DNL Experience Events] para exibir um relatório agregado de valores de análise para um usuário especificado.

Consulte os seguintes casos de uso para saber mais sobre outros casos de uso baseados em visitantes:

- [Recupere uma lista de visitantes organizados pelo número de exibições da página.](./visitors-by-number-of-page-views.md)
- [Lista as sessões anteriores de um visitante.](./list-visitor-sessions.md)
- [Crie um relatório de tendências de eventos por dia.](./trended-report-of-events.md)
