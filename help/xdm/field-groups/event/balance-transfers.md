---
title: Grupo de Campos de Esquema de Transferências de Saldo
description: Este documento fornece uma visão geral do grupo de campos de esquema Transferências de Saldo.
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 4%

---

# [!UICONTROL Transferências de Saldo] grupo de campos de esquema

[!UICONTROL Transferências de Saldo] é um grupo de campos de esquema padrão para a variável [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). O grupo de campos fornece um único `personalFinances.balanceTransfers` objeto a um schema, que captura detalhes sobre uma transferência de saldo financeiro entre contas.

![](../../images/field-groups/balance-transfers.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `accountFrom` | [[!UICONTROL Conta financeira]](../../data-types/financial-account.md) | Descreve a conta financeira da qual o saldo está sendo transferido. |
| `accountTo` | [[!UICONTROL Conta financeira]](../../data-types/financial-account.md) | Descreve a conta financeira para a qual o saldo está sendo transferido. |
| `transaction` | [[!UICONTROL Transação]](../../data-types/transaction.md) | Descreve a transação financeira associada à transferência de saldo. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte [repositório XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-balance-transfers.schema.json).
