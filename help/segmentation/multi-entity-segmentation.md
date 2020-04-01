---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentação de várias entidades
topic: overview
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# Segmentação de várias entidades

A segmentação de várias entidades é a capacidade de estender os dados do Perfil com dados adicionais baseados em produtos, lojas ou outras classes que não sejam perfis. Depois de conectados, os dados de classes adicionais ficam disponíveis como se fossem nativos para o schema do Perfil.

Para obter mais informações sobre a segmentação de várias entidades, leia a visão geral [da](./home.md)segmentação.

## Introdução

Este tutorial requer uma compreensão funcional dos vários serviços da plataforma Adobe Experience envolvidos no uso da segmentação. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [Perfil](../profile/home.md)do cliente em tempo real: Fornece um perfil unificado do consumidor em tempo real, com base em dados agregados de várias fontes.
- [Serviço](./home.md)de segmentação da plataforma Adobe Experience: Permite criar segmentos a partir do Perfil do cliente em tempo real.
- [Modelo de dados de experiência (XDM)](../xdm/home.md): A estrutura padronizada pela qual a Plataforma organiza os dados de experiência do cliente.

## Como definir relações XDM

A definição de relações com a estrutura dos schemas do Modelo de Dados de Experiência (XDM) é uma parte importante e integral da criação de segmentos.

Esse processo pode ser feito usando a API do Registro do Schema ou o Editor do Schema. Para obter um guia detalhado sobre como usar a API para definir uma relação entre dois schemas, leia [o tutorial sobre como definir uma relação entre dois schemas usando a API](../xdm/tutorials/relationship-api.md). Para obter um guia detalhado sobre como usar o Editor de Schemas para definir uma relação entre dois schemas, leia [o tutorial sobre como definir uma relação entre dois schemas usando o Editor](../xdm/tutorials/relationship-ui.md)de Schemas.

## Como usar a criação de segmentos que usam relações XDM

Depois de definir seus relacionamentos XDM, você pode usar as APIs de Perfil do cliente em tempo real para criar um segmento.

Esse processo pode ser feito usando a API de Perfil do cliente em tempo real ou o Construtor de segmentos. Para obter um guia detalhado sobre como usar a API para criar um segmento, leia [o tutorial sobre como criar um segmento usando a API](./tutorials/create-a-segment.md)de Perfil do cliente em tempo real. Para obter um guia detalhado sobre como usar o Construtor de segmentos para criar um segmento, leia [o guia](./ui/overview.md)do usuário do Construtor de segmentos.

## Como avaliar e acessar segmentos para segmentos multientidades

Depois de criar um segmento, você pode avaliar e acessar os resultados do segmento usando as APIs de Perfil do cliente em tempo real. A avaliação de um segmento multientidade é muito semelhante à avaliação de um segmento regular.

Esse processo só pode ser feito usando a API de Perfil do cliente em tempo real. Para obter um guia detalhado sobre como usar a API para avaliar e acessar segmentos, leia [o tutorial sobre como avaliar e acessar segmentos](./tutorials/evaluate-a-segment.md).