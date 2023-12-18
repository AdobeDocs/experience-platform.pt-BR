---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;perfil individual;campos;esquemas;Esquemas;Design de esquema;grupo de campos;grupo de campos;pessoa;detalhes da pessoa;detalhes da pessoa do perfil;pessoa;
solution: Experience Platform
title: Grupo de Campos de Esquema de Detalhes Demográficos
description: Saiba mais sobre o grupo de campos de esquema Detalhes demográficos.
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 4%

---


# [!UICONTROL Detalhes demográficos] grupo de campos de esquema

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento sobre [atualizações do nome do grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL Detalhes demográficos] é um grupo de campos de esquema padrão para o [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). O grupo de campos fornece um nível raiz `person` objeto, cujos subcampos descrevem informações sobre uma pessoa individual.

![](../../images/field-groups/demographic-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `person.name` | [Nome da pessoa](../../data-types/person-name.md) | Um objeto cujos subcampos descrevem vários elementos do nome de uma pessoa. |
| `person.birthDate` | Data | A data de nascimento completa de uma pessoa, na forma de um carimbo de data e hora ISO 8601. |
| `person.birthDayAndMonth` | String | O dia e mês em que uma pessoa nasceu, no formato MM-DD. Este campo deve ser usado quando o dia e o mês de nascimento de uma pessoa são conhecidos, mas não o ano. |
| `person.birthYear` | Número inteiro | O ano em que uma pessoa nasceu, incluindo o século (como 1989). Este campo deve ser usado quando apenas a idade da pessoa é conhecida, não a data de nascimento completa. |
| `person.gender` | String | A identidade de gênero da pessoa. |
| `person.martialStatus` | String | Descreve o relacionamento de uma pessoa com uma outra pessoa importante. |
| `person.nationality` | String | A relação jurídica entre uma pessoa e seu estado representado usando o código ISO 3166-1 Alpha-2. |
| `person.taxId` | String | A ID fiscal da pessoa, como o TIN nos EUA ou o CIF/NIF na Espanha. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.schema.json)