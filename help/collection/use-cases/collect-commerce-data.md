---
title: Coletar informações de comércio, produto e pedido usando o Adobe Experience Platform Web SDK
description: Saiba como adicionar dados relacionados a produtos ou um carrinho de compras usando o Adobe Experience Platform Web SDK.
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
source-git-commit: 9b2ecedfafbafed042eba73a034cb9b9e95af579
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 2%

---

# Coletar informações de comércio, produto e pedido

Se sua organização vende produtos ou serviços, você pode usar esta página como um guia sobre como rastrear esses produtos e serviços.

Esta página usa o grupo de campos [Esquema Commerce](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md) do XDM.

Este grupo de campos consiste em duas partes principais:

* O objeto `commerce`. Este objeto permite indicar quais ações ocorrem com a matriz `productListItems`.
* A matriz `productListItems`.

>[!TIP]
>
>Se você estiver familiarizado com o Adobe Analytics, o objeto `commerce` conterá dados semelhantes aos eventos de comércio na variável `events`. A matriz de objetos `productListItems` contém dados semelhantes à variável `products`.

## O objeto `commerce` {#commerce-object}

Esta seção descreve os campos disponíveis no objeto `commerce`.

>[!TIP]
>
>Uma medida tem dois campos: `id` e `value`. Na maioria das vezes, você só usa o campo `value` (por exemplo, `'value':1`). O campo `id` permite definir um identificador exclusivo para rastreamento quando a medida foi enviada. Consulte a documentação do XDM para [Medida](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/measure.schema.md) para obter mais informações.

| Medição | Recomendação | Descrição |
|---|---|---|
| [`cartAbandons`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcartabandons) | Opcional | Um carrinho não pode mais ser acessado ou comprado pelo usuário. |
| [`checkouts`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcheckouts) | Altamente recomendado | Um usuário não está mais procurando produtos, mas está comprando um produto. |
| [`productListAdds`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistadds) | Altamente recomendado | Um produto é adicionado a uma lista. Defina o produto no `productListItems` ao mesmo tempo. |
| [`productListOpens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistopens) | Opcional | Uma nova lista de produtos é criada. Por exemplo, um novo carrinho de compras é criado. |
| [`productListRemovals`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistremovals) | Altamente recomendado | Um produto é removido de uma lista de produtos. |
| [`productListReopens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistreopens) | Opcional | Uma lista de produtos é reativada pelo usuário. Essa ação geralmente acontece em campanhas de remarketing. |
| [`productListViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistviews) | Altamente recomendado | Uma lista de produtos é exibida. |
| [`productViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductviews) | Altamente recomendado | Ocorreu uma exibição de um produto. Defina o produto exibido no `productListItems`. |
| [`purchases`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmpurchases) | Altamente recomendado | Um pedido é aceito. Deve ter uma lista de produtos. |
| [`saveForLaters`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmsaveforlaters) | Opcional | Um produto é salvo para uso futuro. |

{style="table-layout:auto"}

### Exemplos de objeto `Commerce`

Expanda a seção abaixo para ver um exemplo de um comando do Web SDK usando um campo do objeto `commerce`.

+++`productViews`

Uma chamada `sendEvent` básica do Web SDK definindo o campo `productViews` como `1`:

```javascript
alloy("sendEvent", {
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    }
  }
});
```

+++

## O objeto `order` {#order-object}

O objeto `commerce` contém um objeto dedicado para coletar detalhes do pedido. Isso é chamado de objeto `order`.

Esta seção descreve todos os campos suportados pelo objeto `order`.

