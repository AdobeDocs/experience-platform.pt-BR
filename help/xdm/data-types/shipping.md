---
title: Tipo de dados de remessa
description: Saiba mais sobre o tipo de dados Modelo de dados da experiência de envio (XDM).
exl-id: c3a58e46-c80e-4896-b21c-47dc5a6c869b
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 18%

---

# Tipo de dados de [!UICONTROL Remessa]

[!UICONTROL Remessa] é um tipo de dados padrão do Experience Data Model (XDM) que fornece detalhes relacionados à remessa de um ou mais produtos. Ele inclui detalhes sobre a logística e as especificidades relacionadas à entrega de itens solicitados.


![Um diagrama do tipo de dados [!UICONTROL Envio].](../images/data-types/shipping.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|----------------------|-----------------------|-----------|------------------------------------------------------|
| [!UICONTROL Método de envio] | `shippingMethod` | sequência de caracteres | O método de envio escolhido pelo cliente. |
| [!UICONTROL Valor da remessa] | `shippingAmount` | número | O valor que o cliente teve de pagar pelo envio. |
| [!UICONTROL Código de moeda] | `currencyCode` | sequência de caracteres | O código alfabético de moeda ISO 4217 usado para definir o preço do produto. |
| [!UICONTROL Destino de envio] | `shippingDestination` | sequência de caracteres | O destino de entrega especificado pelo usuário (por exemplo, início, armazenamento etc.). |
| [!UICONTROL Data de envio] | `shipDate` | sequência de caracteres | A data em que um ou mais itens de uma ordem são entregues. |
| [!UICONTROL Endereço de entrega] | `address` | [[!UICONTROL endereço]](./address.md) | O endereço de entrega. |
| [!UICONTROL Número de Acompanhamento] | `trackingNumber` | número | O número de rastreamento fornecido pela transportadora. |
| [!UICONTROL URL de Acompanhamento] | `trackingURL` | sequência de caracteres | O URL para rastrear o status de envio de um item do pedido. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json)
