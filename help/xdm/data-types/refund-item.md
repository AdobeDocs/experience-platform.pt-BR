---
title: Tipo de Dados do Item de Reembolso
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência (XDM) do item de reembolso.
exl-id: 9968d314-c6f3-49d9-b860-709d7478c43a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 8%

---

# Tipo de dados [!UICONTROL Item de reembolso]

[!UICONTROL Item de Reembolso] é um tipo de dados padrão do Experience Data Model (XDM) que descreve as informações de capturas relacionadas a um reembolso associado a um pedido.

![Um diagrama do tipo de dados Item de Restituição.](../images/data-types/refund-item.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|--------------------|-----------------------|-----------|---------------------------------------------------------------------------------------------------|
| [!UICONTROL ID da transação] | `transactionID` | sequência de caracteres | O identificador de transação exclusivo para este item de reembolso. |
| [!UICONTROL Valor de reembolso] | `refundAmount` | número | O valor da restituição. |
| [!UICONTROL Motivo do reembolso] | `refundReason` | sequência de caracteres | O motivo pelo qual um reembolso foi emitido. |
| [!UICONTROL Tipo de Pagamento de Reembolso] | `refundPaymentType` | sequência de caracteres | O método de pagamento deste pedido. Valores personalizados são permitidos. |
| [!UICONTROL Código de moeda] | `currencyCode` | sequência de caracteres | O código de moeda ISO 4217 usado para este item de reembolso. Por exemplo: &quot;USD&quot;, &quot;EUR&quot;. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.schema.json)
