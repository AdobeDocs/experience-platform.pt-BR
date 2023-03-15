---
keywords: Experience Platform;casa;tópicos populares;esquema;Esquema;XDM;ExperienceEvent;campos;esquemas;Esquemas;Design de esquema;grupo de campos;grupo de campos;reserva;jantar;
title: Grupo de Campos de Esquema para Reserva de Jantar
description: Este documento fornece uma visão geral do grupo de campos do esquema Reserva de jantar.
exl-id: 672b7a77-c433-4502-a1ad-a17c811b253e
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 5%

---

# [!UICONTROL Reserva para o jantar] grupo de campos de esquema

[!UICONTROL Reserva para o jantar] é um grupo de campos de esquema padrão para o [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) usado para registrar informações sobre uma reserva de jantar.

O grupo de campos é uma extensão do [!UICONTROL Detalhes da reserva] grupo de campos, e contém todos os mesmos campos sob um único campo de tipo de objeto, `reservations`. Além desses campos genéricos, [!UICONTROL Reserva para o jantar] também inclui `diningReservations` matriz. Esta matriz de objetos é usada para descrever uma ou mais reservas com propriedades específicas do restaurante.

>[!NOTE]
>
>Este documento abrange os detalhes da `diningReservations` matriz. Para obter informações sobre os outros campos fornecidos no `reservations` objeto, consulte o [[!UICONTROL Detalhes da reserva] referência do grupo de campos](./reservation-details.md).

![Estrutura de reserva para o jantar](../../images/field-groups/dining-reservation/structure.png)

## `diningReservations`

`diningReservations` é uma matriz de objetos que representa uma lista de reservas de jantar. Se um evento de reserva envolver reservas em vários restaurantes diferentes em diferentes horários do dia, por exemplo, essas reservas podem ser listadas como objetos individuais em `diningReservations` por um único evento.

A estrutura de cada objeto fornecido em `diningReservations` é fornecido abaixo.

![estrutura jantarreservas](../../images/field-groups/dining-reservation/diningReservations.png)

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
