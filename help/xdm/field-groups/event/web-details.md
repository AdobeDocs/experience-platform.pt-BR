---
keywords: Experience Platform, home, tópicos populares, esquema, Esquema, XDM, ExperienceEvent, campos, esquemas, Esquemas, Design de esquema, grupo de campos, grupo de campos;
solution: Experience Platform
title: Grupo de Campos do Esquema de Detalhes da Web
topic-legacy: overview
description: Este documento fornece uma visão geral do grupo de campos Detalhes da Web .
source-git-commit: b22dce52563d5f3bbd1796c11d7c7b2a49fa6d5f
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 3%

---


# [!UICONTROL Grupo de campos ] Detalhes da Web

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento em [atualizações do nome do grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL Detalhes da Web ] são um grupo de campo de esquema padrão para a  [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), usado para descrever informações relacionadas a eventos de detalhes da Web, como interação, detalhes da página e referenciador.

![](../../images/field-groups/web-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `web` | [Informações da Web](../../data-types/web-information.md) | Descreve cliques em links, detalhes da página da Web, informações do referenciador e detalhes do navegador. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-web.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-web.schema.json)
