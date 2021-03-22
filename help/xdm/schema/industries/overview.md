---
solution: Experience Platform
title: Visão geral dos modelos de dados do setor
topic: visão geral
description: Saiba mais sobre os modelos de dados padronizados para vários ramos do setor que podem ser construídos com os componentes padrão do Experience Data Model (XDM).
translation-type: tm+mt
source-git-commit: 6a7aebb64a533158f7ab17af0cd28243aeda0eca
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# Visão geral dos modelos de dados do setor

O Experience Data Model (XDM) permite que você crie esquemas altamente personalizáveis para capturar os principais dados de experiência do cliente relacionados à sua empresa. Para ajudar a simplificar o processo de modelagem de seus dados em conformidade com o XDM, o Adobe Experience Platform fornece um conjunto versátil de componentes padrão do XDM, que capturam conceitos normalmente usados em vários setores.

>[!NOTE]
>
>Novos componentes padrão do XDM estão sendo continuamente lançados para atender melhor às necessidades do consumidor. Para obter uma lista dos componentes mais atualizados, você pode [explorar recursos existentes na interface do usuário](../../ui/explore.md) ou consultar o [repositório XDM oficial](https://github.com/adobe/xdm/tree/master/components) no GitHub.

Dependendo do setor no qual sua empresa opera, alguns componentes XDM serão mais relevantes para suas necessidades do que outros. Além disso, os relacionamentos estabelecidos entre seus esquemas XDM variam de acordo com o setor.

Para ajudar a orientar sua estratégia de modelagem de dados com base em seu setor específico, este guia fornece uma referência de diagramas de relacionamento de entidade (ERDs) para vários ramos do setor compatíveis.

## Pré-requisitos

Para ler os ERDs referenciados neste guia, você deve ter um entendimento prático de como os componentes XDM interagem para formar esquemas e como os esquemas XDM operam no Experience Platform como um todo. Certifique-se de ter lido a seguinte documentação de visão geral antes de continuar:

* [Visão geral](../../home.md) do sistema XDM: Saiba como o XDM opera no ecossistema da plataforma.
* [Noções básicas da composição](../../schema/composition.md) do schema: Saiba como os componentes XDM (como mixins, classes e tipos de dados) contribuem para a estrutura de um schema, bem como a função dos campos de identidade.

Também é recomendável revisar o [guia de práticas recomendadas de modelagem de dados](../../schema/best-practices.md) para obter diretrizes gerais sobre como mapear seus dados para XDM.

## ERDs do modelo de dados do setor {#erds}

Os modelos verticais do setor representados por ERDs abaixo são criados intencionalmente de forma desnormalizada e considerando como os dados são armazenados na plataforma.

Para um determinado ERD, cada entidade mostrada em é baseada em uma classe XDM subjacente. Para uma determinada entidade, cada linha marcada em **bold** representa uma mixin ou um tipo de dados, com os campos relevantes que ela fornece listados abaixo em texto sem negrito. Os campos mais importantes para uma determinada entidade são destacados em vermelho.

>[!NOTE]
>
>Algumas entidades podem incluir um campo &quot;_ID&quot;. Isso representa o identificador exclusivo (`_id`) que a Platform atribui automaticamente a entidades de evento ou perfil quando são assimiladas. No entanto, é possível optar por usar seus próprios valores de ID exclusivos para esse campo, se desejar.

Todas as propriedades que podem ser usadas para identificar clientes individuais são marcadas como &quot;identidade&quot;, com uma dessas propriedades marcadas como &quot;identidade primária&quot;.

Os relacionamentos de entidade são marcados como não dependentes, já que os eventos baseados em cookies geralmente não podem determinar a pessoa ou o indivíduo que fez a transação.

Os perfumes são fornecidos para os seguintes setores industriais:

* [[!UICONTROL Retail]](./retail.md)
* [[!UICONTROL Financial services]](./financial.md)
* [[!UICONTROL Travel and hospitality]](./travel-hospitality.md)
* [[!UICONTROL Telecommunications]](./telecom.md)

## Próximas etapas

Este documento forneceu uma visão geral dos ERDs do modelo de dados do setor e como interpretá-los. Para exibir um ERD, selecione um na lista acima.