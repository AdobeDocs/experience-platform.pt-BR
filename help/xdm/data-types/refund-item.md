---
title: Tipo de Dados do Item de Reembolso
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência (XDM) do item de reembolso.
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 8%

---

# [!UICONTROL Item de reembolso] tipo de dados

[!UICONTROL Item de reembolso] é um tipo de dados padrão do Experience Data Model (XDM) que descreve informações de capturas relacionadas a um reembolso associado a um pedido.

![Um diagrama do tipo de dados Item de Restituição.](../images/data-types/refund-item.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|--------------------|-----------------------|-----------|---------------------------------------------------------------------------------------------------|
| [!UICONTROL ID da transação] | `transactionID` | string | O identificador de transação exclusivo para este item de reembolso. |
| [!UICONTROL Valor do reembolso] | `refundAmount` | number | O valor da restituição. |
| [!UICONTROL Motivo do reembolso] | `refundReason` | string | O motivo pelo qual um reembolso foi emitido. |
| [!UICONTROL Tipo de Pagamento de Reembolso] | `refundPaymentType` | string | O método de pagamento deste pedido. Valores personalizados são permitidos. |
| [!UICONTROL Código de moeda] | `currencyCode` | string | O código de moeda ISO 4217 usado para este item de reembolso. Por exemplo: &quot;USD&quot;, &quot;EUR&quot;. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.schema.json)
