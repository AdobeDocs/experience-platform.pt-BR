---
keywords: Experience Platform; home; tópicos populares; esquema; esquema; XDM; perfil individual; campos; esquemas; esquemas; detalhes pessoais; design do esquema; grupo de campos; grupo de campos;
solution: Experience Platform
title: Personal Contact Details Schema Field Group
topic-legacy: overview
description: Este documento fornece uma visão geral do grupo de campos Detalhes do contato pessoal .
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 7%

---


# [!UICONTROL Personal Contact Details] schema field group

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento em [atualizações do nome do grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL Personal Contact Details] is a standard schema field group for the [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) which describes the contact information for an individual person.

![](../../images/field-groups/personal-contact-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `faxPhone` | [Número de telefone](../../data-types/phone-number.md) | Describes the person&#39;s fax number. |
| `homeAddress` | [Endereço postal](../../data-types/postal-address.md) | Describes the person&#39;s residential address. |
| `homePhone` | [Número de telefone](../../data-types/phone-number.md) | Descreve o número de telefone residencial da pessoa. |
| `mobilePhone` | [Número de telefone](../../data-types/phone-number.md) | Descreve o número de telefone celular da pessoa. |
| `personalEmail` | [Endereço de email](../../data-types/email-address.md) | Descreve o endereço de email da pessoa. |

{style=&quot;table-layout:auto&quot;}

For more details on the field group, refer to the public XDM repository:

* [Populated example](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
