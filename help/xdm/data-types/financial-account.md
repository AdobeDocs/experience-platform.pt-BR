---
title: Tipo de Dados da Conta Financeira
description: Este documento fornece uma visão geral do tipo de dados XDM da Conta Financeira.
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 8%

---

# [!UICONTROL Conta financeira] tipo de dados

[!UICONTROL Conta financeira] é um tipo de dados XDM padrão que descreve os detalhes de uma conta financeira, incluindo seu tipo, proprietário e saldo atual.

![](../images/data-types/financial-account.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `currentAccountBalance` | [[!UICONTROL Moeda]](./currency.md) | O saldo corrente da conta. |
| `financialAccountId` | [!UICONTROL String] | Uma ID exclusiva para a conta. |
| `financialAccountName` | [!UICONTROL String] | O nome atribuído à conta. |
| `financialAccountType` | [!UICONTROL String] | O tipo de conta financeira, como verificação, poupança ou aposentadoria. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados, consulte [repositório XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/financial-account.schema.json).
