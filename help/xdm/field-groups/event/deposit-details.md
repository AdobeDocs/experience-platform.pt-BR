---
title: Grupo de Campos do Esquema Detalhes do Depósito
description: Este documento fornece uma visão geral do grupo de campos Detalhes do Depósito.
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 5%

---

# [!UICONTROL Detalhes do Depósito] grupo de campos de esquema

[!UICONTROL Detalhes do Depósito] é um grupo de campos de esquema padrão para a variável [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). O grupo de campos fornece um único `personalFinances.deposits` para um schema, que captura detalhes sobre um depósito financeiro.

![](../../images/field-groups/deposit-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `account` | [[!UICONTROL Conta financeira]](../../data-types/financial-account.md) | Descreve a conta financeira associada ao depósito. |
| `transaction` | [[!UICONTROL Transação]](../../data-types/transaction.md) | Descreve a transação financeira associada ao depósito. |
| `mobileDeposit` | [!UICONTROL Booleano] | Indica se o depósito foi feito por meio de uma plataforma móvel. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte [repositório XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json).
