---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;mixin;mixin;enduserids;end-user;end user;ids;
solution: Experience Platform
title: Mistura Detalhes da ID do usuário final
topic: overview
description: Este documento fornece uma visão geral do mixin Detalhes da ID de usuário final.
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 1%

---


# [!UICONTROL Mistura Detalhes] da ID do usuário final

>[!NOTE]
>
>Os nomes de várias misturas mudaram. Consulte o documento sobre atualizações [de nome de](../name-updates.md) mixin para obter mais informações.

[!UICONTROL Detalhes] da ID de usuário final é uma combinação padrão para a [[!DNL XDM ExperienceEvent] classe](../../classes/individual-profile.md), usada para descrever as informações de identidade de um indivíduo em vários aplicativos de Adobe. O mixin fornece um `endUserIDs` objeto de nível raiz, que contém um campo somente leitura `_experience` cujos valores são automaticamente atualizados à medida que os dados são assimilados.

<img src="../../images/mixins/enduserids.png" width="700" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `aacustomid` | [Identidade](../../data-types/identity.md) | IDs de usuário final personalizadas para Adobe Analytics Cloud. |
| `aaid` | [Identidade](../../data-types/identity.md) | IDs de usuário final para Adobe Analytics Cloud. |
| `acid` | [Identidade](../../data-types/identity.md) | IDs de usuário final para Adobe Campaign. |
| `adcloud` | [Identidade](../../data-types/identity.md) | IDs de usuário final para Adobe Advertising Cloud. |
| `emailid` | [Identidade](../../data-types/identity.md) | IDs de endereço de email. |
| `mcid` | [Identidade](../../data-types/identity.md) | Adobe Marketing Cloud ID. |
| `phonenumberid` | [Identidade](../../data-types/identity.md) | IDs de número de telefone. |
| `tntid` | [Identidade](../../data-types/identity.md) | IDs de usuário final para Adobe Target. |

Para obter mais detalhes sobre a mistura, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.schema.json)
