---
title: Grupo de campos de esquema de detalhes da campanha de negócios XDM
description: Saiba mais sobre o grupo de campos de esquema Detalhes da campanha de negócios XDM.
exl-id: 3ef6c0b9-cba1-449e-8868-46446c00465f
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 5%

---

# [!UICONTROL Detalhes da campanha de negócios XDM] grupo de campos de esquema

[!UICONTROL Detalhes da Campanha Comercial XDM] é um grupo de campos de esquema padrão para a [[!UICONTROL Campanha Comercial XDM] classe](../../classes/b2b/business-campaign.md), que captura informações detalhadas sobre uma campanha comercial.

![A estrutura do grupo de campos Detalhes da Campanha Comercial XDM como aparece na interface do usuário](../../images/field-groups/b2b/business-campaign-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `actualCost` | [[!UICONTROL Moeda]](../../data-types/currency.md) | Representa o custo real da campanha comercial. |
| `budgetedCost` | [[!UICONTROL Moeda]](../../data-types/currency.md) | Representa o custo orçado da campanha comercial. |
| `expectedRevenue` | [[!UICONTROL Moeda]](../../data-types/currency.md) | Representa a receita que a campanha comercial deve gerar. |
| `parentCampaignKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | A ID composta para uma campanha principal, se aplicável. |
| `campaignEndDate` | [!UICONTROL DateTime] | Um carimbo de data e hora ISO 8601 que indica quando a campanha terminou ou quando terminará. |
| `campaignProgressionName` | [!UICONTROL String] | O nome da progressão da campanha. |
| `campaignStartDate` | [!UICONTROL DateTime] | Um carimbo de data e hora ISO 8601 de quando a campanha começou ou iniciará. |
| `campaignStatus` | [!UICONTROL String] | O status atual da campanha. |
| `channelName` | [!UICONTROL String] | O nome do canal associado a esta campanha. |
| `expectedResponse` | [!UICONTROL String] | A resposta esperada para a campanha. |
| `integrationPartnerName` | [!UICONTROL String] | O nome do parceiro que se integrou a esta campanha. |
| `isActive` | [!UICONTROL Booleano] | Indica se esta campanha está ativa. |
| `isDeleted` | [!UICONTROL Booleano] | Indica se esta campanha foi excluída no Marketo Engage.<br><br>Ao usar o [conector de origem do Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), todos os registros excluídos no Marketo serão refletidos automaticamente no Perfil do Cliente em Tempo Real. No entanto, os registros relacionados a esses perfis ainda podem persistir no Data Lake. Ao configurar `isDeleted` como `true`, você pode usar o campo para filtrar quais registros foram excluídos de suas fontes ao consultar o Data Lake. |
| `lastActivityDate` | [!UICONTROL DateTime] | Um carimbo de data e hora ISO 8601 da última atividade associada à campanha. |
| `timeZone` | [!UICONTROL String] | O fuso horário em que a campanha opera. |
| `timeZoneDelivery` | [!UICONTROL String] | O fuso horário de delivery no qual a campanha opera. |
| `timeZoneName` | [!UICONTROL String] | O nome do fuso horário em que a campanha opera. |
| `webinarHistorySyncDate` | [!UICONTROL DateTime] | Um carimbo de data e hora ISO 8601 da última sincronização do histórico do webinário para esta campanha. |
| `webinarHistorySyncStatus` | [!UICONTROL String] | O status da sincronização do histórico do webinário para esta campanha. |
| `webinarSessionDescription` | [!UICONTROL String] | Uma descrição da sessão de webinário associada a esta campanha. |
| `webinarSessionName` | [!UICONTROL String] | Um nome da sessão de webinário associada a esta campanha. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign/campaign-details.schema.json).
