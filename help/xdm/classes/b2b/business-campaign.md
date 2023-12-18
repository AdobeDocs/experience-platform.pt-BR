---
title: Classe de campanha de negócios XDM
description: Saiba mais sobre a classe Campanha comercial XDM no Experience Data Model (XDM).
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---

# [!UICONTROL Campanha de negócios XDM] classe

>[!IMPORTANT]
>
>Esta classe deve ser usada por organizações com acesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Você deve ter acesso ao Real-Time CDP B2B Edition para que esta classe participe [Perfil do cliente em tempo real](../../../profile/home.md).

[!UICONTROL Campanha de negócios XDM] é uma classe padrão do Experience Data Model (XDM) que captura as propriedades mínimas necessárias de uma campanha de negócios.

![A estrutura da classe Campanha de negócios XDM como aparece na interface do usuário](../../images/classes/b2b/business-campaign.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto da entidade da campanha. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoria do sistema de origem externa]](../../data-types/external-source-system-audit-attributes.md) | Se a campanha vier de um sistema de origem externo, esse objeto capturará atributos de auditoria para esse sistema. |
| `_id` | String | Um identificador exclusivo do registro. É um valor gerado pelo sistema separado da variável `campaignID`. |
| `campaignDescription` | String | Uma descrição para a campanha. |
| `campaignID` | String | Um identificador exclusivo da entidade da campanha. |
| `campaignName` | String | O nome da campanha. |
| `campaignType` | String | O tipo de campanha ou público-alvo. |

{style="table-layout:auto"}

Para saber como essa classe se relaciona conceitualmente com as outras classes B2B e como você pode estabelecer esses relacionamentos na interface do usuário do Adobe Experience Platform, consulte o manual sobre [relacionamentos de esquema no Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md)

Para obter campos adicionais compatíveis com essa classe, consulte a referência do grupo de campos para [[!UICONTROL Detalhes da campanha de negócios XDM]](../../field-groups/b2b-campaign/details.md).
