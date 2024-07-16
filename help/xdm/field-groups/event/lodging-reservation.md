---
keywords: Experience Platform;início;tópicos populares;esquema;Esquema;XDM;ExperienceEvent;campos;esquemas;Esquemas;Design de esquema;grupo de campos;grupo de campos;reserva;hospedagem;
title: Grupo de Campos de Esquema de Reserva de Hospedagem
description: Saiba mais sobre o grupo de campos de esquema Reserva de Hospedagem.
exl-id: f0eafc83-21f1-483d-9397-1133e3777699
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 7%

---

# Grupo de campos de esquema [!UICONTROL Reserva de Hospedagem]

A [!UICONTROL Reserva de Hospedagem] é um grupo de campos de esquema padrão para a [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) usada para capturar informações sobre uma reserva de hospedagem.

O grupo de campos é uma extensão do grupo de campos [!UICONTROL Detalhes da Reserva] e contém todos os mesmos campos em um único campo de tipo de objeto, `reservations`. Além desses campos genéricos, a [!UICONTROL Reserva de Hospedagem] também inclui a matriz `lodgingReservations`. Essa matriz de objetos é usada para descrever uma ou mais reservas com propriedades exclusivas de hospedagem.

>[!NOTE]
>
>Este documento aborda os detalhes da matriz `lodgingReservations`. Para obter informações sobre os outros campos fornecidos sob o objeto `reservations`, consulte a [[!UICONTROL Referência do grupo de campos Detalhes da reserva]](./reservation-details.md).

![Estrutura de Reserva de Hospedagem](../../images/field-groups/lodging-reservation/structure.png)

## `lodgingReservations`

`lodgingReservations` é uma matriz de objetos que representa uma lista de reservas de hospedagem. Se um evento de reserva envolve reservas em vários hotéis diferentes ao longo da rota de uma viagem, por exemplo, essas reservas podem ser listadas como objetos individuais em `lodgingReservations` para um único evento.

A estrutura de cada objeto fornecido em `lodgingReservations` é fornecida abaixo.

![estrutura lodgingReservations](../../images/field-groups/lodging-reservation/lodgingReservations.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `averageDailyPrice` | [[!UICONTROL Moeda]](../../data-types/currency.md) | O preço médio diário do quarto de hotel. |
| `lodgingCheckIn` | Objeto | Um objeto que descreve os detalhes do check-in da hospedagem. Inclui os seguintes valores:<ul><li>`digitalKey`: (Inteiro) Indica quando um convidado seleciona o uso de uma chave digital ao fazer check-in.</li><li>`earlyCheckInRequested`: (Número Inteiro) Indica quando um convidado solicita o check-in antes do horário normal.</li><li>`lateCheckInRequested`: (Número Inteiro) Indica quando um convidado solicita o check-in após o horário normal.</li><li>`noRoomCheckIn`: (Inteiro) Este valor é capturado quando um convidado termina o check-in quando não há salas disponíveis no momento.</li><li>`oneRoomCheckIn`: (Integer) Este valor é capturado quando um convidado termina o check-in quando há apenas um quarto disponível no momento.</li><li>`roomKeys`: (Número inteiro) o número de chaves de quarto padrão fornecidas no check-in.</li><li>`userSelectedRoom`: (Booleano) Indica se o hóspede escolheu o quarto no check-in.</li></ul> |
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
