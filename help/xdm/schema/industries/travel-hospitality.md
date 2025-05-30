---
solution: Experience Platform
title: ERD do modelo de dados do setor de viagem e hospitalidade
description: Visualize um diagrama de relacionamento de entidade (ERD) que descreve um modelo de dados padronizado para o setor de viagem e hospitalidade, compatível com o Experience Data Model (XDM) para uso no Adobe Experience Platform.
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# [!UICONTROL Viagens e hospitalidade] ERD de modelo de dados do setor

O diagrama de relacionamento de entidade (ERD) a seguir representa um modelo de dados padronizado para o setor de viagens e hospitalidade. O ERD é intencionalmente apresentado de forma desnormalizada e considerando a forma como os dados são armazenados no Adobe Experience Platform.

>[!NOTE]
>
>O ERD, conforme descrito, é uma recomendação sobre como você deve modelar seus dados para esse caso de uso do setor. Para usar esse modelo de dados no Experience Platform, você deve criar os esquemas recomendados e seus relacionamentos sozinho. Consulte os guias sobre gerenciamento de [esquemas](../../ui/resources/schemas.md) e [relações](../../tutorials/relationship-ui.md) na interface do usuário para obter mais informações.

Use a seguinte legenda para interpretar este ERD:

* Cada entidade mostrada no é baseada em uma [classe do Experience Data Model (XDM)](../composition.md#class) subjacente.
* Os campos recuados em um campo pai representam um campo filho, ou subcampo, que pertence ao grupo de campos do pai.
* Os campos mais importantes para uma determinada entidade são destacados em vermelho.
* Todas as propriedades que poderiam ser usadas para identificar clientes individuais são marcadas como &quot;identidade&quot;, com uma dessas propriedades marcada como &quot;identidade principal&quot;.
* Os relacionamentos de entidade são marcados como não dependentes, já que os eventos baseados em cookies geralmente não podem determinar a pessoa ou indivíduo que fez a transação.

![Um exemplo de ERD para um modelo de dados de hospitalidade em viagem](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>A entidade Evento de experiência inclui um campo &quot;_ID&quot;, que representa o atributo de identificador exclusivo (`_id`) fornecido pela classe XDM ExperienceEvent. Consulte o documento de referência em [XDM ExperienceEvent](../../classes/experienceevent.md) para obter mais detalhes sobre o que é esperado para esse valor.

## [!UICONTROL Casos de uso de viagem e hospitalidade]

A tabela a seguir descreve as classes e os grupos de campos de esquema recomendados para vários casos de uso comuns no setor de viagem e hospitalidade.

| Caso de uso | Classes e grupos de campos recomendados |
| --- | --- |
| Venda cruzada de restaurantes e outras atrações residentes para hóspedes e hóspedes com reservas de hotel em breve. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Detalhes da reserva](../../field-groups/event/reservation-details.md)</li><li>[Reserva de hospedagem](../../field-groups/event/lodging-reservation.md)</li><li>[Reserva para o jantar](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[Perfil Individual XDM](../../classes/individual-profile.md)**:<ul><li>[Detalhes demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Detalhes de contato pessoal](../../field-groups/profile/personal-contact-details.md)</li><li>[Detalhes de contato comercial](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Venda adicional de restaurantes e outras atrações residentes para os hóspedes e hóspedes do mercado com reservas de hotel em breve. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Detalhes da reserva](../../field-groups/event/reservation-details.md)</li><li>[Reserva para o jantar](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[Perfil Individual XDM](../../classes/individual-profile.md)**:<ul><li>[Detalhes demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Detalhes de contato pessoal](../../field-groups/profile/personal-contact-details.md)</li><li>[Detalhes de contato comercial](../../field-groups/profile/work-contact-details.md)</li><li>[Detalhes de fidelidade](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Promova a venda de hotéis e outras atrações residentes para hóspedes no mercado e hóspedes com reservas futuras de hotéis. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Detalhes da reserva](../../field-groups/event/reservation-details.md)</li><li>[Reserva de hospedagem](../../field-groups/event/lodging-reservation.md)</li></ul></li><li>**[Perfil Individual XDM](../../classes/individual-profile.md)**:<ul><li>[Detalhes demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Detalhes de contato pessoal](../../field-groups/profile/personal-contact-details.md)</li><li>[Detalhes de contato comercial](../../field-groups/profile/work-contact-details.md)</li><li>[Detalhes de fidelidade](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Venda adicional de voos e outras atrações residentes para hóspedes no mercado e hóspedes com reservas futuras de hotel. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Detalhes da reserva](../../field-groups/event/reservation-details.md)</li><li>[Reserva de voo](../../field-groups/event/flight-reservation.md)</li></ul></li><li>**[Perfil Individual XDM](../../classes/individual-profile.md)**:<ul><li>[Detalhes demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Detalhes de contato pessoal](../../field-groups/profile/personal-contact-details.md)</li><li>[Detalhes de contato comercial](../../field-groups/profile/work-contact-details.md)</li><li>[Detalhes de fidelidade](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
