---
title: Tipo de dados de tempo
description: Saiba mais sobre o tipo de dados Timing Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e1bc16ed-4dd8-4316-b3c8-88d49d393859
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 8%

---

# [!UICONTROL Tempo] tipo de dados

[!UICONTROL Tempo] é um tipo de dados padrão do Experience Data Model (XDM) que descreve um cronograma de tempo que fornece informações sobre um evento que pode ocorrer várias vezes. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Estrutura de tipo de dados de tempo](../../../images/healthcare/data-types/timing.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Evento] | `event` | Matriz de DateTime | Quando o evento ocorre. |
| [!UICONTROL Repetir] | `repeat` | [[!UICONTROL Repetir]](../data-types/repeat.md) | Informações sobre quando o evento ocorre. |
| [!UICONTROL Código] | `code` | [[!UICONTROL Conceito codificável]](../data-types/codeable-concept.md) | O código relacionado ao evento. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.schema.json)
