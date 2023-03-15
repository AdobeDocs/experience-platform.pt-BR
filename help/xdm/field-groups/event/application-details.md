---
title: Grupo de Campos de Esquema de Detalhes do Aplicativo
description: Este documento fornece uma visão geral do grupo de campos de esquema Detalhes do aplicativo.
exl-id: 5df99f9a-b36a-4c2b-a4a4-d3cf054f09b8
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 2%

---

# [!UICONTROL Detalhes do aplicativo] grupo de campos de esquema

[!UICONTROL Detalhes do aplicativo] é um grupo de campos de esquema padrão para o [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). O grupo de campos fornece um único `application` para um esquema, que captura detalhes relacionados ao aplicativo, como travamentos, uso de recursos, inicializações e atualizações.

![](../../images/field-groups/application-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `application` | [[!UICONTROL Aplicativo]](../../data-types/financial-account.md) | Captura informações do aplicativo relacionadas a um evento, incluindo o nome do aplicativo, a versão do aplicativo, instalações, inicializações, falhas e fechamentos. Pode ser o aplicativo direcionado pelo evento (como o destino de uma notificação por push enviada) ou o aplicativo que origina o evento (como um clique ou um logon). |

{style="table-layout:auto"}

Para obter mais informações sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-application.schema.json).
