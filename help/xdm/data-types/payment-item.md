---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, campos, esquemas, esquemas, esquema, item de pagamento, tipo de dados, tipo de dados, tipo de dados;
solution: Experience Platform
title: Tipo de Dados do Item de Pagamento
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados do Modelo de Dados de Experiência de Item de Pagamento (XDM).
exl-id: d25a358b-73c1-468b-a9c5-808385689932
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 7%

---

# [!UICONTROL Tipo de dados ] dos Itens de Pagamento

[!UICONTROL O ] Item de Pagamento é um tipo de dados padrão do Experience Data Model (XDM) que descreve um pagamento associado a uma ordem que define o tipo de pagamento, a quantia e a moeda associada.

<img src="../images/data-types/payment-item.PNG" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `currencyCode` | String | O código monetário ISO 4217 usado para os totais de pedidos. Todas as instâncias devem estar em conformidade com a expressão regular `^[A-Z]{3}$`. Os exemplos incluem `USD` e `EUR`. |
| `paymentAmount` | Duplo | O valor do pagamento. |
| `paymentType` | String | O método de pagamento desta ordem. Os valores de enum aceitos incluem: <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | String | O identificador exclusivo de transação para este item de pagamento. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)
