---
title: Produtos
seo-title: Suporte a produtos com Adobe Experience Platform Web SDK
description: Saiba como adicionar dados se você tiver produtos ou um carrinho de compras com o Experience Platform Web SDK
seo-description: Saiba como adicionar dados se você tiver produtos ou um carrinho de compras com o Experience Platform Web SDK
keywords: products;commerce;measures;measure;order;cartAbandons;checkouts;productListAdds;productListOpens;productListRemovals;productListReopens;productListViews;productViews;purchases;saveForLaters;currencyCode;payments;paymentAmount;paymentType;transactionID;priceTotal;purchaseID;purchaseOrderNumber;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 6%

---


# Produtos

Se você tiver produtos em seu site, esse é um conjunto padrão de itens que você pode querer enviar para ativar a maioria dos recursos do Adobe. Embora esta seja uma sugestão, ela fornece um conjunto muito forte de dados diretamente do start.

Este documento usa a combinação Detalhes [do Comércio de](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) ExperienceEvent. A `commerce` mistura é dividida em duas partes: o `commerce` objeto e a `productListItems` matriz. O `commerce` objeto permite indicar quais ações estão acontecendo na `productListItems` matriz.

>[!TIP]
>
>Se você estiver familiarizado com o Adobe Analytics, o The `commerce` está mais relacionado à `events` variável. O `productListItems` está mais relacionado à `products` variável.

## Ações relacionadas a produtos

Abaixo está uma lista de `measures` disponível no `commerce` objeto.

>[!TIP]
>
>Uma medida tem dois campos: `id` e `value`. Na maioria das vezes, você usará somente o `value` campo (por exemplo, `'value':1`). O `id` campo permite definir um identificador exclusivo que você pode usar para rastrear quando a medida foi enviada. Consulte a documentação XDM para [Medir](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md).

| **Medição** | **Recomendação** | **Descrição** |
|---|---|---|
| [cartAbandons](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | Opcional | Um carrinho não pode mais ser acessado ou comprado pelo usuário. |
| [check-outs](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | Altamente recomendado | Um usuário não está mais procurando produtos, mas está comprando um produto. |
| [productListAdds](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | Altamente recomendado | Um produto é adicionado a uma lista. Certifique-se de definir o produto ao `productListItems` mesmo tempo. |
| [productListOpens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | Opcional | Uma nova lista de produto é criada. (Por exemplo, um novo carrinho de compras é criado.) |
| [productListRemoces](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | Altamente recomendado | Um produto é removido de uma lista de produto. |
| [productListReopen](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | Opcional | Uma lista de produto é reativada pelo usuário. Isso frequentemente acontece em campanhas de remarketing. |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | Altamente recomendado | Uma lista de produtos é visualizada. |
| [productViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | Altamente recomendado | Ocorreu uma visualização de um produto. Certifique-se de definir o produto exibido no `productListItems`. |
| [compras](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | Altamente recomendado | Um pedido é aceito. Deve ter uma lista de produto. |
| [saveForLaters](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | Opcional | Um produto é salvo para uso futuro. |

Este é um exemplo de como você pode defini-los `Measures` no SDK.

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

O objeto commerce também tem um campo especial para coletar detalhes de pedidos chamados `order`.

| **Pedido** | **Opção** | **Recomendação** | **Descrição** |
|---|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) |  |  | A moeda [ISO 4217](https://pt.wikipedia.org/wiki/ISO_4217) para o total do pedido. |
| [payments[paymentItems]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | A lista de pagamentos em uma ordem. Um [paymentItem](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema) inclui o seguinte. |
|  | [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | Opcional | A moeda [ISO 4217](https://pt.wikipedia.org/wiki/ISO_4217) para este método de pagamento. |
|  | [paymentAmount](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | Altamente recomendado | O valor do pagamento no código de moeda especificado. |
|  | [paymentType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | Altamente recomendado | O tipo de pagamento (por exemplo, `credit_card`, `gift_card`, `paypal`). Consulte a lista de valores [](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values) conhecidos para obter detalhes. |
|  | [transactionID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmtransactionid) | Opcional | Uma ID exclusiva para esta transação de pagamento. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpricetotal) |  | Altamente recomendado | O total desse pedido depois que todos os descontos e impostos tiverem sido aplicados. |
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

A lista do produto indica quais produtos estão relacionados à ação correspondente. É uma lista de [productListItems](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md). Cada produto tem vários campos opcionais.

| **Campo** | **Recomendação** | **Descrição** |
|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmcurrencycode) | Opcional | Moeda [ISO 4217](https://pt.wikipedia.org/wiki/ISO_4217) para o produto. Isso só é útil quando você pode ter produtos com códigos monetários diferentes e quando se aplica. Por exemplo, quando há uma compra ou adição ao carrinho. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | Altamente recomendado | Só deve ser definido quando aplicável. Por exemplo, pode não ser possível partir do zero `productView` porque diferentes variações do produto podem ter preços diferentes, mas sim preços `productListAdds`. |
| [produto](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | Altamente recomendado | A ID XDM do produto. |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | Altamente recomendado | O método usado para adicionar um item de produto à lista pelo visitante. Definido com `productListAdds` medidas e deve ser usado somente quando um produto é adicionado à lista. Examples include `add to cart button`, `quick add`, and `upsell`. |
| [productName](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | Altamente recomendado | Isso é definido para o nome de exibição ou para o nome legível por humanos do produto. |
| [quantidade](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | Altamente recomendado | O número de unidades que o cliente indicou que necessitavam do produto. Deve ser definido como `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters`, e assim por diante. |
| [SKU](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md) | Altamente recomendado | Unidade de Manutenção de Loja. É o identificador exclusivo do produto. |

## Exemplos

`productView` evento

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

`productView` evento

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

`checkout` evento

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

`purchase` evento

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
