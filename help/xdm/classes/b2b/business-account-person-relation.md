---
title: Classe de relação pessoal da conta comercial XDM
description: Este documento fornece uma visão geral da classe de relação pessoal da conta comercial XDM no Experience Data Model (XDM).
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 2%

---

# [!UICONTROL Relação pessoal da conta de negócios XDM] classe

>[!IMPORTANT]
>
>Esta classe deve ser usada por organizações com acesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Você deve ter acesso ao Real-Time CDP B2B Edition para que esta classe participe [Perfil do cliente em tempo real](../../../profile/home.md).

[!UICONTROL Relação pessoal da conta de negócios XDM] é uma classe padrão do Experience Data Model (XDM) que captura as propriedades mínimas necessárias de uma pessoa associada a uma conta comercial.

![A estrutura da classe de relação pessoal da conta comercial XDM como aparece na interface do usuário](../../images/classes/b2b/business-account-person-relation.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a conta na relação conta-pessoa. |
| `accountPersonKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a entidade de relação conta-pessoa. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoria do sistema de origem externa]](../../data-types/external-source-system-audit-attributes.md) | Se o relacionamento conta-pessoa vem de um sistema de origem externo, esse objeto captura atributos de auditoria para esse sistema. |
| `personKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a pessoa na relação conta-pessoa. |
| `_id` | String | Um identificador exclusivo do registro. Este é um valor gerado pelo sistema separado dos outros campos de ID capturados pela classe. |
| `accountID` | String | Um identificador exclusivo da conta na relação conta-pessoa. |
| `accountPersonID` | String | Um identificador exclusivo da entidade de relação conta-pessoa. |
| `currencyCode` | String | O código de moeda ISO 4217 usado para o relacionamento entre a conta e a pessoa. |
| `isActive` | Booleano | Indica se o relacionamento entre a conta e a pessoa está ativo. |
| `isDeleted` | Booleano | Indica se esta relação conta-pessoa foi excluída no Marketo Engage.<br><br>Ao usar o [Conector de origem do Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), todos os registros excluídos no Marketo são refletidos automaticamente no Perfil do cliente em tempo real. No entanto, os registros relacionados a esses perfis ainda podem persistir no Data Lake. Ao configurar `isDeleted` para `true`, você pode usar o campo para filtrar quais registros foram excluídos de suas fontes ao consultar o Data Lake. |
| `isDirect` | Booleano | Indica se é uma relação direta entre a conta e a pessoa. |
| `isPrimary` | Booleano | Indica se a pessoa é o contato principal nesta conta. |
| `personID` | String | Um identificador exclusivo da pessoa na relação conta-pessoa. |
| `personRoles` | Matriz de cadeias de caracteres | Lista as funções da pessoa no relacionamento conta-pessoa. |
| `relationEndDate` | DateTime | A data em que o relacionamento entre a conta e a pessoa terminou. |
| `relationStartDate` | DateTime | A data em que o relacionamento entre a conta e a pessoa começou. |
| `relationshipSource` | String | A origem da relação conta-pessoa. |

{style="table-layout:auto"}

Consulte o guia sobre [relacionamentos de esquema no Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) para saber como essa classe se relaciona conceitualmente com as outras classes B2B e como você pode estabelecer esses relacionamentos na interface do usuário do Adobe Experience Platform.
