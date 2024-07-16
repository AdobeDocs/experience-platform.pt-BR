---
keywords: Experience Platform;início;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;ordem;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de dados do pedido
description: Saiba mais sobre o tipo de dados do Order Experience Data Model (XDM).
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
source-git-commit: 09ca510da0819ab38687edadbcc632ccbbe8ef83
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 13%

---

# Tipo de dados [!UICONTROL Ordem]

[!UICONTROL Pedido] é um tipo de dados padrão do Experience Data Model (XDM) que descreve o pedido feito para uma lista de produtos.

![Um diagrama do tipo de dados [!UICONTROL Ordem].](../images/data-types/order.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|-------------------------|-------------------------|-----------|------------------------------------------------------------------------------------------------------------------|
| ID de compra | `purchaseID` | String | Um identificador exclusivo atribuído pelo vendedor para esta compra ou contrato. Não há garantia de que a ID seja exclusiva porque a ID é definida pelo vendedor. |
| Número do pedido de compra | `purchaseOrderNumber` | String | Um identificador exclusivo atribuído pelo comprador para esta compra ou contrato. |
| Lista de pagamentos | `payments` | Matriz de [[!UICONTROL Itens de Pagamento]](./payment-item.md) | A lista de pagamentos deste pedido. Os pagamentos são detalhados na especificação [!UICONTROL Itens de Pagamento]. |
| Lista de Reembolsos | `refunds` | Matriz de [[!UICONTROL Itens de Reembolso]](./refund-item.md) | A lista de reembolsos para este pedido. As restituições estão detalhadas na especificação [!UICONTROL Itens de reembolso]. |
| Informações de devolução | `returns` | [[!UICONTROL Informações de Retorno]](./return.md) | A RMA (Autorização para devolução de mercadoria) emitida. As devoluções estão detalhadas na especificação [!UICONTROL Informações de devolução]. |
| Currency | `currencyCode` | String | O código de moeda ISO 4217 usado para os totais do pedido. Exemplos incluem `USD` e `EUR`. Todas as instâncias devem corresponder ao padrão `^[A-Z]{3}$`. |
| Valor do imposto | `taxAmount` | Número | O valor do imposto pago pelo comprador como parte do pagamento final. |
| Valor do desconto | `discountAmount` | Número | A diferença entre o preço normal e o preço especial aplicado a todo o pedido, e não a produtos individuais. |
| Preço total | `priceTotal` | Número | O preço total deste pedido após a aplicação de todos os descontos e impostos. |
| Tipo de pedido | `orderType` | String | O tipo de pedido que foi feito. Os valores possíveis são `checkout` e `instant_purchase`. |
| Data da última atualização | `lastUpdatedDate` | String | A hora em que um determinado registro de pedido foi atualizado pela última vez no sistema de comércio. Format: date-time. |
| Data de criação | `createdDate` | String | A hora/data em que um novo pedido é criado no sistema de comércio. Format: date-time. |
| Data de cancelamento | `cancelDate` | String | A data/hora em que o cancelamento de um pedido é iniciado pelo comprador. Format: date-time. |
| Valor total reembolsado | `refundTotal` | Número | O valor total fornecido neste reembolso na ordem, combinando todos os itens reembolsados e após quaisquer descontos, etc. foram aplicadas. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
