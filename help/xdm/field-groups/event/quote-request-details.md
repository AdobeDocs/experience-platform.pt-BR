---
title: Grupo de Campos de Esquema de Detalhes da Solicitação de Cotação
description: Este documento fornece uma visão geral do grupo de campos de esquema Detalhes da Solicitação de Cotação.
exl-id: 19be76fa-d212-4b00-815a-d3869c1054e2
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 4%

---

# [!UICONTROL Detalhes da solicitação de orçamento] grupo de campos de esquema

[!UICONTROL Detalhes da solicitação de orçamento] é um grupo de campos de esquema padrão para o [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). O grupo de campos fornece um único `quotes` faça objeto a um esquema, que captura os detalhes do processo de solicitação para vários tipos de cotações, incluindo apólices de seguro, saúde, pedidos de fabricação e pedidos de alta tecnologia.

![](../../images/field-groups/quote-request-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `discount` | [[!UICONTROL Moeda]](../../data-types/currency.md) | O valor do desconto para uma cotação exibida a um visitante. |
| `premium` | [[!UICONTROL Moeda]](../../data-types/currency.md) | O valor do prêmio para uma cotação exibida a um visitante. |
| `location` | [!UICONTROL String] | O código postal usado para localizar varejistas próximos à localização do visitante. |
| `requestID` | [!UICONTROL String] | Um identificador exclusivo para a solicitação de cotação. |
| `selectedRetailer` | [!UICONTROL String] | O varejista selecionado para a solicitação de cotação, se aplicável. |

{style="table-layout:auto"}

Para obter mais informações sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-quote-request-details.schema.json).
