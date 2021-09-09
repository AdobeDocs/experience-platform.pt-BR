---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, ExperienceEvent, campos, esquemas, Esquemas, Design de esquema, grupo de campos, grupo de campos, reserva, jantar;
title: Grupo de Campo Esquema de Reserva Dinâmica
description: Este documento fornece uma visão geral do grupo de campos de esquema Reserva de Dining.
source-git-commit: d230cfa9e74eb96aa44e8b83ca8f2306db4ba4ec
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 5%

---


# [!UICONTROL Grupo ] de campos Dining Reservationschema

[!UICONTROL A ] Reserva de jantar é um grupo de campo de esquema padrão da classe  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) usada para capturar informações relacionadas a uma reserva de jantar.

O grupo de campos é uma extensão do grupo de campos [!UICONTROL Detalhes da Reserva] e contém todos os mesmos campos em um único campo do tipo de objeto, `reservations`. Além desses campos genéricos, a [!UICONTROL Reserva de Dining] também inclui a matriz `diningReservations`. Essa matriz de objetos é usada para descrever uma ou mais reservas com propriedades específicas de restaurantes.

>[!NOTE]
>
>Este documento aborda os detalhes da matriz `diningReservations`. Para obter informações sobre os outros campos fornecidos no objeto `reservations`, consulte a [[!UICONTROL Referência do grupo de campos Detalhes da Reserva]](./reservation-details.md).

![Estrutura da reserva de jantar](../../images/field-groups/dining-reservation/structure.png)

## `diningReservations`

`diningReservations` é uma matriz de objetos que representa uma lista de reservas de jantar. Se um evento de reserva envolver reservas em vários restaurantes diferentes em horários diferentes do dia, por exemplo, essas reservas podem ser listadas como objetos individuais em `diningReservations` para um único evento.

A estrutura de cada objeto fornecido em `diningReservations` é fornecida abaixo.

![estrutura diningReservations](../../images/field-groups/dining-reservation/diningReservations.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `ID` | String | O número ou identificador da reserva. |
| `cancellation` | Número inteiro | Esse valor é capturado quando uma reserva é cancelada. |
| `confirmationNumber` | String | O número ou identificador de confirmação da reserva. |
| `created` | Número inteiro | Esse valor é capturado quando uma reserva é criada. |
| `cuisine` | Número inteiro | O tipo de cozinha do restaurante. |
| `currencyCode` | String | O código monetário ISO 4217 usado para fazer a compra. |
| `deliveryPartners` | String | Parceiros de delivery disponíveis no restaurante. |
| `diningOptions` | String | Opções de entrega e jantar disponíveis no restaurante. |
| `groupReservation` | Booleano | Indica se a reserva está sendo feita para um grupo. |
| `length` | Número inteiro | O número total de dias para a reserva. |
| `loyaltyID` | String | A ID do programa de fidelidade para o convidado listado na reserva. |
| `modification` | Número inteiro | Esse valor é capturado quando uma reserva é modificada. |
| `modificationDate` | DateTime | A hora em que a reserva foi modificada pela última vez. |
| `numberOfAdults` | Número inteiro | O número de adultos associado à reserva. |
| `numberOfChildren` | Número inteiro | O número de filhos associados à reserva. |
| `numberOfRooms` | Número inteiro | O número de salas associadas à reserva. |
| `partySize` | Número inteiro | O número de indivíduos na festa de jantar. |
| `priceCategory` | String | A categoria de preço da reserva que está sendo feita. |
| `purpose` | String | A finalidade da reserva, normalmente comercial ou pessoal. |
| `reservationTime` | DateTime | A hora para a qual a reserva de jantar é reservada. |
| `restaurantID` | String | Um identificador para o restaurante ou local de jantar. |
| `reservationStatus` | String | O status da reserva. |
| `specialOccasion` | Booleano | Indica se a reserva está a ser feita para uma ocasião especial. |
| `status` | Número inteiro | O status da reserva de jantar. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.schema.json)
