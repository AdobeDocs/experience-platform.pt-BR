---
title: Classe de membros da campanha de negócios XDM
description: Saiba mais sobre a classe de membros da campanha de negócios XDM no Experience Data Model (XDM).
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 2%

---

# Classe [!UICONTROL Membros da Campanha Comercial XDM]

>[!IMPORTANT]
>
>Esta classe deve ser usada por organizações com acesso ao [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Você deve ter acesso ao Real-Time CDP B2B Edition para que esta classe participe do [Perfil de Cliente em Tempo Real](../../../profile/home.md).

[!UICONTROL Membros da Campanha Comercial XDM] é uma classe padrão do Experience Data Model (XDM) que descreve um contato ou cliente potencial associado a uma campanha comercial.

![A estrutura da classe de Membros da Campanha Comercial XDM como aparece na interface](../../images/classes/b2b/business-campaign-members.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Um identificador composto para a campanha associada. |
| `campaignMemberKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Um identificador composto para a entidade de associação da campanha. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de Auditoria de Sistema Source Externos]](../../data-types/external-source-system-audit-attributes.md) | Se a associação à campanha vier de um sistema de origem externa, esse objeto capturará atributos de auditoria para esse sistema. |
| `personKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Um identificador composto para a pessoa que é membro da campanha associada. |
| `_id` | String | Um identificador exclusivo do registro. Este é um valor gerado pelo sistema separado de `campaignMemberID`. |

{style="table-layout:auto"}

Para saber como essa classe se relaciona conceitualmente com as outras classes B2B e como você pode estabelecer essas relações na interface do usuário do Adobe Experience Platform, consulte o manual sobre [relações de esquema no Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md)

Para obter campos adicionais compatíveis com essa classe, consulte a referência do grupo de campos para [[!UICONTROL Detalhes do membro da campanha de negócios XDM]](../../field-groups/b2b-campaign-members/details.md).
