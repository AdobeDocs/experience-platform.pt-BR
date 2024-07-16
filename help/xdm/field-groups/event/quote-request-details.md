---
title: Grupo de Campos de Esquema de Detalhes da Solicitação de Cotação
description: Saiba mais sobre o grupo de campos de esquema Detalhes da solicitação de cotação.
exl-id: 19be76fa-d212-4b00-815a-d3869c1054e2
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 6%

---

# [!UICONTROL Detalhes da Solicitação de Cotação] grupo de campos de esquema

[!UICONTROL Detalhes da Solicitação de Cotação] é um grupo de campos de esquema padrão para a [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). O grupo de campos fornece um único objeto `quotes` para um esquema, que captura os detalhes do processo de solicitação para vários tipos de cotações, incluindo apólices de seguro, saúde, pedidos de fabricação e pedidos de alta tecnologia.

![](../../images/field-groups/quote-request-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `discount` | [[!UICONTROL Moeda]](../../data-types/currency.md) | O valor do desconto para uma cotação exibida a um visitante. |
| `premium` | [[!UICONTROL Moeda]](../../data-types/currency.md) | O valor do prêmio para uma cotação exibida a um visitante. |
| `location` | [!UICONTROL String] | O código postal usado para localizar varejistas próximos à localização do visitante. |
| `requestID` | [!UICONTROL String] | Um identificador exclusivo para a solicitação de cotação. |
| `selectedRetailer` | [!UICONTROL String] | O varejista selecionado para a solicitação de cotação, se aplicável. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-quote-request-details.schema.json).
