---
title: Tipo de dados de conceito codificável
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência de conceito codificável (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 9%

---

# Tipo de dados [!UICONTROL Conceito codificável]

[!UICONTROL Conceito Codificável] é um tipo de dados padrão do Experience Data Model (XDM) que descreve uma referência de um recurso a outro. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Estrutura de tipo de dados de conceito codificável](../../images/data-types/healthcare/codeable-concept.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Codificação] | `coding` | Matriz de [[!UICONTROL Codificação]](../healthcare/coding.md) | Código definido por um sistema de terminologia. |
| [!UICONTROL Texto] | `text` | String | A representação em texto simples do conceito. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeableconcept.schema.json)
