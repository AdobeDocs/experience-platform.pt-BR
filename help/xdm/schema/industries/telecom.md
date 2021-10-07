---
solution: Experience Platform
title: ERD do Modelo de Dados do Setor de Telecomunicações
topic-legacy: overview
description: Visualize um ERD (entity relacionamento diagrama) que descreve um modelo de dados padronizado para o setor de telecomunicações, compatível com o Experience Data Model (XDM) para uso no Adobe Experience Platform.
exl-id: 96f267ce-a177-4384-a512-841c89d942ba
source-git-commit: 421b4a448370f9903b8bc826fd9be9e5b2e11c59
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 1%

---

#  Telecomunicações Modelo de dados do setor ERD

O diagrama de relacionamento de entidade (ERD) a seguir representa um modelo de dados padronizado para o setor de telecomunicações. O ERD é intencionalmente apresentado de forma desnormalizada e considerando como os dados são armazenados no Adobe Experience Platform.

>[!NOTE]
>
>O ERD conforme descrito é uma recomendação sobre como você deve modelar seus dados para este caso de uso do setor. Para usar esse modelo de dados no Platform, você deve construir os esquemas recomendados e seus relacionamentos sozinho. Consulte os guias sobre como gerenciar [schemas](../../ui/resources/schemas.md) e [relações](../../tutorials/relationship-ui.md) na interface do usuário para obter mais informações.

Use a seguinte legenda para interpretar este ERD:

* Cada entidade mostrada no é baseada em uma classe [Experience Data Model (XDM) subjacente](../composition.md#class).
* Para uma determinada entidade, cada linha marcada em **bold** representa um grupo de campos ou um tipo de dados, com os campos relevantes que ela fornece listados abaixo em texto sem negrito.
* Os campos mais importantes para uma determinada entidade são destacados em vermelho.
* Todas as propriedades que podem ser usadas para identificar clientes individuais são marcadas como &quot;identidade&quot;, com uma dessas propriedades marcadas como &quot;identidade primária&quot;.
* Os relacionamentos de entidade são marcados como não dependentes, já que os eventos baseados em cookies geralmente não podem determinar a pessoa ou o indivíduo que fez a transação.


![](../../images/industries/telecom.png)

>[!NOTE]
>
>A entidade Evento de experiência inclui um campo &quot;_ID&quot;, que representa o atributo identificador exclusivo (`_id`) fornecido pela classe XDM ExperienceEvent. Consulte o documento de referência em [XDM ExperienceEvent](../../classes/experienceevent.md) para obter mais detalhes sobre o que é esperado para esse valor.

##  Casos de uso de telecomunicações

A tabela a seguir descreve as classes recomendadas e os grupos de campos de schema para vários casos de uso comuns para o setor de telecomunicações.

| Caso de uso | Classes e grupos de campos recomendados |
| --- | --- |
| Entenda os clientes que são bons candidatos para oportunidades de venda adicional ou venda cruzada com base em suas participações atuais e seu comportamento de navegação. | <ul><li>**[ExperienceEvent](../../classes/experienceevent.md)** XDM:<ul><li>[[!UICONTROL Detalhes da venda adicional]](../../field-groups/event/upsell-details.md)</li><li>[[!UICONTROL Detalhes da atualização]](../../field-groups/event/upgrade-details.md)</li></ul></li><li>**[[!UICONTROL Perfil]](../../classes/individual-profile.md)** individual XDM:<ul><li>[[!UICONTROL Subscrição Telecom]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Detalhes demográficos]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Detalhes de contato pessoal]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| Redirecione os abandonadores de carrinho por meio de anúncios relevantes e emails personalizados automatizados. Suprimir publicidades ao converter. | <ul><li>**[ExperienceEvent](../../classes/experienceevent.md)** XDM:<ul><li>[[!UICONTROL Detalhes de comércio]](../../field-groups/event/upsell-details.md)  (para capturar abandonos de carrinho)</li></ul></li><li>**[[!UICONTROL Perfil]](../../classes/individual-profile.md)** individual XDM:<ul><li>[[!UICONTROL Subscrição Telecom]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Detalhes demográficos]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Detalhes de contato pessoal]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| Quando um cliente estiver marcado como passível de churn (com base em uma interação de funcionário ou em um algoritmo automatizado de aprendizado de máquina), envie os detalhes do cliente para canais digitais e não digitais. | <ul><li>**[ExperienceEvent](../../classes/experienceevent.md)** XDM:<ul><li>[[!UICONTROL Detalhes de marketing da campanha]](../../field-groups/event/campaign-marketing-details.md)</li><li>[[!UICONTROL Detalhes do canal]](../../field-groups/event/channel-details.md)</li><li>Um grupo de campos personalizado contendo conteúdo personalizado</li></ul></li><li>**[[!UICONTROL Perfil]](../../classes/individual-profile.md)** individual XDM:<ul><li>[[!UICONTROL Detalhes demográficos]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Detalhes de contato pessoal]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}
