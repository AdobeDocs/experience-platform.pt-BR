---
title: Classe do produto
description: Saiba mais sobre a classe de produto no Experience Data Model (XDM).
exl-id: 911680ae-b761-4945-9ad3-0233eaea89b0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 8%

---

# Classe [!UICONTROL Produto]

No Experience Data Model (XDM), a classe [!UICONTROL Product] captura o conjunto mínimo de propriedades que definem um produto de varejo.

![](../images/classes/product.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `productListPrice` | [Moeda](../data-types/currency.md) | Descreve o preço padrão do produto antes das vendas e descontos. |
| `_id` | String | Um identificador de sequência de caracteres exclusivo gerado pelo sistema para o registro. Este campo é usado para rastrear a exclusividade de um registro individual, impedir a duplicação de dados e pesquisar esse registro nos serviços downstream.<br><br>Como este campo é gerado pelo sistema, ele não receberá um valor explícito durante a assimilação de dados. No entanto, você ainda pode optar por fornecer seus próprios valores de ID exclusivos, se desejar. |
| `productDescription` | String | Uma descrição do produto. |
| `productID` | String | Um identificador exclusivo do produto. |
| `productLastModifiedDate` | DateTime | Um carimbo de data/hora [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) de quando este produto foi modificado pela última vez para qualquer atualização. |
| `productManufacturedDate` | DateTime | Um carimbo de data/hora [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) de quando este produto foi criado. |
| `productName` | String | O nome do produto. |
| `productRating` | String | A classificação da revisão do cliente do produto. |

{style="table-layout:auto"}

## Grupos de campos compatíveis {#field-groups}

O Adobe fornece vários grupos de campos padrão para uso com a classe [!UICONTROL Product]. Veja a seguir uma lista de alguns grupos de campos comumente usados para a classe:

* [[!UICONTROL Catálogo de produtos]](../field-groups/product/product-catalog.md)
* [[!UICONTROL Categoria do produto]](../field-groups/product/product-category.md)
