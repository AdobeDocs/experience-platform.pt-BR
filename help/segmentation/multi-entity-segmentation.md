---
keywords: Experience Platform, home, tópicos populares, segmentação, Segmentação, serviço de segmento, segmentos, segmentos, várias entidades, segmentação de várias entidades, segmentos de várias entidades;
solution: Experience Platform
title: Visão geral da segmentação de várias entidades
topic: overview
description: A segmentação de várias entidades é a capacidade de estender os dados do Perfil com dados adicionais com base em produtos, lojas ou outras classes que não sejam de perfil. Depois de conectados, os dados de classes adicionais ficam disponíveis como se fossem nativos no esquema Perfil.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---


# Visão geral da segmentação de várias entidades

A segmentação de várias entidades é um recurso avançado disponível como parte da Adobe Experience Platform [!DNL Segmentation Service]. Esse recurso permite estender [!DNL Real-time Customer Profile] dados com dados adicionais de &quot;não pessoas&quot; (também conhecidos como &quot;entidades de dimensão&quot;) que sua organização pode definir, como dados relacionados a produtos ou lojas. A segmentação de várias entidades oferece flexibilidade ao definir segmentos de público-alvo com base em dados relevantes para suas necessidades comerciais exclusivas e pode ser executada sem ter experiência em consultar bancos de dados. Com a segmentação de várias entidades, é possível adicionar dados principais aos seus segmentos sem precisar fazer alterações caras nos fluxos de dados ou esperar uma mesclagem de dados de back-end.

## Introdução

A segmentação de várias entidades requer uma compreensão funcional dos vários serviços da Adobe Experience Platform envolvidos na segmentação. Antes de continuar com este guia, reveja a seguinte documentação:

* [[!DNL Real-time Customer Profile]](../profile/home.md): Fornece um perfil de consumidor unificado em tempo real, com base em dados agregados de várias fontes.
   * [Medidas de proteção](../profile/guardrails.md) do perfil: Práticas recomendadas para criar modelos de dados compatíveis com o  [!DNL Profile].
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Permite criar segmentos a partir de  [!DNL Real-time Customer Profile] dados.
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): A estrutura padronizada pela qual a Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../xdm/schema/composition.md#union) do schema: Saiba mais sobre as práticas recomendadas para a composição de schemas a serem usados na Experience Platform.

## Casos de uso

Para ilustrar o valor da segmentação de várias entidades, considere três casos de uso de marketing padrão que ilustram os desafios presentes na maioria dos aplicativos de marketing:

### Combinação de dados de compra online e offline

Um profissional de marketing que criou uma campanha por email pode ter tentado criar um segmento para um público-alvo usando compras recentes de lojas de clientes nos últimos três meses. Idealmente, esse segmento exigiria o nome do item e o nome da loja onde a compra foi feita. Anteriormente, o desafio era capturar o identificador da loja do evento de compra e atribuí-lo a um perfil de cliente individual.

### Redirecionamento de email para abandono de carrinho

Geralmente é complexo criar e qualificar usuários em segmentos direcionados ao abandono do carrinho. Saber quais produtos incluir em uma campanha de redirecionamento personalizada requer dados relacionados aos produtos que foram abandonados por cada indivíduo. Esses dados estão vinculados a eventos comerciais dos quais era desafiante monitorar e extrair dados.

## Criação de segmentos de várias entidades

A criação de um segmento de várias entidades exige primeiro a definição de relacionamentos entre schemas, antes de usar a API [!DNL Segmentation] ou a interface do usuário do Construtor de segmentos para criar a definição de segmentos.

### Definir relacionamentos

Definir relacionamentos dentro da estrutura dos seus esquemas do Experience Data Model (XDM) é parte integrante da criação de segmentos de várias entidades. Para relacionamentos, o campo no destino precisa ser marcado como a identidade primária desse schema. Uma identidade só pode ser marcada em cadeias de caracteres e não pode ser marcada em matrizes. Além disso, os relacionamentos não precisam ser necessariamente um para um, pois você pode conectar perfis e eventos de experiência a vários destinos.

A definição de relacionamentos pode ser feita usando a API do Registro de Esquema ou o Editor de Esquema. Para etapas detalhadas mostrando como definir uma relação entre dois schemas, escolha entre os seguintes tutoriais:

* [Definição de uma relação entre dois schemas usando a API](../xdm/tutorials/relationship-api.md)
* [Definição de uma relação entre dois schemas usando a interface do Editor de esquemas](../xdm/tutorials/relationship-ui.md)

### Criar um segmento de várias entidades

Depois de definir as relações XDM necessárias, você pode começar a criar um segmento de várias entidades. Isso pode ser feito usando a API de segmentação ou a interface do usuário do Construtor de segmentos. Para obter mais informações, escolha entre os seguintes guias:

* [Criação de um segmento usando a API de segmentação](./tutorials/create-a-segment.md)
* [Criar um segmento usando a interface do usuário do Construtor de segmentos](./ui/overview.md)

## Avaliar e acessar segmentos de várias entidades

Depois de criar um segmento, você pode avaliar e acessar os resultados do segmento usando a API de segmentação. A avaliação de um segmento de várias entidades é muito semelhante à avaliação de um segmento padrão. Esse processo só pode ser feito usando a API de segmentação. Para obter um guia detalhado mostrando como usar a API para avaliar e acessar segmentos, leia o tutorial [avaliar e acessar segmentos](./tutorials/evaluate-a-segment.md).
