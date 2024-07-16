---
title: Tipo de dados de escopo do Commerce
description: Saiba mais sobre o tipo de dados do Commerce Scope Experience Data Model (XDM).
exl-id: c2888c3a-a49c-43c4-8d36-0a485cb76a58
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 8%

---

# Tipo de dados [!UICONTROL Escopo do Commerce]

O [!UICONTROL Escopo do Commerce] é um tipo de dados padrão do Experience Data Model (XDM) que define identificadores para onde um evento ocorreu em um ecossistema de comércio. Ele distingue ambientes, sites, lojas e visualizações de loja.

![Um diagrama do tipo de dados Escopo do Commerce.](../images/data-types/commerce-scope.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|---------------------------------|-------------------|-----------|-------------------------------------------------------|
| [!UICONTROL ID do ambiente] | `environmentID` | sequência de caracteres | A ID do ambiente. Uma ID alfanumérica de 32 dígitos. |
| [!UICONTROL Código do Site] | `websiteCode` | sequência de caracteres | O código exclusivo do site em um ambiente. |
| [!UICONTROL Armazenar código] | `storeCode` | sequência de caracteres | O código de armazenamento exclusivo em um site. |
| [!UICONTROL Código de Exibição da Loja] | `storeViewCode` | sequência de caracteres | O código de exibição de loja exclusivo em uma loja. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.schema.json)
