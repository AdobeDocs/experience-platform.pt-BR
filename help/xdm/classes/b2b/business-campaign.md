---
title: Classe de Campanha Comercial XDM
description: Este documento fornece uma visão geral da classe de Campanha comercial XDM no Experience Data Model (XDM).
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 5%

---

# [!UICONTROL Classe de ] campanha comercial XDM (Beta)

>[!IMPORTANT]
>
>Essa classe está disponível como parte da Real-time Customer Data Platform B2B Edition, que está atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

[!UICONTROL O XDM Business ] Campaign é uma classe padrão do Experience Data Model (XDM) que captura as propriedades mínimas necessárias de uma campanha comercial.

![](../../images/classes/b2b/business-campaign.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a entidade de campanha. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de Auditoria do Sistema de Origem Externa]](../../data-types/external-source-system-audit-attributes.md) | Se a campanha provém de um sistema de origem externo, esse objeto captura atributos de auditoria para esse sistema. |
| `_id` | String | Um identificador exclusivo para o registro. Este é um valor gerado pelo sistema separado do `campaignID`. |
| `campaignDescription` | String | Uma descrição para a campanha. |
| `campaignID` | String | Um identificador exclusivo para a entidade de campanha. |
| `campaignName` | String | O nome da campanha. |
| `campaignType` | String | O tipo de campanha ou público-alvo. |

{style=&quot;table-layout:auto&quot;}

Consulte o guia sobre [relações de esquema na CDP em tempo real B2B Edition](../../tutorials/relationship-b2b.md) para saber como essa classe se relaciona conceitualmente com as outras classes B2B e como você pode estabelecer esses relacionamentos na interface do usuário do Adobe Experience Platform.
