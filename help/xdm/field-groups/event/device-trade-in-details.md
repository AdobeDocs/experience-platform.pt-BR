---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;ExperienceEvent;campos;esquemas;Esquemas;Design de esquema;grupo de campos;grupo de campos;dispositivo;troca;troca;troca;
solution: Experience Platform
title: Grupo de Campos de Esquema de Detalhes de Trade-In do Dispositivo
description: Saiba mais sobre o grupo de campos do esquema Detalhes de troca do dispositivo.
exl-id: 744557be-0297-453f-9134-9d0f4ef2df4d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 4%

---

# [!UICONTROL Detalhes de troca do dispositivo] grupo de campos de esquema

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento em [atualizações de nome de grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL Detalhes de troca do dispositivo] é um grupo de campos de esquema padrão para a [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Ele fornece um único campo (`deviceTradeInDetails`) que descreve uma transação de troca do dispositivo, incluindo o valor de troca, a ID do dispositivo original e a ID do novo dispositivo.

![Estrutura de Detalhes de Troca de Dispositivo](../../images/field-groups/device-trade-in-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `tradeInValue` | [Moeda](../../data-types/currency.md) | O valor do dispositivo sendo negociado. |
| `newDeviceID` | String | A ID do novo dispositivo que está sendo negociado. |
| `originalDeviceID` | String | A ID do dispositivo que está sendo negociado. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.schema.json)
