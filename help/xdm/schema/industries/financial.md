---
solution: Experience Platform
title: ERD do Modelo de Dados do Setor dos Serviços Financeiros
topic-legacy: overview
description: Exibir um diagrama de relacionamento de entidade (ERD) que descreve um modelo de dados padronizado para o setor bancário, de serviços financeiros e de seguros (BFSI). Esse modelo de dados é compatível com o Experience Data Model (XDM) para uso no Adobe Experience Platform.
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: 345380c9d4e371bc90acee1f35e75f9da8f9394e
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 1%

---

# [!UICONTROL Serviços financeiros] ERD do modelo de dados do setor

O seguinte diagrama de relacionamento de entidade (ERD) representa um modelo de dados padronizado para o setor bancário, dos serviços financeiros e dos seguros (BFSI). O ERD é intencionalmente apresentado de forma desnormalizada e considerando como os dados são armazenados no Adobe Experience Platform.

>[!NOTE]
>
>O ERD conforme descrito é uma recomendação sobre como você deve modelar seus dados para este caso de uso do setor. Para usar esse modelo de dados no Platform, você deve construir os esquemas recomendados e seus relacionamentos sozinho. Consulte os guias sobre gerenciamento [esquemas](../../ui/resources/schemas.md) e [relações](../../tutorials/relationship-ui.md) na interface do usuário do para obter mais informações.

Use a seguinte legenda para interpretar este ERD:

* Cada entidade mostrada no é baseada em um [Classe do Experience Data Model (XDM)](../composition.md#class).
* Para uma determinada entidade, cada linha marcada em **bold** representa um grupo de campos ou um tipo de dados, com os campos relevantes fornecidos listados abaixo em texto não em negrito.
* Os campos mais importantes para uma determinada entidade são destacados em vermelho.
* Todas as propriedades que podem ser usadas para identificar clientes individuais são marcadas como &quot;identidade&quot;, com uma dessas propriedades marcadas como &quot;identidade primária&quot;.
* Os relacionamentos de entidade são marcados como não dependentes, já que os eventos baseados em cookies geralmente não podem determinar a pessoa ou o indivíduo que fez a transação.

![](../../images/industries/financial.png)

>[!NOTE]
>
>A entidade Evento de experiência inclui um campo &quot;_ID&quot;, que representa o identificador exclusivo (`_id`) atributo fornecido pela classe XDM ExperienceEvent . Consulte o documento de referência em [ExperiênciaEvento XDM](../../classes/experienceevent.md) para obter mais detalhes sobre o que é esperado para esse valor.

## [!UICONTROL Serviços financeiros] casos de uso

A tabela a seguir descreve as classes recomendadas e os grupos de campos do schema para vários casos de uso financeiro comum.

| Caso de uso | Classes e grupos de campos recomendados |
| --- | --- |
| Impulsione a personalização em escala para segmentos preferidos por meio de insights de relatórios omnicanais e automatizando jornadas para aumentar a inscrição em um programa de recompensas preferido. | <ul><li>**[[!UICONTROL Produto]](../../classes/product.md)**:<ul><li>[[!UICONTROL Categoria do produto]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL ExperiênciaEvento XDM]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Ações do cartão]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL Detalhes da solicitação de cotação]](../../field-groups/event/quote-request-details.md)</li><li>[[!UICONTROL Detalhes do Depósito]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL Detalhes do canal]](../../field-groups/event/channel-details.md)</li><li>[[!UICONTROL Transferências de Saldo]](../../field-groups/event/balance-transfers.md)</li></ul></li><li>**[[!UICONTROL Perfil individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalhes demográficos]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Detalhes de contato pessoal]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Detalhes da Fidelidade]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Otimize a personalização entre canais em canais online e offline. | <ul><li>**[[!UICONTROL Produto]](../../classes/product.md)**:<ul><li>[[!UICONTROL Categoria do produto]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL ExperiênciaEvento XDM]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalhes do canal]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL Perfil individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalhes demográficos]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Detalhes de contato pessoal]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Detalhes da Fidelidade]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Impulsione novas oportunidades de receita usando insights obtidos da análise de comportamento entre canais, identificando padrões de uso do produto que podem levar a novas ofertas de produtos. | <ul><li>**[[!UICONTROL Política]](../../classes/policy.md)**</li><li>**[[!UICONTROL Produto]](../../classes/product.md)**:<ul><li>[[!UICONTROL Categoria do produto]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL ExperiênciaEvento XDM]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Ações do cartão]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL Pesquisa de site de suporte]](../../field-groups/event/support-site-search.md)</li><li>[[!UICONTROL Detalhes do Depósito]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL Detalhes do canal]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL Perfil individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalhes demográficos]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Detalhes de contato pessoal]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Detalhes da Fidelidade]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
