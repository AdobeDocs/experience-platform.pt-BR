---
title: Tipo de Dados de Ponto de Contato
description: Saiba mais sobre o tipo de dados do Modelo de dados de experiência (XDM) do ponto de contato.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 7%

---

# Tipo de dados [!UICONTROL Ponto de Contato]

[!UICONTROL Ponto de Contato] é um tipo de dados padrão do Experience Data Model (XDM) que descreve os detalhes de contato de uma pessoa. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Estrutura de tipo de dados do Ponto de Contato](../../images/data-types/healthcare/contact-point.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Período] | `period` | [[!UICONTROL Período]](../healthcare/period.md) | O período em que o ponto de contato estava/está em uso. |
| [!UICONTROL Classificação] | `rank` | Número inteiro | A classificação que indica o uso preferencial do ponto de contato. O valor mínimo é `1` e o valor máximo é `2147483647`, onde `1` é a especificidade mais alta. |
| [!UICONTROL Sistema] | `system` | String | O sistema pelo qual eles podem ser contatados. O valor dessa propriedade deve ser igual a um dos seguintes valores de enumeração conhecidos. <li> `phone` </li> <li> `fax` </li> <li> `email` </li> <li> `pager`</li> <li> `url`</li> <li> `sms`</li> <li> `other`</li> |
| [!UICONTROL Uso] | `use` | String | A finalidade do ponto de contato. O valor dessa propriedade deve ser igual a um dos seguintes valores de enumeração conhecidos. <li> `home` </li> <li> `work` </li> <li> `temp` </li> <li> `old`</li> <li> `mobile`</li> |
| [!UICONTROL Valor] | `value` | String | Os detalhes do ponto de contato. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/contactpoint.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/contactpoint.schema.json)
