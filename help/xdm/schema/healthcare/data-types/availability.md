---
title: Tipo de Dados de Disponibilidade
description: Saiba mais sobre o tipo de dados do Availability Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 18c0b767-adf0-480e-9cf2-63e21d05b362
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 9%

---

# Tipo de dados [!UICONTROL Disponibilidade]

[!UICONTROL Disponibilidade] é um tipo de dados padrão do Experience Data Model (XDM) que descreve os dados de disponibilidade de um item. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Estrutura de tipo de dados de disponibilidade](../../../images/healthcare/data-types/availability/availability.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Tempo Disponível] | `availableTime` | Matriz de objetos | As vezes que o item está disponível. Consulte a [seção abaixo](#available-time) para obter mais informações. |
| [!UICONTROL Tempo Indisponível] | `notAvailableTime` | String | As vezes em que o item não está disponível, com um motivo fornecido. Consulte a [seção abaixo](#not-available-time) para obter mais informações. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/availability.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/availability.schema.json)

## `availableTime` {#available-time}

`availableTime` é fornecido como uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![Estrutura de tempo disponível](../../../images/healthcare/data-types/availability/available-time.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL O Dia Inteiro] | `allDay` | Booleano | Um booleano que indica se o item está sempre disponível. |
| [!UICONTROL Hora de Término Disponível] | `availableEndTime` | String | A hora do dia em que o item deixa de estar disponível. Isso será ignorado se `allDay` for `true`. |
| [!UICONTROL Hora de Início Disponível] | `availableStartTime` | String | A hora do dia em que o item começa a estar disponível. Isso será ignorado se `allDay` for `true`. |
| [!UICONTROL Dias Da Semana] | `daysOfWeek` | Matriz de cadeias de caracteres | Uma matriz de strings detalhando quais dias estão disponíveis. Os valores dessa propriedade devem ser iguais a um ou mais dos seguintes valores de enumeração conhecidos. <li> `mon` </li> <li> `tues` </li> <li> `wed` </li> <li> `thurs`</li>  <li> `fri` </li> <li> `sat`</li> <li> `sun`</li> |

## `notAvailableTime` {#not-available-time}

`notAvailableTime` é fornecido como uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![Estrutura de tempo indisponível](../../../images/healthcare/data-types/availability/not-available-time.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Durante] | `during` | [[!UICONTROL Período]](../data-types/period.md) | O período em que o item deixa de estar disponível. |
| [!UICONTROL Descrição] | `description` | String | O motivo pelo qual o item não está disponível. |
