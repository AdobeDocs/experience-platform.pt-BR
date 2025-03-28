---
keywords: Experience Platform;início;tópicos populares;esquema;Esquema;XDM;ExperienceEvent;campos;esquemas;Esquemas;Design de esquema;grupo de campos;grupo de campos;enduserids;usuário final;usuário final;ids;
solution: Experience Platform
title: Grupo de Campos de Esquema de Detalhes do ID do Usuário Final
description: Saiba mais sobre o grupo de campos de esquema Detalhes da ID do usuário final.
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 5%

---


# [!UICONTROL Detalhes da ID do Usuário Final] grupo de campos de esquema

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento em [atualizações de nome de grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL Detalhes de ID do Usuário Final] é um grupo de campos de esquema padrão para a [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), usado para descrever as informações de identidade de um indivíduo em vários aplicativos Adobe. O grupo de campos fornece um objeto `endUserIDs` de nível raiz, que contém um campo `_experience` somente leitura cujos valores são atualizados automaticamente à medida que os dados são assimilados.

![](../../images/field-groups/enduserids.png){width=700}

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `aacustomid` | [Identidade](../../data-types/identity.md) | IDs de usuário final personalizadas para o Adobe Analytics Cloud. |
| `aaid` | [Identidade](../../data-types/identity.md) | IDs de usuário final do Adobe Analytics Cloud. |
| `acid` | [Identidade](../../data-types/identity.md) | IDs de usuário final do Adobe Campaign. |
| `adcloud` | [Identidade](../../data-types/identity.md) | IDs de usuário final do Adobe Advertising Cloud. |
| `emailid` | [Identidade](../../data-types/identity.md) | IDs de endereço de email. |
| `mcid` | [Identidade](../../data-types/identity.md) | Adobe Marketing Cloud ID (MCID). O MCID agora é conhecido como Experience Cloud ID (ECID). |
| `phonenumberid` | [Identidade](../../data-types/identity.md) | IDs de número de telefone. |
| `tntid` | [Identidade](../../data-types/identity.md) | IDs de usuário final do Adobe Target. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.schema.json)
