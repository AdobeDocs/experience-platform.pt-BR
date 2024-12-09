---
title: Tipo de dados da quantidade
description: Saiba mais sobre o tipo de dados Quantity Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 11%

---

# Tipo de dados [!UICONTROL Quantidade]

[!UICONTROL Quantidade] é um tipo de dados padrão do Experience Data Model (XDM) que fornece uma quantidade medida ou mensurável. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Estrutura de tipo de dados de quantidade](../../images/data-types/healthcare/quantity.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Código] | `code` | String | A forma codificada da unidade. |
| [!UICONTROL Comparador] | `comparator` | String | O operador de comparação. O valor dessa propriedade deve ser igual a um dos seguintes valores de enumeração conhecidos. <li> `<` </li> <li> `<=` </li> <li> `>=` </li> <li> `>`</li> <li> `ad`</li> |
| [!UICONTROL Sistema] | `system` | String | O sistema que define o formulário de unidade codificado, representado como um URI. |
| [!UICONTROL Unidade] | `unit` | String | A representação da unidade. |
| [!UICONTROL Valor] | `value` | Duplo | O valor numérico. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.schema.json)