| Campo | Opção | Recomendação | Descrição |
|---|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmcurrencycode) |  |  | A moeda [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) para o total do pedido. |
| [`payments[]`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpayments) |  |  | A lista de pagamentos de um pedido. Um [paymentItem](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md) inclui o seguinte. |
|  | [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmcurrencycode) | Opcional | A moeda [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) para este método de pagamento. |
|  | [`paymentAmount`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymentamount) | Altamente recomendado | O valor do pagamento no código de moeda especificado. |
|  | [`paymentType`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype) | Altamente recomendado | O tipo de pagamento (por exemplo, `credit_card`, `gift_card`, `paypal`). Consulte a lista de [valores conhecidos](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype-known-values) para obter detalhes. |
|  | [`transactionID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmtransactionid) | Opcional | Um identificador exclusivo para esta transação de pagamento. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpricetotal) |  | Altamente recomendado | O total deste pedido após a aplicação de todos os descontos e impostos. |
| [`purchaseID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseid) |  | Altamente recomendado | O identificador exclusivo atribuído pelo vendedor para esta compra. |
| [`purchaseOrderNumber`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseordernumber) |  | Opcional | Um identificador exclusivo atribuído pelo comprador para esta compra. |

### Exemplos de objetos de ordem

Expanda a seção abaixo para ver um exemplo de um comando do Web SDK usando o objeto `commerce`.

+++Exemplo de objeto `Order`

Uma chamada de Web SDK `sendEvent` definindo o objeto `order` que se aplica a vários produtos na matriz `productListItems`:

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currencyCode":"USD",
        "priceTotal":39.98,
        "payments":[
          {
            "transactionID":"amx12345",
            "paymentAmount":39.98,
            "paymentType":"credit_card",
            "currencyCode":"USD"
          }
        ]
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "priceTotal":29.99,
        "quantity":1
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "priceTotal":9.99,
        "quantity":1
      }
    ]
  }
});
```

+++

## O objeto da lista de produtos {#product-list-object}

A lista de produtos indica quais produtos estão relacionados à ação correspondente. Esta é uma lista de [productListItems](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md). Cada produto tem vários campos opcionais.

| Campo | Recomendação | Descrição |
|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmcurrencycode) | Opcional | A moeda [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) do produto. Normalmente, esse campo só se aplica quando você tem vários produtos na lista de produtos com códigos monetários diferentes. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmpricetotal) | Altamente recomendado | Defina esse campo somente quando aplicável. Por exemplo, talvez não seja possível definir em um evento `productView` porque variações diferentes do produto podem ter preços diferentes, mas em um evento `productListAdds`. |
| [`product`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproduct) | Altamente recomendado | A ID XDM do produto. |
| [`productAddMethod`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproductaddmethod) | Altamente recomendado | O método usado para adicionar um item de produto à lista pelo visitante. Definido com `productListAdds` medidas e usado somente quando um produto é adicionado à lista. Os exemplos incluem `add to cart button`, `quick add` e `upsell`. |
| [`productName`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmname) | Altamente recomendado | O nome de exibição ou o nome legível do produto. |
| [`quantity`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmquantity) | Altamente recomendado | O número de unidades que o cliente indicou que precisa do produto. Deve ser definido em `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters` e assim por diante. |
| [`SKU`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmsku) | Altamente recomendado | Unidade de manutenção de armazenamento. É o identificador exclusivo do produto. |

### Exemplos de lista de produtos

Expanda as seções abaixo para ver exemplos de comandos do Web SDK usando o objeto `productListItems`.

+++Exemplo de `productListItems`

Uma chamada `sendEvent` do Web SDK define o `productViews` para vários produtos na matriz `productListItems`:

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
      }
    ]
  }
});
```

+++

+++Exemplo de `productListAdds`

Uma chamada `sendEvent` do Web SDK que define o evento `productListAdds` para vários produtos na matriz `productListItems`:

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productListAdds":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "quantity":1,
        "priceTotal":29.99,
        "productAddMethod":"Add to Cart Button"
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "quantity":1,
        "priceTotal":9.99,
        "productAddMethod":"Add-on"
      }
    ]
  }
});
```

+++

+++Exemplo de `checkouts`

Uma chamada `sendEvent` do Web SDK que define o evento `checkouts` para vários produtos na matriz `productListItems`:

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "checkouts":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "quantity":1,
        "priceTotal":29.99
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "quantity":1,
        "priceTotal":9.99
      }
    ]
  }
});
```

+++
