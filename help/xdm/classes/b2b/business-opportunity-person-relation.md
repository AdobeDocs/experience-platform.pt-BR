---
title: Classe de Relação de Pessoa da Oportunidade Comercial XDM
description: Este documento fornece uma visão geral da classe de relação de pessoa da oportunidade de negócios XDM no Experience Data Model (XDM).
exl-id: 7be193d2-52eb-4b28-953b-5e0fc21d8f93
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 4%

---

# [!UICONTROL Classe de ] Relacionamento de Pessoa da Oportunidade Comercial XDM (Beta)

>[!IMPORTANT]
>
>Essa classe está disponível como parte da Real-time Customer Data Platform B2B Edition, que está atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

[!UICONTROL O XDM Business Oportunity Person ] Relationé uma classe padrão do Experience Data Model (XDM) que captura as propriedades mínimas necessárias de uma pessoa associada a uma oportunidade de negócios.

![](../../images/classes/b2b/business-opportunity-person-relation.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de Auditoria do Sistema de Origem Externa]](../../data-types/external-source-system-audit-attributes.md) | Se a relação do empresário for proveniente de um sistema de origem externo, esse objeto capturará atributos de auditoria para esse sistema. |
| `opportunityKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a oportunidade na relação oportunidade-pessoa. |
| `opportunityPersonKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a entidade de relação oportunidade-pessoa. |
| `personKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a pessoa na relação oportunidade-pessoa. |
| `_id` | String | Um identificador exclusivo para o registro. Esse é um valor gerado pelo sistema separado dos outros campos de ID capturados pela classe. |
| `opportunityID` | String | Um identificador exclusivo para a oportunidade no relacionamento oportunidade-pessoa. |
| `opportunityPersonID` | String | Um identificador exclusivo para a entidade de relação oportunidade-pessoa |
| `isPrimary` | Booleano | Indica se a pessoa é o contato principal para esta oportunidade. |
| `personID` | String | Um identificador exclusivo para a pessoa na relação oportunidade-pessoa. |
| `personRole` | String | A função da pessoa na relação oportunidade-pessoa. |

{style=&quot;table-layout:auto&quot;}

Consulte o guia sobre [relações de esquema na CDP em tempo real B2B Edition](../../tutorials/relationship-b2b.md) para saber como essa classe se relaciona conceitualmente com as outras classes B2B e como você pode estabelecer esses relacionamentos na interface do usuário do Adobe Experience Platform.
