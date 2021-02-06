---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schemas;design de Schema;mixin;enduserids;usuário final;ids;
solution: Experience Platform
title: Mistura de detalhes da ID de usuário final
topic: overview
description: Este documento fornece uma visão geral do mixin Detalhes da ID de usuário final.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---


# [!UICONTROL Detalhamento da ID de usuário final ] Detailsmixin

>[!NOTE]
>
>Os nomes de várias misturas mudaram. Consulte o documento em [mixin name updates](../name-updates.md) para obter mais informações.

[!UICONTROL ID do usuário final ] detalha uma combinação padrão para a  [[!DNL XDM ExperienceEvent] classe](../../classes/individual-profile.md), usada para descrever as informações de identidade de um indivíduo em vários aplicativos de Adobe. O mixin fornece um objeto `endUserIDs` de nível raiz, que contém um campo somente leitura `_experience` cujos valores são automaticamente atualizados à medida que os dados são assimilados.

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
