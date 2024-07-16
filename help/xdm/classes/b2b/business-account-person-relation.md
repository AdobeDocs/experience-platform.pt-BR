---
title: Classe de relação pessoal da conta comercial XDM
description: Saiba mais sobre a classe de relação pessoal da conta comercial XDM no Experience Data Model (XDM).
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 12%

---

# Classe [!UICONTROL Relação pessoal da conta comercial XDM]

>[!IMPORTANT]
>
>Esta classe deve ser usada por organizações com acesso ao [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Você deve ter acesso ao Real-Time CDP B2B Edition para que esta classe participe do [Perfil de Cliente em Tempo Real](../../../profile/home.md).

A [!UICONTROL Relação de pessoa com a conta comercial XDM] é uma classe padrão do Experience Data Model (XDM) que captura as propriedades mínimas necessárias de uma pessoa associada a uma conta comercial.

![A estrutura da classe de Relação de Pessoa da Conta Comercial XDM como aparece na interface do usuário](../../images/classes/b2b/business-account-person-relation.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Um identificador composto para a conta na relação conta-pessoa. |
| `accountPersonKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Um identificador composto para a entidade de relação conta-pessoa. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de Auditoria de Sistema Source Externos]](../../data-types/external-source-system-audit-attributes.md) | Se o relacionamento conta-pessoa vem de um sistema de origem externo, esse objeto captura atributos de auditoria para esse sistema. |
| `personKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Um identificador composto para a pessoa na relação conta-pessoa. |
| `_id` | String | Um identificador exclusivo do registro. Este é um valor gerado pelo sistema separado dos outros campos de ID capturados pela classe. |
| `accountID` | String | Um identificador exclusivo da conta na relação conta-pessoa. |
| `accountPersonID` | String | Um identificador exclusivo da entidade de relação conta-pessoa. |
| `currencyCode` | String | O código de moeda ISO 4217 usado para o relacionamento entre a conta e a pessoa. |
| `isActive` | Booleano | Indica se o relacionamento entre a conta e a pessoa está ativo. |
| `isDeleted` | Booleano | Indica se esta relação conta-pessoa foi excluída no Marketo Engage.<br><br>Ao usar o [conector de origem do Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), todos os registros excluídos no Marketo serão refletidos automaticamente no Perfil do Cliente em Tempo Real. No entanto, os registros relacionados a esses perfis ainda podem persistir no Data Lake. Ao configurar `isDeleted` como `true`, você pode usar o campo para filtrar quais registros foram excluídos de suas fontes ao consultar o Data Lake. |
| `isDirect` | Booleano | Indica se é uma relação direta entre a conta e a pessoa. |
| `isPrimary` | Booleano | Indica se a pessoa é o contato principal nesta conta. |
| `personID` | String | Um identificador exclusivo da pessoa na relação conta-pessoa. |
| `personRoles` | Matriz de cadeias de caracteres | Lista as funções da pessoa no relacionamento conta-pessoa. |
| `relationEndDate` | DateTime | A data em que o relacionamento entre a conta e a pessoa terminou. |
| `relationStartDate` | DateTime | A data em que o relacionamento entre a conta e a pessoa iniciou. |
| `relationshipSource` | String | A origem da relação conta-pessoa. |

{style="table-layout:auto"}

Consulte o manual sobre [relações de esquema no Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) para saber como essa classe se relaciona conceitualmente com as outras classes B2B e como você pode estabelecer essas relações na interface do usuário do Adobe Experience Platform.
