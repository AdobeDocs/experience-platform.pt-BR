---
title: Repetir tipo de dados
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência de repetição (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 9d40bc1d-33d1-4c33-a143-13fdcf8dc255
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 6%

---

# [!UICONTROL Repetir] tipo de dados

[!UICONTROL Repetir] é um tipo de dados padrão do Experience Data Model (XDM) que fornece um conjunto de regras que descrevem quando um evento é agendado. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Repetir estrutura de tipo de dados](../../../images/healthcare/data-types/reference.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Período Associado] | `boundsPeriod` | [[!UICONTROL Período]](../data-types/period.md) | As horas de início e término. |
| [!UICONTROL Intervalo Associado] | `boundsRange` | [[!UICONTROL Intervalo]](../data-types/range.md) | O limite do intervalo. |
| [!UICONTROL Duração Associada] | `boundsDuration` | [[!UICONTROL Duração]](../data-types/duration.md) | O limite de duração. |
| [!UICONTROL Contagem] | `count` | Número inteiro | O número de vezes para repetir, com um valor mínimo de `0`. |
| [!UICONTROL Contagem Máxima] | `countMax` | Número inteiro | O número máximo de vezes para repetir, com um valor mínimo de `0`. |
| [!UICONTROL Dia Da Semana] | `dayOfWeek` | Matriz de cadeias de caracteres | Uma matriz de strings detalhando quais dias estão disponíveis. Os valores dessa propriedade devem ser iguais a um ou mais dos seguintes valores de enumeração conhecidos. <li> `mon` </li> <li> `tues` </li> <li> `wed` </li> <li> `thurs`</li>  <li> `fri` </li> <li> `sat`</li> <li> `sun`</li> |
| [!UICONTROL Duração] | `duration` | Duplo | A duração. |
| [!UICONTROL Duração Máxima] | `durationMax` | Duplo | O período máximo. |
| [!UICONTROL Unidade de Duração] | `durationUnit` | String | A unidade de duração. Os valores dessa propriedade devem ser iguais a um ou mais dos seguintes valores de enumeração conhecidos. <li> `s` (segundos) </li> <li> `min` (minutos) </li> <li> `h` (por hora) </li> <li> `d` (diariamente) </li>  <li> `wk` (semanalmente) </li> <li> `mo` (mensalmente) </li> <li> `a` (anual)</li> |
| [!UICONTROL Frequência] | `frequency` | Duplo | O número de repetições que devem ocorrer em um período, com um valor mínimo de `0`. |
| [!UICONTROL Frequência Máxima] | `frequencyMax` | Duplo | O número máximo de repetições que devem ocorrer com um ponto, com um valor mínimo de `0`. |
| [!UICONTROL Deslocamento] | `offset` | Número inteiro | O(s) minuto(s) até o evento (antes ou depois). |
| [!UICONTROL Período] | `period` | Duplo | A duração durante a qual a frequência se aplica. |
| [!UICONTROL Período Máximo] | `periodMax` | Duplo | O limite superior do período. |
| [!UICONTROL Unidade do Período] | `periodUnit` | String | A unidade de tempo. Os valores dessa propriedade devem ser iguais a um ou mais dos seguintes valores de enumeração conhecidos. <li> `s` (segundos) </li> <li> `min` (minutos) </li> <li> `h` (por hora) </li> <li> `d` (diariamente) </li>  <li> `wk` (semanalmente) </li> <li> `mo` (mensalmente) </li> <li> `a` (anual)</li> |
| [!UICONTROL Horário Do Dia] | `timeOfDay` | Matriz de cadeias de caracteres | A hora do dia em que a ação ocorrerá. |
| [!UICONTROL When] | `when` | Matriz de cadeias de caracteres | O código do período de tempo da ação. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/repeat.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/repeat.schema.json)
