---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;ExperienceEvent;campos;esquemas;Esquemas;Design de esquema;grupo de campos;grupo de campos;reserva;detalhes da reserva;
title: Grupo de Campos de Esquema de Detalhes da Reserva
description: Este documento fornece uma visão geral do grupo de campos do esquema Detalhes da Reserva.
exl-id: 06f9ee37-9879-4db2-af68-9336366f7521
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 4%

---

# [!UICONTROL Detalhes da reserva] grupo de campos de esquema

[!UICONTROL Detalhes da reserva] é um grupo de campos de esquema padrão para o [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) usado para registrar informações sobre uma reserva, incluindo duração, modificação, status reembolsável e número de quartos.

O grupo de campos fornece um único campo do tipo objeto, `reservations`. As propriedades contidas nesse objeto são explicadas abaixo.

![Estrutura de detalhes da reserva](../../images/field-groups/reservation-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `nonRefundableAmount` | [Moeda](../../data-types/currency.md) | O valor do preço da reserva marcado como não reembolsável. |
| `transaction` | [Transação](../../data-types/transaction.md) | Descreve a transação de moeda da reserva. |
| `id` | String | Um identificador exclusivo para a reserva. |
| `cancellation` | Número inteiro | Esse valor é capturado quando uma reserva é cancelada. |
| `confirmationNumber` | String | O número de confirmação ou identificador da reserva. |
| `created` | Número inteiro | Esse valor é capturado quando a reserva é criada. |
| `currencyCode` | String | O código de moeda ISO 4217 usado para fazer a compra. |
| `endDate` | DateTime | A data final de devolução, entrega ou check-out da reserva. |
| `length` | Número inteiro | O número total de dias da reserva. |
| `modification` | Número inteiro | Esse valor é capturado quando uma reserva é modificada. |
| `modificationDate` | DateTime | A hora em que a reserva foi modificada pela última vez. |
| `numberOfAdults` | Número inteiro | O número de adultos associados à reserva. |
| `numberOfChildren` | Número inteiro | O número de filhos associado à reserva. |
| `purpose` | String | O objetivo da reserva, normalmente comercial ou pessoal. |
| `startDate` | DateTime | A data de início de retirada, saída ou check-in da reserva. |
| `triptype` | String | Indica se a reserva é para uma viagem só de ida, ida e volta ou uma viagem em várias cidades. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.schema.json)

## Grupos de campos de reserva específicos do setor

Há vários outros grupos de campos padrão que estendem a variável [!UICONTROL Detalhes da reserva] esquema para casos de uso específicos do setor. Consulte a seguinte documentação para obter mais detalhes:

* [[!UICONTROL Reserva para o jantar]](./dining-reservation.md)
* [[!UICONTROL Reserva de voo]](./flight-reservation.md)
* [[!UICONTROL Reserva de acomodação]](./lodging-reservation.md)
