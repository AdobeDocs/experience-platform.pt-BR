---
solution: Experience Platform
title: Modelo de dados do setor de varejo
description: Visualizar um modelo de dados padronizado para o setor de varejo, compatível com o Experience Data Model (XDM) para uso no Adobe Experience Platform.
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 5ceb261dbf1cac58d0cfe620875b8fa7c761abf2
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# [!UICONTROL Varejo] modelo de dados do setor

O diagrama de relacionamento de entidade (ERD) a seguir representa um modelo de dados padronizado para o setor de varejo. O ERD é intencionalmente apresentado de forma desnormalizada e considerando a forma como os dados são armazenados no Adobe Experience Platform.

>[!NOTE]
>
>O ERD, conforme descrito, é uma recomendação sobre como você deve modelar seus dados para esse caso de uso do setor. Para usar esse modelo de dados na Platform, você deve criar os esquemas recomendados e seus relacionamentos sozinho. Consulte os guias sobre gerenciamento de [esquemas](../../ui/resources/schemas.md) e [relações](../../tutorials/relationship-ui.md) na interface do usuário para obter mais informações.

Use a seguinte legenda para interpretar este ERD:

* Cada entidade mostrada no é baseada em uma [classe do Experience Data Model (XDM)](../composition.md#class) subjacente.
* Para uma determinada entidade, cada linha marcada em **negrito** representa um grupo de campos ou um tipo de dados, com os campos relevantes fornecidos listados abaixo em texto não negrito.
* Os campos mais importantes para uma determinada entidade são destacados em vermelho.
* Todas as propriedades que poderiam ser usadas para identificar clientes individuais são marcadas como &quot;identidade&quot;, com uma dessas propriedades marcada como &quot;identidade principal&quot;.
* Os relacionamentos de entidade são marcados como não dependentes, já que os eventos baseados em cookies geralmente não podem determinar a pessoa ou indivíduo que fez a transação.

![](../../images/industries/retail.png)

>[!NOTE]
>
>A entidade Evento de experiência inclui um campo &quot;_ID&quot;, que representa o atributo de identificador exclusivo (`_id`) fornecido pela classe XDM ExperienceEvent. Consulte o documento de referência em [XDM ExperienceEvent](../../classes/experienceevent.md) para obter mais detalhes sobre o que é esperado para esse valor.

## Casos de uso de [!UICONTROL Varejo]

A tabela a seguir descreve as classes e os grupos de campos de esquema recomendados para vários casos de uso comuns de varejo.

| Caso de uso | Classes e grupos de campos recomendados |
| --- | --- |
| Combine fontes de dados online e offline e resolva a identidade entre dispositivos e online/offline para fornecer relatórios holísticos de atribuição entre canais e entre dispositivos. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Detalhes do Commerce](../../field-groups/event/commerce-details.md)</li><li>[Detalhes da Web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Produto](../../classes/product.md)**:<ul><li>[Catálogo de Produtos](../../field-groups/product/product-catalog.md)</li><li>[Categoria do produto](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Forneça experiências direcionadas e personalizadas para vários segmentos para aumentar a receita e ajudar a aumentar a plataforma na orquestração omnicanal. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Detalhes de marketing da campanha](../../field-groups/event/campaign-marketing-details.md)</li><li>[Detalhes do canal](../../field-groups/event/channel-details.md)</li><li>[Detalhes do Commerce](../../field-groups/event/commerce-details.md)</li><li>[Detalhes do ambiente](../../field-groups/event/environment-details.md)</li><li>[Detalhes da Web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Perfil Individual XDM](../../classes/individual-profile.md)**:<ul><li>[Detalhes demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Detalhes de contato pessoal](../../field-groups/profile/personal-contact-details.md)</li><li>[Detalhes de contato comercial](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Analise a atribuição multitoque para melhorar a eficiência do marketing. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Detalhes de marketing da campanha](../../field-groups/event/campaign-marketing-details.md)</li><li>[Detalhes do canal](../../field-groups/event/channel-details.md)</li><li>[Detalhes do Commerce](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[Perfil Individual XDM](../../classes/individual-profile.md)**:<ul><li>[Detalhes demográficos](../../field-groups/profile/demographic-details.md)</li></ul></li></ul> |
| Melhore a relevância do email através da melhor segmentação entre homens e mulheres. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Detalhes do Commerce](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[Perfil Individual XDM](../../classes/individual-profile.md)**:<ul><li>[Detalhes demográficos](../../field-groups/profile/demographic-details.md)</li></ul></li><li>**[Produto](../../classes/product.md)**:<ul><li>[Catálogo de Produtos](../../field-groups/product/product-catalog.md)</li><li>[Categoria do produto](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Assimile dados de fidelidade (parceiro) para aumentar informações relevantes do produto na Web, email e canais de marketing digital. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Detalhes da Web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Perfil Individual XDM](../../classes/individual-profile.md)**:<ul><li>[Detalhes demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Detalhes de fidelidade](../../field-groups/profile/loyalty-details.md)</li></ul></li><li>**[Produto](../../classes/product.md)**:<ul><li>[Catálogo de Produtos](../../field-groups/product/product-catalog.md)</li><li>[Categoria do produto](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Redirecione os abandonadores de carrinho por meio de emails automatizados e personalizados. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Detalhes do Commerce](../../field-groups/event/commerce-details.md)</li><li>[Detalhes da Web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Produto](../../classes/product.md)**:<ul><li>[Catálogo de Produtos](../../field-groups/product/product-catalog.md)</li><li>[Categoria do produto](../../field-groups/product/product-category.md)</li></ul></li></ul> |

{style="table-layout:auto"}
