---
keywords: Experience Platform, home, tópicos populares, esquema, Esquema, XDM, ExperienceEvent, campos, esquemas, Esquemas, Design de esquema, grupo de campos, grupo de campos, enduserids, usuário final, usuário final, ids;
solution: Experience Platform
title: Grupo de Campos do Esquema Detalhes da ID do Usuário Final
topic-legacy: overview
description: Este documento fornece uma visão geral do grupo de campos Detalhes da ID do usuário final.
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 2%

---


# [!UICONTROL Grupo de campos Detalhes da ID de usuário final ] do schema

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento em [atualizações do nome do grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL ID de usuário final ] Detalha um grupo de campo de esquema padrão para a  [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), usado para descrever as informações de identidade de um indivíduo em vários aplicativos de Adobe. O grupo de campos fornece um objeto de nível raiz `endUserIDs`, que contém um campo somente leitura `_experience` cujos valores são atualizados automaticamente à medida que os dados são assimilados.

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

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

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.schema.json)
