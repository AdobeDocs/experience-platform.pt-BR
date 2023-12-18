---
keywords: Experience Platform;início;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;transação;tipo de dados;tipo de dados;tipo de dados;
title: Tipo de Dados da Transação
description: Saiba mais sobre o tipo de dados Transaction Experience Data Model (XDM).
exl-id: 47b7152f-a853-44f0-8962-e902631ad8a4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 7%

---

# [!UICONTROL Transação] tipo de dados

[!UICONTROL Transação] é um tipo de dados padrão do Experience Data Model (XDM) que descreve os detalhes de uma transação monetária.

![Estrutura de transação](../images/data-types/transaction.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `transactionAmount` | [[!UICONTROL Moeda]](./currency.md) | Descreve a quantidade de moeda trocada como parte da transação. |
| `transactionDate` | [!UICONTROL DateTime] | Um carimbo de data e hora de quando a transação ocorreu. |
| `transactionId` | [!UICONTROL String] | Um identificador exclusivo para a transação. |
| `transactionType` | [!UICONTROL String] | O tipo de transação usado pelo visitante. |

{style="table-layout:auto"}
