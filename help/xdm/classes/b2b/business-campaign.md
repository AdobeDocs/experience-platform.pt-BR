---
title: Classe de Campanha Comercial XDM
description: Este documento fornece uma visão geral da classe de Campanha comercial XDM no Experience Data Model (XDM).
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: 0084492ed467c5996a94c5c55a79c9faf8f5046e
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 4%

---

# [!UICONTROL Campanha comercial XDM] classe

>[!IMPORTANT]
>
>Esta classe destina-se a ser utilizada por organizações com acesso a [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Você deve ter acesso à CDP B2B Edition em tempo real para que essa classe participe do [Perfil do cliente em tempo real](../../../profile/home.md).

[!UICONTROL Campanha comercial XDM] é uma classe padrão do Experience Data Model (XDM) que captura as propriedades mínimas necessárias de uma campanha comercial.

![A estrutura da classe de Campanha comercial XDM como ela aparece na interface do usuário](../../images/classes/b2b/business-campaign.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a entidade de campanha. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de Auditoria do Sistema de Origem Externa]](../../data-types/external-source-system-audit-attributes.md) | Se a campanha provém de um sistema de origem externo, esse objeto captura atributos de auditoria para esse sistema. |
| `_id` | String | Um identificador exclusivo para o registro. Esse é um valor gerado pelo sistema separado da variável `campaignID`. |
| `campaignDescription` | String | Uma descrição para a campanha. |
| `campaignID` | String | Um identificador exclusivo para a entidade de campanha. |
| `campaignName` | String | O nome da campanha. |
| `campaignType` | String | O tipo de campanha ou público-alvo. |

{style=&quot;table-layout:auto&quot;}

Para saber como essa classe se relaciona conceitualmente com outras classes B2B e como você pode estabelecer esses relacionamentos na interface do usuário do Adobe Experience Platform, consulte o guia em [relações de esquema na Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md)

Para campos adicionais compatíveis com essa classe, consulte a referência de grupo de campos para [[!UICONTROL Detalhes da campanha comercial XDM]](../../field-groups/b2b-campaign/details.md).
