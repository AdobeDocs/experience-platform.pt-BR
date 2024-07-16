---
title: Grupo de Campos de Esquema de Detalhes do Aplicativo
description: Saiba mais sobre o grupo de campos de esquema Detalhes do aplicativo.
exl-id: 5df99f9a-b36a-4c2b-a4a4-d3cf054f09b8
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 3%

---

# Grupo de campos de esquema [!UICONTROL Detalhes do aplicativo]

[!UICONTROL Detalhes do Aplicativo] é um grupo de campos de esquema padrão para a [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). O grupo de campos fornece um único objeto `application` para um esquema, que captura detalhes relacionados ao aplicativo, como falhas, uso de recursos, inicializações e atualizações.

![](../../images/field-groups/application-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `application` | [[!UICONTROL Aplicativo]](../../data-types/financial-account.md) | Captura informações do aplicativo relacionadas a um evento, incluindo o nome do aplicativo, a versão do aplicativo, instalações, inicializações, falhas e fechamentos. Pode ser o aplicativo direcionado pelo evento (como o destino de uma notificação por push enviada) ou o aplicativo que origina o evento (como um clique ou um logon). |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-application.schema.json).
