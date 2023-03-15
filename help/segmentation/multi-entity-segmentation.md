---
keywords: Experience Platform;página inicial;tópicos populares;segmentação;Segmentação;serviço de segmento;segmentos;Segmentos;multientidade;segmentação de várias entidades;segmentos de várias entidades;
solution: Experience Platform
title: Visão geral da segmentação de várias entidades
description: A segmentação de várias entidades é a capacidade de estender dados do Perfil com dados adicionais com base em produtos, lojas ou outras classes que não são de perfil. Depois de conectados, os dados de classes adicionais ficam disponíveis como se fossem nativos do esquema de Perfil.
exl-id: 01a37fdc-2abe-4a84-b7da-fcbd141ff51f
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# Visão geral da segmentação de várias entidades

A segmentação de várias entidades é um recurso avançado disponível como parte do Adobe Experience Platform [!DNL Segmentation Service]. Esse recurso permite estender [!DNL Real-Time Customer Profile] dados com dados adicionais &quot;não pessoais&quot; (também conhecidos como &quot;entidades de dimensão&quot;) que sua organização pode definir, como dados relacionados a produtos ou lojas. A segmentação de várias entidades oferece flexibilidade ao definir segmentos de público com base em dados relevantes às suas necessidades comerciais exclusivas e pode ser realizada sem ter conhecimento especializado em consulta de bancos de dados. Com a segmentação de várias entidades, você pode adicionar dados importantes aos seus segmentos sem precisar fazer alterações dispendiosas nos fluxos de dados ou aguardar uma mesclagem de dados de back-end.

## Introdução

A segmentação de várias entidades requer uma compreensão funcional dos vários serviços da Adobe Experience Platform envolvidos na segmentação. Antes de continuar com este guia, reveja a seguinte documentação:

* [[!DNL Real-Time Customer Profile]](../profile/home.md): fornece um perfil de consumidor unificado em tempo real, com base em dados agregados de várias fontes.
   * [Medidas de proteção de perfil](../profile/guardrails.md): práticas recomendadas para criar modelos de dados compatíveis com o [!DNL Profile].
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): permite criar segmentos a partir do [!DNL Real-Time Customer Profile] dados.
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../xdm/schema/composition.md#union): Conheça as práticas recomendadas para a composição de esquemas a serem usados no Experience Platform. Para melhor usar a segmentação, verifique se seus dados são assimilados como perfis e eventos de acordo com a [práticas recomendadas para modelagem de dados](../xdm/schema/best-practices.md).

## Casos de uso

Para ilustrar o valor da segmentação de várias entidades, considere três casos de uso de marketing padrão que ilustram os desafios presentes na maioria dos aplicativos de marketing:

### Combinação de dados de compra online e offline

Um profissional de marketing que cria uma campanha de email pode ter tentado criar um segmento para um público-alvo usando compras recentes da loja do cliente nos últimos três meses. Idealmente, esse segmento exigiria o nome do item e o nome da loja onde a compra foi feita. Anteriormente, o desafio era capturar o identificador da loja do evento de compra e atribuí-lo a um perfil de cliente individual.

### Redirecionamento de email para abandono de carrinho

Geralmente, é complexo criar e qualificar usuários em segmentos direcionados ao abandono do carrinho. Saber quais produtos incluir em uma campanha personalizada de redirecionamento requer dados sobre quais produtos foram abandonados por cada indivíduo. Esses dados estão vinculados a eventos comerciais que antes eram desafiadores para monitorar e extrair dados do.

## Criação de segmentos com várias entidades

Primeiro, a criação de um segmento de várias entidades requer a definição de relacionamentos entre esquemas antes de usar o [!DNL Segmentation] API ou interface do construtor de segmentos para criar a definição do segmento.

### Definir relacionamentos

A definição de relacionamentos na estrutura dos esquemas do Experience Data Model (XDM) é parte integrante da criação de segmentos com várias entidades. Para relações, o campo no destino precisa ser marcado como a identidade principal desse esquema. Uma identidade só pode ser marcada em cadeias de caracteres e não pode ser marcada em matrizes. Além disso, os relacionamentos não precisam necessariamente ser um para um, pois é possível conectar perfis e eventos de experiência a vários destinos.

A definição de relações pode ser feita usando a API do Registro de esquema ou o Editor de esquemas. Para obter etapas detalhadas que mostram como definir uma relação entre dois schemas, escolha um dos seguintes tutoriais:

* [Definição de uma relação entre dois esquemas usando a API](../xdm/tutorials/relationship-api.md)
* [Definição de uma relação entre dois esquemas usando a interface do Editor de esquemas](../xdm/tutorials/relationship-ui.md)

### Criar um segmento com várias entidades

Depois de definir os relacionamentos XDM necessários, você pode começar a criar um segmento de várias entidades. Isso pode ser feito usando a API de segmentação ou a interface do construtor de segmentos. Para obter mais informações, escolha um dos guias a seguir:

* [Criação de um segmento usando a API de segmentação](./tutorials/create-a-segment.md)
* [Criar um segmento usando a interface do construtor de segmentos](./ui/overview.md)

## Avaliar e acessar segmentos com várias entidades

Depois de criar um segmento, você pode avaliar e acessar os resultados do segmento usando a API de segmentação. A avaliação de um segmento com várias entidades é muito semelhante à avaliação de um segmento padrão. Esse processo só pode ser feito usando a API de segmentação. Para obter um guia detalhado mostrando como usar a API para avaliar e acessar segmentos, leia o [avaliação e acesso a segmentos](./tutorials/evaluate-a-segment.md) tutorial.
