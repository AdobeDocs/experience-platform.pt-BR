---
title: Tipo de dados do carrinho
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência do carrinho (XDM).
source-git-commit: c3590dc2cfe47eb634136eeb88578f965598760d
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 5%

---

# [!UICONTROL Carrinho] tipo de dados

[!UICONTROL Carrinho] é um tipo de dados padrão do Experience Data Model (XDM) que fornece propriedades relacionadas a um carrinho de compras. Use este tipo de dados para registrar o identificador exclusivo atribuído pelo vendedor (`Cart ID`) e a origem (`Cart Source`) em que um ou mais produtos foram adicionados ao carrinho.

![Um diagrama do [!UICONTROL Carrinho] tipo de dados.](../images/data-types/cart.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|----------------|-------------------|-----------|------------------------------------------------------------|
| [!UICONTROL ID do carrinho] | `cartID` | string | Identificador exclusivo atribuído pelo vendedor ao carrinho. |
| [!UICONTROL Origem do carrinho] | `cartSource` | string | De onde um ou mais produtos foram adicionados ao carrinho. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json)
