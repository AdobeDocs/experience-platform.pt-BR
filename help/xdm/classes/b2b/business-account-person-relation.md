---
title: Classe de Relação de Pessoa da Conta Funcional XDM
description: Este documento fornece uma visão geral da classe de relação de pessoa da conta comercial XDM no Experience Data Model (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 3%

---

# [!UICONTROL Classe de ] Relacionamento de Pessoa da Conta Comercial XDM

>[!NOTE]
>
>Essa classe só está disponível para organizações que têm acesso à edição B2B da Plataforma de dados do cliente em tempo real.

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
