---
title: Classe de Membros da Lista de Marketing Corporativo XDM
description: Este documento fornece uma visão geral da classe de membros da lista de negócios XDM no Experience Data Model (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 3%

---

# [!UICONTROL Classe de ] Membros da Lista de Marketing Corporativa XDM

>[!NOTE]
>
>Essa classe só está disponível para organizações que têm acesso à edição B2B da Plataforma de dados do cliente em tempo real.

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
