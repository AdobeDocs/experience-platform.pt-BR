---
title: Tipo de dados da conta financeira
description: Este documento fornece uma visão geral do tipo de dados XDM da conta financeira.
exl-id: badf9b20-d397-4b46-b045-19c69806fe8e
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 5%

---

# [!UICONTROL Conta financeira] tipo de dados

[!UICONTROL Conta financeira] é um tipo de dados XDM padrão que descreve os detalhes de uma conta financeira, incluindo seu tipo, proprietário e saldo atual.

![](../images/data-types/financial-account.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `currentAccountBalance` | [[!UICONTROL Moeda]](./currency.md) | O saldo atual da conta. |
| `financialAccountId` | [!UICONTROL String] | Um identificador exclusivo para a conta. |
| `financialAccountName` | [!UICONTROL String] | O nome atribuído à conta. |
| `financialAccountType` | [!UICONTROL String] | O tipo de conta financeira, como corrente, poupança ou baixa. |

{style="table-layout:auto"}

Para obter mais informações sobre o tipo de dados, consulte a [repositório XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/financial-account.schema.json).
