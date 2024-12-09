---
title: Tipo de dados de referência codificável
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência de referência codificável (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 7%

---

# Tipo de dados [!UICONTROL Referência codificável]

[!UICONTROL Referência codificável] é um tipo de dados padrão do Experience Data Model (XDM) que descreve uma referência a um recurso ou conceito. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Estrutura de tipo de dados de Referência Codificável](../../images/data-types/healthcare/codeable-reference.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Conceito] | `concept` | [[!UICONTROL Conceito codificável]](../healthcare/codeable-concept.md) | Uma referência a um conceito (por classe). |
| [!UICONTROL Referência] | `reference` | [[!UICONTROL Referência]](../healthcare/reference.md) | Uma referência a um recurso. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.schema.json)
