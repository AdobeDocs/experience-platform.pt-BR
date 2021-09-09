---
keywords: Experience Platform; home; tópicos populares; esquema; Esquema; XDM; ExperienceEvent; campos; esquemas; Esquemas; Design de esquema; grupo de campos; grupo de campos; reserva; detalhes de reserva;
title: Detalhes da Reserva Grupo de Campos do Esquema
description: Este documento fornece uma visão geral do grupo de campos Detalhes da reserva .
source-git-commit: 295dc040f3af7342226e3d78d0ae21e73db58d57
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 5%

---


# [!UICONTROL Grupo de campos ] Detalhes da reserva

[!UICONTROL Reserva ] Detalhes é um grupo de campo de esquema padrão para a classe  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) usada para capturar informações relacionadas a uma reserva, incluindo comprimento, modificação, status reembolsável e número de salas.

O grupo de campos fornece um único campo do tipo objeto, `reservations`. As propriedades contidas nesse objeto são explicadas abaixo.

![Estrutura de Detalhes da Reserva](../../images/field-groups/reservation-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `nonRefundableAmount` | [Moeda](../../data-types/currency.md) | A quantia do preço da reserva que é marcada como não reembolsável. |
| `transaction` | [Transação](../../data-types/transaction.md) | Descreve a transação de moeda para a reserva. |
| `id` | String | Um identificador exclusivo para a reserva. |
| `cancellation` | Número inteiro | Esse valor é capturado quando uma reserva é cancelada. |
| `confirmationNumber` | String | O número ou identificador de confirmação da reserva. |
| `created` | Número inteiro | Esse valor é capturado quando a reserva é criada. |
| `currencyCode` | String | O código monetário ISO 4217 usado para fazer a compra. |
| `endDate` | DateTime | A data de desistência, retorno ou check-out final da reserva. |
| `length` | Número inteiro | O número total de dias para a reserva. |
| `modification` | Número inteiro | Esse valor é capturado quando uma reserva é modificada. |
| `modificationDate` | DateTime | A hora em que a reserva foi modificada pela última vez. |
| `numberOfAdults` | Número inteiro | O número de adultos associado à reserva. |
| `numberOfChildren` | Número inteiro | O número de filhos associados à reserva. |
| `purpose` | String | A finalidade da reserva, normalmente comercial ou pessoal. |
| `startDate` | DateTime | A data de início da coleta, saída ou check-in da reserva. |
| `triptype` | String | Indica se a reserva é para uma viagem unidirecional, uma viagem de ida e volta ou uma viagem multicidade. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.schema.json)

## Grupos de campos de reserva específicos do setor

Há vários outros grupos de campos padrão que estendem o schema [!UICONTROL Detalhes da Reserva] para casos de uso específicos do setor. Consulte a seguinte documentação para obter mais detalhes:

* [[!UICONTROL Reserva de Jantar]](./dining-reservation.md)
* [[!UICONTROL Reserva de Voo]](./flight-reservation.md)
* [[!UICONTROL Reserva de Loja]](./lodging-reservation.md)