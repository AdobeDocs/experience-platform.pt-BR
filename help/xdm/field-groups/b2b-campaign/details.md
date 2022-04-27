---
title: Grupo de Campos Detalhes da Campanha Comercial XDM
description: Este documento fornece uma visão geral do grupo de campos Detalhes da campanha comercial do XDM.
source-git-commit: 0084492ed467c5996a94c5c55a79c9faf8f5046e
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 5%

---

# [!UICONTROL Detalhes da campanha comercial XDM] grupo de campos de esquema

[!UICONTROL Detalhes da campanha comercial XDM] é um grupo de campos de esquema padrão para a variável [[!UICONTROL Campanha comercial XDM] classe](../../classes/b2b/business-campaign.md), que captura informações detalhadas sobre uma campanha comercial.

![A estrutura do grupo de campos Detalhes da campanha comercial do XDM, como aparece na interface do usuário](../../images/field-groups/b2b/business-campaign-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `actualCost` | [[!UICONTROL Moeda]](../../data-types/currency.md) | Representa o custo real da campanha comercial. |
| `budgetedCost` | [[!UICONTROL Moeda]](../../data-types/currency.md) | Representa o custo orçado da campanha comercial. |
| `expectedRevenue` | [[!UICONTROL Moeda]](../../data-types/currency.md) | Representa a receita que a campanha comercial deve gerar. |
| `parentCampaignKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | A ID composta de uma campanha pai, se aplicável. |
| `campaignEndDate` | [!UICONTROL DateTime] | Um carimbo de data e hora ISO 8601 de quando a campanha terminou ou terminará. |
| `campaignProgressionName` | [!UICONTROL String] | O nome da progressão da campanha. |
| `campaignStartDate` | [!UICONTROL DateTime] | Um carimbo de data e hora ISO 8601 de quando a campanha começou ou será iniciada. |
| `campaignStatus` | [!UICONTROL String] | O status atual da campanha. |
| `channelName` | [!UICONTROL String] | O nome do canal associado a esta campanha. |
| `expectedResponse` | [!UICONTROL String] | A resposta esperada para a campanha. |
| `integrationPartnerName` | [!UICONTROL String] | O nome do parceiro que se integrou a esta campanha. |
| `isActive` | [!UICONTROL Booleano] | Indica se a campanha está ativa. |
| `isDeleted` | [!UICONTROL Booleano] | Indica se esta campanha foi excluída no Marketo Engage.<br><br>Ao usar a variável [Conector de origem Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), todos os registros excluídos no Marketo são refletidos automaticamente no Perfil do cliente em tempo real. No entanto, os registros relacionados a esses perfis ainda podem persistir no Data Lake. Ao configurar `isDeleted` para `true`, você pode usar o campo para filtrar quais registros foram excluídos de suas fontes ao consultar o Data Lake. |
| `lastActivityDate` | [!UICONTROL DateTime] | Um carimbo de data e hora ISO 8601 da última atividade associada à campanha. |
| `timeZone` | [!UICONTROL String] | O fuso horário em que a campanha opera. |
| `timeZoneDelivery` | [!UICONTROL String] | O fuso horário do delivery no qual a campanha opera. |
| `timeZoneName` | [!UICONTROL String] | O nome do fuso horário em que a campanha opera. |
| `webinarHistorySyncDate` | [!UICONTROL DateTime] | Um carimbo de data e hora ISO 8601 da última sincronização do histórico de webinários para esta campanha. |
| `webinarHistorySyncStatus` | [!UICONTROL String] | O status da sincronização do histórico do webinário para essa campanha. |
| `webinarSessionDescription` | [!UICONTROL String] | Uma descrição da sessão do webinário associada a esta campanha. |
| `webinarSessionName` | [!UICONTROL String] | Um nome da sessão do webinário associada a esta campanha. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte [repositório XDM público](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign/campaign-details.schema.json).
