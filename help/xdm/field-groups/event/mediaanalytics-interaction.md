---
title: Grupo de campos Esquema de detalhes de interação do MediaAnalytics
description: Saiba mais sobre o grupo de campos do esquema Detalhes da interação do MediaAnalytics.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 2%

---

# [!UICONTROL Detalhes de interação do MediaAnalytics] grupo de campos de esquema

[!UICONTROL Detalhes de interação do MediaAnalytics] é um grupo de campos de esquema padrão para o [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Use este grupo de campos para capturar campos de dados enriquecidos que monitoram e analisam interações com conteúdo de mídia de forma abrangente em várias plataformas ou canais.

![Um diagrama de esquema do [!UICONTROL Detalhes de interação do MediaAnalytics] grupo de campos de esquema.](../../images/field-groups/mediaanalytics-interaction.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|---| --- | --- | --- |
| [!UICONTROL Detalhes da coleção de mídia] | `mediaCollection` | [[!UICONTROL Informações de detalhes de mídia]](../../data-types/media-details-information.md) | Atributos relacionados a uma coleção de itens de mídia. |
| [!UICONTROL Detalhes de relatórios de mídia] | `mediaReporting` | [[!UICONTROL Informações de detalhes de mídia]](../../data-types/media-details-information.md) | Relatar detalhes e métricas associados ao conteúdo de mídia. |
| [!UICONTROL Lista De Eventos De Conteúdo Baixados Da Coleção De Mídia] | `mediaDownloadedEvents` | [!UICONTROL Matriz] de [[!UICONTROL mediaEvent]](../../data-types/media-event-information.md) | Eventos que rastreiam o download de conteúdo na coleção de mídia. |

{style="table-layout:auto"}

Para obter mais informações sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json)
