---
title: Grupo de Campos de Esquema de Transferências de Saldo
description: Este documento fornece uma visão geral do grupo de campos de esquema Transferências de Saldo.
exl-id: be0d2ed6-6547-432a-af2f-409c33e268d4
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 1%

---

# [!UICONTROL Transferências de saldo] grupo de campos de esquema

[!UICONTROL Transferências de saldo] é um grupo de campos de esquema padrão para o [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). O grupo de campos fornece um único `personalFinances.balanceTransfers` para um schema, que captura detalhes sobre uma transferência de saldo financeiro entre contas.

![](../../images/field-groups/balance-transfers.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `accountFrom` | [[!UICONTROL Conta financeira]](../../data-types/financial-account.md) | Descreve a conta financeira da qual o saldo está sendo transferido. |
| `accountTo` | [[!UICONTROL Conta financeira]](../../data-types/financial-account.md) | Descreve a conta financeira para a qual o saldo está sendo transferido. |
| `transaction` | [[!UICONTROL Transação]](../../data-types/transaction.md) | Descreve a transação financeira associada à transferência de saldo. |

{style="table-layout:auto"}

Para obter mais informações sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-balance-transfers.schema.json).
