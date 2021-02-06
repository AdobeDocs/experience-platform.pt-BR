---
keywords: Experience Platform;home;populares tópicos;schema;Schema;XDM;perfil individual;campos;schemas;Schemas;design de Schema;mixin;mixin;pessoa;informações da pessoa;informações da pessoa do perfil;pessoa;
solution: Experience Platform
title: Mistura de detalhes demográficos
topic: overview
description: Este documento fornece uma visão geral da combinação Detalhes demográficos.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 3%

---


# [!UICONTROL Demográfico ] Detailsmixin

>[!NOTE]
>
>Os nomes de várias misturas mudaram. Consulte o documento em [mixin name updates](../name-updates.md) para obter mais informações.

[!UICONTROL Detalhes Demográficos ] são uma mistura padrão para a  [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). O mixin fornece um objeto `person` de nível raiz, cujos subcampos descrevem informações sobre uma pessoa individual.

<img src="../../images/mixins/profile-person-details.png" width="600" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `person.name` | [Nome da pessoa](../../data-types/person-name.md) | Um objeto cujos subcampos descrevem vários elementos do nome de uma pessoa. |
| `person.birthDate` | Data | A data completa em que uma pessoa nasceu, na forma de um carimbo de data e hora ISO 8601. |
| `person.birthDayAndMonth` | String | O dia e o mês em que uma pessoa nasceu, no formato MM-DD. Este campo deve ser usado quando se conhece o dia e o mês do nascimento de uma pessoa, mas não o ano. |
| `person.birthYear` | Número inteiro | O ano em que nasceu uma pessoa, incluindo o século (como 1989). Este campo deve ser utilizado quando apenas a idade da pessoa for conhecida, e não a data de nascimento completa. |
| `person.gender` | String | A identidade de gênero da pessoa. |
| `person.martialStatus` | String | Descreve a relação de uma pessoa com uma outra significativa. |
| `person.nationality` | String | A relação jurídica entre uma pessoa e seu estado representada por meio do código ISO 3166-1 Alpha-2. |
| `person.taxId` | String | A identificação fiscal/fiscal da pessoa, como a TIN nos EUA ou o CIF/NIF em Espanha. |

Para obter mais detalhes sobre a mistura, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.example.1.json)
* [Total ](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.schema.json)
schemaå