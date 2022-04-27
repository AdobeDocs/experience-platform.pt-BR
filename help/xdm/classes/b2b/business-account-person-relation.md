---
title: Classe de Relação de Pessoa da Conta Funcional XDM
description: Este documento fornece uma visão geral da classe de relação de pessoa da conta comercial XDM no Experience Data Model (XDM).
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: 50e5fe8573d828f88867ed33fe86e974c85de60a
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 3%

---

# [!UICONTROL Relação de Pessoa da Conta Comercial XDM] classe

>[!IMPORTANT]
>
>Esta classe destina-se a ser utilizada por organizações com acesso a [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Você deve ter acesso à CDP B2B Edition em tempo real para que essa classe participe do [Perfil do cliente em tempo real](../../../profile/home.md).

[!UICONTROL Relação de Pessoa da Conta Comercial XDM] é uma classe padrão do Experience Data Model (XDM) que captura as propriedades mínimas necessárias de uma pessoa associada a uma conta comercial.

![A estrutura da classe de Relação de Pessoa da Conta Comercial XDM como ela aparece na interface do usuário](../../images/classes/b2b/business-account-person-relation.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a conta no relacionamento conta-pessoa. |
| `accountPersonKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a entidade de relação conta-pessoa. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de Auditoria do Sistema de Origem Externa]](../../data-types/external-source-system-audit-attributes.md) | Se o relacionamento conta-pessoa for proveniente de um sistema de origem externo, esse objeto capturará atributos de auditoria para esse sistema. |
| `personKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto da pessoa no relacionamento conta-pessoa. |
| `_id` | String | Um identificador exclusivo para o registro. Esse é um valor gerado pelo sistema separado dos outros campos de ID capturados pela classe. |
| `accountID` | String | Um identificador exclusivo da conta no relacionamento conta-pessoa. |
| `accountPersonID` | String | Um identificador exclusivo para a entidade de relação conta-pessoa. |
| `currencyCode` | String | Código monetário ISO 4217 utilizado para a relação entre a conta e a pessoa. |
| `isActive` | Booleano | Indica se a relação entre a conta e a pessoa está ativa. |
| `isDeleted` | Booleano | Indica se esta relação conta-pessoa foi excluída no Marketo Engage.<br><br>Ao usar a variável [Conector de origem Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), todos os registros excluídos no Marketo são refletidos automaticamente no Perfil do cliente em tempo real. No entanto, os registros relacionados a esses perfis ainda podem persistir no Data Lake. Ao configurar `isDeleted` para `true`, você pode usar o campo para filtrar quais registros foram excluídos de suas fontes ao consultar o Data Lake. |
| `isDirect` | Booleano | Indica se esta é uma relação direta entre a conta e a pessoa. |
| `isPrimary` | Booleano | Indica se a pessoa é o contato principal nesta conta. |
| `personID` | String | Um identificador exclusivo da pessoa no relacionamento conta-pessoa. |
| `personRoles` | Matriz de cadeias de caracteres | Lista as funções da pessoa na relação conta-pessoa. |
| `relationEndDate` | DateTime | A data em que o relacionamento entre a conta e a pessoa terminou. |
| `relationStartDate` | DateTime | A data em que a relação entre a conta e a pessoa começou. |
| `relationshipSource` | String | A origem da relação conta-pessoa. |

{style=&quot;table-layout:auto&quot;}

Consulte o guia sobre [relações de esquema na Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) para saber como essa classe se relaciona conceitualmente com as outras classes B2B e como você pode estabelecer esses relacionamentos na interface do usuário do Adobe Experience Platform.
