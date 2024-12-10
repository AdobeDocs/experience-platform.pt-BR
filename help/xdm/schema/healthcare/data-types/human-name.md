---
title: Tipo de Dados de Nome Humano
description: Saiba mais sobre o tipo de dados do Modelo de dados de experiência (XDM) de nome humano.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 5dd6fda4-c076-4c34-bdd9-259203b6ea73
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 6%

---

# Tipo de dados [!UICONTROL Nome Humano]

[!UICONTROL Nome Humano] é um tipo de dados padrão do Experience Data Model (XDM) que fornece informações sobre o nome de uma entidade humana ou outra entidade viva. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Estrutura de tipo de dados de Nome Humano](../../../images/healthcare/data-types/human-name.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Período] | `period` | [[!UICONTROL Período]](../data-types/period.md) | O período em que o nome está ou estava em uso. |
| [!UICONTROL Família] | `family` | String | A família ou sobrenome. |
| [!UICONTROL Concedido] | `given` | Matriz de cadeias de caracteres | O nome fornecido, incluindo qualquer nome do meio. |
| [!UICONTROL Prefixo] | `prefix` | Matriz de cadeias de caracteres | Qualquer parte do nome antes do nome ou do nome fornecido. |
| [!UICONTROL Sufixo] | `suffix` | Matriz de cadeias de caracteres | Qualquer parte do nome depois da família ou sobrenome. |
| [!UICONTROL Texto] | `text` | String | A representação em texto sem formatação do nome completo. |
| [!UICONTROL Uso] | `use` | String | O uso do nome. Os valores dessa propriedade devem ser iguais a um ou mais dos seguintes valores de enumeração conhecidos. <li> `usual` </li> <li> `offical` </li> <li> `temp` </li> <li> `nickname` </li> <li> `anonymous` </li> <li> `old` </li> <li> `maiden` </li> |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/humanname.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/humanname.schema.json)
