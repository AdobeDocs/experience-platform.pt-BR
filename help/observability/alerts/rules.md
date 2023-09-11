---
keywords: Experience Platform;página inicial;tópicos populares;intervalo de datas
title: Regras de alerta padrão
description: Este documento aborda as regras de alerta predefinidas fornecidas pelo Experience Platform.
feature: Alerts
exl-id: b4af1c15-b1bc-4e4b-a447-09cc17a63988
source-git-commit: 9120377f5f2048579d7e2a4740cfcbc56d49d61a
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 1%

---

# Regras de alerta padrão

A Adobe Experience Platform fornece várias regras de alerta predefinidas que você pode ativar para sua organização. Este documento aborda os detalhes dessas regras de alerta fornecidas por Adobe. Para obter informações mais gerais sobre alertas no Experience Platform, consulte [visão geral dos alertas](./overview.md).

Quando [exibição de regras de alerta na interface do usuário da Platform](./ui.md), você pode assinar cada regra individualmente. Ao assinar alertas por meio do [Notificações de Eventos de E/S](./subscribe.md)No entanto, as regras de alerta são organizadas em diferentes pacotes de assinatura. Nas tabelas abaixo, cada regra é mostrada com seu nome de inscrição de Evento de E/S correspondente.

## Assimilação de dados

As seguintes regras de alerta são específicas do [Assimilação de dados](../../ingestion/home.md) e  [origens](../../sources/home.md):

>[!NOTE]
>
>Atualmente, os alertas não oferecem suporte para fontes de transmissão. Você só pode assinar notificações de alerta para origens de lote.

| Inscrição no evento de E/S | Regra de alerta | Descrição |
| --- | --- | --- |
| Informações de execução do fluxo de origem | Início da execução do fluxo de fontes | Esse alerta é disparado quando uma conexão de origem inicia o processamento de dados. |
| Informações de execução do fluxo de origem | Êxito na execução do fluxo de fontes | Esse alerta é disparado quando os dados são assimilados com êxito de uma conexão de origem. |
| Atrasos, falhas e erros na execução do fluxo de origem | Falha na execução do fluxo de fontes | Esse alerta é disparado quando ocorre um erro ao assimilar dados de uma conexão de origem. |
| Atrasos, falhas e erros na execução do fluxo de origem | Atraso de assimilação | Esse alerta é disparado quando uma execução de fluxo de assimilação de lote demora mais de 150 minutos para ser processada. |
| Atrasos, falhas e erros na execução do fluxo de origem | Falha na assimilação | Esse alerta é disparado quando a proporção de registros com falha para todos os registros excede um limite de 0,5%. |

{style="table-layout:auto"}

Se você se inscreveu anteriormente no seguinte tipo de alerta, não receberá mais alertas, pois esse alerta foi descontinuado:

| Inscrição no evento de E/S | Regra de alerta | Descrição |
| --- | --- | --- |
| Atrasos, falhas e erros na execução do fluxo de origem | Falta de assimilação | Esse alerta envia uma mensagem se a assimilação for atrasada em mais de sete horas e nenhum dado for assimilado na Platform. |

{style="table-layout:auto"}

## Identity Service

As seguintes regras de alerta são específicas do [Serviço de identidade](../../identity-service/home.md):

| Inscrição no evento de E/S | Regra de alerta | Descrição |
| --- | --- | --- |
| Informações de assimilação de identidade | Início da execução do fluxo do serviço de identidade | Esse alerta é disparado quando uma execução do fluxo do Serviço de identidade inicia o processamento dos dados. Em outras palavras, os dados assimilados estão sendo carregados do Data Lake no Serviço de identidade. |
| Informações de assimilação de identidade | Êxito na execução do fluxo do serviço de identidade | Esse alerta é disparado quando os dados são carregados com êxito do Data Lake no Serviço de identidade. |
| Atrasos, falhas e erros na assimilação de identidade | Atraso na execução do fluxo do serviço de identidade | Esse alerta é disparado quando uma execução do fluxo do Serviço de identidade demora mais de 150 minutos para ser processada. |
| Atrasos, falhas e erros na assimilação de identidade | Falha na execução do fluxo do serviço de identidade | Esse alerta é disparado quando ocorre um erro ao assimilar dados no Serviço de identidade. |

{style="table-layout:auto"}

## Perfil do cliente em tempo real

As seguintes regras de alerta são específicas do [Perfil do cliente em tempo real](../../profile/home.md):

