---
title: Tipo de dados de duração
description: Saiba mais sobre o tipo de dados Duration Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 9%

---

# Tipo de dados [!UICONTROL Duração]

[!UICONTROL Duration] é um tipo de dados padrão do Experience Data Model (XDM) que descreve um período. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Estrutura de tipo de dados de duração](../../images/data-types/healthcare/duration.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Código] | `code` | String | A forma codificada da unidade de tempo. |
| [!UICONTROL Sistema] | `system` | String | O sistema que descreve a unidade codificada, representada como um URI. |
| [!UICONTROL Unidade] | `unit` | String | A unidade de tempo representada em milissegundos, segundos, minutos, horas, dias, semanas, meses ou anos. Os valores dessa propriedade devem ser iguais a um ou mais dos seguintes valores de enumeração conhecidos. <li> `ms` (milissegundos) </li> <li> `s` (segundos) </li> <li> `min` (minutos) </li> <li> `h` (horas) </li>  <li> `d` (dias) </li> <li> `wk` (semanas) </li> <li> `mo` (meses) </li> <li> `a` (anos) </li> |
| [!UICONTROL Valor] | `value` | Duplo | O valor numérico para a unidade de tempo. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/duration.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/duration.schema.json)
