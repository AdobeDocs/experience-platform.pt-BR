---
title: Grupo de Campos de Esquema de Detalhes do Depósito
description: Este documento fornece uma visão geral do grupo de campos de esquema Detalhes do depósito.
exl-id: a40d17b3-cb76-4b63-9328-735fc7c55672
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 2%

---

# [!UICONTROL Detalhes do depósito] grupo de campos de esquema

[!UICONTROL Detalhes do depósito] é um grupo de campos de esquema padrão para o [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). O grupo de campos fornece um único `personalFinances.deposits` para um esquema, que captura detalhes sobre um depósito financeiro.

![](../../images/field-groups/deposit-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `account` | [[!UICONTROL Conta financeira]](../../data-types/financial-account.md) | Descreve a conta financeira associada ao depósito. |
| `transaction` | [[!UICONTROL Transação]](../../data-types/transaction.md) | Descreve a transação financeira associada ao depósito. |
| `mobileDeposit` | [!UICONTROL Booleano] | Indica se o depósito foi feito por meio de uma plataforma móvel. |

{style="table-layout:auto"}

Para obter mais informações sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json).
