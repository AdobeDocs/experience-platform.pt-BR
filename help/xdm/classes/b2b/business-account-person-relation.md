---
title: Classe de Relação de Pessoa da Conta Funcional XDM
description: Este documento fornece uma visão geral da classe de relação de pessoa da conta comercial XDM no Experience Data Model (XDM).
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 4%

---

# [!UICONTROL Classe de ] Relacionamento de Pessoa da Conta Comercial XDM (Beta)

>[!IMPORTANT]
>
>Essa classe está disponível como parte da Real-time Customer Data Platform B2B Edition, que está atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

[!UICONTROL O XDM Business Account Person ] Relationé uma classe padrão do Experience Data Model (XDM) que captura as propriedades mínimas exigidas de uma pessoa associada a uma conta comercial.

![](../../images/classes/b2b/business-account-person-relation.png)

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
| `isDirect` | Booleano | Indica se esta é uma relação direta entre a conta e a pessoa. |
| `isPrimary` | Booleano | Indica se a pessoa é o contato principal nesta conta. |
| `personID` | String | Um identificador exclusivo da pessoa no relacionamento conta-pessoa. |
| `personRole` | String | A função da pessoa no relacionamento conta-pessoa. |
| `relationEndDate` | DateTime | A data em que o relacionamento entre a conta e a pessoa terminou. |
| `relationStartDate` | DateTime | A data em que a relação entre a conta e a pessoa começou. |

{style=&quot;table-layout:auto&quot;}

Consulte o guia sobre [relações de esquema na CDP em tempo real B2B Edition](../../tutorials/relationship-b2b.md) para saber como essa classe se relaciona conceitualmente com as outras classes B2B e como você pode estabelecer esses relacionamentos na interface do usuário do Adobe Experience Platform.
