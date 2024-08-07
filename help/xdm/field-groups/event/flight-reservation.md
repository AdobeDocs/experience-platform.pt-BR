---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;ExperienceEvent;campos;esquemas;Esquemas;Design de esquema;grupo de campos;grupo de campos;reserva;voo;
title: Grupo de Campos de Esquema de Reserva de Voo
description: Saiba mais sobre o grupo de campos Esquema de reserva de voo.
exl-id: df4bb525-c2d3-4e1d-921f-903142a570ac
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 10%

---

# Grupo de campos de esquema [!UICONTROL Reserva de voo]

A [!UICONTROL Reserva de Voo] é um grupo de campos de esquema padrão para a [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) usada para registrar informações sobre uma reserva de voo.

O grupo de campos é uma extensão do grupo de campos [!UICONTROL Detalhes da Reserva] e contém todos os mesmos campos em um único campo de tipo de objeto, `reservations`. Além desses campos genéricos, a [!UICONTROL Reserva de Voo] também inclui a matriz `flightReservations`. Esta matriz de objetos é usada para descrever uma ou mais reservas com propriedades exclusivas da viagem aérea.

>[!NOTE]
>
>Este documento aborda os detalhes da matriz `flightReservations`. Para obter informações sobre os outros campos fornecidos sob o objeto `reservations`, consulte a [[!UICONTROL Referência do grupo de campos Detalhes da reserva]](./reservation-details.md).

![Estrutura de Reserva de Voo](../../images/field-groups/flight-reservation/structure.png)

## `flightReservations`

`flightReservations` é uma matriz de objetos que representa uma lista de reservas de voo. Se um evento de reserva envolve reservas para vários voos de conexão em uma viagem, por exemplo, essas reservas podem ser listadas como objetos individuais em `flightReservations` para um único evento.

A estrutura de cada objeto fornecido em `flightReservations` é fornecida abaixo.

![estrutura flightReservations](../../images/field-groups/flight-reservation/flightReservations.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `flightCheckIn` | Objeto | Registra detalhes sobre o check-in do voo. O objeto inclui as seguintes propriedades:<ul><li>`arrivalAirportCode`: (String) O código do aeroporto da cidade de chegada.</li><li>`boardingGroup`: (String) O indicador específico da linha aérea do pedido de embarque.</li><li>`checkInMethod`: (Cadeia de caracteres) O método usado para fazer check-in, como contador, online, quiosque ou autoatendimento.</li><li>`checkedBags`: (Número inteiro) o número de malas despachadas para o voo.</li><li>`checkedPassengers`: (Integer) O número de passageiros registrados para o voo, se houver vários passageiros para o mesmo número de reserva.</li><li>`confirmationNumber`: (Cadeia de caracteres) O número ou identificador de confirmação de reserva.</li><li>`departureAirportCode`: (String) O código do aeroporto da cidade de partida.</li><li>`flightNumber`: (Cadeia de caracteres) O número do voo que está sendo reservado.</li></ul> |
| `flightStatusSearch` | Objeto | Registra os detalhes retornados quando o status do voo é pesquisado. O objeto inclui as seguintes propriedades:<ul><li>`arrivalAirportCode`: (String) O código do aeroporto da cidade de chegada.</li><li>`boardingGroup`: (String) O indicador específico da linha aérea do pedido de embarque.</li><li>`departureAirportCode`: (String) O código do aeroporto da cidade de partida.</li><li>`departureDate`: (DateTime) A data de partida do voo que está sendo reservado.</li><li>`flightNumber`: (Cadeia de caracteres) O número do voo que está sendo reservado.</li><li>`searchCount`: (Número inteiro) O número de vezes que o status do voo reservado foi pesquisado.</li></ul> |
| `agentID` | String | O agente ou a agência responsável pela realização da reserva, se aplicável. |
| `aircraftID` | String | Um identificador da aeronave. |
| `aircraftType` | String | O tipo de aeronave. |
| `arrivalAirportCode` | String | O código do aeroporto da cidade de chegada. |
| `arrivalDate` | DateTime | A data de chegada do voo que está sendo reservado. |
| `cancellation` | Número inteiro | Esse valor é capturado quando uma reserva é cancelada. |
| `confirmationNumber` | String | O número ou identificador de confirmação de reserva. |
| `created` | String | Esse valor é capturado quando uma reserva é criada. |
| `currencyCode` | String | O código de moeda ISO 4217 usado para fazer a compra. |
| `departureAirportCode` | String | O código do aeroporto da cidade de partida. |
| `departureDate` | DateTime | A data de partida do voo que está sendo reservado. |
| `fareClass` | String | A classe de tarifa do voo que está sendo reservado. |
| `flightNumber` | String | O número do voo que está sendo reservado. |
| `length` | Número inteiro | O número total de dias da reserva. |
| `loyaltyID` | String | A ID do programa de fidelidade ou recompensa do passageiro listado na reserva. |
| `modification` | Número inteiro | Esse valor é capturado quando uma reserva é modificada. |
| `modificationDate` | DateTime | A hora em que a reserva foi modificada pela última vez. |
| `numberOfAdults` | Número inteiro | O número de adultos associados à reserva. |
| `numberOfChildren` | Número inteiro | O número de filhos associado à reserva. |
| `passengerID` | String | Informações do passageiro associadas à reserva. |
| `purpose` | String | O objetivo da reserva, normalmente comercial ou pessoal. |
| `salesChannel` | String | O canal de vendas do qual a reserva foi feita. |
| `securityScreening` | String | O tipo de triagem de segurança a que o passageiro está sujeito. |
| `status` | String | O status da reserva do voo. |
| `ticketNumber` | String | O número ou identificador da reserva. |
| `tripType` | String | Indica se a reserva é para uma viagem só de ida, ida e volta ou uma viagem em várias cidades. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.schema.json)
