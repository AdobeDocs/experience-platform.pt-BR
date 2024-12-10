---
title: Tipo de dados da pessoa
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência da pessoa (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: a19823f2-25d0-45cb-86f4-7816041b27f9
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 7%

---

# Tipo de dados [!UICONTROL Pessoa]

[!UICONTROL Pessoa] é um tipo de dados padrão do Experience Data Model (XDM) que fornece informações sobre um registro pessoal genérico. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Estrutura de tipo de dados da pessoa](../../../images/healthcare/data-types/person/person.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Endereço] | `address` | Matriz de [[!UICONTROL Endereço]](../data-types/address.md) | Um ou mais endereços da pessoa. |
| [!UICONTROL Comunicação] | `communication` | Matriz de objetos | Um idioma que pode ser usado para comunicar com a pessoa sobre sua saúde. Consulte a [seção abaixo](#communication) para obter mais informações. |
| [!UICONTROL Identificador] | `identifier` | Matriz de [[!UICONTROL Identificador]](../data-types/identifier.md) | Um identificador humano para esta pessoa. |
| [!UICONTROL Detalhes do link da pessoa] | `link` | Matriz de objetos | Um link para um recurso que diz respeito à mesma pessoa real. Consulte a [seção abaixo](#link) para obter mais informações. |
| [!UICONTROL Gerenciando a Organização] | `managingOrganization` | [[!UICONTROL Referência]](../data-types/reference.md) | A organização que é a responsável pelo registro do paciente. |
| [!UICONTROL Estado civil] | `maritalStatus` | [[!UICONTROL Conceito codificável]](../data-types/codeable-concept.md) | O estado civil de uma pessoa |
| [!UICONTROL Nome] | `name` | Matriz de [[!UICONTROL Nome Humano]](../data-types/human-name.md) | Os nomes associados a uma pessoa. |
| [!UICONTROL Detalhes de contato] | `telecom` | Matriz de [[!UICONTROL Ponto de Contato]] | Os detalhes de contato pelos quais a pessoa pode ser contatada. |
| [!UICONTROL Está Ativo] | `active` | Booleano | Indica se o registro da pessoa está em uso ativo. |
| [!UICONTROL Data de nascimento] | `birthDate` | Data | A data de nascimento da pessoa. |
| [!UICONTROL Indicador de Falecimento] | `deceasedBoolean` | Booleano | Indica se a pessoa morreu ou não. |
| [!UICONTROL Data e hora da morte] | `deceasedDateTime` | DateTime | A data e a hora da morte se a pessoa falecer. |
| [!UICONTROL Gênero] | `gender` | String | A identidade de gênero da pessoa. O valor dessa propriedade deve ser igual a um dos seguintes valores de enumeração conhecidos. <li> `female` </li> <li> `male` </li> <li> `other` </li> <li> `unknown`</li> |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.schema.json)

## `communication` {#communication}

`communication` é fornecido como uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![estrutura de comunicação](../../../images/healthcare/data-types/person/communication.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Idioma] | `language` | [[!UICONTROL Conceito codificável]](../data-types/codeable-concept.md) | Idioma que pode ser usado para comunicar com a pessoa sobre sua saúde. |
| [!UICONTROL É o Idioma Preferencial] | `preferred` | Booleano | Indica se o idioma é o idioma preferido ou não. |

## `link` {#link}

`link` é fornecido como uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![estrutura do link](../../../images/healthcare/data-types/person/link.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Target] | `target` | [[!UICONTROL Referência]](../data-types/reference.md) | O recurso ao qual esta pessoa real está associada. |
| [!UICONTROL Assurance] | `assurance` | String | O nível de garantia associado ao link. Os valores dessa propriedade devem ser iguais a um ou mais dos seguintes valores de enumeração conhecidos. <li> `level1` </li> <li> `level2` </li> <li> `level3` </li> <li> `level4` </li> |
