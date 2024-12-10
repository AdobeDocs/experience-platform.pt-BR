---
title: Tipo de dados de conceito codificável
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência de conceito codificável (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: c172a7cd-24c6-484b-8552-8745dfd3a8e9
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 9%

---

# Tipo de dados [!UICONTROL Conceito codificável]

[!UICONTROL Conceito Codificável] é um tipo de dados padrão do Experience Data Model (XDM) que descreve uma referência de um recurso a outro. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Estrutura de tipo de dados de conceito codificável](../../../images/healthcare/data-types/codeable-concept.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Codificação] | `coding` | Matriz de [[!UICONTROL Codificação]](../data-types/coding.md) | Código definido por um sistema de terminologia. |
| [!UICONTROL Texto] | `text` | String | A representação em texto simples do conceito. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeableconcept.schema.json)
