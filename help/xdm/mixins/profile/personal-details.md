---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;perfil individual;campos;schemas;Schemas;detalhes pessoais;design de Schema;mixin;Mixin;
solution: Experience Platform
title: Mistura de Detalhes de Contato Pessoal
topic: overview
description: Este documento fornece uma visão geral da combinação Detalhes do contato pessoal.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 6%

---


# [!UICONTROL Contato pessoal ] Detailsmixin

>[!NOTE]
>
>Os nomes de várias misturas mudaram. Consulte o documento em [mixin name updates](../name-updates.md) para obter mais informações.

[!UICONTROL Contato pessoal ] Detalhes de uma combinação padrão para a  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) classe que descreve as informações de contato de uma pessoa individual.

<img src="../../images/mixins/profile-personal-details.png" width="700" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `faxPhone` | [Número de telefone](../../data-types/phone-number.md) | Descreve o número de fax da pessoa. |
| `homeAddress` | [Endereço postal](../../data-types/postal-address.md) | Descreve o endereço residencial da pessoa. |
| `homePhone` | [Número de telefone](../../data-types/phone-number.md) | Descreve o número de telefone residencial da pessoa. |
| `mobilePhone` | [Número de telefone](../../data-types/phone-number.md) | Descreve o número do telefone celular da pessoa. |
| `personalEmail` | [Endereço de email](../../data-types/email-address.md) | Descreve o endereço de email da pessoa. |

Para obter mais detalhes sobre a mistura, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
