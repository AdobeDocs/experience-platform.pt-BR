---
title: Tipo de Dados Detalhados do Contato Estendido
description: Saiba mais sobre o tipo de dados do Extended Contact Detail Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 6%

---

# Tipo de dados [!UICONTROL Detalhes do Contato Estendido]

[!UICONTROL Detalhes do Contato Estendido] é um tipo de dados padrão do Experience Data Model (XDM) que descreve as informações de um contato estendido. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Estrutura de tipo de dados Detalhes do Contato Estendido](../../images/data-types/healthcare/extended-contact-detail.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Endereço] | `address` | [[!UICONTROL Endereço]](../healthcare/address.md) | O endereço do contato. |
| [!UICONTROL Nome] | `name` | Matriz de [[!UICONTROL Nome Humano]](../healthcare/human-name.md) | O(s) nome(s) da(s) pessoa(s) a contactar. |
| [!UICONTROL Organização] | `organization` | [[!UICONTROL Referência]](../healthcare/reference.md) | A organização que manipula/monitora os detalhes de contato. |
| [!UICONTROL Período] | `period` | [[!UICONTROL Período]](../healthcare/period.md) | O período em que o contato é ou era válido para uso. |
| [!UICONTROL Propósito] | `purpose` | [[!UICONTROL Conceito codificável]](../healthcare/codeable-concept.md) | O tipo de contato. |
| [!UICONTROL Telecom] | `telecom` | Matriz de [[!UICONTROL Ponto de Contato]](../healthcare/contact-point.md) | Os detalhes de contato. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/extendedcontactdetail.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/extendedcontactdetail.schema.json)
