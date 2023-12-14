---
title: Tipo de dados das informações do evento de mídia
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência (XDM) de informações de evento de mídia.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 6%

---

# [!UICONTROL Informações do evento de mídia] tipo de dados

[!UICONTROL Informações do evento de mídia] é um tipo de dados padrão do Experience Data Model (XDM) que descreve as informações de detalhes de mídia relacionadas ao evento de experiência.

![Um diagrama do tipo de dados Informações do evento de mídia.](../images/data-types/media-event-information.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `mediaCollection` | [[!UICONTROL mediaDetails]](./media-details-information.md) | Informações detalhadas da mídia relacionadas ao evento de experiência. |
| `mediaEventTimestamp` | [!UICONTROL String] | A hora em que um evento de mídia ocorreu. |
| `mediaEventType` | [!UICONTROL String] | O tipo de evento de mídia. |

{style="table-layout:auto"}

Para obter mais informações sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/mediaevent.schema.json)
