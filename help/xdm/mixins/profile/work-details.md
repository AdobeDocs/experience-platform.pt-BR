---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;Schema design;mixin;mixins;work details;profile work;
solution: Experience Platform
title: Mistura Detalhes do contato de trabalho
topic: overview
description: Este documento fornece uma visão geral da combinação Detalhes do contato de trabalho.
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 3%

---


# [!UICONTROL Mistura de Detalhes] do Contato de Trabalho

>[!NOTE]
>
>Os nomes de várias misturas mudaram. Consulte o documento sobre atualizações [de nome de](../name-updates.md) mixin para obter mais informações.

[!UICONTROL Detalhes] do contato de trabalho é uma combinação padrão para a [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). O mixin fornece vários campos que capturam informações profissionais relacionadas a uma pessoa individual, como endereço de trabalho, email de trabalho, número de telefone de trabalho e organizações às quais a pessoa pertence.

<img src="../../images/mixins/profile-work-details.png" width="550" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `workAddress` | [Endereço postal](../../data-types/postal-address.md) | Descreve o endereço de trabalho da pessoa. |
| `workEmail` | [Endereço de email](../../data-types/email-address.md) | Descreve o endereço de email da pessoa. |
| `workPhone` | [Número de telefone](../../data-types/phone-number.md) | Descreve o número de telefone do trabalho da pessoa. |
| `organizations` | String (Array) | Uma matriz de strings de forma livre que representam as organizações das quais a pessoa é membro. |

Para obter mais detalhes sobre a mistura, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.schema.json)