---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, campos, esquemas, esquemas, ordem, tipo de dados, tipo de dados, tipo de dados;
solution: Experience Platform
title: Tipo de dados do pedido
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados do Order Experience Data Model (XDM).
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 4%

---

# [!UICONTROL Order] tipo de dados

[!UICONTROL Order] é um tipo de dados padrão do Experience Data Model (XDM) que descreve a ordem colocada para uma lista de produtos.

<img src="../images/data-types/order.PNG" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `payments` | Matriz de [[!UICONTROL Payment Items]](./payment-item.md) | A lista de pagamentos para esta ordem. |
| `currencyCode` | String | O código monetário ISO 4217 usado para os totais de pedidos. Todas as instâncias devem estar em conformidade com a expressão regular `^[A-Z]{3}$`. Os exemplos incluem `USD` e `EUR`. |
| `priceTotal` | Duplo | O preço total deste pedido após a aplicação de todos os descontos e impostos. |
| `purchaseID` | String | Um identificador exclusivo atribuído pelo vendedor para esta compra ou contrato. Como isso é definido pelo vendedor, não há garantia de que a ID seja exclusiva. |
| `purchaseOrderNumber` | String | O identificador exclusivo atribuído pelo comprador para esta compra ou contrato. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
