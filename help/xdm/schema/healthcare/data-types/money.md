---
title: Tipo de dados Money
description: Saiba mais sobre o tipo de dados Money Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 8b910a45-01d5-404b-9710-a2fad9885452
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 18%

---

# Tipo de dados [!UICONTROL Money]

[!UICONTROL Money] é um tipo de dados padrão do Experience Data Model (XDM) que fornece uma quantidade de utilidade econômica em alguma moeda reconhecida. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Estrutura de tipo de dados Money](../../../images/healthcare/data-types/money.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Moeda] | `currency` | String | O código de moeda ISO 4217. |
| [!UICONTROL Valor] | `value` | Duplo | O valor numérico. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/money.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/money.schema.json)
