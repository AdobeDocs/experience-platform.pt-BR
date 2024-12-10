---
title: Tipo de dados da anotação
description: Saiba mais sobre o tipo de dados do Modelo de dados de experiência de anotação (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: f46b5fb6-d64a-4a37-91f6-b470599d9130
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 11%

---

# Tipo de dados de [!UICONTROL Anotação]

[!UICONTROL Anotação] é um tipo de dados padrão do Experience Data Model (XDM) que contém um nó de texto com atribuição ao autor. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Estrutura de tipo de dados de anotação](../../../images/healthcare/data-types/annotation.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Referência do autor] | `authorReference` | [[!UICONTROL Referência]](../data-types/reference.md) | Uma referência ao autor. |
| [!UICONTROL Autor] | `authorString` | String | O indivíduo responsável pela anotação. |
| [!UICONTROL Texto] | `text` | String | O conteúdo da anotação. |
| [!UICONTROL Hora] | `time` | DateTime | Quando a anotação foi feita. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.schema.json)
