---
title: Classe de conta de negócios XDM
description: Este documento fornece uma visão geral da classe Conta comercial XDM no Experience Data Model (XDM).
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 1%

---

# [!UICONTROL Conta de negócios XDM] classe

>[!IMPORTANT]
>
>Esta classe deve ser usada por organizações com acesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Você deve ter acesso ao Real-Time CDP B2B Edition para que esta classe participe [Perfil do cliente em tempo real](../../../profile/home.md).

[!UICONTROL Conta de negócios XDM] é uma classe padrão do Experience Data Model (XDM) que captura as propriedades mínimas necessárias de uma conta comercial.

![A estrutura da classe da Conta Comercial XDM como aparece na interface do usuário](../../images/classes/b2b/business-account.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto da entidade da conta. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoria do sistema de origem externa]](../../data-types/external-source-system-audit-attributes.md) | Se a conta vem de um sistema de origem externa, esse objeto captura atributos de auditoria para esse sistema. |
| `_id` | String | Um identificador exclusivo do registro. É um valor gerado pelo sistema separado da variável `accountKey` identificador. |
| `isDeleted` | Booleano | Indica se esta entidade de conta foi excluída no Marketo Engage.<br><br>Ao usar o [Conector de origem do Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), todos os registros excluídos no Marketo são refletidos automaticamente no Perfil do cliente em tempo real. No entanto, os registros relacionados a esses perfis ainda podem persistir no Data Lake. Ao configurar `isDeleted` para `true`, você pode usar o campo para filtrar quais registros foram excluídos de suas fontes ao consultar o Data Lake. |

{style="table-layout:auto"}

Consulte o guia sobre [relacionamentos de esquema no Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) para saber como essa classe se relaciona conceitualmente com as outras classes B2B e como você pode estabelecer esses relacionamentos na interface do usuário do Adobe Experience Platform.
