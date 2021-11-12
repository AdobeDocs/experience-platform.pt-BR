---
title: Classe de Membros da Campanha Comercial XDM
description: Este documento fornece uma visão geral da classe de membros da campanha comercial XDM no Experience Data Model (XDM).
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 4%

---

# [!UICONTROL Membros da Campanha Comercial XDM] classe

[!UICONTROL Membros da Campanha Comercial XDM] é uma classe padrão do Experience Data Model (XDM) que descreve um contato ou um cliente potencial associado a uma campanha comercial.

![](../../images/classes/b2b/business-campaign-members.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a campanha associada. |
| `campaignMemberKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a entidade de associação da campanha. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de Auditoria do Sistema de Origem Externa]](../../data-types/external-source-system-audit-attributes.md) | Se a associação da campanha provém de um sistema de origem externo, esse objeto captura atributos de auditoria para esse sistema. |
| `personKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a pessoa que é membro da campanha associada. |
| `_id` | String | Um identificador exclusivo para o registro. Esse é um valor gerado pelo sistema separado da variável `campaignMemberID`. |
| `campaignID` | String | Uma ID exclusiva para a campanha associada. |
| `campaignMemberID` | String | Uma ID exclusiva para a entidade de associação de campanha. |
| `personId` | String | Uma ID exclusiva para a pessoa que é membro da campanha associada. |

{style=&quot;table-layout:auto&quot;}

Consulte o guia sobre [relações de esquema na Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) para saber como essa classe se relaciona conceitualmente com as outras classes B2B e como você pode estabelecer esses relacionamentos na interface do usuário do Adobe Experience Platform.
