---
title: Classe de Oportunidade de Negócios XDM
description: Este documento fornece uma visão geral da classe de Oportunidade de Negócios XDM no Experience Data Model (XDM).
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 4%

---

# [!UICONTROL Ciclo de ] oportunidades de negócios XDM

>[!NOTE]
>
>Essa classe só está disponível para organizações que têm acesso à Plataforma de dados do cliente em tempo real B2B Edition.

[!UICONTROL A XDM Business ] Oportunity é uma classe padrão do Experience Data Model (XDM) que captura as propriedades mínimas necessárias de uma oportunidade de negócios.

![](../../images/classes/b2b/business-opportunity.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a conta à qual esta oportunidade está associada. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de Auditoria do Sistema de Origem Externa]](../../data-types/external-source-system-audit-attributes.md) | Se a oportunidade vem de um sistema de origem externo, esse objeto captura atributos de auditoria para esse sistema. |
| `opportunityKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a entidade de oportunidade. |
| `_id` | String | Um identificador exclusivo para o registro. Este é um valor gerado pelo sistema separado do `opportunityID`. |
| `accountID` | String | Uma ID exclusiva para a conta à qual esta oportunidade está associada. |
| `opportunityDescription` | String | Uma descrição para a oportunidade. |
| `opportunityID` | String | Uma ID exclusiva para a entidade de oportunidade. |
| `opportunityName` | String | O nome da oportunidade. |
| `opportunityStage` | String | O estágio de vendas da oportunidade. |
| `opportunityType` | String | O tipo de oportunidade. |

Consulte o guia sobre [relações de esquema na CDP em tempo real B2B Edition](../../tutorials/relationship-b2b.md) para saber como essa classe se relaciona conceitualmente com as outras classes B2B e como você pode estabelecer esses relacionamentos na interface do usuário do Adobe Experience Platform.
