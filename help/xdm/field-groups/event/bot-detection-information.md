---
title: Grupo de campos de detecção de bot
description: Saiba mais sobre o grupo de campos Detecção de bot (XDM), grupo de campos de esquema.
exl-id: 8ade14a8-9a34-4060-95b2-812d1a21deeb
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 7%

---

# Grupo de campos [!UICONTROL Detecção de bot]

[!UICONTROL Detecção de bot] é um grupo de campos de esquema padrão para a [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). O grupo de campos fornece informações sobre o tráfego gerado por bots.

![Um diagrama do grupo de campos [!UICONTROL Detecção de bot].](../../images/field-groups/bot-detection-information.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|----------------------------|-----------------|-----------|---------------------------------------------------------|
| [!UICONTROL Detecção de bot] | `botDetection` | objeto | Fornece informações sobre o tráfego gerado por bot. |
| [!UICONTROL Pontuação] | `score` | número | A pontuação de probabilidade de bot de zero a um. Uma pontuação de zero significa que o tráfego não é um bot. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.schema.json)
