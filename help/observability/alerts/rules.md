---
keywords: Experience Platform, home, tópicos populares, intervalo de datas
title: Regras padrão de alerta
description: Este documento aborda as regras de alerta predefinidas fornecidas pelo Experience Platform.
feature: Alerts
exl-id: b4af1c15-b1bc-4e4b-a447-09cc17a63988
source-git-commit: d82487f34c0879ed27ac55e42d70346f45806131
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 12%

---

# Regras padrão de alerta

O Adobe Experience Platform fornece várias regras de alerta predefinidas que podem ser ativadas para sua organização. A tabela abaixo cobre os detalhes dessas regras de alerta fornecidas por Adobe. Para obter informações mais gerais sobre alertas no Experience Platform, consulte a [visão geral de alertas](./overview.md).

| Regra | Descrição | Frequência de avaliação | Repetir janela |
| --- | --- | --- | --- |
| Êxito na Execução do Fluxo de Fontes | Esse alerta dispara quando os dados são assimilados com êxito de uma conexão de origem. | N/D | N/D |
| Falha na Execução do Fluxo de Fontes | Esse alerta dispara quando ocorre um erro ao assimilar dados de uma conexão de origem. | N/D | N/D |
| Atraso no trabalho do segmento | Esse alerta é disparado quando as tarefas de um segmento levam mais de 150 minutos para serem concluídas. | 30 segundos | 3 horas |
| Definição de segmento desativada | Esse alerta é disparado quando uma definição de segmento é desativada. | N/D | N/D |

{style=&quot;table-layout:auto&quot;}

<!-- (Definitions to be added once available)
| Entitlement Threshold Exceeded | This alert triggers when the number of created profiles exceeds 80% of your organization's entitlement. | 30 seconds | N/A |
| No ingestion activity in past 24 hours | This alert triggers when no new data has been ingested in the last 24-hour period. | 1 day | 1 day |
| SFTP source has not ingested data | This alert triggers when an [SFTP source](../../sources/connectors/cloud-storage/sftp.md) has not ingested any data within a certain time period. | 1 day | 1 day |
| Ingestion error rate exceeded | This alert triggers when the error rate for data ingestion exceeds 20%. | 30 seconds | 30 seconds |
| Feed Message | This alert when an identity sharing feed message has been sent to a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Access Revoked | This alert triggers when another Platform user revokes access to an identity sharing feed using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Modified | This alert triggers when an identity sharing feed is modified by a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Shared | This alert triggers when a user shares a new feed in [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Link Request | This alert triggers when a user requests to connect for partner sharing. | N/A | N/A |
| Link Action | This alert triggers when a user accepts a request to connect for partner sharing. | N/A | N/A |
-->
