---
title: Classe de Oportunidade de Negócios XDM
description: Este documento fornece uma visão geral da classe de Oportunidade de Negócios XDM no Experience Data Model (XDM).
exl-id: d816b0f9-fd37-45da-aa55-247f7f662da0
source-git-commit: 50e5fe8573d828f88867ed33fe86e974c85de60a
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 4%

---

# [!UICONTROL Oportunidade de negócios XDM] classe

>[!IMPORTANT]
>
>Esta classe destina-se a ser utilizada por organizações com acesso a [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Você deve ter acesso à CDP B2B Edition em tempo real para que essa classe participe do [Perfil do cliente em tempo real](../../../profile/home.md).

[!UICONTROL Oportunidade de negócios XDM] é uma classe padrão do Experience Data Model (XDM) que captura as propriedades mínimas necessárias de uma oportunidade de negócios.

![A estrutura da classe de Oportunidade de Negócios XDM como ela aparece na interface do usuário](../../images/classes/b2b/business-opportunity.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a conta à qual esta oportunidade está associada. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de Auditoria do Sistema de Origem Externa]](../../data-types/external-source-system-audit-attributes.md) | Se a oportunidade vem de um sistema de origem externo, esse objeto captura atributos de auditoria para esse sistema. |
| `opportunityKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a entidade de oportunidade. |
| `_id` | String | Um identificador exclusivo para o registro. Esse é um valor gerado pelo sistema separado da variável `opportunityID`. |
| `accountID` | String | Uma ID exclusiva para a conta à qual esta oportunidade está associada. |
| `isDeleted` | Booleano | Indica se esta entidade da lista de marketing foi excluída no Marketo Engage.<br><br>Ao usar a variável [Conector de origem Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), todos os registros excluídos no Marketo são refletidos automaticamente no Perfil do cliente em tempo real. No entanto, os registros relacionados a esses perfis ainda podem persistir no Data Lake. Ao configurar `isDeleted` para `true`, você pode usar o campo para filtrar quais registros foram excluídos de suas fontes ao consultar o Data Lake. |
| `opportunityDescription` | String | Uma descrição para a oportunidade. |
| `opportunityID` | String | Uma ID exclusiva para a entidade de oportunidade. |
| `opportunityName` | String | O nome da oportunidade. |
| `opportunityStage` | String | O estágio de vendas da oportunidade. |
| `opportunityType` | String | O tipo de oportunidade. |

{style=&quot;table-layout:auto&quot;}

Consulte o guia sobre [relações de esquema na Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) para saber como essa classe se relaciona conceitualmente com as outras classes B2B e como você pode estabelecer esses relacionamentos na interface do usuário do Adobe Experience Platform.
