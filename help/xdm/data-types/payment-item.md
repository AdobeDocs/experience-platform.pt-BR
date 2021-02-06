---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;campos;schemas;Schemas;item de pagamento;datatype;data-type;tipo de dados;
solution: Experience Platform
title: Tipo de Dados de Item de Pagamento
topic: overview
description: Este documento fornece uma visão geral do tipo de dados XDM (Payment Item Experience Data Model, Modelo de Dados de Experiência de Item de Pagamento).
translation-type: tm+mt
source-git-commit: 8bbb062df47b6e94630626d0a89a179d759d922d
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 5%

---


# [!UICONTROL Tipo de dados ] dos Itens de Pagamento

[!UICONTROL O ] Item de Pagamento é um tipo de dados padrão do Modelo de Dados de Experiência (XDM) que descreve um pagamento associado a uma ordem que define o tipo de pagamento, a quantia e a moeda associada.

<img src="../images/data-types/payment-item.PNG" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `currencyCode` | String | O código monetário ISO 4217 usado para os totais das ordens. Todas as instâncias devem estar em conformidade com a expressão regular `^[A-Z]{3}$`. Os exemplos incluem `USD` e `EUR`. |
| `paymentAmount` | Duplo | O valor do pagamento. |
| `paymentType` | String | O método de pagamento desta ordem. Os valores de enumeração aceitos incluem: <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | String | O identificador de transação exclusivo para este item de pagamento. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)