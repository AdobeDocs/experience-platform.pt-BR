---
keywords: Experience Platform, home, tópicos populares, intervalo de datas
title: Regras padrão de alerta
description: Este documento aborda as regras de alerta predefinidas fornecidas pelo Experience Platform.
feature: Alerts
exl-id: b4af1c15-b1bc-4e4b-a447-09cc17a63988
source-git-commit: 67aef7ca2ad4061003af8d91fb29339397d8af01
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 3%

---

# Regras padrão de alerta

O Adobe Experience Platform fornece várias regras de alerta predefinidas que podem ser ativadas para sua organização. Este documento aborda os detalhes dessas regras de alerta fornecidas por Adobe. Para obter informações mais gerais sobre alertas no Experience Platform, consulte o [visão geral dos alertas](./overview.md).

When [exibição de regras de alerta na interface do usuário da plataforma](./ui.md), é possível assinar cada regra individualmente. Ao assinar alertas por meio de [Notificações de Evento de E/S](./subscribe.md), no entanto, as regras de alerta são organizadas em pacotes de assinatura diferentes. Nas tabelas abaixo, cada regra é exibida com o nome de assinatura do Evento de E/S correspondente.

## Assimilação de dados

As seguintes regras de alerta são específicas para [Assimilação de dados](../../ingestion/home.md) e  [fontes](../../sources/home.md):

| Assinatura de Evento de E/S | Regra de alerta | Descrição |
| --- | --- | --- |
| Informações de Execução do Fluxo de Origem | Início da Execução de Fluxo de Fontes | Esse alerta é disparado quando uma conexão de origem inicia o processamento de dados. |
| Informações de Execução do Fluxo de Origem | Êxito na Execução do Fluxo de Fontes | Esse alerta dispara quando os dados são assimilados com êxito de uma conexão de origem. |
| Atrasos, falhas e erros de execução do fluxo de origem | Falha na Execução do Fluxo de Fontes | Esse alerta dispara quando ocorre um erro ao assimilar dados de uma conexão de origem. |
| Atrasos, falhas e erros de execução do fluxo de origem | Atraso de assimilação | Esse alerta é disparado quando a execução de um fluxo de ingestão em lote demora mais de 150 minutos para ser processada. |
| Atrasos, falhas e erros de execução do fluxo de origem | Falta de assimilação | Esse alerta envia uma mensagem se a assimilação for atrasada em mais de sete horas e nenhum dado for assimilado na Platform. |
| Atrasos, falhas e erros de execução do fluxo de origem | Falha de Assimilação | Esse alerta dispara quando a proporção de registros com falha para todos os registros excede um limite de 0,5%. |
| Atrasos, falhas e erros de execução do fluxo de origem | A taxa de página ignorada excede o limite | Esse alerta é disparado quando a proporção de ids ignoradas em relação ao total de ids excede um limite. |

{style=&quot;table-layout:auto&quot;}

## Identity Service

As seguintes regras de alerta são específicas para [Serviço de identidade](../../identity-service/home.md):

| Assinatura de Evento de E/S | Regra de alerta | Descrição |
| --- | --- | --- |
| Informações de assimilação de identidade | Início da Execução do Fluxo do Serviço de Identidade | Esse alerta é disparado quando uma execução de fluxo do Serviço de identidade inicia o processamento de dados. Em outras palavras, dados assimilados estão sendo carregados do Data Lake para o Serviço de identidade. |
| Informações de assimilação de identidade | Êxito na Execução do Fluxo do Serviço de Identidade | Esse alerta dispara quando os dados são carregados com êxito do Data Lake no Identity Service. |
| Atrasos, falhas e erros da assimilação de identidade | Atraso na Execução do Fluxo do Serviço de Identidade | Esse alerta é disparado quando uma execução do fluxo do Serviço de identidade demora mais de 150 minutos para ser processada. |
| Atrasos, falhas e erros da assimilação de identidade | Falha na Execução do Fluxo do Serviço de Identidade | Esse alerta dispara quando ocorre um erro ao assimilar dados no Serviço de identidade. |

{style=&quot;table-layout:auto&quot;}

## Perfil do cliente em tempo real

As seguintes regras de alerta são específicas para [Perfil do cliente em tempo real](../../profile/home.md):

