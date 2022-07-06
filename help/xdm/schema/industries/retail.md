---
solution: Experience Platform
title: Modelo de dados do setor de varejo
topic-legacy: overview
description: Visualizar um modelo de dados padronizado para o setor de varejo, compatível com o Experience Data Model (XDM) para uso no Adobe Experience Platform.
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 2d7314f11837ca5c5ca1411553f20f58c4cad1ec
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 1%

---

# [!UICONTROL Varejo] modelo de dados do setor

O diagrama de relacionamento de entidade (ERD) a seguir representa um modelo de dados padronizado para o setor de varejo. O ERD é intencionalmente apresentado de forma desnormalizada e considerando como os dados são armazenados no Adobe Experience Platform.

>[!NOTE]
>
>O ERD conforme descrito é uma recomendação sobre como você deve modelar seus dados para este caso de uso do setor. Para usar esse modelo de dados no Platform, você deve construir os esquemas recomendados e seus relacionamentos sozinho. Consulte os guias sobre gerenciamento [esquemas](../../ui/resources/schemas.md) e [relações](../../tutorials/relationship-ui.md) na interface do usuário do para obter mais informações.

Use a seguinte legenda para interpretar este ERD:

* Cada entidade mostrada no é baseada em um [Classe do Experience Data Model (XDM)](../composition.md#class).
* Para uma determinada entidade, cada linha marcada em **bold** representa um grupo de campos ou um tipo de dados, com os campos relevantes fornecidos listados abaixo em texto não em negrito.
* Os campos mais importantes para uma determinada entidade são destacados em vermelho.
* Todas as propriedades que podem ser usadas para identificar clientes individuais são marcadas como &quot;identidade&quot;, com uma dessas propriedades marcadas como &quot;identidade primária&quot;.
* Os relacionamentos de entidade são marcados como não dependentes, já que os eventos baseados em cookies geralmente não podem determinar a pessoa ou o indivíduo que fez a transação.

![](../../images/industries/retail.png)

>[!NOTE]
>
>A entidade Evento de experiência inclui um campo &quot;_ID&quot;, que representa o identificador exclusivo (`_id`) atributo fornecido pela classe XDM ExperienceEvent . Consulte o documento de referência em [ExperiênciaEvento XDM](../../classes/experienceevent.md) para obter mais detalhes sobre o que é esperado para esse valor.

## [!UICONTROL Varejo] casos de uso

A tabela a seguir descreve as classes recomendadas e os grupos de campos de esquema para vários casos de uso de varejo comuns.

| Caso de uso | Classes e grupos de campos recomendados |
| --- | --- |
| Combine fontes de dados online e offline e resolva a identidade entre dispositivos e online/offline para fornecer relatórios holísticos de atribuição entre canais e dispositivos. | <ul><li>**[ExperiênciaEvento XDM](../../classes/experienceevent.md)**:<ul><li>[Detalhes de comércio](../../field-groups/event/commerce-details.md)</li><li>[Detalhes da Web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Produto](../../classes/product.md)**:<ul><li>[Catálogo de produtos](../../field-groups/product/product-catalog.md)</li><li>[Categoria do produto](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Forneça experiências direcionadas e personalizadas para vários segmentos para aumentar a receita e ajudar a aumentar a plataforma em orquestração omnicanal. | <ul><li>**[ExperiênciaEvento XDM](../../classes/experienceevent.md)**:<ul><li>[Detalhes de marketing da campanha](../../field-groups/event/campaign-marketing-details.md)</li><li>[Detalhes do canal](../../field-groups/event/channel-details.md)</li><li>[Detalhes de comércio](../../field-groups/event/commerce-details.md)</li><li>[Detalhes do ambiente](../../field-groups/event/environment-details.md)</li><li>[Detalhes da Web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Perfil individual XDM](../../classes/individual-profile.md)**:<ul><li>[Detalhes demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Detalhes de contato pessoal](../../field-groups/profile/personal-contact-details.md)</li><li>[Detalhes do Contato do Trabalho](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Analise a atribuição de multitoque para melhorar a eficiência do marketing. | <ul><li>**[ExperiênciaEvento XDM](../../classes/experienceevent.md)**:<ul><li>[Detalhes de marketing da campanha](../../field-groups/event/campaign-marketing-details.md)</li><li>[Detalhes do canal](../../field-groups/event/channel-details.md)</li><li>[Detalhes de comércio](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[Perfil individual XDM](../../classes/individual-profile.md)**:<ul><li>[Detalhes demográficos](../../field-groups/profile/demographic-details.md)</li></ul></li></ul> |
| Melhore a relevância do email por meio da segmentação aprimorada de homens e mulheres. | <ul><li>**[ExperiênciaEvento XDM](../../classes/experienceevent.md)**:<ul><li>[Detalhes de comércio](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[Perfil individual XDM](../../classes/individual-profile.md)**:<ul><li>[Detalhes demográficos](../../field-groups/profile/demographic-details.md)</li></ul></li><li>**[Produto](../../classes/product.md)**:<ul><li>[Catálogo de produtos](../../field-groups/product/product-catalog.md)</li><li>[Categoria do produto](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Assimilar dados de fidelidade (parceiro) para aumentar as informações relevantes do produto na Web, no email e nos canais de marketing digital. | <ul><li>**[ExperiênciaEvento XDM](../../classes/experienceevent.md)**:<ul><li>[Detalhes da Web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Perfil individual XDM](../../classes/individual-profile.md)**:<ul><li>[Detalhes demográficos](../../field-groups/profile/demographic-details.md)</li><li>[Detalhes da Fidelidade](../../field-groups/profile/loyalty-details.md)</li></ul></li><li>**[Produto](../../classes/product.md)**:<ul><li>[Catálogo de produtos](../../field-groups/product/product-catalog.md)</li><li>[Categoria do produto](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Redirecione os abandonadores de carrinho por meio de emails automatizados e personalizados. | <ul><li>**[ExperiênciaEvento XDM](../../classes/experienceevent.md)**:<ul><li>[Detalhes de comércio](../../field-groups/event/commerce-details.md)</li><li>[Detalhes da Web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Produto](../../classes/product.md)**:<ul><li>[Catálogo de produtos](../../field-groups/product/product-catalog.md)</li><li>[Categoria do produto](../../field-groups/product/product-category.md)</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}

*\*Embora uma classe de produto padrão esteja planejada para uma versão futura, os esquemas de produto devem ser criados atualmente usando uma classe personalizada. Portanto, é necessário criar manualmente a estrutura da classe do schema, bem como a de qualquer grupo de campos que você adiciona a ele. Consulte a seção sobre [criação de uma classe personalizada](../../ui/resources/classes.md#create) no guia da interface do usuário do XDM para obter mais informações.*
