---
title: Tipo de dados de codificação
description: Saiba mais sobre o tipo de dados Coding Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 23b789da-1feb-4001-8268-f0d7e2e8563b
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 10%

---

# [!UICONTROL Codificação] tipo de dados

[!UICONTROL Codificação] é um tipo de dados padrão do Experience Data Model (XDM) que descreve uma referência a um código definido por um sistema de terminologia. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Codificando estrutura de tipo de dados](../../../images/healthcare/data-types/coding.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Código] | `code` | String | O símbolo na sintaxe definida pelo sistema. |
| [!UICONTROL Exibir] | `display` | String | A representação definida pelo sistema. |
| [!UICONTROL Sistema] | `system` | String | O namespace do valor do identificador, representado como um URI. |
| [!UICONTROL Foi Selecionado Pelo Usuário] | `userSelected` | Booleano | Um indicador de se essa codificação foi escolhida pelo usuário. O valor padrão é false. |
| [!UICONTROL Versão] | `version` | String | A versão do sistema. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/coding.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/coding.schema.json)
