---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;pessoa;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de dados da pessoa
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência da pessoa (XDM).
exl-id: f28a52be-90c7-4ed0-a460-97165bb58046
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 3%

---

# [!UICONTROL Person] tipo de dados

[!UICONTROL Person] é um tipo de dados padrão do Experience Data Model (XDM) que descreve uma pessoa. Esse tipo de dados pode representar uma pessoa que atua em várias funções, como cliente, contato ou proprietário.

<img src="../images/data-types/person.PNG" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `name` | [[!UICONTROL Nome da pessoa]](./person-name.md) | Descreve detalhes sobre o nome completo da pessoa. |
| `birthDate` | Data | A data de nascimento completa de uma pessoa. O formato de data (sem hora) deve seguir o [RFC 3339, seção 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) padrão. |
| `birthDayAndMonth` | String | O dia e mês em que uma pessoa nasceu, no formato MM-DD. Este campo deve ser usado quando o dia e o mês de nascimento de uma pessoa são conhecidos, mas não o ano. O formato dessa propriedade deve estar em conformidade com essa expressão regular `[0-1][0-9]-[0-9][0-9]`. |
| `birthYear` | Número inteiro | O ano em que uma pessoa nasceu, incluindo o século (por exemplo, `1983`). Este campo deve ser usado quando apenas a idade da pessoa é conhecida e não a data de nascimento completa. Esse valor deve estar entre 1 e 32767. |
| `gender` | String | A identidade de gênero da pessoa. O valor dessa propriedade deve ser igual a um dos seguintes valores de enumeração conhecidos. <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> O padrão para esse valor é `not_specified`. |
| `maritalStatus` | String | Descreve o relacionamento de uma pessoa com uma outra pessoa importante. O valor dessa propriedade deve ser igual a um dos seguintes valores de enumeração. <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> O padrão para esse valor é `not_specified`. |
| `nationality` | String | A relação jurídica entre uma pessoa e seu estado representado usando o código ISO 3166-1 Alpha-2. O formato dessa propriedade deve estar em conformidade com essa expressão regular `^[A-Z]{2}$`. |
| `taxId` | String | A ID fiscal ou de imposto da pessoa, como o Número de Identificação do Contribuinte (TIN) nos EUA ou o Certificado de Identificação Fiscal (CIF/NIF) na Espanha. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)
