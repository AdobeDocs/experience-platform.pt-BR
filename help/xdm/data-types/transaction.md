---
keywords: Experience Platform;início;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;transação;tipo de dados;tipo de dados;tipo de dados;
title: Tipo de Dados da Transação
description: Este documento fornece uma visão geral do tipo de dados Transaction Experience Data Model (XDM).
exl-id: 47b7152f-a853-44f0-8962-e902631ad8a4
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 5%

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
