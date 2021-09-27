---
title: Classe de Membros da Lista de Marketing Corporativo XDM
description: Este documento fornece uma visão geral da classe de membros da lista de negócios XDM no Experience Data Model (XDM).
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 2%

---

# [!UICONTROL Classe de ] Membros da Lista de Marketing Corporativa XDM

>[!NOTE]
>
>Essa classe só está disponível para organizações que têm acesso à Plataforma de dados do cliente em tempo real B2B Edition.

[!UICONTROL A ] associação da lista de marketing comercial XDM é uma classe padrão do Experience Data Model (XDM) que descreve membros, pessoas ou contatos associados a uma lista de marketing.

![](../../images/classes/b2b/business-marketing-list-members.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de Auditoria do Sistema de Origem Externa]](../../data-types/external-source-system-audit-attributes.md) | Se a associação à lista de marketing for proveniente de um sistema de origem externo, esse objeto capturará atributos de auditoria para esse sistema. |
| `marketingListKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto da lista de marketing de que a pessoa é membro. |
| `marketingListMemberKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a entidade de associação da lista de marketing. |
| `personKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a pessoa que é membro da lista de marketing. |
| `_id` | String | Um identificador exclusivo para o registro. Este é um valor gerado pelo sistema separado do `marketingListMemberID`. |
| `marketingListID` | String | Uma ID exclusiva para a lista de marketing. |
| `marketingListMemberID` | String | Uma ID exclusiva para a entidade de associação da lista de marketing. |
| `personId` | String | Uma ID exclusiva para a pessoa. |

Consulte o guia sobre [relações de esquema na CDP em tempo real B2B Edition](../../tutorials/relationship-b2b.md) para saber como essa classe se relaciona conceitualmente com as outras classes B2B e como você pode estabelecer esses relacionamentos na interface do usuário do Adobe Experience Platform.
