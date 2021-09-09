---
solution: Experience Platform
title: ERD do Modelo de Dados do Setor de Viagem e Hospitalidade
topic-legacy: overview
description: Visualize um diagrama de relacionamento de entidade (ERD) que descreve um modelo de dados padronizado para o setor de viagem e hospitalidade, compatível com o Experience Data Model (XDM) para uso no Adobe Experience Platform.
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: 295dc040f3af7342226e3d78d0ae21e73db58d57
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---

# [!UICONTROL Modelo de dados do setor de viagem e ] hospitalidade

O diagrama de relacionamento de entidade (ERD) a seguir representa um modelo de dados padronizado para o setor de viagem e hospitalidade. O ERD é intencionalmente apresentado de forma desnormalizada e considerando como os dados são armazenados no Adobe Experience Platform.

>[!NOTE]
>
>O ERD conforme descrito é uma recomendação sobre como você deve modelar seus dados para este caso de uso do setor. Para usar esse modelo de dados no Platform, você deve construir os esquemas recomendados e seus relacionamentos sozinho. Consulte os guias sobre como gerenciar [schemas](../../ui/resources/schemas.md) e [relações](../../tutorials/relationship-ui.md) na interface do usuário para obter mais informações.

Use a seguinte legenda para interpretar este ERD:

* Cada entidade mostrada no é baseada em uma classe [Experience Data Model (XDM) subjacente](../composition.md#class).
* Para uma determinada entidade, cada linha marcada em **bold** representa um grupo de campos ou um tipo de dados, com os campos relevantes que ela fornece listados abaixo em texto sem negrito.
* Os campos mais importantes para uma determinada entidade são destacados em vermelho.
* Todas as propriedades que podem ser usadas para identificar clientes individuais são marcadas como &quot;identidade&quot;, com uma dessas propriedades marcadas como &quot;identidade primária&quot;.
* Os relacionamentos de entidade são marcados como não dependentes, já que os eventos baseados em cookies geralmente não podem determinar a pessoa ou o indivíduo que fez a transação.

![](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>A entidade Evento de experiência inclui um campo &quot;_ID&quot;, que representa o atributo identificador exclusivo (`_id`) fornecido pela classe XDM ExperienceEvent. Consulte o documento de referência em [XDM ExperienceEvent](../../classes/experienceevent.md) para obter mais detalhes sobre o que é esperado para esse valor.

## [!UICONTROL Casos de ] hospitalização e de viagem

A tabela a seguir descreve as classes recomendadas e os grupos de campos de schema para vários casos de uso comuns para o setor de viagem e hospitalidade.

| Caso de uso | Classes e grupos de campos recomendados |
| --- | --- |
| O jantar de venda cruzada e outras atrações residentes para convidados e convidados do mercado com futuras reservas de hotel. | <ul><li>**[ExperienceEvent](../../classes/experienceevent.md)** XDM:<ul><li>[Detalhes da Reserva](../../field-groups/event/reservation-details.md)</li><li>[Reserva de Loja](../../field-groups/event/lodging-reservation.md)</li><li>[Reserva de Jantar](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[Perfil](../../classes/individual-profile.md)** individual XDM:<ul><li>[Detalhes demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Detalhes de contato pessoal](../../field-groups/profile/personal-contact-details.md)</li><li>[Detalhes do Contato do Trabalho](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| O jantar de venda adicional e outros atrativos residentes para convidados e convidados do mercado com futuras reservas de hotel. | <ul><li>**[ExperienceEvent](../../classes/experienceevent.md)** XDM:<ul><li>[Detalhes da Reserva](../../field-groups/event/reservation-details.md)</li><li>[Reserva de Jantar](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[Perfil](../../classes/individual-profile.md)** individual XDM:<ul><li>[Detalhes demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Detalhes de contato pessoal](../../field-groups/profile/personal-contact-details.md)</li><li>[Detalhes do Contato do Trabalho](../../field-groups/profile/work-contact-details.md)</li><li>[Detalhes da Fidelidade](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Venda agregada de hotéis e outros atrativos residentes a convidados e convidados do mercado com reservas futuras de hotéis. | <ul><li>**[ExperienceEvent](../../classes/experienceevent.md)** XDM:<ul><li>[Detalhes da Reserva](../../field-groups/event/reservation-details.md)</li><li>[Reserva de Loja](../../field-groups/event/lodging-reservation.md)</li></ul></li><li>**[Perfil](../../classes/individual-profile.md)** individual XDM:<ul><li>[Detalhes demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Detalhes de contato pessoal](../../field-groups/profile/personal-contact-details.md)</li><li>[Detalhes do Contato do Trabalho](../../field-groups/profile/work-contact-details.md)</li><li>[Detalhes da Fidelidade](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Voo de venda adicional e outros atrativos residentes para convidados e convidados do mercado com reservas de hotel futuras. | <ul><li>**[ExperienceEvent](../../classes/experienceevent.md)** XDM:<ul><li>[Detalhes da Reserva](../../field-groups/event/reservation-details.md)</li><li>[Reserva de Voo](../../field-groups/event/flight-reservation.md)</li></ul></li><li>**[Perfil](../../classes/individual-profile.md)** individual XDM:<ul><li>[Detalhes demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Detalhes de contato pessoal](../../field-groups/profile/personal-contact-details.md)</li><li>[Detalhes do Contato do Trabalho](../../field-groups/profile/work-contact-details.md)</li><li>[Detalhes da Fidelidade](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}
