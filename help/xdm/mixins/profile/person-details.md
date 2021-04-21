---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, perfil individual, campos, esquemas, esquemas, design de esquema, mixin, mixin, pessoa, detalhes da pessoa, detalhes da pessoa do perfil, pessoa;
solution: Experience Platform
title: Mistura de detalhes demográficos
topic-legacy: overview
description: Este documento fornece uma visão geral da combinação de Detalhes demográficos .
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 3%

---

# [!UICONTROL Demographic Details] mistura

>[!NOTE]
>
>Os nomes de várias mixins mudaram. Consulte o documento em [mixin name updates](../name-updates.md) para obter mais informações.

[!UICONTROL Demographic Details] é uma mixin padrão para a  [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) . O mixin fornece um objeto de nível raiz `person`, cujos subcampos descrevem informações sobre uma pessoa individual.

<img src="../../images/mixins/profile-person-details.png" width="600" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `person.name` | [Nome da pessoa](../../data-types/person-name.md) | Um objeto cujos subcampos descrevem vários elementos do nome de uma pessoa. |
| `person.birthDate` | Data | A data completa em que uma pessoa nasceu, na forma de um carimbo de data e hora ISO 8601. |
| `person.birthDayAndMonth` | String | O dia e o mês em que uma pessoa nasceu, no formato MM-DD. Este campo deve ser usado quando o dia e o mês de nascimento de uma pessoa forem conhecidos, mas não o ano. |
| `person.birthYear` | Número inteiro | O ano em que uma pessoa nasceu, incluindo o século (como 1989). Este campo deve ser usado quando somente a idade da pessoa é conhecida, não a data de nascimento completa. |
| `person.gender` | String | A identidade de gênero da pessoa. |
| `person.martialStatus` | String | Descreve a relação de uma pessoa com uma outra significativa. |
| `person.nationality` | String | A relação jurídica entre uma pessoa e seu estado representado usando o código alfa-2 da ISO 3166-1. |
| `person.taxId` | String | A ID fiscal/fiscal da pessoa, como a TIN nos EUA ou a CIF/NIF em Espanha. |

Para obter mais detalhes sobre o mixin, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.example.1.json)
* [Full ](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.schema.json)
schemaå
