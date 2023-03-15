---
solution: Experience Platform
title: ERD do modelo de dados do setor de viagem e hospitalidade
description: Visualize um diagrama de relacionamento de entidade (ERD) que descreve um modelo de dados padronizado para o setor de viagem e hospitalidade, compatível com o Experience Data Model (XDM) para uso no Adobe Experience Platform.
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# [!UICONTROL Viagens e hospitalidade] ERD do modelo de dados do setor

O diagrama de relacionamento de entidade (ERD) a seguir representa um modelo de dados padronizado para o setor de viagens e hospitalidade. O ERD é intencionalmente apresentado de forma desnormalizada e considerando a forma como os dados são armazenados no Adobe Experience Platform.

>[!NOTE]
>
>O ERD, conforme descrito, é uma recomendação sobre como você deve modelar seus dados para esse caso de uso do setor. Para usar esse modelo de dados na Platform, você deve criar os esquemas recomendados e seus relacionamentos sozinho. Consulte os guias sobre gerenciamento [schemas](../../ui/resources/schemas.md) e [relacionamentos](../../tutorials/relationship-ui.md) na interface para obter mais informações.

Use a seguinte legenda para interpretar este ERD:

* Cada entidade mostrada no é baseada em um subjacente [Classe do Experience Data Model (XDM)](../composition.md#class).
* Para uma determinada entidade, cada linha marcada em **negrito** representa um grupo de campos ou um tipo de dados, com os campos relevantes fornecidos listados abaixo em texto não negrito.
* Os campos mais importantes para uma determinada entidade são destacados em vermelho.
* Todas as propriedades que poderiam ser usadas para identificar clientes individuais são marcadas como &quot;identidade&quot;, com uma dessas propriedades marcada como &quot;identidade principal&quot;.
* Os relacionamentos de entidade são marcados como não dependentes, já que os eventos baseados em cookies geralmente não podem determinar a pessoa ou indivíduo que fez a transação.

![](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>A entidade Evento de experiência inclui um campo &quot;_ID&quot;, que representa o identificador exclusivo (`_id`) fornecido pela classe XDM ExperienceEvent. Consulte o documento de referência sobre [XDM ExperienceEvent](../../classes/experienceevent.md) para obter mais detalhes sobre o que é esperado para esse valor.

## [!UICONTROL Viagens e hospitalidade] casos de uso

A tabela a seguir descreve as classes e os grupos de campos de esquema recomendados para vários casos de uso comuns no setor de viagem e hospitalidade.

| Caso de uso | Classes e grupos de campos recomendados |
| --- | --- |
| Venda cruzada de restaurantes e outras atrações residentes para hóspedes e hóspedes com reservas de hotel em breve. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Detalhes da reserva](../../field-groups/event/reservation-details.md)</li><li>[Reserva de acomodação](../../field-groups/event/lodging-reservation.md)</li><li>[Reserva para o jantar](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[Perfil individual XDM](../../classes/individual-profile.md)**:<ul><li>[Detalhes demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Detalhes de contato pessoal](../../field-groups/profile/personal-contact-details.md)</li><li>[Detalhes de contato comercial](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Venda adicional de restaurantes e outras atrações residentes para os hóspedes e hóspedes do mercado com reservas de hotel em breve. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Detalhes da reserva](../../field-groups/event/reservation-details.md)</li><li>[Reserva para o jantar](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[Perfil individual XDM](../../classes/individual-profile.md)**:<ul><li>[Detalhes demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Detalhes de contato pessoal](../../field-groups/profile/personal-contact-details.md)</li><li>[Detalhes de contato comercial](../../field-groups/profile/work-contact-details.md)</li><li>[Detalhes de fidelidade](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Promova a venda de hotéis e outras atrações residentes para hóspedes no mercado e hóspedes com reservas futuras de hotéis. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Detalhes da reserva](../../field-groups/event/reservation-details.md)</li><li>[Reserva de acomodação](../../field-groups/event/lodging-reservation.md)</li></ul></li><li>**[Perfil individual XDM](../../classes/individual-profile.md)**:<ul><li>[Detalhes demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Detalhes de contato pessoal](../../field-groups/profile/personal-contact-details.md)</li><li>[Detalhes de contato comercial](../../field-groups/profile/work-contact-details.md)</li><li>[Detalhes de fidelidade](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Venda adicional de voos e outras atrações residentes para hóspedes no mercado e hóspedes com reservas futuras de hotéis. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Detalhes da reserva](../../field-groups/event/reservation-details.md)</li><li>[Reserva de voo](../../field-groups/event/flight-reservation.md)</li></ul></li><li>**[Perfil individual XDM](../../classes/individual-profile.md)**:<ul><li>[Detalhes demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Detalhes de contato pessoal](../../field-groups/profile/personal-contact-details.md)</li><li>[Detalhes de contato comercial](../../field-groups/profile/work-contact-details.md)</li><li>[Detalhes de fidelidade](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
