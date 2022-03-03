---
title: Grupo de campos do esquema Ações do cartão
description: Este documento fornece uma visão geral do grupo de campos Ações do cartão .
source-git-commit: eaea904ddda6b7ffee6f52cd4af897c2a8885714
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 8%

---

# [!UICONTROL Ações do cartão] grupo de campos de esquema

[!UICONTROL Ações do cartão] é um grupo de campos de esquema padrão para a variável [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). O grupo de campos fornece um único `personalFinances.cardActions` para um esquema, que captura detalhes sobre uma ação do cartão, como tipo de cartão, status de ativação e status de bloqueio.

![](../../images/field-groups/card-actions.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `cardActivated` | Número inteiro | Rastreia quando o cartão foi ativado com êxito. |
| `cardActivationStart` | Número inteiro | Rastreia quando o processo de ativação do cartão foi iniciado. |
| `cardCancelled` | Número inteiro | Rastreia quando um cartão foi cancelado. |
| `cardControlsLocked` | Número inteiro | Rastreia quando os controles de um cartão foram bloqueados. |
| `cardControlsUnlocked` | Número inteiro | Rastreia quando os controles de um cartão foram desbloqueados. |
| `cardID` | String | O identificador do cartão que está sendo ativado. Esse valor pode ser diferente do número do cartão. |
| `cardLocked` | Número inteiro | Rastreia quando um cartão foi bloqueado. |
| `cardOrderNew` | Número inteiro | Rastreia quando um cartão foi solicitado. |
| `cardOrderType` | String | O tipo de pedido de cartão associado a um evento de pedido de cartão. |
| `cardType` | String | O tipo de cartão. |
| `cardUnlocked` | Número inteiro | Rastreia quando um cartão foi desbloqueado. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte [repositório XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-card-actions.schema.json).
