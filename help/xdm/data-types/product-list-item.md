---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;endereço;xdm:endereço;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de Dados do Item de Lista de Produtos
description: Saiba mais sobre o tipo de dados XDM do item de lista de produtos.
exl-id: 056fdb5b-6782-4e29-9d62-90b270c05795
source-git-commit: ba6c6eb2c6b0fc1dfc4e7440fd16a85bc7b46457
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 20%

---

# Tipo de dados [!UICONTROL Item de lista de produtos]

[!UICONTROL O item da lista de produtos] é um tipo de dados XDM padrão que descreve um produto selecionado por um cliente com opções, preços e contexto de uso específicos para um determinado momento.

Os valores capturados nesse tipo de dados podem diferir do registro do produto. Por exemplo, o registro do produto contém detalhes do sistema de informações do produto que são consistentes para todos os clientes, onde o item da lista de produtos tem o preço real oferecido ao cliente no momento da compra, que pode variar devido a campanhas de vendas ou preços sazonais.

![](../images/data-types/product-list-item.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `selectedOptions` | Matriz de objetos | Contém opções personalizadas escolhidas para um produto configurável. Cada item da lista é um objeto com as seguintes propriedades:<ul><li>`attribute`: Um nome para o atributo configurável.</li><li>`value`: O valor do atributo.</li></ul> |
| `SKU` | [!UICONTROL String] | Unidade de manutenção de estoque (SKU), o identificador exclusivo de um produto definido pelo fornecedor. |
| `_id` | [!UICONTROL String] | O identificador de item de linha para esta entrada de produto. O produto em si é identificado através de `product`. |
| `currencyCode` | [!UICONTROL String] | O código alfabético de moeda [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) usado para definir o preço do produto. |
| `discountAmount` | [!UICONTROL Duplo] | Se o produto for descontado, isso representa a diferença entre o preço normal e o preço especial do produto. |
| `name` | [!UICONTROL String] | O nome de exibição do produto conforme apresentado ao usuário para esta visualização do produto. |
| `priceTotal` | [!UICONTROL Duplo] | O preço total do item de linha do produto. |
| `product` | [!UICONTROL Cadeia de caracteres] (URI) | O identificador XDM do próprio produto. |
| `productAddMethod` | [!UICONTROL String] | O método usado para adicionar um item de produto à lista pelo visitante. |
| `productImageUrl` | [!UICONTROL String] | Um URL para a imagem principal do produto. |
| `quantity` | [!UICONTROL Inteiro] | O número de unidades que o cliente indicou que precisa do produto. |
| `unitOfMeasureCode` | [!UICONTROL String] | O [código de unidade de medida](https://ucum.org/ucum) padrão do produto relacionado à propriedade `quantity`. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados do endereço postal, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)
