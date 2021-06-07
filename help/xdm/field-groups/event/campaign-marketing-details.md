---
keywords: Experience Platform, home, tópicos populares, esquema, Esquema, XDM, ExperienceEvent, campos, esquemas, Esquemas, Design de esquema, grupo de campos, grupo de campos;
solution: Experience Platform
title: Grupo de Campos Detalhes do Esquema de Marketing da Campanha
topic-legacy: overview
description: Este documento fornece uma visão geral do grupo de campos Detalhes de marketing da campanha .
source-git-commit: cb4afb0979bd65a9a82a6018323fa7beacdbf605
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 3%

---


# [!UICONTROL Grupo de campos Detalhes do ] schema de marketing da campanha

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento em [atualizações do nome do grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL Detalhes de marketing da campanha ] é um grupo de campo de esquema padrão para a  [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), usado para descrever informações da campanha de marketing, como grupo da campanha, nome e código de rastreamento.

![](../../images/field-groups/campaign-marketing-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `marketing` | [Marketing](../../data-types/marketing.md) | Um objeto que descreve as informações da campanha de marketing, como grupo da campanha, nome e código de rastreamento. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-marketing.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-marketing.schema.json)
