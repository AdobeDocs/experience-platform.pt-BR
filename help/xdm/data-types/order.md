---
keywords: Experience Platform;início;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;ordem;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de dados do pedido
description: Saiba mais sobre o tipo de dados do Order Experience Data Model (XDM).
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 6%

---

# [!UICONTROL Pedido] tipo de dados

[!UICONTROL Pedido] é um tipo de dados padrão do Experience Data Model (XDM) que descreve o pedido feito para uma lista de produtos.

<img src="../images/data-types/order.PNG" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `payments` | Matriz de [[!UICONTROL Itens de pagamento]](./payment-item.md) | A lista de pagamentos deste pedido. |
| `currencyCode` | String | O código de moeda ISO 4217 usado para os totais do pedido. Todas as instâncias devem estar em conformidade com a expressão regular `^[A-Z]{3}$`. Os exemplos incluem `USD` e `EUR`. |
| `priceTotal` | Duplo | O preço total deste pedido após a aplicação de todos os descontos e impostos. |
| `purchaseID` | String | Um identificador exclusivo atribuído pelo vendedor para esta compra ou contrato. Como isso é definido pelo vendedor, não há garantia de que a ID seja exclusiva. |
| `purchaseOrderNumber` | String | O identificador exclusivo atribuído pelo comprador para esta compra ou contrato. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
