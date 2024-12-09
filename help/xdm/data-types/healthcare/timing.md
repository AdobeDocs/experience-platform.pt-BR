---
title: Tipo de dados de tempo
description: Saiba mais sobre o tipo de dados Timing Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 0640d0c2daab67ad7a77d3265ccae45851ba45b8
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 8%

---

# [!UICONTROL Tempo] tipo de dados

[!UICONTROL Tempo] é um tipo de dados padrão do Experience Data Model (XDM) que descreve um cronograma de tempo que fornece informações sobre um evento que pode ocorrer várias vezes. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Estrutura de tipo de dados de tempo](../../images/data-types/healthcare/timing.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Evento] | `event` | Matriz de DateTime | Quando o evento ocorre. |
| [!UICONTROL Repetir] | `repeat` | [[!UICONTROL Repetir]](../healthcare/repeat.md) | Informações sobre quando o evento ocorre. |
| [!UICONTROL Código] | `code` | [[!UICONTROL Conceito codificável]](../healthcare/codeable-concept.md) | O código relacionado ao evento. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.schema.json)
