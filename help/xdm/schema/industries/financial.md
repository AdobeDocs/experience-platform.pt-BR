---
solution: Experience Platform
title: ERD do modelo de dados do setor de serviços financeiros
description: Exibir um diagrama de relacionamento de entidade (ERD) que descreva um modelo de dados padronizado para o setor bancário, de serviços financeiros e de seguros (BFSI). Esse modelo de dados é compatível com o Experience Data Model (XDM) para uso no Adobe Experience Platform.
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# [!UICONTROL Serviços financeiros] ERD de modelo de dados do setor

O diagrama de relacionamento de entidade (ERD) a seguir representa um modelo de dados padronizado para o setor bancário, de serviços financeiros e de seguros (BFSI). O ERD é intencionalmente apresentado de forma desnormalizada e considerando a forma como os dados são armazenados no Adobe Experience Platform.

>[!NOTE]
>
>O ERD, conforme descrito, é uma recomendação sobre como você deve modelar seus dados para esse caso de uso do setor. Para usar esse modelo de dados na Platform, você deve criar os esquemas recomendados e seus relacionamentos sozinho. Consulte os guias sobre gerenciamento de [esquemas](../../ui/resources/schemas.md) e [relações](../../tutorials/relationship-ui.md) na interface do usuário para obter mais informações.

Use a seguinte legenda para interpretar este ERD:

* Cada entidade mostrada no é baseada em uma [classe do Experience Data Model (XDM)](../composition.md#class) subjacente.
* Para uma determinada entidade, cada linha marcada em **negrito** representa um grupo de campos ou um tipo de dados, com os campos relevantes fornecidos listados abaixo em texto não negrito.
* Os campos mais importantes para uma determinada entidade são destacados em vermelho.
* Todas as propriedades que poderiam ser usadas para identificar clientes individuais são marcadas como &quot;identidade&quot;, com uma dessas propriedades marcada como &quot;identidade principal&quot;.
* Os relacionamentos de entidade são marcados como não dependentes, já que os eventos baseados em cookies geralmente não podem determinar a pessoa ou indivíduo que fez a transação.

![](../../images/industries/financial.png)

>[!NOTE]
>
>A entidade Evento de experiência inclui um campo &quot;_ID&quot;, que representa o atributo de identificador exclusivo (`_id`) fornecido pela classe XDM ExperienceEvent. Consulte o documento de referência em [XDM ExperienceEvent](../../classes/experienceevent.md) para obter mais detalhes sobre o que é esperado para esse valor.

## Casos de uso de [!UICONTROL serviços financeiros]

A tabela a seguir descreve as classes e os grupos de campos de esquema recomendados para vários casos de uso financeiro comuns.

| Caso de uso | Classes e grupos de campos recomendados |
| --- | --- |
| Impulsione a personalização em escala para segmentos preferenciais por meio de insights de relatórios omnicanal e da automatização de jornadas para aumentar a inscrição em um programa de recompensas preferencial. | <ul><li>**[[!UICONTROL Produto]](../../classes/product.md)**:<ul><li>[[!UICONTROL Categoria do produto]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Ações do cartão]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL Detalhes da solicitação de orçamento]](../../field-groups/event/quote-request-details.md)</li><li>[[!UICONTROL Detalhes do depósito]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL Detalhes do canal]](../../field-groups/event/channel-details.md)</li><li>[[!UICONTROL Transferências de saldo]](../../field-groups/event/balance-transfers.md)</li></ul></li><li>**[[!UICONTROL Perfil Individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalhes demográficos]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Detalhes de contato pessoal]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Detalhes de fidelidade]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Otimize a personalização entre canais em canais online e offline. | <ul><li>**[[!UICONTROL Produto]](../../classes/product.md)**:<ul><li>[[!UICONTROL Categoria do produto]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalhes do canal]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL Perfil Individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalhes demográficos]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Detalhes de contato pessoal]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Detalhes de fidelidade]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Impulsionar novas oportunidades de receita usando insights obtidos da análise de comportamento entre canais, identificando padrões de uso do produto que podem levar a novas ofertas de produtos. | <ul><li>**[[!UICONTROL Política]](../../classes/policy.md)**</li><li>**[[!UICONTROL Produto]](../../classes/product.md)**:<ul><li>[[!UICONTROL Categoria do produto]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Ações do cartão]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL Pesquisa de Site de Suporte]](../../field-groups/event/support-site-search.md)</li><li>[[!UICONTROL Detalhes do depósito]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL Detalhes do canal]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL Perfil Individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalhes demográficos]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Detalhes de contato pessoal]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Detalhes de fidelidade]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
