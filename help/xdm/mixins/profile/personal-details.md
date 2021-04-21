---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, perfil individual, campos, esquemas, esquemas, esquemas, detalhes pessoais, design do esquema, mixin, Mixin;
solution: Experience Platform
title: Mistura de Detalhes de Contato Pessoal
topic-legacy: overview
description: Este documento fornece uma visão geral da combinação de Detalhes de contato pessoal.
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 6%

---

# [!UICONTROL Personal Contact Details] mistura

>[!NOTE]
>
>Os nomes de várias mixins mudaram. Consulte o documento em [mixin name updates](../name-updates.md) para obter mais informações.

[!UICONTROL Personal Contact Details] é uma mistura padrão para a  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) classe que descreve as informações de contato de uma pessoa individual.

<img src="../../images/mixins/profile-personal-details.png" width="700" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `faxPhone` | [Número de telefone](../../data-types/phone-number.md) | Descreve o número de fax da pessoa. |
| `homeAddress` | [Endereço postal](../../data-types/postal-address.md) | Descreve o endereço residencial da pessoa. |
| `homePhone` | [Número de telefone](../../data-types/phone-number.md) | Descreve o número de telefone residencial da pessoa. |
| `mobilePhone` | [Número de telefone](../../data-types/phone-number.md) | Descreve o número de telefone celular da pessoa. |
| `personalEmail` | [Endereço de email](../../data-types/email-address.md) | Descreve o endereço de email da pessoa. |

Para obter mais detalhes sobre o mixin, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
