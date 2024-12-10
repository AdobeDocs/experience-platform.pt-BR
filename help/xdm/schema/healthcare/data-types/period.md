---
title: Tipo de Dados do Período
description: Saiba mais sobre o tipo de dados Period Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: aecd09e4-2797-4d2d-be62-acad28fb7bba
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 12%

---

# Tipo de dados [!UICONTROL Período]

[!UICONTROL Período] é um tipo de dados padrão do Experience Data Model (XDM) que fornece um período definido por uma data/hora de início e término. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Estrutura de tipo de dados de período](../../../images/healthcare/data-types/period.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL End] | `end` | DateTime | A data e a hora de término. |
| [!UICONTROL Start] | `start` | DateTime | A data e a hora de início. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.schema.json)
