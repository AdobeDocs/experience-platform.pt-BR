---
title: Grupo de campos Esquema de detalhes de interação do MediaAnalytics
description: Saiba mais sobre o grupo de campos do esquema Detalhes da interação do MediaAnalytics.
exl-id: 1096d28a-5796-49cc-bd45-b3f5188f699e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 2%

---

# [!UICONTROL Detalhes de interação do MediaAnalytics] grupo de campos de esquema

[!UICONTROL Detalhes de Interação do MediaAnalytics] é um grupo de campos de esquema padrão para a [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Use este grupo de campos para capturar campos de dados enriquecidos que monitoram e analisam interações com conteúdo de mídia de forma abrangente em várias plataformas ou canais.

![Um diagrama de esquema do [!UICONTROL Detalhes de interação do MediaAnalytics] grupo de campos de esquema.](../../images/field-groups/mediaanalytics-interaction.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|---| --- | --- | --- |
| [!UICONTROL Detalhes da coleção de mídia] | `mediaCollection` | [[!UICONTROL Detalhes da coleção de mídia]](../../data-types/media-collection-details.md) | Atributos relacionados a uma coleção de itens de mídia. Use os campos da Coleção de mídia para capturar dados e enviá-los para outros serviços da Adobe para processamento adicional. |
| [!UICONTROL Detalhes de Relatórios de Mídia] | `mediaReporting` | [[!UICONTROL Detalhes de Relatórios de Mídia]](../../data-types/media-reporting-details.md) | Relatar detalhes e métricas associados ao conteúdo de mídia. * Os campos Relatórios de mídia são usados pelos serviços da Adobe para analisar os campos Coleção de mídia enviados pelos usuários. Esses dados, juntamente com outras métricas específicas do usuário, são calculados e relatados. |
| [!UICONTROL Lista De Eventos De Conteúdo Baixados Pela Coleção De Mídia] | `mediaDownloadedEvents` | [!UICONTROL Matriz] de [[!UICONTROL mediaEvent]](../../data-types/media-event-information.md) | Eventos que rastreiam o download de conteúdo na coleção de mídia. |

{style="table-layout:auto"}

>[!TIP]
>
>Você pode ocultar campos que não são usados pela API do Media Edge. Ocultar esses campos facilita a leitura e a compreensão do schema, mas não é obrigatório. Esses campos se referem apenas àqueles no grupo de campos [!UICONTROL Detalhes de interação do MediaAnalytics]. Para melhorar a legibilidade na interface do usuário do Experience Platform, siga as instruções na [documentação do Media Analytics sobre como ocultar campos não utilizados](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html#set-up-the-schema-in-adobe-experience-platform).

<!-- 
>[!NOTE]
>
>Schemas contain fields that are not used in every context or situation. They provide a potential blueprint to map an object. Schemas displayed for the Media Edge API Collection or Reporting data types only portray the relevant fields. You can manually select and deselect the fields that you want to use if you intend to use a schema for the Media Edge API interaction. You can find instructions on [hiding unnecessary fields](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html#set-up-the-schema-in-adobe-experience-platform) in the guide to install Media Analytics with Experience Platform Edge.
 -->
