---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentação de várias entidades
topic: overview
translation-type: tm+mt
source-git-commit: f44e42a4faa3b10f147dbaf929048054ce0bec42
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# Segmentação de várias entidades

A segmentação de várias entidades é a capacidade de estender os dados do Perfil com dados adicionais baseados em produtos, lojas ou outras classes que não sejam perfis. Depois de conectados, os dados de classes adicionais ficam disponíveis como se fossem nativos para o schema do Perfil.

Para saber mais sobre a segmentação de várias entidades, continue lendo a documentação e complete seu aprendizado assistindo ao vídeo abaixo ou explorando a visão geral [da](./home.md)segmentação.]

>[!VIDEO](https://video.tv.adobe.com/v/28947?quality=12&learn=on)

## Introdução

Este tutorial requer um entendimento prático dos vários serviços de Adobe Experience Platform envolvidos no uso da segmentação. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [Perfil](../profile/home.md)do cliente em tempo real: Fornece um perfil unificado do consumidor em tempo real, com base em dados agregados de várias fontes.
- [Serviço](./home.md)de segmentação de Adobe Experience Platform: Permite criar segmentos a partir do Perfil do cliente em tempo real.
- [Modelo de dados de experiência (XDM)](../xdm/home.md): A estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.

## Como definir relações XDM

A definição de relações com a estrutura dos schemas do Modelo de Dados de Experiência (XDM) é uma parte importante e integral da criação de segmentos.

Esse processo pode ser feito usando a API do Registro do Schema ou o Editor do Schema. Para obter um guia detalhado sobre como usar a API para definir uma relação entre dois schemas, leia [o tutorial sobre como definir uma relação entre dois schemas usando a API](../xdm/tutorials/relationship-api.md). Para obter um guia detalhado sobre como usar o Editor de Schemas para definir uma relação entre dois schemas, leia [o tutorial sobre como definir uma relação entre dois schemas usando o Editor](../xdm/tutorials/relationship-ui.md)de Schemas.

## Como criar segmentos que usam relações XDM

Depois de definir seus relacionamentos XDM, você pode usar a API do Serviço de segmentação para criar um segmento.

Esse processo pode ser feito usando a API de segmentação ou a interface do usuário do Construtor de segmentos. Para obter um guia detalhado sobre como usar a API para criar um segmento, leia [o tutorial sobre como criar um segmento usando a API](./tutorials/create-a-segment.md)de segmentação. Para obter um guia detalhado sobre como usar o Construtor de segmentos para criar um segmento, leia [o guia](./ui/overview.md)do usuário do Construtor de segmentos.

## Como avaliar e acessar segmentos para segmentos multientidades

Depois de criar um segmento, você pode avaliar e acessar os resultados do segmento usando a [!DNL Segmentation Service] API. A avaliação de um segmento multientidade é muito semelhante à avaliação de um segmento regular.

Esse processo só pode ser feito usando a [!DNL Segmentation Service] API. Para obter um guia detalhado sobre como usar a API para avaliar e acessar segmentos, leia o tutorial sobre como [avaliar e acessar segmentos](./tutorials/evaluate-a-segment.md).