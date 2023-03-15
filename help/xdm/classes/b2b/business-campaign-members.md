---
title: Classe de membros da campanha de negócios XDM
description: Este documento fornece uma visão geral da classe de membros da campanha de negócios XDM no Experience Data Model (XDM).
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 1%

---

# [!UICONTROL Membros da campanha de negócios XDM] classe

>[!IMPORTANT]
>
>Esta classe deve ser usada por organizações com acesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Você deve ter acesso ao Real-Time CDP B2B Edition para que esta classe participe [Perfil do cliente em tempo real](../../../profile/home.md).

[!UICONTROL Membros da campanha de negócios XDM] é uma classe padrão do Experience Data Model (XDM) que descreve um contato ou um cliente potencial associado a uma campanha de negócios.

![A estrutura da classe de Membros da campanha de negócios XDM como aparece na interface do](../../images/classes/b2b/business-campaign-members.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a campanha associada. |
| `campaignMemberKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a entidade de associação da campanha. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoria do sistema de origem externa]](../../data-types/external-source-system-audit-attributes.md) | Se a associação à campanha vier de um sistema de origem externa, esse objeto capturará atributos de auditoria para esse sistema. |
| `personKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a pessoa que é membro da campanha associada. |
| `_id` | String | Um identificador exclusivo do registro. É um valor gerado pelo sistema separado da variável `campaignMemberID`. |

{style="table-layout:auto"}

Para saber como essa classe se relaciona conceitualmente com as outras classes B2B e como você pode estabelecer esses relacionamentos na interface do usuário do Adobe Experience Platform, consulte o manual sobre [relacionamentos de esquema no Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md)

Para obter campos adicionais compatíveis com essa classe, consulte a referência do grupo de campos para [[!UICONTROL Detalhes do membro da campanha de negócios XDM]](../../field-groups/b2b-campaign-members/details.md).
