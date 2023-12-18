---
title: Tipo de dados de remessa
description: Saiba mais sobre o tipo de dados Modelo de dados da experiência de envio (XDM).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 6%

---

# [!UICONTROL Envio] tipo de dados

[!UICONTROL Envio] é um tipo de dados padrão do Experience Data Model (XDM) que fornece detalhes relacionados ao envio de um ou mais produtos. Ele inclui detalhes sobre a logística e as especificidades relacionadas à entrega de itens solicitados.


![Um diagrama do [!UICONTROL Envio] tipo de dados.](../images/data-types/shipping.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|----------------------|-----------------------|-----------|------------------------------------------------------|
| [!UICONTROL Método de envio] | `shippingMethod` | string | O método de envio escolhido pelo cliente. |
| [!UICONTROL Valor da remessa] | `shippingAmount` | number | O valor que o cliente teve de pagar pelo envio. |
| [!UICONTROL Código de moeda] | `currencyCode` | string | O código alfabético de moeda ISO 4217 usado para definir o preço do produto. |
| [!UICONTROL Destino de envio] | `shippingDestination` | string | O destino de entrega especificado pelo usuário (por exemplo, início, armazenamento etc.). |
| [!UICONTROL Data de envio] | `shipDate` | string | A data em que um ou mais itens de uma ordem são entregues. |
| [!UICONTROL Endereço de entrega] | `address` | [[!UICONTROL endereço]](./address.md) | O endereço de entrega. |
| [!UICONTROL Número de Acompanhamento] | `trackingNumber` | number | O número de rastreamento fornecido pela transportadora. |
| [!UICONTROL URL de rastreamento] | `trackingURL` | string | O URL para rastrear o status de envio de um item do pedido. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json)
