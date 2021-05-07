---
keywords: Experience Platform, home, tópicos populares, schema, esquema, XDM, perfil individual, campos, esquemas, esquemas, design de esquema, mixin, mixins, detalhes de trabalho, trabalho de perfil;
solution: Experience Platform
title: Grupo de Campos do Esquema Detalhes do Contato de Trabalho
topic-legacy: overview
description: Este documento fornece uma visão geral do grupo de campos Detalhes do contato de trabalho .
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
translation-type: tm+mt
source-git-commit: 4755f9b7666efd8354a5f15aeed40a7da4a06efe
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 3%

---


# [!UICONTROL Work Contact Details] grupo de campos de esquema

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento em [atualizações do nome do grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL Work Contact Details] é um grupo de campos de esquema padrão para a  [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). O grupo de campos fornece vários campos que capturam informações profissionais relacionadas a uma pessoa individual, como endereço de trabalho, email de trabalho, número de telefone de trabalho e organizações às quais a pessoa pertence.

![](../../images/field-groups/work-contact-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `workAddress` | [Endereço postal](../../data-types/postal-address.md) | Descreve o endereço de trabalho da pessoa. |
| `workEmail` | [Endereço de email](../../data-types/email-address.md) | Descreve o endereço de email de trabalho da pessoa. |
| `workPhone` | [Número de telefone](../../data-types/phone-number.md) | Descreve o número de telefone de trabalho da pessoa. |
| `organizations` | Sequência (Matriz) | Uma matriz de strings de forma livre que representam as organizações das quais a pessoa é membro. |

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.schema.json)
