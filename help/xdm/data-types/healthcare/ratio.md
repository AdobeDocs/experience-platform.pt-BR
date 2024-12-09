---
title: Tipo de Dados de Proporção
description: Saiba mais sobre o tipo de dados Ratio Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7d33c5474629b2b02c19e752cdf2cb0a2ba19f19
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 6%

---

# [!UICONTROL Taxa] tipo de dados

[!UICONTROL Ratio] é um tipo de dados padrão do Experience Data Model (XDM) que fornece uma proporção de dois valores [[!UICONTROL Quantidade]](../healthcare/quantity.md) por meio de um numerador e um denominador. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Estrutura de tipo de dados de taxa](../../images/data-types/healthcare/ratio.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Denominador] | `denominator` | [[!UICONTROL Quantidade Simples]](../healthcare/simple-quantity.md) | O valor do denominador. |
| [!UICONTROL Numerador] | `numerator` | [[!UICONTROL Quantidade]](../healthcare/quantity.md) | O valor do numerador. |

>[!NOTE]
>
> O `denominator` e o `numerator` têm tipos de dados diferentes devido à especificação criada de acordo com o HL7 FHIR Versão 5.

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.schema.json)
