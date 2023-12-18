---
title: Grupo de campos de detecção de bot
description: Saiba mais sobre o grupo de campos Detecção de bot (XDM), grupo de campos de esquema.
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 4%

---

# [!UICONTROL Detecção de bot] grupo de campos

[!UICONTROL Detecção de bot] é um grupo de campos de esquema padrão para o [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). O grupo de campos fornece informações sobre o tráfego gerado por bots.

![Um diagrama do [!UICONTROL Detecção de bot] grupo de campos.](../../images/field-groups/bot-detection-information.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|----------------------------|-----------------|-----------|---------------------------------------------------------|
| [!UICONTROL Detecção de bot] | `botDetection` | objeto | Fornece informações sobre o tráfego gerado por bot. |
| [!UICONTROL Pontuação] | `score` | number | A pontuação de probabilidade de bot de zero a um. Uma pontuação de zero significa que o tráfego não é um bot. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.schema.json)

