---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;perfil individual;campos;esquemas;Esquemas;Design de esquema;mixin;mixins;detalhes de trabalho;trabalho de perfil;
solution: Experience Platform
title: Grupo de Campos de Esquema de Detalhes do Contato Comercial
description: Este documento fornece uma visão geral do grupo de campos de esquema Detalhes do contato de trabalho.
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 3%

---


# [!UICONTROL Detalhes de contato comercial] grupo de campos de esquema

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento sobre [atualizações do nome do grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL Detalhes de contato comercial] é um grupo de campos de esquema padrão para o [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). O grupo de campos fornece vários campos que capturam informações profissionais sobre uma pessoa individual, como endereço comercial, email comercial, número de telefone comercial e organizações às quais a pessoa pertence.

![](../../images/field-groups/work-contact-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `workAddress` | [Endereço postal](../../data-types/postal-address.md) | Descreve o endereço comercial da pessoa. |
| `workEmail` | [Endereço de email](../../data-types/email-address.md) | Descreve o endereço de email comercial da pessoa. |
| `workPhone` | [Número de telefone](../../data-types/phone-number.md) | Descreve o número de telefone comercial da pessoa. |
| `organizations` | String (Matriz) | Uma matriz de cadeias de caracteres de forma livre que representam as organizações das quais a pessoa é membro. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.schema.json)
