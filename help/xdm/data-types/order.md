---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;order;datatype;data-type;data type;Schema;home;popular topics;;XDM;fields;processors;order;datatype;data-type;data type;
solution: Experience Platform
title: Tipo de dados da ordem
topic: overview
description: Este documento fornece uma visão geral do tipo de dados do Order Experience Data Model (XDM).
translation-type: tm+mt
source-git-commit: 8bbb062df47b6e94630626d0a89a179d759d922d
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 4%

---


# [!UICONTROL Tipo ] de dados de pedido

[!UICONTROL O ] Orderé um tipo de dados padrão do Experience Data Model (XDM) que descreve o pedido feito para uma lista de produto.

<img src="../images/data-types/order.PNG" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `payments` | Matriz de [[!UICONTROL Itens de Pagamento]](./payment-item.md) | A lista de pagamentos desta ordem. |
| `currencyCode` | String | O código monetário ISO 4217 usado para os totais das ordens. Todas as instâncias devem estar em conformidade com a expressão regular `^[A-Z]{3}$`. Os exemplos incluem `USD` e `EUR`. |
| `priceTotal` | Duplo | O preço total deste pedido após todos os descontos e impostos terem sido aplicados. |
| `purchaseID` | String | Um identificador exclusivo atribuído pelo vendedor para esta compra ou contrato. Como isso é definido pelo vendedor, não há garantia de que a ID seja exclusiva. |
| `purchaseOrderNumber` | String | O identificador exclusivo atribuído pelo comprador para esta compra ou contrato. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)