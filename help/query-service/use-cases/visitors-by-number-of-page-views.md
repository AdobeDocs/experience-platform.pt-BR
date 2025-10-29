---
keywords: Experience Platform;página inicial;tópicos populares;serviço de consulta;serviço de consulta;consultas experienceevent;consulta experienceevent;consulta Experience Event;
title: Listar visitantes pelo número de visualizações de página
description: Saiba como escrever consultas que usam Eventos de experiência para recuperar uma lista de visitantes organizada pelo número de exibições de página.
exl-id: 6e8eed0c-838e-4cd0-ae8c-453114fbf4ea
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 1%

---

# Listar visitantes pelo número de exibições de página

Este documento fornece um exemplo do SQL necessário para recuperar uma lista de visitantes organizada pelo número de exibições de página. Com o Serviço de Consulta da Adobe Experience Platform, você pode gravar consultas que usam o [!DNL Experience Events] para capturar uma variedade de casos de uso. Eventos de experiência são representados pela classe Experience Data Model (XDM) ExperienceEvent, que captura um instantâneo imutável e não agregado do sistema quando um usuário interage com um site ou serviço. Eventos de experiência podem até ser usados para análise de domínio de tempo. Consulte a [seção das próximas etapas](#next-steps) para obter mais casos de uso que envolvem [!DNL Experience Events] para gerar relatórios de visitantes.

Mais informações sobre o XDM e o [!DNL Experience Events] podem ser encontradas na [[!DNL XDM System] visão geral](../../xdm/home.md). Ao combinar o Serviço de consulta com o [!DNL Experience Events], é possível rastrear com eficiência as tendências comportamentais entre os usuários. Este documento fornece exemplos de consultas envolvendo [!DNL Experience Events].

## Objetivo

O exemplo a seguir cria um relatório que lista as 10 IDs dos usuários que visualizaram a maioria das páginas.

```sql
SELECT 
endUserIds._experience.aaid.id, 
SUM(web.webPageDetails.pageviews.value) as pageViews 
FROM your_analytics_table
GROUP BY endUserIds._experience.aaid.id 
ORDER BY pageViews DESC
LIMIT 10;
```

Os resultados da query são exibidos na tabela abaixo.

```console
               id                  | pageViews
|-----------------------------------+-----------
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

Ao ler este documento, você entende melhor como usar o Serviço de Consulta com [!DNL Experience Events] para listar usuários que visualizaram mais páginas.

Consulte os seguintes casos de uso para saber mais sobre outros casos de uso com base em visitantes:

- [Liste as sessões anteriores de um visitante.](./list-visitor-sessions.md)
- [Exibir um relatório de rollup de um visitante.](./roll-up-report-of-a-visitor.md)
- [Criar um relatório de tendências de eventos por dia.](./trended-report-of-events.md)
