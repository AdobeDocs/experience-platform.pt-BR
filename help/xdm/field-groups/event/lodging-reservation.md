---
keywords: Experience Platform;início;tópicos populares;esquema;Esquema;XDM;ExperienceEvent;campos;esquemas;Esquemas;Design de esquema;grupo de campos;grupo de campos;reserva;hospedagem;
title: Grupo de Campos de Esquema de Reserva de Hospedagem
description: Este documento fornece uma visão geral do grupo de campos do esquema de Reserva de Hospedagem.
exl-id: f0eafc83-21f1-483d-9397-1133e3777699
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 5%

---

# [!UICONTROL Reserva de acomodação] grupo de campos de esquema

[!UICONTROL Reserva de acomodação] é um grupo de campos de esquema padrão para o [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) usado para registrar informações sobre uma reserva de hospedagem.

O grupo de campos é uma extensão do [!UICONTROL Detalhes da reserva] grupo de campos, e contém todos os mesmos campos sob um único campo de tipo de objeto, `reservations`. Além desses campos genéricos, [!UICONTROL Reserva de acomodação] também inclui `lodgingReservations` matriz. Essa matriz de objetos é usada para descrever uma ou mais reservas com propriedades exclusivas de hospedagem.

>[!NOTE]
>
>Este documento abrange os detalhes da `lodgingReservations` matriz. Para obter informações sobre os outros campos fornecidos no `reservations` objeto, consulte o [[!UICONTROL Detalhes da reserva] referência do grupo de campos](./reservation-details.md).

![Estrutura de reserva de hospedagem](../../images/field-groups/lodging-reservation/structure.png)

## `lodgingReservations`

`lodgingReservations` é uma matriz de objetos que representa uma lista de reservas de hospedagem. Se um evento de reserva envolve reservas em vários hotéis diferentes ao longo da rota de uma viagem, por exemplo, essas reservas podem ser listadas como objetos individuais em `lodgingReservations` por um único evento.

A estrutura de cada objeto fornecido em `lodgingReservations` é fornecido abaixo.

![Estrutura lodgingReservations](../../images/field-groups/lodging-reservation/lodgingReservations.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `averageDailyPrice` | [[!UICONTROL Moeda]](../../data-types/currency.md) | O preço médio diário do quarto de hotel. |
| `lodgingCheckIn` | Objeto | Um objeto que descreve os detalhes do check-in da hospedagem. Inclui os seguintes valores:<ul><li>`digitalKey`: (Número inteiro) indica quando um convidado seleciona o uso de uma chave digital ao fazer check-in.</li><li>`earlyCheckInRequested`: (Número inteiro) indica quando um convidado solicita o check-in antes do horário normal.</li><li>`lateCheckInRequested`: (Número inteiro) indica quando um convidado solicita o check-in após o horário normal.</li><li>`noRoomCheckIn`: (Número inteiro) Esse valor é capturado quando um convidado conclui o check-in quando não há salas disponíveis no momento.</li><li>`oneRoomCheckIn`: (Número inteiro) Esse valor é capturado quando um convidado termina o check-in quando há apenas um quarto disponível no momento.</li><li>`roomKeys`: (número inteiro) o número de chaves padrão do quarto fornecidas no check-in.</li><li>`userSelectedRoom`: (Booleano) Indica se o hóspede escolheu o quarto no check-in.</li></ul> |
| `rackrate` | [[!UICONTROL Moeda]](../../data-types/currency.md) | O custo de uma reserva no mesmo dia sem acordo prévio de reserva. |
| `ID` | String | O número ou identificador da reserva. |
| `agentID` | String | A ID do agente associada à reserva de hotel. |
| `basePrice` | String | O preço base antes da adição de descontos. |
| `bookingID` | String | A ID da reserva associada à reserva de hotel. |
| `cancellation` | Número inteiro | Esse valor é capturado quando uma reserva é cancelada. |
| `checkInDate` | DateTime | A data de check-in da reserva do quarto. |
| `checkOutDate` | DateTime | A data de check-out da reserva do quarto. |
| `confirmationNumber` | String | O número ou identificador de confirmação de reserva. |
| `couponCode` | String | Um código de cupom associado à reserva de hotel. |
| `created` | Número inteiro | Esse valor é capturado quando uma reserva é criada. |
| `currencyCode` | String | O código de moeda ISO 4217 usado para fazer a compra. |
| `discountPercent` | Duplo | A porcentagem de desconto associada à reserva. |
| `freeCancelation` | Booleano | Indica se o quarto tem uma política de cancelamento gratuito. |
| `guestID` | String | A ID do hóspede associada à reserva de hotel. |
| `length` | Número inteiro | O número total de dias da reserva. |
| `loyaltyID` | String | A ID do programa de fidelidade do convidado listado na reserva. |
| `modification` | Número inteiro | Esse valor é capturado quando uma reserva é modificada. |
| `modificationDate` | DateTime | A hora em que a reserva foi modificada pela última vez. |
| `numberOfAdults` | Número inteiro | O número de adultos associados à reserva. |
| `numberOfChildren` | Número inteiro | O número de filhos associado à reserva. |
| `numberOfRooms` | Número inteiro | O número de quartos associado à reserva. |
| `propertyID` | String | Um identificador do hotel ou resort da reserva. |
| `propertyName` | String | O nome do hotel ou resort da reserva. |
| `purpose` | String | O objetivo da reserva, normalmente comercial ou pessoal. |
| `ratePlan` | String | A tarifa em que o quarto foi vendido. |
| `refundable` | Booleano | Indica se o quarto é reembolsável. |
| `reservationStatus` | String | O status da reserva. |
| `roomAccessibilityType` | String | O tipo de acessibilidade da sala, como mobilidade, audição ou outro. |
| `roomCapacity` | Número inteiro | O número de pessoas que o quarto de hotel comporta. |
| `roomType` | String | O tipo de quarto que está sendo reservado. |
| `smoking` | Booleano | Indica se o quarto permite fumar. |
| `tripType` | String | Indica se a reserva é para uma viagem só de ida, ida e volta ou uma viagem em várias cidades. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.schema.json)
