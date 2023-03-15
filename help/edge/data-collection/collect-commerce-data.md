---
title: Coletar informações de comércio e produto usando o SDK da Web da Adobe Experience Platform
description: Saiba como adicionar dados relacionados a produtos ou um carrinho de compras usando o Adobe Experience Platform Web SDK.
keywords: products;commerce;measures;measure;order;cartAbandons;checkouts;productListAdds;productListOpens;productListRemovals;productListReopens;productListViews;productViews;purchases;saveForLaters;currencyCode;payments;paymentAmount;paymentType;transactionID;priceTotal;purchaseID;purchaseOrderNumber;
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
source-git-commit: 51a18ca3a9d0817eafeecea328900eb2f4d1d9a4
workflow-type: tm+mt
source-wordcount: '1326'
ht-degree: 6%

---

# Coletar informações de comércio e produto

Se você tiver produtos em seu site, esse é um conjunto padrão de itens que você pode desejar enviar para ativar a maioria dos recursos do Adobe. Embora essa seja uma sugestão, ela fornece um conjunto de dados muito forte desde o início.

Este documento usa o [Detalhes de comércio do ExperienceEvent](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) grupo de campos de esquema. A variável `commerce` O grupo de campos é dividido em duas partes: a variável `commerce` e o `productListItems` matriz. A variável `commerce` permite indicar quais ações estão acontecendo com o `productListItems` matriz.

>[!TIP]
>
>Se você estiver familiarizado com o Adobe Analytics, o `commerce` está mais estreitamente relacionado com a `events` variável. A variável `productListItems` está mais estreitamente relacionada com a `products` variável.

## Ações relacionadas a produtos

Veja abaixo uma lista de `measures` disponível no `commerce` objeto.

>[!TIP]
>
>Uma medida tem dois campos: `id` e `value`. Na maioria das vezes, você usará o `value` somente campo (por exemplo, `'value':1`). A variável `id` permite definir um identificador exclusivo que pode ser usado para rastrear quando a medida foi enviada. Consulte a documentação do XDM para [Medir](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md).

| **Medição** | **Recomendação** | **Descrição** |
|---|---|---|
| [cartAbandons](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | Opcional | Um carrinho não pode mais ser acessado ou comprado pelo usuário. |
| [check-outs](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | Altamente recomendado | Um usuário não está mais procurando produtos, mas está comprando um produto. |
| [productListAdds](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | Altamente recomendado | Um produto é adicionado a uma lista. Certifique-se de definir o produto no `productListItems` ao mesmo tempo. |
| [productListOpens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | Opcional | Uma nova lista de produtos é criada. (Por exemplo, um novo carrinho de compras é criado.) |
| [productListRemovals](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | Altamente recomendado | Um produto é removido de uma lista de produtos. |
| [productListReopens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | Opcional | Uma lista de produtos é reativada pelo usuário. Isso geralmente acontece em campanhas de remarketing. |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | Altamente recomendado | Uma lista de produtos é exibida. |
| [productViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | Altamente recomendado | Ocorreu uma visualização de um produto. Certifique-se de definir o produto visualizado na `productListItems`. |
| [compras](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | Altamente recomendado | Um pedido é aceito. Deve ter uma lista de produtos. |
| [saveForLaters](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | Opcional | Um produto é salvo para uso futuro. |

Este é um exemplo de como você define esses `Measures` no SDK.

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

O objeto de comércio também tem um campo especial para coletar detalhes do pedido chamado `order`.

| **Pedido** | **Option** | **Recomendação** | **Descrição** |
|---|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) |  |  | A variável [ISO 4217](https://pt.wikipedia.org/wiki/ISO_4217) moeda do total do pedido. |
| [pagamentos[paymentItems]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | A lista de pagamentos de um pedido. A [paymentItem](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema) inclui o seguinte. |
|  | [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | Opcional | A variável [ISO 4217](https://pt.wikipedia.org/wiki/ISO_4217) moeda para este método de pagamento. |
|  | [paymentAmount](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | Altamente recomendado | O valor do pagamento no código de moeda especificado. |
|  | [paymentType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | Altamente recomendado | O tipo de pagamento (por exemplo, `credit_card`, `gift_card`, `paypal`). Consulte a lista de [valores conhecidos](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values) para obter detalhes. |
|  | [transactionID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmtransactionid) | Opcional | Um identificador exclusivo para esta transação de pagamento. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpricetotal) |  | Altamente recomendado | O total deste pedido após a aplicação de todos os descontos e impostos. |
| [purchaseID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseid) |  | Altamente recomendado | O identificador exclusivo atribuído pelo vendedor para esta compra. |
| [purchaseOrderNumber](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseordernumber) |  | Opcional | Um identificador exclusivo atribuído pelo comprador para esta compra. |

Este é um exemplo de uma compra típica no SDK.

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

## Listas de produtos

A lista de produtos indica quais produtos estão relacionados à ação correspondente. É uma lista de [productListItems](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md). Cada produto tem vários campos opcionais.

| **Campo** | **Recomendação** | **Descrição** |
|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmcurrencycode) | Opcional | A variável [ISO 4217](https://pt.wikipedia.org/wiki/ISO_4217) moeda do produto. Isso só é útil quando você pode ter produtos com códigos de moeda diferentes e quando se aplica. Por exemplo, quando há uma compra ou adição ao carrinho. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | Altamente recomendado | Só deve ser definido quando aplicável. Por exemplo, talvez não seja possível definir em `productView` diferentes variações do produto podem ter preços diferentes, mas numa base `productListAdds` evento. |
| [produto](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | Altamente recomendado | A ID XDM do produto. |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | Altamente recomendado | O método usado para adicionar um item de produto à lista pelo visitante. Definir com `productListAdds` e só devem ser usadas quando um produto for adicionado à lista. Os exemplos incluem `add to cart button`, `quick add` e `upsell`. |
| [productName](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | Altamente recomendado | É definido como o nome de exibição ou nome legível do produto. |
| [quantidade](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | Altamente recomendado | O número de unidades que o cliente indicou que precisa do produto. Deve ser definido em `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters`e assim por diante. |
| [SKU](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md) | Altamente recomendado | Unidade de manutenção de armazenamento. É o identificador exclusivo do produto. |

## Exemplos

`productViews` evento

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

`productListAdds` evento

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

`checkouts` evento

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

`order` evento

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
