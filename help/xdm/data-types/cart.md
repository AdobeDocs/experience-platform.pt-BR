---
title: Tipo de dados do carrinho
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência do carrinho (XDM).
exl-id: 24ae3882-60f3-4962-b0b5-7dba48170da8
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 14%

---

# Tipo de dados [!UICONTROL Carrinho]

[!UICONTROL Carrinho] é um tipo de dados padrão do Experience Data Model (XDM) que fornece propriedades relacionadas a um carrinho de compras. Use este tipo de dados para capturar o identificador exclusivo atribuído pelo vendedor (`Cart ID`) e a origem (`Cart Source`) em que um ou mais produtos foram adicionados ao carrinho.

![Um diagrama do tipo de dados [!UICONTROL Carrinho].](../images/data-types/cart.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|----------------|-------------------|-----------|------------------------------------------------------------|
| [!UICONTROL ID do carrinho] | `cartID` | sequência de caracteres | Identificador exclusivo atribuído pelo vendedor ao carrinho. |
| [!UICONTROL Source do carrinho] | `cartSource` | sequência de caracteres | De onde um ou mais produtos foram adicionados ao carrinho. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json)
