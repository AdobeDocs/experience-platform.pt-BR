---
title: Classe de Membros da Campanha Comercial XDM
description: Este documento fornece uma visão geral da classe de membros da campanha comercial XDM no Experience Data Model (XDM).
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 2%

---

# [!UICONTROL Classe de ] membros da campanha comercial XDM

>[!NOTE]
>
>Essa classe só está disponível para organizações que têm acesso à Plataforma de dados do cliente em tempo real B2B Edition.

[!UICONTROL A ] associação de campanha comercial XDM é uma classe padrão do Experience Data Model (XDM) que descreve um contato ou um cliente potencial associado a uma campanha comercial.

![](../../images/classes/b2b/business-campaign-members.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a campanha associada. |
| `campaignMemberKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a entidade de associação da campanha. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de Auditoria do Sistema de Origem Externa]](../../data-types/external-source-system-audit-attributes.md) | Se a associação da campanha provém de um sistema de origem externo, esse objeto captura atributos de auditoria para esse sistema. |
| `personKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a pessoa que é membro da campanha associada. |
| `_id` | String | Um identificador exclusivo para o registro. Este é um valor gerado pelo sistema separado do `campaignMemberID`. |
| `campaignID` | String | Uma ID exclusiva para a campanha associada. |
| `campaignMemberID` | String | Uma ID exclusiva para a entidade de associação de campanha. |
| `personId` | String | Uma ID exclusiva para a pessoa que é membro da campanha associada. |

Consulte o guia sobre [relações de esquema na CDP em tempo real B2B Edition](../../tutorials/relationship-b2b.md) para saber como essa classe se relaciona conceitualmente com as outras classes B2B e como você pode estabelecer esses relacionamentos na interface do usuário do Adobe Experience Platform.
