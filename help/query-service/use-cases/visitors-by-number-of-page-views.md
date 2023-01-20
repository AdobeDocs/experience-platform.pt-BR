---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, consultas de evento de experiência, consulta de evento de experiência, consulta de evento de experiência, consulta de evento de experiência;
title: Listar visitantes por seu número de exibições de página
description: Saiba como gravar consultas que usam Eventos de experiência para recuperar uma lista de visitantes organizada pelo número de visualizações de página.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 1%

---

# Listar visitantes por seu número de exibições de página

Este documento fornece um exemplo do SQL necessário para recuperar uma lista de visitantes organizada pelo número de exibições de página. Com o Adobe Experience Platform Query Service, você pode gravar consultas que usam [!DNL Experience Events] para capturar uma variedade de casos de uso. Os Eventos de experiência são representados pela classe ExperienceEvent do Experience Data Model (XDM), que captura um instantâneo imutável e não agregado do sistema quando um usuário interage com um site ou serviço. Os Eventos de experiência podem ser usados para análise de domínio de tempo. Consulte a [seção próximas etapas](#next-steps) para mais casos de uso que envolvam [!DNL Experience Events] para gerar relatórios de visitante.

Mais informações sobre o XDM e [!DNL Experience Events] podem ser encontradas no [[!DNL XDM System] visão geral](../../xdm/home.md). Ao combinar o Serviço de query com [!DNL Experience Events], você pode efetivamente rastrear tendências comportamentais entre seus usuários. O documento a seguir fornece exemplos de consultas envolvendo [!DNL Experience Events].

## Objetivo

O exemplo a seguir cria um relatório que lista as 10 IDs dos usuários que mais visualizaram.

```sql
SELECT 
endUserIds._experience.aaid.id, 
SUM(web.webPageDetails.pageviews.value) as pageViews 
FROM your_analytics_table
GROUP BY endUserIds._experience.aaid.id 
ORDER BY pageViews DESC
LIMIT 10;
```

Os resultados da consulta são exibidos na tabela abaixo.

```console
               id                  | pageViews
-----------------------------------+-----------
 457C3510571E5930-69AA721C4CBF9339 |     706.0
 776F85658792C017-6491FE6570382A01 |     700.0
 6BEC9C6AB52E779F-28F5B023113F2C85 |     654.0
 1C0CCFB2DC63611E-6E4A4D4142AEB613 |     642.0
 112EE9A6F3BE29D1-514A6C355A2C9EF6 |     629.0
 CCC75A0E6AC7F2FA-11D58515D370F626 |     624.0
 749F850A44153120-3710C53FA2162349 |     614.0
 2B668C6DDDAF0C505-92EDCC072F7CDDA |     587.0
 7EB7257335935320-101921AF45111FE6 |     586.0
 5F4759CA80DCA9C9-2C0DA93D80D9DBFA |     586.0
(10 rows)
```

## Próximas etapas {#next-steps}

Ao ler este documento, você tem uma melhor compreensão de como usar o Serviço de query com [!DNL Experience Events] para listar usuários que visualizaram mais páginas.

Consulte os seguintes casos de uso para saber mais sobre outros casos de uso baseados em visitantes:

- [Lista as sessões anteriores de um visitante.](./list-visitor-sessions.md)
- [Exibir um relatório de roll-up de um visitante.](./roll-up-report-of-a-visitor.md)
- [Crie um relatório de tendências de eventos por dia.](./trended-report-of-events.md)
