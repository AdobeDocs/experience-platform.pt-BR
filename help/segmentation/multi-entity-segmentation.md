---
solution: Experience Platform
title: Visão geral da segmentação de várias entidades
description: A segmentação de várias entidades é a capacidade de estender dados do Perfil com dados adicionais com base em produtos, lojas ou outras classes que não são de perfil. Depois de conectados, os dados de classes adicionais ficam disponíveis como se fossem nativos do esquema de Perfil.
exl-id: 01a37fdc-2abe-4a84-b7da-fcbd141ff51f
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# Visão geral da segmentação de várias entidades

A segmentação de várias entidades é um recurso avançado disponível como parte do Adobe Experience Platform [!DNL Segmentation Service]. Esse recurso permite estender dados do [!DNL Real-Time Customer Profile] com dados adicionais de &quot;pessoas&quot; (também conhecidos como &quot;entidades de dimensão&quot;) que sua organização pode definir, como dados relacionados a produtos ou lojas. A segmentação de várias entidades oferece flexibilidade ao definir definições de segmento com base em dados relevantes às suas necessidades de negócios exclusivas e pode ser realizada sem ter conhecimento especializado em consulta de bancos de dados. Com a segmentação de várias entidades, você pode adicionar dados importantes às definições de segmento sem precisar fazer alterações dispendiosas nos fluxos de dados ou aguardar uma mesclagem de dados de back-end.

## Introdução

A segmentação de várias entidades requer uma compreensão funcional dos vários serviços da Adobe Experience Platform envolvidos na segmentação. Antes de continuar com este guia, reveja a seguinte documentação:

* [[!DNL Real-Time Customer Profile]](../profile/home.md): Fornece um perfil de consumidor unificado em tempo real, com base em dados agregados de múltiplas fontes.
   * [Medidas de proteção de perfil](../profile/guardrails.md): práticas recomendadas para criar modelos de dados com suporte no [!DNL Profile].
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): permite que você compile públicos a partir de dados de [!DNL Real-Time Customer Profile].
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../xdm/schema/composition.md#union): conheça as práticas recomendadas para compor esquemas a serem usadas no Experience Platform. Para melhor usar a Segmentação, verifique se seus dados são assimilados como perfis e eventos de acordo com as [práticas recomendadas para modelagem de dados](../xdm/schema/best-practices.md).

## Casos de uso

Para ilustrar o valor da segmentação de várias entidades, considere três casos de uso de marketing padrão que ilustram os desafios presentes na maioria dos aplicativos de marketing:

### Combinação de dados de compra online e offline

Um profissional de marketing que cria uma campanha de email pode ter tentado criar um público-alvo usando compras recentes da loja do cliente nos últimos três meses. Idealmente, esse público-alvo exigiria o nome do item e o nome da loja onde a compra foi feita. Anteriormente, o desafio era capturar o identificador da loja do evento de compra e atribuí-lo a um perfil de cliente individual.

### Redirecionamento de email para abandono de carrinho

É complexo criar e qualificar usuários nas definições de segmento direcionadas ao abandono do carrinho. Saber quais produtos incluir em uma campanha personalizada de redirecionamento requer dados sobre quais produtos foram abandonados por cada indivíduo. Esses dados estão vinculados a eventos comerciais que antes eram desafiadores para monitorar e extrair dados do.

## Criação de definições de segmento de várias entidades

Criar uma definição de segmento de várias entidades primeiro requer definir relações entre esquemas antes de usar a API [!DNL Segmentation] ou a interface do Construtor de segmentos para criar a definição do segmento.

### Definir relacionamentos

A definição de relacionamentos na estrutura dos esquemas do Experience Data Model (XDM) é parte integrante da criação de segmentos com várias entidades. Para relações, o campo no destino precisa ser marcado como a identidade principal desse esquema. Uma identidade só pode ser marcada em cadeias de caracteres e não pode ser marcada em matrizes. Além disso, os relacionamentos não precisam necessariamente ser um para um, pois é possível conectar perfis e eventos de experiência a vários destinos.

A definição de relações pode ser feita usando a API do Registro de esquema ou o Editor de esquemas. Para obter etapas detalhadas que mostram como definir uma relação entre dois schemas, escolha um dos seguintes tutoriais:

* [Definição de uma relação entre dois esquemas usando a API](../xdm/tutorials/relationship-api.md)
* [Definição de uma relação entre dois esquemas usando a interface do Editor de esquemas](../xdm/tutorials/relationship-ui.md)

### Criar uma definição de segmento de várias entidades

Depois de definir os relacionamentos XDM necessários, você pode começar a criar uma definição de segmento de várias entidades. Isso pode ser feito usando a API de segmentação ou a interface do construtor de segmentos. Para obter mais informações, escolha um dos guias a seguir:

* [Criação de uma definição de segmento usando a API de segmentação](./tutorials/create-a-segment.md)
* [Criar uma definição de segmento usando a interface do construtor de segmentos](./ui/overview.md)

## Avaliar e acessar definições de segmento de várias entidades

Depois de criar uma definição de segmento, você pode avaliar e acessar os resultados usando a API de segmentação. A avaliação de uma definição de segmento de várias entidades é muito semelhante à avaliação de uma definição de segmento padrão. Esse processo só pode ser feito usando a API de segmentação. Para obter um guia detalhado sobre como usar a API para avaliar e acessar definições de segmento, leia o [tutorial Avaliação e acesso a definições de segmento](./tutorials/evaluate-a-segment.md).
