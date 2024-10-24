---
title: Tipo de dados das informações do evento de mídia
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência (XDM) de informações de evento de mídia.
exl-id: 91bb7f28-b629-4044-b687-768c545ac8a2
source-git-commit: b81afb8f6c4eaedb19a58b6fe3896286f1486804
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 5%

---

# [!UICONTROL Tipo de dados de Informações sobre o Evento de Mídia]

[!UICONTROL Informações de Evento de Mídia] é um tipo de dados padrão do Experience Data Model (XDM) que descreve as informações de detalhes de mídia relacionadas ao evento de experiência.

![Um diagrama do tipo de dados Informações do Evento de Mídia.](../images/data-types/media-event-information.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `mediaCollection` | [!UICONTROL detalhesDaMídia] | Informações detalhadas da mídia relacionadas ao evento de experiência. Este tipo de dados é usado para [coleta de dados de mídia](./media-collection-details.md) e [relatório de dados de mídia](./media-reporting-details.md). |
| `mediaEventTimestamp` | [!UICONTROL String] | A hora em que um evento de mídia ocorreu. |
| `mediaEventType` | [!UICONTROL String] | O tipo de evento de mídia. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/mediaevent.schema.json)
