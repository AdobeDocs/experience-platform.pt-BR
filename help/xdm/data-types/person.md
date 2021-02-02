---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;campos;schemas;pessoa;datatype;data-type;data type;Schema;home;popular topics;;XDM;fields;processors;people;people;people;date-type;data-type;data type;data type;
solution: Experience Platform
title: Tipo de dados da pessoa
topic: overview
description: Este documento fornece uma visão geral do tipo de dados do Modelo de Dados de Experiência da Pessoa (XDM).
translation-type: tm+mt
source-git-commit: 194b604d4b23f2acfaa4243155b04a6793fb0727
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 4%

---


# [!UICONTROL Tipo de ] Persondata

 Personaliza um tipo de dados padrão do Modelo de Dados de Experiência (XDM) que descreve uma pessoa individual. Esse tipo de dados pode representar uma pessoa agindo em várias funções, como cliente, contato ou proprietário.

<img src="../images/data-types/person.PNG" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `name` | [[!UICONTROL Nome da pessoa]](./person-name.md) | Descreve detalhes sobre o nome completo da pessoa. |
| `birthDate` | Data | A data completa em que uma pessoa nasceu. O formato de data (sem tempo) deve seguir o padrão [RFC 3339, seção 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `birthDayAndMonth` | String | O dia e o mês em que uma pessoa nasceu, no formato MM-DD. Este campo deve ser usado quando se conhece o dia e o mês do nascimento de uma pessoa, mas não o ano. O formato dessa propriedade deve estar em conformidade com essa expressão regular `[0-1][0-9]-[0-9][0-9]`. |
| `birthYear` | Número inteiro | O ano em que uma pessoa nasceu incluindo o século (por exemplo, `1983`). Este campo deve ser utilizado quando apenas a idade da pessoa for conhecida e não a data de nascimento completa. Esse valor deve estar entre 1 e 32767. |
| `gender` | String | A identidade de gênero da pessoa. O valor dessa propriedade deve ser igual a um dos seguintes valores de enumeração conhecidos. <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> O padrão para esse valor é `not_specified`. |
| `maritalStatus` | String | Descreve a relação de uma pessoa com uma outra significativa. O valor dessa propriedade deve ser igual a um dos valores de enumeração a seguir. <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> O padrão para esse valor é `not_specified`. |
| `nationality` | String | A relação jurídica entre uma pessoa e seu estado representada por meio do código ISO 3166-1 Alpha-2. O formato dessa propriedade deve estar em conformidade com essa expressão regular `^[A-Z]{2}$`. |
| `taxId` | String | O ID fiscal ou fiscal da pessoa, como o Número de Identificação do Contribuinte (TIN) nos EUA ou o Certificado de Identificação Fiscal (CIF/NIF) em Espanha. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)