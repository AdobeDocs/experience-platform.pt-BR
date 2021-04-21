---
keywords: Experience Platform; home; tópicos populares; esquema; Esquema; XDM; ExperienceEvent; campos; esquemas; esquemas; design de esquema; mixin; mixin; enduserids; usuário final; usuário final; ids;
solution: Experience Platform
title: Mistura de detalhes da ID do usuário final
topic-legacy: overview
description: Este documento fornece uma visão geral do mixin Detalhes da ID de usuário final .
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---

# [!UICONTROL End User ID Details] mistura

>[!NOTE]
>
>Os nomes de várias mixins mudaram. Consulte o documento em [mixin name updates](../name-updates.md) para obter mais informações.

[!UICONTROL End User ID Details] é uma mixin padrão para a  [[!DNL XDM ExperienceEvent] classe](../../classes/individual-profile.md), usada para descrever as informações de identidade de um indivíduo em vários aplicativos de Adobe. O mixin fornece um objeto de nível raiz `endUserIDs`, que contém um campo somente leitura `_experience` cujos valores são atualizados automaticamente à medida que os dados são assimilados.

<img src="../../images/mixins/enduserids.png" width="700" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `aacustomid` | [Identidade](../../data-types/identity.md) | IDs de usuário final personalizadas para o Adobe Analytics Cloud. |
| `aaid` | [Identidade](../../data-types/identity.md) | IDs de usuário final do Adobe Analytics Cloud. |
| `acid` | [Identidade](../../data-types/identity.md) | IDs de usuário final do Adobe Campaign. |
| `adcloud` | [Identidade](../../data-types/identity.md) | IDs de usuário final do Adobe Advertising Cloud. |
| `emailid` | [Identidade](../../data-types/identity.md) | IDs de endereço de email. |
| `mcid` | [Identidade](../../data-types/identity.md) | Adobe Marketing Cloud ID. |
| `phonenumberid` | [Identidade](../../data-types/identity.md) | IDs de número de telefone. |
| `tntid` | [Identidade](../../data-types/identity.md) | IDs de usuário final do Adobe Target. |

Para obter mais detalhes sobre o mixin, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.schema.json)
