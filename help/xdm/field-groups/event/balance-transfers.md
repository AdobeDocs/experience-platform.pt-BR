---
title: Grupo de Campos de Esquema de Transferências de Saldo
description: Saiba mais sobre o grupo de campos de esquema Transferências de saldo.
exl-id: be0d2ed6-6547-432a-af2f-409c33e268d4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 3%

---

# [!UICONTROL Transferências de saldo] grupo de campos de esquema

[!UICONTROL Transferências de Saldo] é um grupo de campos de esquema padrão para a [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). O grupo de campos fornece um único objeto `personalFinances.balanceTransfers` para um esquema, que captura detalhes sobre uma transferência de saldo financeiro entre contas.

![](../../images/field-groups/balance-transfers.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `accountFrom` | [[!UICONTROL Conta financeira]](../../data-types/financial-account.md) | Descreve a conta financeira da qual o saldo está sendo transferido. |
| `accountTo` | [[!UICONTROL Conta financeira]](../../data-types/financial-account.md) | Descreve a conta financeira para a qual o saldo está sendo transferido. |
| `transaction` | [[!UICONTROL Transação]](../../data-types/transaction.md) | Descreve a transação financeira associada à transferência de saldo. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-balance-transfers.schema.json).
