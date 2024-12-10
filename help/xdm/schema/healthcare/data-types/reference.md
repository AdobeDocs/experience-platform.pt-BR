---
title: Tipo de dados de referência
description: Saiba mais sobre o tipo de dados Referência do Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: eb724dbb-2918-43b5-8e50-c8aabfe6e96c
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 10%

---

# Tipo de dados [!UICONTROL Referência]

[!UICONTROL Referência] é um tipo de dados padrão do Experience Data Model (XDM) que fornece uma referência de um recurso para outro. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Referenciar estrutura de tipo de dados](../../../images/healthcare/data-types/reference.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Identificador] | `identifier` | [[!UICONTROL Identificador]](../data-types/identifier.md) | A referência lógica quando a referência literal não é conhecida. |
| [!UICONTROL Exibir] | `display` | String | A alternativa em texto para a referência. |
| [!UICONTROL Referência] | `reference` | String | A referência literal, relativa, interna ou URL absoluto. |
| [!UICONTROL Tipo] | `type` | String | O tipo ao qual a referência se refere, representado como um URI. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.schema.json)
