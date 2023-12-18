---
keywords: Experience Platform;início;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;comércio;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de dados do Commerce
description: Saiba mais sobre o tipo de dados do Commerce Experience Data Model (XDM).
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
source-git-commit: f70ca0d8ab0e92cc0e1007021c0778361701dc84
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 2%

---

# [!UICONTROL Commerce] tipo de dados

[!UICONTROL Commerce] é um tipo de dados padrão do Experience Data Model (XDM) que descreve os registros relacionados à compra e venda.

![Um diagrama do [!UICONTROL Commerce] tipo de dados.](../images/data-types/commerce.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|------------------------------------------|-----------------------|------------------------------------|----------------------------------------------------------------------------------------------------------|
| [!UICONTROL Pedido] | `order` | [[!UICONTROL Pedido]](./order.md) | Descreve o pedido feito de um ou mais produtos. |
| [!UICONTROL ID da promoção] | `promotionID` | [!UICONTROL string] | Um identificador de promoção para a ordem feita, se existir. |
| [!UICONTROL Abandonos do carrinho] | `cartAbandons` | [[!UICONTROL Medir]](./measure.md) | Descreve quando uma lista de produtos foi identificada como não acessível ou comprada pelo usuário. |
| [!UICONTROL Check-outs] | `checkouts` | [[!UICONTROL Medir]](./measure.md) | Uma ação durante o processo de check-out de uma lista de produtos. Pode haver mais de um evento de check-out se houver várias etapas em um processo de check-out. Se houver várias etapas, as informações de tempo do evento e a página ou experiência referenciada serão usadas para identificar a etapa e os eventos individuais representados em ordem. |
| [!UICONTROL Adições à lista de produtos (carrinho)] | `productListAdds` | [[!UICONTROL Medir]](./measure.md) | A adição de um produto à lista de produtos, como um produto sendo adicionado a um carrinho de compras. |
| [!UICONTROL Aberturas de lista de produtos (carrinho)] | `productListOpens` | [[!UICONTROL Medir]](./measure.md) | As inicializações de uma nova lista de produtos, como um carrinho de compras que está sendo criado. |
| [!UICONTROL Remoções da lista de produtos (carrinho)] | `productListRemovals` | [[!UICONTROL Medir]](./measure.md) | A remoção ou as remoções de uma entrada de produto de uma lista de produtos, como um produto que está sendo removido de um carrinho de compras. |
| [!UICONTROL Reaberturas de lista de produtos (carrinho)] | `productListReopens` | [[!UICONTROL Medir]](./measure.md) | Uma lista de produtos que foi abandonada anteriormente e que foi reativada pelo usuário. |
| [!UICONTROL Visualizações da lista de produtos (carrinho)] | `productListViews` | [[!UICONTROL Medir]](./measure.md) | Descreve quando uma ou mais exibições de uma lista de produtos ocorreram. A exibição ou as exibições de uma lista de produtos ocorreram. |
| [!UICONTROL Visualizações do produto] | `productViews` | [[!UICONTROL Medir]](./measure.md) | Descreve quando uma ou mais exibições de um produto individual ocorreram. |
| [!UICONTROL Compras] | `purchases` | [[!UICONTROL Medir]](./measure.md) | Usado para rastrear quando um pedido foi aceito. O evento de compra é a única ação necessária em uma conversão de comércio. O evento de compra deve ter uma lista de produtos referenciada. |
| [!UICONTROL Salvar para mais tarde] | `saveForLaters` | [[!UICONTROL Medir]](./measure.md) | Descreve quando uma lista de produtos é salva para uso futuro, como uma lista de desejos. |
| [!UICONTROL Compra na loja] | `inStorePurchase` | [[!UICONTROL Medir]](./measure.md) | Indica uma compra &quot;inStore&quot;. Essas informações são salvas para uso de análise. |
| [!UICONTROL Carrinho] | `cart` | [[!UICONTROL carrinho]](./cart.md) | As propriedades do carrinho que contém um ou mais produtos. |
| [!UICONTROL Envio] | `shipping` | [[!UICONTROL envio]](./shipping.md) | Os detalhes de remessa de um ou mais produtos. |
| [!UICONTROL Faturamento] | `billing` | [[!UICONTROL faturamento]](#billing) | Os detalhes de faturamento de um ou mais pagamentos. |
| [!UICONTROL Compra instantânea] | `instantPurchase` | [[!UICONTROL Medir]](./measure.md) | Descreve quando um produto foi comprado instantaneamente, possivelmente ignorando o carrinho ou o checkout. |
| [!UICONTROL Aberturas de Lista de Requisições] | `requisitionListOpens` | [[!UICONTROL Medir]](./measure.md) | Indica a inicialização de uma nova lista de requisições. |
| [!UICONTROL Exclusões da Lista de Requisições] | `requisitionListDeletes` | [[!UICONTROL Medir]](./measure.md) | Indica a remoção da lista de requisições. |
| [!UICONTROL Adições à Lista de Requisições] | `requisitionListAdds` | [[!UICONTROL Medir]](./measure.md) | Indica a adição de um ou mais produtos a uma lista de requisições. |
| [!UICONTROL Remoções da Lista de Requisições] | `requisitionListRemovals` | [[!UICONTROL Medir]](./measure.md) | Indica a remoção de um ou mais produtos de uma lista de produtos de requisição. |
| [!UICONTROL Lista de requisições] | `requisitionList` | [[!UICONTROL requisitionlist]](./requisition-list.md) | As propriedades da lista de requisições criadas pelo cliente. |
| [!UICONTROL Escopo] | `commerceScope` | [[!UICONTROL commerce escope]](./commerce-scope.md) | Os identificadores de escopo de comércio de onde um evento ocorreu (exibição de loja, loja, site etc.). |

{style="table-layout:auto"}

## [!UICONTROL faturamento] tipo de dados {#billing}

[!UICONTROL faturamento] é um tipo de dados padrão do Experience Data Model (XDM) que contém informações sobre detalhes de faturamento. Especificamente, ele se concentra no endereço de faturamento.

![Um diagrama do tipo de dados de faturamento.](../images/data-types/billing.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|-------------------------------|-----------------|-----------------|--------------------------|
| [!UICONTROL Endereço de cobrança] | `address` | [[!UICONTROL Endereço postal]](./postal-address.md) | O endereço de cobrança. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o [!UICONTROL Commerce] tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
