---
title: Detalhes da solicitação de cotação Grupo de campos do esquema
description: Este documento fornece uma visão geral do grupo de campos Detalhes da solicitação de cotação .
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 6%

---

# [!UICONTROL Detalhes da solicitação de cotação] grupo de campos de esquema

[!UICONTROL Detalhes da solicitação de cotação] é um grupo de campos de esquema padrão para a variável [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). O grupo de campos fornece um único `quotes` objeto de um esquema, que captura os detalhes do processo de solicitação para vários tipos de cotações, incluindo apólices de seguro, assistência médica, ordens de fabricação e ordens de alta tecnologia.

![](../../images/field-groups/quote-request-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `discount` | [[!UICONTROL Moeda]](../../data-types/currency.md) | A quantia de desconto de uma cotação exibida para um visitante. |
| `premium` | [[!UICONTROL Moeda]](../../data-types/currency.md) | O valor premium de uma cotação exibida para um visitante. |
| `location` | [!UICONTROL String] | O código postal usado para encontrar varejistas perto do local do visitante. |
| `requestID` | [!UICONTROL String] | Um identificador exclusivo para a solicitação de cotação. |
| `selectedRetailer` | [!UICONTROL String] | O varejista selecionado para a solicitação de cotação, se aplicável. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte [repositório XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-quote-request-details.schema.json).
