---
title: Grupo de Campos de Esquema Detalhes do Membro da Campanha Empresarial XDM
description: Este documento fornece uma visão geral do grupo de campos Detalhes do membro da campanha comercial XDM.
source-git-commit: 0084492ed467c5996a94c5c55a79c9faf8f5046e
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 4%

---

# [!UICONTROL Detalhes do Membro da Campanha Empresarial XDM] grupo de campos de esquema

[!UICONTROL Detalhes do Membro da Campanha Empresarial XDM] é um grupo de campos de esquema padrão para a variável [[!UICONTROL Membros da Campanha Comercial XDM] classe](../../classes/b2b/business-campaign-members.md), que captura informações detalhadas sobre uma campanha comercial.

![A estrutura do grupo de campos Detalhes do Membro da Campanha Empresarial XDM, como aparece na interface do usuário](../../images/field-groups/b2b/business-campaign-member-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `acquiredByCampaignKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | A ID composta da campanha que adquiriu esse membro da campanha. |
| `acquiredByCampaignID` | [!UICONTROL String] | Um identificador de string da campanha que adquiriu esse membro de campanha. |
| `firstRespondedDate` | [!UICONTROL DateTime] | Um carimbo de data e hora ISO 8601 de quando a pessoa respondeu pela primeira vez à campanha. |
| `hasReachedSuccess` | [!UICONTROL Booleano] | Indica se esse membro da campanha resultou em uma conversão bem-sucedida. |
| `hasResponded` | [!UICONTROL Booleano] | Indica se esse membro da campanha respondeu à campanha. |
| `isDeleted` | [!UICONTROL Booleano] | Indica se este membro da campanha foi excluído no Marketo Engage.<br><br>Ao usar a variável [Conector de origem Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), todos os registros excluídos no Marketo são refletidos automaticamente no Perfil do cliente em tempo real. No entanto, os registros relacionados a esses perfis ainda podem persistir no Data Lake. Ao configurar `isDeleted` para `true`, você pode usar o campo para filtrar quais registros foram excluídos de suas fontes ao consultar o Data Lake. |
| `isExhausted` | [!UICONTROL Booleano] | Indica se esse membro da campanha esgotou todas as interações da campanha. |
| `lastStatus` | [!UICONTROL String] | O último status do membro da campanha. |
| `memberStatus` | [!UICONTROL String] | O status atual do membro da campanha. |
| `memberStatusReason` | [!UICONTROL String] | O motivo por trás do status atual do membro da campanha. |
| `membershipDate` | [!UICONTROL DateTime] | O motivo por trás do status atual do membro da campanha. |
| `nurtureCadence` | [!UICONTROL String] | O intervalo de tempo para que informações relacionadas à campanha sejam apresentadas ao membro da campanha. |
| `nurtureTrackName` | [!UICONTROL String] | O nome do programa de criação ao qual este membro da campanha está sujeito. |
| `reachedSuccessDate` | [!UICONTROL DateTime] | Um carimbo de data e hora ISO 8601 para quando uma conversão bem-sucedida foi feita para o membro da campanha. |
| `webinarConfirmationUrl` | [!UICONTROL String] | O URL de confirmação do webinar para o membro da campanha. |
| `webinarRegistrationID` | [!UICONTROL String] | A ID de registro do webinar do membro da campanha. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.schema.json)
