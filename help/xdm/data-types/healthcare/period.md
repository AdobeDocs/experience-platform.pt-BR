---
title: Tipo de Dados do Período
description: Saiba mais sobre o tipo de dados Period Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 12%

---

# Tipo de dados [!UICONTROL Período]

[!UICONTROL Período] é um tipo de dados padrão do Experience Data Model (XDM) que fornece um período definido por uma data/hora de início e término. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Estrutura de tipo de dados de período](../../images/data-types/healthcare/period.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL End] | `end` | DateTime | A data e a hora de término. |
| [!UICONTROL Start] | `start` | DateTime | A data e a hora de início. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.schema.json)
