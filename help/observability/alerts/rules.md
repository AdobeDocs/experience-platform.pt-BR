---
keywords: Experience Platform, home, tópicos populares, intervalo de datas
title: Regras padrão de alerta
description: 'Este documento aborda as regras de alerta predefinidas fornecidas pelo Experience Platform. '
source-git-commit: 8c00fb98a213b578f6970c1e1978f0159f8f38df
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 13%

---


# Regras padrão de alerta

O Adobe Experience Platform fornece várias regras de alerta predefinidas que podem ser ativadas para sua organização. A tabela abaixo cobre os detalhes dessas regras de alerta fornecidas por Adobe. Para obter informações mais gerais sobre alertas no Experience Platform, consulte a [visão geral de alertas](./overview.md).

| Regra | Descrição | Frequência de avaliação | Repetir janela |
| --- | --- | --- | --- |
| Limite De Direito Excedido | Esse alerta é disparado quando o número de perfis criados excede 80% do direito da organização. | 30 segundos | N/D |
| Nenhuma atividade de ingestão nas últimas 24 horas | Esse alerta é disparado quando nenhum novo dado é assimilado nos últimos 24 horas. | 1 dia | 1 dia |
| A fonte SFTP não assimilou dados | Esse alerta é disparado quando uma [fonte SFTP](../../sources/connectors/cloud-storage/sftp.md) não assimilou dados em um determinado período de tempo. | 1 dia | 1 dia |
| Taxa de erro de assimilação excedida | Esse alerta é disparado quando a taxa de erro para a assimilação de dados excede 20%. | 30 segundos | 30 segundos |
| Mensagem de feed | Este alerta quando uma mensagem de feed de compartilhamento de identidade for enviada a um usuário usando [Correspondência de segmento](../../segmentation/ui/segment-match.md). | N/D | N/D |
| Acesso ao feed Revogado | Esse alerta é disparado quando outro usuário da Platform revoga o acesso a um feed de compartilhamento de identidade usando [Correspondência de segmento](../../segmentation/ui/segment-match.md). | N/D | N/D |
| Feed modificado | Esse alerta é disparado quando um feed de compartilhamento de identidade é modificado por um usuário usando [Correspondência de segmento](../../segmentation/ui/segment-match.md). | N/D | N/D |
| Feed compartilhado | Esse alerta é disparado quando um usuário compartilha um novo feed em [Correspondência de segmentos](../../segmentation/ui/segment-match.md). | N/D | N/D |
| Solicitação de link | Esse alerta é disparado quando um usuário solicita a conexão para compartilhamento de parceiros. | N/D | N/D |
| Ação do link | Esse alerta é disparado quando um usuário aceita uma solicitação para se conectar para compartilhamento do parceiro. | N/D | N/D |
| Definição de segmento desativada | Esse alerta é disparado quando uma definição de segmento é desativada. | N/D | N/D |
| Atraso no trabalho do segmento | Esse alerta é disparado quando as tarefas de um segmento levam mais de 150 minutos para serem concluídas. | 30 segundos | 3 horas |
| Falha na Execução do Fluxo de Fontes | Esse alerta dispara quando ocorre um erro ao assimilar dados de uma conexão de origem. | N/D | N/D |
| Êxito na Execução do Fluxo de Fontes | Esse alerta dispara quando os dados são assimilados com êxito de uma conexão de origem. | N/D | N/D |

{style=&quot;table-layout:auto&quot;}