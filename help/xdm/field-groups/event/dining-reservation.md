---
keywords: Experience Platform;casa;tópicos populares;esquema;Esquema;XDM;ExperienceEvent;campos;esquemas;Esquemas;Design de esquema;grupo de campos;grupo de campos;reserva;jantar;
title: Grupo de Campos de Esquema para Reserva de Jantar
description: Saiba mais sobre o grupo de campos Esquema de reserva de jantar.
exl-id: 672b7a77-c433-4502-a1ad-a17c811b253e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 13%

---

# Grupo de campos de esquema [!UICONTROL Reserva de jantar]

A [!UICONTROL Reserva para o Jantar] é um grupo de campos de esquema padrão para a [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) usada para capturar informações sobre uma reserva de jantar.

O grupo de campos é uma extensão do grupo de campos [!UICONTROL Detalhes da Reserva] e contém todos os mesmos campos em um único campo de tipo de objeto, `reservations`. Além desses campos genéricos, a [!UICONTROL Reserva de Jantar] também inclui a matriz `diningReservations`. Esta matriz de objetos é usada para descrever uma ou mais reservas com propriedades específicas do restaurante.

>[!NOTE]
>
>Este documento aborda os detalhes da matriz `diningReservations`. Para obter informações sobre os outros campos fornecidos sob o objeto `reservations`, consulte a [[!UICONTROL Referência do grupo de campos Detalhes da reserva]](./reservation-details.md).

![Estrutura de Reserva de Jantar](../../images/field-groups/dining-reservation/structure.png)

## `diningReservations`

`diningReservations` é uma matriz de objetos que representa uma lista de reservas de jantar. Se um evento de reserva envolve reservas em vários restaurantes diferentes em diferentes horários do dia, por exemplo, essas reservas podem ser listadas como objetos individuais em `diningReservations` para um único evento.

A estrutura de cada objeto fornecido em `diningReservations` é fornecida abaixo.

![Estrutura de reservas de jantar](../../images/field-groups/dining-reservation/diningReservations.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `ID` | String | O número ou identificador da reserva. |
| `cancellation` | Número inteiro | Esse valor é capturado quando uma reserva é cancelada. |
| `confirmationNumber` | String | O número ou identificador de confirmação de reserva. |
| `created` | Número inteiro | Esse valor é capturado quando uma reserva é criada. |
| `cuisine` | Número inteiro | O tipo de cozinha do restaurante. |
| `currencyCode` | String | O código de moeda ISO 4217 usado para fazer a compra. |
| `deliveryPartners` | String | Parceiros de entrega disponíveis no restaurante. |
| `diningOptions` | String | Delivery e opções de refeições disponíveis no restaurante. |
| `groupReservation` | Booleano | Indica se a reserva está sendo feita para um grupo. |
| `length` | Número inteiro | O número total de dias da reserva. |
| `loyaltyID` | String | A ID do programa de fidelidade do convidado listado na reserva. |
| `modification` | Número inteiro | Esse valor é capturado quando uma reserva é modificada. |
| `modificationDate` | DateTime | A hora em que a reserva foi modificada pela última vez. |
| `numberOfAdults` | Número inteiro | O número de adultos associados à reserva. |
| `numberOfChildren` | Número inteiro | O número de filhos associado à reserva. |
| `numberOfRooms` | Número inteiro | O número de quartos associado à reserva. |
| `partySize` | Número inteiro | O número de indivíduos no jantar. |
| `priceCategory` | String | A categoria de preço para a reserva que está sendo feita. |
| `purpose` | String | O objetivo da reserva, normalmente comercial ou pessoal. |
| `reservationTime` | DateTime | O horário para o qual a reserva do jantar é feita. |
| `restaurantID` | String | Um identificador para o restaurante ou local da refeição. |
| `reservationStatus` | String | O status da reserva. |
| `specialOccasion` | Booleano | Indica se a reserva está sendo feita para uma ocasião especial. |
| `status` | Número inteiro | O status da reserva para o jantar. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.schema.json)
