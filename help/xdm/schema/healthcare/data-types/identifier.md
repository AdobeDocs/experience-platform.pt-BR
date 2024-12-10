---
title: Tipo de dados do identificador
description: Saiba mais sobre o tipo de dados Identifier Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 0664f52d-bea6-4aa1-b2a5-de0bd6d5edd9
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 9%

---

# Tipo de dados [!UICONTROL Identificador]

[!UICONTROL Identificador] é um tipo de dados padrão do Experience Data Model (XDM) que fornece um identificador destinado à computação. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Estrutura de tipo de dados de identificador](../../../images/healthcare/data-types/identifier.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Período] | `period` | [[!UICONTROL Período]](../data-types/period.md) | O período em que a ID é ou era válida para uso. |
| [!UICONTROL Tipo] | `type` | [[!UICONTROL Conceito codificável]](../data-types/codeable-concept.md) | A descrição do identificador. |
| [!UICONTROL Atribuidor] | `assigner` | String | A organização que emitiu a ID. |
| [!UICONTROL Sistema] | `system` | String | O namespace do valor do identificador, representado como um URI. |
| [!UICONTROL Uso] | `use` | String | O uso do identificador. Os valores dessa propriedade devem ser iguais a um ou mais dos seguintes valores de enumeração conhecidos. <li> `usual` </li> <li> `offical` </li> <li> `temp` </li> <li> `secondary` </li> <li> `old` </li> |
| [!UICONTROL Valor] | `value` | String | O valor exclusivo da ID. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.schema.json)
