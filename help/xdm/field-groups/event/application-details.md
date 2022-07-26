---
title: Grupo de Campos do Esquema Detalhes do Aplicativo
description: Este documento fornece uma visão geral do grupo de campos Detalhes do aplicativo .
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 4%

---

# [!UICONTROL Detalhes do aplicativo] grupo de campos de esquema

[!UICONTROL Detalhes do aplicativo] é um grupo de campos de esquema padrão para a variável [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). O grupo de campos fornece um único `application` objeto de um esquema, que captura detalhes relacionados ao aplicativo, como falhas, uso de recursos, inicializações e atualizações.

![](../../images/field-groups/application-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `application` | [[!UICONTROL Aplicativo]](../../data-types/financial-account.md) | Captura informações do aplicativo relacionadas a um evento, incluindo o nome do aplicativo, a versão do aplicativo, as instalações, inicializações, falhas e fechamentos. Pode ser o aplicativo direcionado pelo evento (como o destino de uma notificação por push que está sendo enviada) ou o aplicativo que está originando o evento (como um clique ou um logon). |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte [repositório XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-application.schema.json).
