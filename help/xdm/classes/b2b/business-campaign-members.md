---
title: Classe de Membros da Campanha Comercial XDM
description: Este documento fornece uma visão geral da classe de membros da campanha comercial XDM no Experience Data Model (XDM).
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 2%

---

# [!UICONTROL Membros da Campanha Comercial XDM] classe

>[!IMPORTANT]
>
>Esta classe destina-se a ser utilizada por organizações com acesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Você deve ter acesso ao Real-Time CDP B2B Edition para que essa classe participe do [Perfil do cliente em tempo real](../../../profile/home.md).

[!UICONTROL Membros da Campanha Comercial XDM] é uma classe padrão do Experience Data Model (XDM) que descreve um contato ou um cliente potencial associado a uma campanha comercial.

![A estrutura da classe membros da campanha comercial XDM como ela aparece na interface do usuário](../../images/classes/b2b/business-campaign-members.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a campanha associada. |
| `campaignMemberKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a entidade de associação da campanha. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de Auditoria do Sistema de Origem Externa]](../../data-types/external-source-system-audit-attributes.md) | Se a associação da campanha provém de um sistema de origem externo, esse objeto captura atributos de auditoria para esse sistema. |
| `personKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a pessoa que é membro da campanha associada. |
| `_id` | String | Um identificador exclusivo para o registro. Esse é um valor gerado pelo sistema separado da variável `campaignMemberID`. |

{style=&quot;table-layout:auto&quot;}

Para saber como essa classe se relaciona conceitualmente com outras classes B2B e como você pode estabelecer esses relacionamentos na interface do usuário do Adobe Experience Platform, consulte o guia em [relações de esquema no Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md)

Para campos adicionais compatíveis com essa classe, consulte a referência de grupo de campos para [[!UICONTROL Detalhes do Membro da Campanha Empresarial XDM]](../../field-groups/b2b-campaign-members/details.md).
