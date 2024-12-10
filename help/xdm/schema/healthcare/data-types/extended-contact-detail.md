---
title: Tipo de Dados Detalhados do Contato Estendido
description: Saiba mais sobre o tipo de dados do Extended Contact Detail Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 4ac9b3d7-acc8-4a82-b34f-ec63a8bf12e0
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 6%

---

# Tipo de dados [!UICONTROL Detalhes do Contato Estendido]

[!UICONTROL Detalhes do Contato Estendido] é um tipo de dados padrão do Experience Data Model (XDM) que descreve as informações de um contato estendido. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Estrutura de tipo de dados Detalhes do Contato Estendido](../../../images/healthcare/data-types/extended-contact-detail.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Endereço] | `address` | [[!UICONTROL Endereço]](../data-types/address.md) | O endereço do contato. |
| [!UICONTROL Nome] | `name` | Matriz de [[!UICONTROL Nome Humano]](../data-types/human-name.md) | O(s) nome(s) da(s) pessoa(s) a contactar. |
| [!UICONTROL Organização] | `organization` | [[!UICONTROL Referência]](../data-types/reference.md) | A organização que manipula/monitora os detalhes de contato. |
| [!UICONTROL Período] | `period` | [[!UICONTROL Período]](../data-types/period.md) | O período em que o contato é ou era válido para uso. |
| [!UICONTROL Propósito] | `purpose` | [[!UICONTROL Conceito codificável]](../data-types/codeable-concept.md) | O tipo de contato. |
| [!UICONTROL Telecom] | `telecom` | Matriz de [[!UICONTROL Ponto de Contato]](../data-types/contact-point.md) | Os detalhes de contato. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/extendedcontactdetail.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/extendedcontactdetail.schema.json)
