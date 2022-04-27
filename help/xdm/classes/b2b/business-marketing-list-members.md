---
title: Classe de Membros da Lista de Marketing Corporativo XDM
description: Este documento fornece uma visão geral da classe de membros da lista de negócios XDM no Experience Data Model (XDM).
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: 50e5fe8573d828f88867ed33fe86e974c85de60a
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 2%

---

# [!UICONTROL Membros da Lista de Marketing Comercial XDM] classe

>[!IMPORTANT]
>
>Esta classe destina-se a ser utilizada por organizações com acesso a [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Você deve ter acesso à CDP B2B Edition em tempo real para que essa classe participe do [Perfil do cliente em tempo real](../../../profile/home.md).

[!UICONTROL Membros da Lista de Marketing Comercial XDM] é uma classe padrão do Experience Data Model (XDM) que descreve membros, pessoas ou contatos associados a uma lista de marketing.

![A estrutura da classe Membros da lista de negócios XDM como ela aparece na interface do usuário](../../images/classes/b2b/business-marketing-list-members.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de Auditoria do Sistema de Origem Externa]](../../data-types/external-source-system-audit-attributes.md) | Se a associação à lista de marketing for proveniente de um sistema de origem externo, esse objeto capturará atributos de auditoria para esse sistema. |
| `marketingListKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto da lista de marketing de que a pessoa é membro. |
| `marketingListMemberKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a entidade de associação da lista de marketing. |
| `personKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a pessoa que é membro da lista de marketing. |
| `_id` | String | Um identificador exclusivo para o registro. Esse é um valor gerado pelo sistema separado da variável `marketingListMemberID`. |
| `isDeleted` | Booleano | Indica se esta entidade de membro da lista de marketing foi excluída no Marketo Engage.<br><br>Ao usar a variável [Conector de origem Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), todos os registros excluídos no Marketo são refletidos automaticamente no Perfil do cliente em tempo real. No entanto, os registros relacionados a esses perfis ainda podem persistir no Data Lake. Ao configurar `isDeleted` para `true`, você pode usar o campo para filtrar quais registros foram excluídos de suas fontes ao consultar o Data Lake. |
| `marketingListID` | String | Uma ID exclusiva para a lista de marketing. |
| `marketingListMemberID` | String | Uma ID exclusiva para a entidade de associação da lista de marketing. |
| `personId` | String | Uma ID exclusiva para a pessoa. |

{style=&quot;table-layout:auto&quot;}

Consulte o guia sobre [relações de esquema na Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) para saber como essa classe se relaciona conceitualmente com as outras classes B2B e como você pode estabelecer esses relacionamentos na interface do usuário do Adobe Experience Platform.
