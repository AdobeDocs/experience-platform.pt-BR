---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, ExperienceEvent, campos, esquemas, Esquemas, Design de esquema, grupo de campos, grupo de campos, dispositivo, transação, troca, troca, troca;
solution: Experience Platform
title: Grupo de Campos do Esquema de Detalhes de Entrada do Dispositivo
topic-legacy: overview
description: Este documento fornece uma visão geral do grupo de campos Detalhes de Comércio do Dispositivo.
source-git-commit: 2592d4f494d4d3dcfba63eb539498416fbdf6707
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 4%

---

# [!UICONTROL Grupo de campos ] Detalhes do Trade-In do Dispositivo

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento em [atualizações do nome do grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL Os detalhes de trade-in do dispositivo ] são um grupo de campos de esquema padrão para a  [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Ele fornece um único campo (`deviceTradeInDetails`) que descreve uma transação de troca de dispositivo, incluindo valor de troca, ID do dispositivo original e nova ID do dispositivo.

![Estrutura de detalhes de troca de dispositivo](../../images/field-groups/device-trade-in-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `tradeInValue` | [Moeda](../../data-types/currency.md) | O valor do dispositivo que está sendo trocado. |
| `newDeviceID` | String | A ID do novo dispositivo para o qual está sendo trocado. |
| `originalDeviceID` | String | A ID do dispositivo que está sendo trocado. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.schema.json)
