---
solution: Experience Platform
title: ERD do modelo de dados do setor de telecomunicações
description: Visualize um diagrama de relacionamento de entidade (ERD) que descreva um modelo de dados padronizado para o setor de telecomunicações, compatível com o Experience Data Model (XDM) para uso no Adobe Experience Platform.
exl-id: 96f267ce-a177-4384-a512-841c89d942ba
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# [!UICONTROL Telecomunicações] ERD do modelo de dados do setor

O diagrama de relacionamento de entidade (ERD) a seguir representa um modelo de dados padronizado para o setor de telecomunicações. O ERD é intencionalmente apresentado de forma desnormalizada e considerando a forma como os dados são armazenados no Adobe Experience Platform.

>[!NOTE]
>
>O ERD, conforme descrito, é uma recomendação sobre como você deve modelar seus dados para esse caso de uso do setor. Para usar esse modelo de dados no Experience Platform, você deve criar os esquemas recomendados e seus relacionamentos sozinho. Consulte os guias sobre gerenciamento de [esquemas](../../ui/resources/schemas.md) e [relações](../../tutorials/relationship-ui.md) na interface do usuário para obter mais informações.

Use a seguinte legenda para interpretar este ERD:

* Cada entidade mostrada no é baseada em uma [classe do Experience Data Model (XDM)](../composition.md#class) subjacente.
* Os campos recuados em um campo pai representam um campo filho, ou subcampo, que pertence ao grupo de campos do pai.
* Os campos mais importantes para uma determinada entidade são destacados em vermelho.
* Todas as propriedades que poderiam ser usadas para identificar clientes individuais são marcadas como &quot;identidade&quot;, com uma dessas propriedades marcada como &quot;identidade principal&quot;.
* Os relacionamentos de entidade são marcados como não dependentes, já que os eventos baseados em cookies geralmente não podem determinar a pessoa ou indivíduo que fez a transação.


![Um exemplo de ERD para um modelo de dados do setor de telecomunicações](../../images/industries/telecom.png)

>[!NOTE]
>
>A entidade Evento de experiência inclui um campo &quot;_ID&quot;, que representa o atributo de identificador exclusivo (`_id`) fornecido pela classe XDM ExperienceEvent. Consulte o documento de referência em [XDM ExperienceEvent](../../classes/experienceevent.md) para obter mais detalhes sobre o que é esperado para esse valor.

## Casos de uso de [!UICONTROL Telecomunicações]

A tabela a seguir descreve as classes e os grupos de campos de esquema recomendados para vários casos de uso comuns no setor de telecomunicações.

| Caso de uso | Classes e grupos de campos recomendados |
| --- | --- |
| Entenda os clientes que são bons candidatos a oportunidades de venda adicional ou venda cruzada com base em suas participações atuais e seu comportamento de navegação. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalhes de venda adicional]](../../field-groups/event/upsell-details.md)</li><li>[[!UICONTROL Detalhes da Atualização]](../../field-groups/event/upgrade-details.md)</li></ul></li><li>**[[!UICONTROL Perfil Individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Assinatura de serviço de telecomunicação]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Detalhes demográficos]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Detalhes de contato pessoal]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| Redirecione os abandonadores do carrinho por meio de anúncios relevantes e emails personalizados automatizados. Suprimir anúncios ao converter. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalhes do Commerce]](../../field-groups/event/upsell-details.md) (Para capturar abandonos de carrinho)</li></ul></li><li>**[[!UICONTROL Perfil Individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Assinatura de serviço de telecomunicação]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Detalhes demográficos]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Detalhes de contato pessoal]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| Quando um cliente é marcado como provável de churn (com base na interação de um funcionário ou em um algoritmo de aprendizado de máquina automatizado), envie os detalhes do cliente para canais digitais e não digitais. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalhes de marketing da campanha]](../../field-groups/event/campaign-marketing-details.md)</li><li>[[!UICONTROL Detalhes do canal]](../../field-groups/event/channel-details.md)</li><li>Um grupo de campos personalizados com conteúdo personalizado</li></ul></li><li>**[[!UICONTROL Perfil Individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalhes demográficos]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Detalhes de contato pessoal]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
