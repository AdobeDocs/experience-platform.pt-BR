---
keywords: Experience Platform, home, tópicos populares, esquema, Esquema, XDM, ExperienceEvent, campos, esquemas, Esquemas, Design de esquema, grupo de campos, grupo de campos;
solution: Experience Platform
title: Grupo de Campos Detalhes do Esquema de Marketing da Campanha
topic-legacy: overview
description: This document provides an overview of the Campaign Marketing Details schema field group.
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 3%

---


# [!UICONTROL Grupo de campos Detalhes do ] schema de marketing da campanha

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento em [atualizações do nome do grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL Campaign Marketing Details] is a standard schema field group for the [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md), used to describe marketing campaign information such as campaign group, name, and tracking code.

![](../../images/field-groups/campaign-marketing-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `marketing` | [Marketing](../../data-types/marketing.md) | Um objeto que descreve as informações da campanha de marketing, como grupo da campanha, nome e código de rastreamento. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Populated example](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.schema.json)
