---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;segment service;segments;Segments;multi-entity;multi-entity segmentation;multi-entity segments;
solution: Experience Platform
title: Segmentação de várias entidades
topic: overview
description: A segmentação de várias entidades é a capacidade de estender os dados do Perfil com dados adicionais baseados em produtos, lojas ou outras classes que não sejam perfis. Depois de conectados, os dados de classes adicionais ficam disponíveis como se fossem nativos para o schema do Perfil.
translation-type: tm+mt
source-git-commit: 4dd5a91146b116953ba180e3f39d24b4e1ec289e
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---


# Segmentação de várias entidades

A segmentação de várias entidades é um recurso avançado disponível como parte do Adobe Experience Platform [!DNL Segmentation Service]. Esse recurso permite estender [!DNL Real-time Customer Profile] dados com dados adicionais &quot;não-pessoas&quot; (também conhecidos como &quot;entidades de dimensão&quot;) que sua organização pode definir, como dados relacionados a produtos ou lojas. A segmentação de várias entidades proporciona flexibilidade ao definir segmentos de audiência com base em dados relevantes às suas necessidades comerciais exclusivas e pode ser executada sem que haja experiência em consultar bancos de dados. Com a segmentação de várias entidades, você pode adicionar dados principais aos seus segmentos sem precisar fazer alterações dispendiosas nos fluxos de dados ou aguardar uma união de dados back-end.

## Introdução

A segmentação de várias entidades requer uma compreensão funcional dos vários serviços da Adobe Experience Platform envolvidos na segmentação. Antes de continuar com este guia, reveja a seguinte documentação:

* [[!DNL Real-time Customer Profile]](../profile/home.md): Fornece um perfil unificado do consumidor em tempo real, com base em dados agregados de várias fontes.
   * [Perfis](../profile/guardrails.md): Práticas recomendadas para a criação de modelos de dados compatíveis com [!DNL Profile].
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Permite que você crie segmentos a partir de [!DNL Real-time Customer Profile] dados.
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../xdm/schema/composition.md#union)do schema: Saiba mais sobre as práticas recomendadas para a composição de schemas a serem usados no Experience Platform.

## Casos de uso

Para ilustrar o valor da segmentação de várias entidades, considere três casos de uso de marketing padrão que ilustram os desafios presentes na maioria dos aplicativos de marketing:

### Combinação de dados de compra online e offline

Um profissional de marketing que está criando uma campanha de email pode ter tentado criar um segmento para uma audiência de público alvo usando compras recentes de lojas de clientes nos últimos três meses. Idealmente, esse segmento exigiria o nome do item e o nome da loja onde a compra foi realizada. Anteriormente, o desafio era capturar o identificador da loja do evento de compra e atribuí-lo a um perfil de cliente individual.

### Redirecionamento de email para abandono de carrinho

Geralmente, é complexo criar e qualificar usuários em segmentos direcionados ao abandono do carrinho. Saber quais produtos incluir em uma campanha de redefinição de metas personalizada requer dados sobre quais produtos foram abandonados por cada indivíduo. Esses dados estão ligados a eventos de comércio dos quais antes desafiavam o monitoramento e a extração de dados.

## Criação de segmentos multientidades

A criação de um segmento de várias entidades requer primeiro a definição de relações entre schemas antes de usar a [!DNL Segmentation] API ou a interface do usuário do Construtor de segmentos para criar a definição de segmentos.

### Definir relacionamentos

A definição de relacionamentos dentro da estrutura dos schemas do Modelo de Dados de Experiência (XDM) é parte integrante da criação de segmentos de várias entidades. Para relacionamentos, o campo no destino precisa ser marcado como a identidade primária desse schema. Uma identidade só pode ser marcada em strings e não pode ser marcada em arrays. Além disso, os relacionamentos não precisam ser necessariamente um para um, pois você pode conectar perfis e experimentar eventos a vários destinos.

A definição de relações pode ser feita usando a API de Registro do Schema ou o Editor do Schema. Para obter etapas detalhadas mostrando como definir uma relação entre dois schemas, escolha um dos seguintes tutoriais:

* [Definição de uma relação entre dois schemas usando a API](../xdm/tutorials/relationship-api.md)
* [Definição de uma relação entre dois schemas usando a interface do editor de Schemas](../xdm/tutorials/relationship-ui.md)

### Criar um segmento multientidade

Depois de definir os relacionamentos XDM necessários, você pode começar a criar um segmento multientidade. Isso pode ser feito usando a API de segmentação ou a interface do usuário do Construtor de segmentos. Para obter mais informações, escolha um dos seguintes guias:

* [Criação de um segmento usando a API de segmentação](./tutorials/create-a-segment.md)
* [Criação de um segmento usando a interface do usuário do Construtor de segmentos](./ui/overview.md)

## Avaliar e acessar segmentos de várias entidades

Depois de criar um segmento, você pode avaliar e acessar os resultados do segmento usando a API de segmentação. A avaliação de um segmento de várias entidades é muito semelhante à avaliação de um segmento padrão. Esse processo só pode ser feito usando a API de segmentação. Para obter um guia detalhado que mostra como usar a API para avaliar e acessar segmentos, leia o tutorial de [avaliação e acesso a segmentos](./tutorials/evaluate-a-segment.md) .
