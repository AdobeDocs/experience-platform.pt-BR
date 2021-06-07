---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, campos, esquemas, esquemas, endereço, xdm:endereço, tipo de dados, tipo de dados, tipo de dados;
solution: Experience Platform
title: Tipo de Dados do Item da Lista de Produtos
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados XDM do item da lista de produtos.
source-git-commit: b22dce52563d5f3bbd1796c11d7c7b2a49fa6d5f
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 4%

---

# [!UICONTROL Tipo de dados de ] itens da lista de produtos

[!UICONTROL O item de lista de produtos ] é um tipo de dados XDM padrão que descreve um produto selecionado por um cliente com opções, preços e contexto de uso específicos para um ponto de tempo específico.

Os valores capturados neste tipo de dados podem diferir do registro do produto. Por exemplo, o registro do produto contém detalhes do sistema de informações do produto que são consistentes para todos os clientes, onde o item da lista de produtos tem o preço real oferecido ao cliente no momento da compra, que pode variar devido a campanhas de vendas ou preços sazonais.

![](../images/data-types/product-list-item.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `SKU` | [!UICONTROL String] | Unidade de manutenção de estoque (SKU), o identificador exclusivo de um produto definido pelo fornecedor. |
| `_id` | [!UICONTROL String] | O identificador de item de linha para esta entrada de produto. O próprio produto é identificado por meio de `product`. |
| `currencyCode` | [!UICONTROL String] | O código alfabético de moeda [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) usado para precificar o produto. |
| `name` | [!UICONTROL String] | O nome de exibição do produto, conforme apresentado ao usuário para esta exibição de produto. |
| `priceTotal` | [!UICONTROL Duplo] | O preço total do item de linha do produto. |
| `product` | [!UICONTROL String]  (URI) | O URI `$id` do esquema XDM que captura o próprio produto. |
| `productAddMethod` | [!UICONTROL String] | O método usado para adicionar um item de produto à lista pelo visitante. |
| `quantity` | [!UICONTROL Número inteiro] | O número de unidades que o cliente indicou que necessita do produto. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados de endereço postal, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)
