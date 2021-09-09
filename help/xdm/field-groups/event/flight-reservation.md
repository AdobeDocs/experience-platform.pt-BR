---
keywords: Experience Platform; home; tópicos populares; esquema; Esquema; XDM; ExperienceEvent; campos; esquemas; Esquemas; Design de esquema; grupo de campos; grupo de campos; reserva; voo;
title: Grupo de Campos do Esquema de Reserva de Voo
description: Este documento fornece uma visão geral do grupo de campos de esquema Reserva de Voo.
source-git-commit: 295dc040f3af7342226e3d78d0ae21e73db58d57
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 4%

---


# [!UICONTROL Grupo de campos ] Reservationschema de voo

[!UICONTROL A ] Reserva de Voo é um grupo de campos de esquema padrão para a classe  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) usada para capturar informações relacionadas a uma reserva de voo.

O grupo de campos é uma extensão do grupo de campos [!UICONTROL Detalhes da Reserva] e contém todos os mesmos campos em um único campo do tipo de objeto, `reservations`. Além desses campos genéricos, [!UICONTROL Reserva de voo] também inclui a matriz `flightReservations`. Essa matriz de objetos é usada para descrever uma ou mais reservas com propriedades exclusivas para viagens aéreas.

>[!NOTE]
>
>Este documento aborda os detalhes da matriz `flightReservations`. Para obter informações sobre os outros campos fornecidos no objeto `reservations`, consulte a [[!UICONTROL Referência do grupo de campos Detalhes da Reserva]](./reservation-details.md).

![Estrutura da reserva de voo](../../images/field-groups/flight-reservation/structure.png)

## `flightReservations`

`flightReservations` é uma matriz de objetos que representa uma lista de reservas de voo. Se um evento de reserva envolver reservas para vários voos de conexão em uma viagem, por exemplo, essas reservas podem ser listadas como objetos individuais em `flightReservations` para um único evento.

A estrutura de cada objeto fornecido em `flightReservations` é fornecida abaixo.

![estrutura flightReservations](../../images/field-groups/flight-reservation/flightReservations.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `flightCheckIn` | Objeto | Captura detalhes sobre o check-in do voo. O objeto inclui as seguintes propriedades:<ul><li>`arrivalAirportCode`: (String) O código do aeroporto da cidade de chegada.</li><li>`boardingGroup`: (Cadeia de caracteres) O indicador específico da ordem de embarque da companhia aérea.</li><li>`checkInMethod`: (String) O método usado na verificação, como contador, online, quiosque ou autoatendimento.</li><li>`checkedBags`: (Número inteiro) O número de sacos verificados para o voo.</li><li>`checkedPassengers`: (Número inteiro) O número de passageiros registrados para o voo, se existirem vários passageiros para o mesmo número de reserva.</li><li>`confirmationNumber`: (String) O número ou identificador de confirmação da reserva.</li><li>`departureAirportCode`: (String) O código do aeroporto da cidade de partida.</li><li>`flightNumber`: (String) O número do voo para o voo que está sendo reservado.</li></ul> |
| `flightStatusSearch` | Objeto | Captura os detalhes retornados quando o status do voo é pesquisado. O objeto inclui as seguintes propriedades:<ul><li>`arrivalAirportCode`: (String) O código do aeroporto da cidade de chegada.</li><li>`boardingGroup`: (Cadeia de caracteres) O indicador específico da ordem de embarque da companhia aérea.</li><li>`departureAirportCode`: (String) O código do aeroporto da cidade de partida.</li><li>`departureDate`: (DateTime) A data de partida do voo reservado.</li><li>`flightNumber`: (String) O número do voo para o voo que está sendo reservado.</li><li>`searchCount`: (Número inteiro) O número de vezes que o status do voo reservado foi procurado.</li></ul> |
| `agentID` | String | O agente ou agente responsável pela reserva, se aplicável. |
| `aircraftID` | String | Um identificador para a aeronave. |
| `aircraftType` | String | O tipo de aeronave. |
| `arrivalAirportCode` | String | O código do aeroporto da cidade de chegada. |
| `arrivalDate` | DateTime | A data de chegada do voo que está sendo reservado. |
| `cancellation` | Número inteiro | Esse valor é capturado quando uma reserva é cancelada. |
| `confirmationNumber` | String | O número ou identificador de confirmação da reserva. |
| `created` | String | Esse valor é capturado quando uma reserva é criada. |
| `currencyCode` | String | O código monetário ISO 4217 usado para fazer a compra. |
| `departureAirportCode` | String | O código do aeroporto da cidade de partida. |
| `departureDate` | DateTime | A data de partida do voo reservado. |
| `fareClass` | String | A classe de tarifa do voo que está sendo reservada. |
| `flightNumber` | String | O número do voo que está sendo reservado. |
| `length` | Número inteiro | O número total de dias para a reserva. |
| `loyaltyID` | String | A ID do programa de fidelidade ou recompensas para o passageiro listado na reserva. |
| `modification` | Número inteiro | Esse valor é capturado quando uma reserva é modificada. |
| `modificationDate` | DateTime | A hora em que a reserva foi modificada pela última vez. |
| `numberOfAdults` | Número inteiro | O número de adultos associado à reserva. |
| `numberOfChildren` | Número inteiro | O número de filhos associados à reserva. |
| `passengerID` | String | Informações do passageiro associadas à reserva. |
| `purpose` | String | A finalidade da reserva, normalmente comercial ou pessoal. |
| `salesChannel` | String | O canal de vendas do qual a reserva foi registrada. |
| `securityScreening` | String | O tipo de rastreio de segurança a que o passageiro está sujeito. |
| `status` | String | O status da reserva de voo. |
| `ticketNumber` | String | O número ou identificador da reserva. |
| `tripType` | String | Indica se a reserva é para uma viagem unidirecional, uma viagem de ida e volta ou uma viagem multicidade. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.schema.json)
