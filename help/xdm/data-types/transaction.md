---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, campos, esquemas, esquemas, transação, tipo de dados, tipo de dados, tipo de dados;
title: Tipo de dados da transação
description: Este documento fornece uma visão geral do tipo de dados do Modelo de dados de experiência de transação (XDM).
source-git-commit: bbe5456ddba1db9044b8a7f94a7ba8e450f89f0f
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 8%

---

#  Tipo de dados de transação

 A transação é um tipo de dados padrão do Experience Data Model (XDM) que descreve os detalhes de uma transação monetária.

![Estrutura da transação](../images/data-types/transaction.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `transactionAmount` | [[!UICONTROL Moeda]](./currency.md) | Descreve a quantia de moeda trocada como parte da transação. |
| `transactionDate` | [!UICONTROL DateTime] | Um carimbo de data e hora de quando a transação ocorreu. |
| `transactionId` | [!UICONTROL String] | Um identificador exclusivo para a transação. |
| `transactionType` | [!UICONTROL String] | O tipo de transação usado pelo visitante. |

{style=&quot;table-layout:auto&quot;}
