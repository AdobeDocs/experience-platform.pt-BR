---
keywords: Experience Platform;início;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;comércio;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de dados do Commerce
description: Este documento fornece uma visão geral do tipo de dados do Commerce Experience Data Model (XDM).
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 3%

---

# [!UICONTROL Commerce] tipo de dados

[!UICONTROL Commerce] é um tipo de dados padrão do Experience Data Model (XDM) que descreve os registros relacionados à atividade de compra e venda.

<img src="../images/data-types/commerce.PNG" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `order` | [[!UICONTROL Pedido]](./order.md) | Descreve o pedido feito de um ou mais produtos. |
| `cartAbandons` | [[!UICONTROL Medição]](./measure.md) | Usado para descrever quando uma lista de produtos foi identificada como não acessível ou comprada pelo usuário. |
| `checkouts` | [[!UICONTROL Medição]](./measure.md) | Uma ação durante o processo de check-out de uma lista de produtos. Pode haver mais de um evento de check-out se houver várias etapas em um processo de check-out. Se houver várias etapas, as informações de tempo do evento e a página ou experiência referenciada serão usadas para identificar a etapa e os eventos individuais representados em ordem. |
| `inStorePurchase` | [[!UICONTROL Medição]](./measure.md) | Descreve um valor associado a uma compra na loja para uso de análise. |
| `productListAdds` | [[!UICONTROL Medição]](./measure.md) | A adição de um produto à lista de produtos, como um produto sendo adicionado a um carrinho de compras. |
| `productListOpens` | [[!UICONTROL Medição]](./measure.md) | As inicializações de uma nova lista de produtos, como um carrinho de compras que está sendo criado. |
| `productListRemovals` | [[!UICONTROL Medição]](./measure.md) | A remoção ou as remoções de uma entrada de produto de uma lista de produtos, como um produto que está sendo removido de um carrinho de compras. |
| `productListReopens` | [[!UICONTROL Medição]](./measure.md) | Uma lista de produtos que foi abandonada anteriormente e que foi reativada pelo usuário. |
| `productListViews` | [[!UICONTROL Medição]](./measure.md) | Descreve quando uma ou mais exibições de uma lista de produtos ocorreram. |
| `productViews` | [[!UICONTROL Medição]](./measure.md) | Descreve quando uma ou mais exibições de um produto individual ocorreram. |
| `purchases` | [[!UICONTROL Medição]](./measure.md) | Usado para rastrear quando um pedido foi aceito. O evento de compra é a única ação necessária em uma conversão de comércio. O evento de compra deve ter uma lista de produtos referenciada. |
| `saveForLaters` | [[!UICONTROL Medição]](./measure.md) | Uma lista de produtos é salva para uso futuro, como uma lista de desejos. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
