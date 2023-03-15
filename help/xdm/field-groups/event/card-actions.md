---
title: Grupo de campos de esquema de ações do cartão
description: Este documento fornece uma visão geral do grupo de campos do esquema Ações do cartão.
exl-id: 49851544-9118-4b73-b1d1-4cf49b3f1dee
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 6%

---

# [!UICONTROL Ações do cartão] grupo de campos de esquema

[!UICONTROL Ações do cartão] é um grupo de campos de esquema padrão para o [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). O grupo de campos fornece um único `personalFinances.cardActions` para um esquema, que captura detalhes sobre a ação de um cartão, como tipo de cartão, status de ativação e status de bloqueio.

![](../../images/field-groups/card-actions.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `cardActivated` | Número inteiro | Rastreia quando o cartão é ativado com sucesso. |
| `cardActivationStart` | Número inteiro | Rastreia quando o processo de ativação do cartão foi iniciado. |
| `cardCancelled` | Número inteiro | Rastreia quando um cartão é cancelado. |
| `cardControlsLocked` | Número inteiro | Rastreia quando os controles de um cartão foram bloqueados. |
| `cardControlsUnlocked` | Número inteiro | Rastreia quando os controles de um cartão foram desbloqueados. |
| `cardID` | String | O identificador do cartão que está sendo ativado. Esse valor pode ser diferente do número do cartão. |
| `cardLocked` | Número inteiro | Rastreia quando um cartão é bloqueado. |
| `cardOrderNew` | Número inteiro | Rastreia quando um cartão é solicitado. |
| `cardOrderType` | String | O tipo de ordem de cartão associado a um evento de ordem de cartão. |
| `cardType` | String | O tipo de cartão. |
| `cardUnlocked` | Número inteiro | Rastreia quando um cartão é desbloqueado. |

{style="table-layout:auto"}

Para obter mais informações sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-card-actions.schema.json).
