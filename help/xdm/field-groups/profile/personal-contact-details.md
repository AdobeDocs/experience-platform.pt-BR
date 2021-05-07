---
keywords: Experience Platform; home; tópicos populares; esquema; esquema; XDM; perfil individual; campos; esquemas; esquemas; detalhes pessoais; design do esquema; grupo de campos; grupo de campos;
solution: Experience Platform
title: Grupo de Campos do Esquema Detalhes do Contato Pessoal
topic-legacy: overview
description: Este documento fornece uma visão geral do grupo de campos Detalhes do contato pessoal .
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
translation-type: tm+mt
source-git-commit: 4755f9b7666efd8354a5f15aeed40a7da4a06efe
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 6%

---


# [!UICONTROL Personal Contact Details] grupo de campos de esquema

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento em [atualizações do nome do grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL Personal Contact Details] é um grupo de campos de esquema padrão para a  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) classe que descreve as informações de contato de uma pessoa individual.

![](../../images/field-groups/personal-contact-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `faxPhone` | [Número de telefone](../../data-types/phone-number.md) | Descreve o número de fax da pessoa. |
| `homeAddress` | [Endereço postal](../../data-types/postal-address.md) | Descreve o endereço residencial da pessoa. |
| `homePhone` | [Número de telefone](../../data-types/phone-number.md) | Descreve o número de telefone residencial da pessoa. |
| `mobilePhone` | [Número de telefone](../../data-types/phone-number.md) | Descreve o número de telefone celular da pessoa. |
| `personalEmail` | [Endereço de email](../../data-types/email-address.md) | Descreve o endereço de email da pessoa. |

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