| Inscrição no evento de E/S | Regra de alerta | Descrição |
| --- | --- | --- |
| Informações de assimilação de perfil | Início da execução do fluxo de perfil | Esse alerta é acionado quando uma execução do fluxo de perfil inicia o processamento dos dados. |
| Informações de assimilação de perfil | Êxito na execução do fluxo de perfil | Esse alerta é disparado quando os dados são carregados com êxito no Perfil do Data Lake. |
| Atrasos, falhas e erros na assimilação de perfis | Atraso na execução do fluxo de perfil | Esse alerta é acionado ao carregar dados do Data Lake no Perfil que leva mais de 150 minutos para ser processado. |
| Atrasos, falhas e erros na assimilação de perfis | Falha na execução do fluxo de perfil | Esse alerta é disparado quando ocorre um erro ao assimilar dados no Perfil. |

{style="table-layout:auto"}

## Segmentação

As seguintes regras de alerta são específicas do [Serviço de segmentação](../../segmentation/home.md):

| Inscrição no evento de E/S | Regra de alerta | Descrição |
| --- | --- | --- |
| Informações do trabalho de avaliação do segmento | Início do trabalho de segmento | Esse alerta é disparado quando um trabalho de avaliação de segmento inicia o processamento de dados. |
| Informações do trabalho de avaliação do segmento | Sucesso do trabalho do segmento | Esse alerta é disparado quando um trabalho de avaliação de segmento é concluído com sucesso. |
| Atrasos, falhas e erros no trabalho de avaliação de segmento | Atraso no trabalho do segmento | Esse alerta é acionado quando os trabalhos de avaliação de um segmento levam mais de 150 minutos para serem concluídos. <br> Um dos seguintes status será exibido: <br>- ACIONAMENTO - A condição de falha ou atraso foi atendida (Considere-a em um estado ATIVO). <br>- INATIVO - A condição não foi atendida ou não foi resolvida (Considere-a em um estado RESOLVIDO). |
| Atrasos, falhas e erros no trabalho de avaliação de segmento | Falha no trabalho do segmento | Esse alerta é acionado quando um trabalho de avaliação de segmento resulta em um erro. |
| Atrasos, falhas e erros no trabalho de avaliação de segmento | Definição de segmento desativada | Esse alerta é disparado quando uma definição de segmento é desativada devido a um erro interno. Isso aciona automaticamente uma sala de guerra para que uma equipe de engenharia de Adobe investigue o problema. Este alerta é apenas informativo e não requer nenhuma ação sua. |

{style="table-layout:auto"}

## Destinos

As seguintes regras de alerta são específicas do [destinos](../../destinations/home.md):

| Inscrição no evento de E/S | Regra de alerta | Descrição |
| --- | --- | --- |
| Informações de execução do fluxo de destino | Início da execução do fluxo de destino | Esse alerta é acionado quando uma execução de fluxo de destino começa a ativar um segmento. |
| Informações de execução do fluxo de destino | Êxito na execução do fluxo de destino | Esse alerta é disparado quando um segmento é ativado com êxito para um destino. |
| Atrasos, falhas e erros na execução do fluxo de destino | Atraso na execução do fluxo de destino | Esse alerta é acionado quando uma execução de fluxo de destino leva mais de 150 minutos para ativar um segmento. |
| Atrasos, falhas e erros na execução do fluxo de destino | Falha na execução do fluxo de destino | Esse alerta é disparado quando ocorre um erro ao ativar um segmento para um destino. |
| Atrasos, falhas e erros na execução do fluxo de destino | A taxa de salto excede o limite | Esse alerta é disparado quando a proporção de IDs ignoradas em relação ao total de IDs excede um limite. |

{style="table-layout:auto"}

## Query Service

As seguintes regras de alerta são específicas do [Serviço de consulta](../../query-service/home.md):

| Inscrição no evento de E/S | Regra de alerta | Descrição |
| --- | --- | --- |
| Informações de consulta agendada do serviço de consulta | Início da consulta agendada do Serviço de Consulta | Esse alerta é disparado quando uma consulta agendada começa a ser executada. |
| Informações de consulta agendada do serviço de consulta | Êxito na consulta agendada do Serviço de consulta | Este alerta é disparado quando um trabalho de consulta agendado é concluído com sucesso. |
| Atrasos, falhas e erros na consulta programada do Serviço de consulta | falha na consulta agendada do serviço de consulta | Esse alerta é disparado quando um trabalho de consulta agendado falha. |

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
