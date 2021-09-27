---
title: Classe de Oportunidade de Negócios XDM
description: Este documento fornece uma visão geral da classe de Oportunidade de Negócios XDM no Experience Data Model (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 5%

---

# [!UICONTROL Ciclo de ] oportunidades de negócios XDM

>[!NOTE]
>
>Essa classe só está disponível para organizações que têm acesso à edição B2B da Plataforma de dados do cliente em tempo real.

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