| Assinatura de Evento de E/S | Regra de alerta | Descrição |
| --- | --- | --- |
| Informações de assimilação de perfil | Início da execução do fluxo de perfil | Esse alerta é disparado quando uma execução de fluxo de Perfil inicia o processamento de dados. |
| Informações de assimilação de perfil | Êxito na Execução do Fluxo de Perfil | Esse alerta é disparado quando os dados são carregados com êxito no Perfil a partir do Data Lake. |
| Atrasos, falhas e erros de assimilação de perfil | Atraso de execução do fluxo de perfil | Esse alerta é disparado ao carregar dados do Data Lake no Profile por mais de 150 minutos. |
| Atrasos, falhas e erros de assimilação de perfil | Falha na execução do fluxo de perfil | Esse alerta dispara quando ocorre um erro ao assimilar dados no Perfil. |

{style=&quot;table-layout:auto&quot;}

## Segmentação

As seguintes regras de alerta são específicas para [Serviço de segmentação](../../segmentation/home.md):

| Assinatura de Evento de E/S | Regra de alerta | Descrição |
| --- | --- | --- |
| Informações do trabalho de avaliação de segmento | Início do trabalho de segmento | Esse alerta é disparado quando um trabalho de avaliação de segmento inicia o processamento de dados. |
| Informações do trabalho de avaliação de segmento | Êxito do trabalho de segmento | Esse alerta é disparado quando um trabalho de avaliação de segmento é concluído com êxito. |
| Atrasos, falhas e erros do trabalho de avaliação de segmentos | Atraso no trabalho do segmento | Esse alerta é disparado quando as tarefas de avaliação de segmento levam mais de 150 minutos para serem concluídas. |
| Atrasos, falhas e erros do trabalho de avaliação de segmentos | Falha no trabalho do segmento | Esse alerta é disparado quando um trabalho de avaliação de segmento resulta em um erro. |
| Atrasos, falhas e erros do trabalho de avaliação de segmentos | Definição de segmento desativada | Esse alerta dispara quando uma definição de segmento é desativada devido a um erro interno. Isso aciona automaticamente uma sala de guerra para uma equipe de engenharia de Adobe para investigar o problema. Este alerta destina-se apenas a ser informativo e não requer nenhuma ação da sua parte. |

{style=&quot;table-layout:auto&quot;}

## Destinos

As seguintes regras de alerta são específicas para [destinos](../../destinations/home.md):

| Assinatura de Evento de E/S | Regra de alerta | Descrição |
| --- | --- | --- |
| Informações de execução do fluxo de destino | Início da Execução do Fluxo de Destino | Esse alerta é disparado quando uma execução de fluxo de destino inicia a ativação de um segmento. |
| Informações de execução do fluxo de destino | Êxito na Execução do Fluxo de Destino | Esse alerta é disparado quando um segmento é ativado com êxito para um destino. |
| Atrasos de execução, falhas e erros do fluxo de destino | Atraso de execução do fluxo de destino | Esse alerta é disparado quando uma execução de fluxo de destino demora mais de 150 minutos para ativar um segmento. |
| Atrasos de execução, falhas e erros do fluxo de destino | Falha na Execução do Fluxo de Destino | Esse alerta dispara quando ocorre um erro ao ativar um segmento para um destino. |

{style=&quot;table-layout:auto&quot;}

<!-- (Definitions to be added once available)
| Segment Job Delay | This alert triggers when a segment job takes longer than 150 minutes to complete. | N/A | 30 seconds | 3 hours |
| No Ingestion Activity in Past 24 Hours | This alert triggers when no new data has been ingested in the last 24-hour period. | N/A | 1 day | 1 day |
| Ingestion Error Rate Exceeded | This alert triggers when the error rate for data ingestion exceeds the allotted threshold. | 20% | 30 seconds | 30 seconds |
| Entitlement Threshold Exceeded | This alert triggers when the number of created profiles exceeds 80% of your organization's entitlement. | 30 seconds | N/A |
| SFTP source has not ingested data | This alert triggers when an [SFTP source](../../sources/connectors/cloud-storage/sftp.md) has not ingested any data within a certain time period. | 1 day | 1 day |
| Feed Message | This alert when an identity sharing feed message has been sent to a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Access Revoked | This alert triggers when another Platform user revokes access to an identity sharing feed using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Modified | This alert triggers when an identity sharing feed is modified by a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Shared | This alert triggers when a user shares a new feed in [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Link Request | This alert triggers when a user requests to connect for partner sharing. | N/A | N/A |
| Link Action | This alert triggers when a user accepts a request to connect for partner sharing. | N/A | N/A |
-->
