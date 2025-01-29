---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;item de pagamento;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de Dados do Item de Pagamento
description: Saiba mais sobre o tipo de dados do Modelo de dados de experiência de item de pagamento (XDM).
exl-id: d25a358b-73c1-468b-a9c5-808385689932
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 14%

---

# Tipo de dados [!UICONTROL Item de pagamento]

[!UICONTROL Item de Pagamento] é um tipo de dados padrão do Experience Data Model (XDM) que descreve um pagamento associado a um pedido que define o tipo de pagamento, o valor e a moeda associada.

![imagem do item de pagamento](../images/data-types/payment-item.PNG){width=400}

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `currencyCode` | String | O código de moeda ISO 4217 usado para os totais do pedido. Todas as instâncias devem estar em conformidade com a expressão regular `^[A-Z]{3}$`. Exemplos incluem `USD` e `EUR`. |
| `paymentAmount` | Duplo | O valor do pagamento. |
| `paymentType` | String | O método de pagamento deste pedido. Os valores de enumeração aceitos incluem: <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | String | O identificador de transação exclusivo para este item de pagamento. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)
