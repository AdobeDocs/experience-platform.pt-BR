---
title: Classe do produto
description: Este documento fornece uma visão geral da classe Product no Experience Data Model (XDM).
exl-id: 911680ae-b761-4945-9ad3-0233eaea89b0
source-git-commit: fdd68e5a94d841992a6f8abe10f3cffe0ebb6794
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 10%

---

# [!UICONTROL Produto] classe

No Experience Data Model (XDM), a variável [!UICONTROL Produto] A classe captura o conjunto mínimo de propriedades que definem um produto de varejo.

![](../images/classes/product.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `productListPrice` | [Moeda](../data-types/currency.md) | Descreve o preço padrão do produto antes das vendas e descontos. |
| `_id` | String | Um identificador de sequência de caracteres exclusivo gerado pelo sistema para o registro. Este campo é usado para rastrear a exclusividade de um registro individual, impedir a duplicação de dados e pesquisar esse registro nos serviços downstream.<br><br>Como esse campo é gerado pelo sistema, ele não recebe um valor explícito durante a assimilação de dados. No entanto, você ainda pode optar por fornecer seus próprios valores de ID exclusivos, se desejar. |
| `productDescription` | String | Uma descrição do produto. |
| `productID` | String | Um identificador exclusivo do produto. |
| `productLastModifiedDate` | DateTime | Um [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) carimbo de data e hora de quando este produto foi modificado pela última vez para qualquer atualização. |
| `productManufacturedDate` | DateTime | Um [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) carimbo de data e hora de quando este produto foi criado. |
| `productName` | String | O nome do produto. |
| `productRating` | String | A classificação da revisão do cliente do produto. |

{style="table-layout:auto"}

## Grupos de campos compatíveis {#field-groups}

O Adobe fornece vários grupos de campos padrão para uso com o [!UICONTROL Produto] classe. Veja a seguir uma lista de alguns grupos de campos comumente usados para a classe:

* [[!UICONTROL Catálogo de produtos]](../field-groups/product/product-catalog.md)
* [[!UICONTROL Categoria do produto]](../field-groups/product/product-category.md)
