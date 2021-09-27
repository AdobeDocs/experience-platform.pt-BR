---
title: Classe de Conta Comercial XDM
description: Este documento fornece uma visão geral da classe de conta comercial XDM no Experience Data Model (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 3%

---

# [!UICONTROL Classe de ] Conta Comercial XDM

>[!NOTE]
>
>Essa classe só está disponível para organizações que têm acesso à edição B2B da Plataforma de dados do cliente em tempo real.

[!UICONTROL A XDM Business ] Accountis é uma classe padrão do Experience Data Model (XDM) que captura as propriedades mínimas exigidas de uma conta comercial.

![](../../images/classes/b2b/business-account.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a entidade da conta. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de Auditoria do Sistema de Origem Externa]](../../data-types/external-source-system-audit-attributes.md) | Se a conta for proveniente de um sistema de origem externo, esse objeto capturará atributos de auditoria para esse sistema. |
| `_id` | String | Um identificador exclusivo para o registro. Este é um valor gerado pelo sistema separado do `accountID`. |
| `accountID` | String | Um identificador exclusivo para a entidade da conta. |
