---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;campos;schemas;Schemas;commerce;datatype;data-type;data type;;home;popular topics;;XDM;fields;details;commerce;datatype;data-type;data type;data type;
solution: Experience Platform
title: Tipo de dados de comércio
topic: overview
description: Este documento fornece uma visão geral do tipo de dados Commerce Experience Data Model (XDM).
translation-type: tm+mt
source-git-commit: 8bbb062df47b6e94630626d0a89a179d759d922d
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 3%

---


# [!UICONTROL Tipo de ] dados de comercialização

[!UICONTROL O ] Commerce é um tipo de dados padrão do Experience Data Model (XDM) que descreve os registros relacionados à atividade de compra e venda.

<img src="../images/data-types/commerce.PNG" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `order` | [[!UICONTROL Pedido]](./order.md) | Descreve o pedido feito para um ou mais produtos. |
| `cartAbandons` | [[!UICONTROL Medição]](./measure.md) | Usado para descrever quando uma lista de produto foi identificada como não acessível ou comprável pelo usuário. |
| `checkouts` | [[!UICONTROL Medição]](./measure.md) | Uma ação durante o processo de finalização de uma lista de produto. Pode haver mais de um evento de finalização se houver várias etapas em um processo de finalização. Se houver várias etapas, as informações de hora do evento e a página ou experiência referenciada serão usadas para identificar a etapa e os eventos individuais representados em ordem. |
| `inStorePurchase` | [[!UICONTROL Medição]](./measure.md) | Descreve um valor associado a uma compra na loja para uso do Analytics. |
| `productListAdds` | [[!UICONTROL Medição]](./measure.md) | A adição de um produto à lista do produto, como um produto adicionado a um carrinho de compras. |
| `productListOpens` | [[!UICONTROL Medição]](./measure.md) | As inicializações de uma nova lista de produto, como um carrinho de compras que está sendo criado. |
| `productListRemovals` | [[!UICONTROL Medição]](./measure.md) | A remoção ou remoção de uma entrada de produto de uma lista de produto, como um produto sendo removido de um carrinho de compras. |
| `productListReopens` | [[!UICONTROL Medição]](./measure.md) | Uma lista de produto que foi abandonada anteriormente e que foi reativada pelo usuário. |
| `productListViews` | [[!UICONTROL Medição]](./measure.md) | Descreve quando uma visualização ou visualizações de uma lista de produto ocorreram. |
| `productViews` | [[!UICONTROL Medição]](./measure.md) | Descreve quando uma visualização ou visualizações de um produto individual ocorreu. |
| `purchases` | [[!UICONTROL Medição]](./measure.md) | Usado para rastrear quando um pedido é aceito. O evento purchase é a única ação necessária em uma conversão de comércio. O evento purchase deve ter uma lista de produto referenciada. |
| `saveForLaters` | [[!UICONTROL Medição]](./measure.md) | Uma lista de produto é salva para uso futuro, como uma lista de desejo. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)