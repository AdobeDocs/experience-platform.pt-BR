---
title: Classe de membros da lista de marketing de negócios XDM
description: Este documento fornece uma visão geral da classe de membros da lista de marketing empresarial XDM no Experience Data Model (XDM).
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 2%

---

# [!UICONTROL Membros da lista de marketing de negócios XDM] classe

>[!IMPORTANT]
>
>Esta classe deve ser usada por organizações com acesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Você deve ter acesso ao Real-Time CDP B2B Edition para que esta classe participe [Perfil do cliente em tempo real](../../../profile/home.md).

[!UICONTROL Membros da lista de marketing de negócios XDM] é uma classe padrão do Experience Data Model (XDM) que descreve membros, pessoas ou contatos associados a uma lista de marketing.

![A estrutura da classe de Membros da Lista de marketing empresarial XDM como aparece na interface](../../images/classes/b2b/business-marketing-list-members.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoria do sistema de origem externa]](../../data-types/external-source-system-audit-attributes.md) | Se a associação à lista de marketing for proveniente de um sistema de origem externa, esse objeto capturará os atributos de auditoria desse sistema. |
| `marketingListKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto da lista de marketing da qual a pessoa é membro. |
| `marketingListMemberKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a entidade de associação da lista de marketing. |
| `personKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto da pessoa que é membro da lista de marketing. |
| `_id` | String | Um identificador exclusivo do registro. É um valor gerado pelo sistema separado da variável `marketingListMemberID`. |
| `isDeleted` | Booleano | Indica se esta entidade de membro da lista de marketing foi excluída no Marketo Engage.<br><br>Ao usar o [Conector de origem do Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), todos os registros excluídos no Marketo são refletidos automaticamente no Perfil do cliente em tempo real. No entanto, os registros relacionados a esses perfis ainda podem persistir no Data Lake. Ao configurar `isDeleted` para `true`, você pode usar o campo para filtrar quais registros foram excluídos de suas fontes ao consultar o Data Lake. |
| `marketingListID` | String | Uma ID exclusiva para a lista de marketing. |
| `marketingListMemberID` | String | Uma ID exclusiva para a entidade de associação da lista de marketing. |
| `personId` | String | Um identificador exclusivo para a pessoa. |

{style="table-layout:auto"}

Consulte o guia sobre [relacionamentos de esquema no Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) para saber como essa classe se relaciona conceitualmente com as outras classes B2B e como você pode estabelecer esses relacionamentos na interface do usuário do Adobe Experience Platform.
