---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, campos, esquemas, esquemas, endereço, xdm:endereço, tipo de dados, tipo de dados, tipo de dados;
solution: Experience Platform
title: Tipo de Dados do Item da Lista de Produtos
description: Este documento fornece uma visão geral do tipo de dados XDM do item da lista de produtos.
exl-id: 056fdb5b-6782-4e29-9d62-90b270c05795
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 4%

---

# [!UICONTROL Item da lista de produtos] tipo de dados

[!UICONTROL Item da lista de produtos] é um tipo de dados XDM padrão que descreve um produto selecionado por um cliente com opções, preços e contexto de uso específicos para um ponto de tempo específico.

Os valores capturados neste tipo de dados podem diferir do registro do produto. Por exemplo, o registro do produto contém detalhes do sistema de informações do produto que são consistentes para todos os clientes, onde o item da lista de produtos tem o preço real oferecido ao cliente no momento da compra, que pode variar devido a campanhas de vendas ou preços sazonais.

![](../images/data-types/product-list-item.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `selectedOptions` | Matriz de objetos | Contém opções personalizadas escolhidas para um produto configurável. Cada item de lista é um objeto com as seguintes propriedades:<ul><li>`attribute`: Um nome para o atributo configurável.</li><li>`value`: O valor do atributo.</li></ul> |
| `SKU` | [!UICONTROL String] | Unidade de manutenção de estoque (SKU), o identificador exclusivo de um produto definido pelo fornecedor. |
| `_id` | [!UICONTROL String] | O identificador de item de linha para esta entrada de produto. O próprio produto é identificado por meio de `product`. |
| `currencyCode` | [!UICONTROL String] | O [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) código alfabético de moeda usado para precificar o produto. |
| `discountAmount` | [!UICONTROL Duplo] | Se o produto for atualizado, isso representa a diferença entre o preço normal e o preço especial do produto. |
| `name` | [!UICONTROL String] | O nome de exibição do produto, conforme apresentado ao usuário para esta exibição de produto. |
| `priceTotal` | [!UICONTROL Duplo] | O preço total do item de linha do produto. |
| `product` | [!UICONTROL String] (URI) | O URI `$id` do esquema XDM que captura o próprio produto. |
| `productAddMethod` | [!UICONTROL String] | O método usado para adicionar um item de produto à lista pelo visitante. |
| `productImageUrl` | [!UICONTROL String] | Um URL para a imagem principal do produto. |
| `quantity` | [!UICONTROL Número inteiro] | O número de unidades que o cliente indicou que necessita do produto. |
| `unitOfMeasureCode` | [!UICONTROL String] | O padrão [código da unidade de medida](https://ucum.org/ucum) para o produto relacionado com a `quantity` propriedade. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados de endereço postal, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)
