---
title: Tipo de dados de referência
description: Saiba mais sobre o tipo de dados Referência do Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 10%

---

# Tipo de dados [!UICONTROL Referência]

[!UICONTROL Referência] é um tipo de dados padrão do Experience Data Model (XDM) que fornece uma referência de um recurso para outro. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Referenciar estrutura de tipo de dados](../../images/data-types/healthcare/reference.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Identificador] | `identifier` | [[!UICONTROL Identificador]](../healthcare/identifier.md) | A referência lógica quando a referência literal não é conhecida. |
| [!UICONTROL Exibir] | `display` | String | A alternativa em texto para a referência. |
| [!UICONTROL Referência] | `reference` | String | A referência literal, relativa, interna ou URL absoluto. |
| [!UICONTROL Tipo] | `type` | String | O tipo ao qual a referência se refere, representado como um URI. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.schema.json)
