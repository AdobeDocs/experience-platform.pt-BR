---
keywords: Experience Platform;fórmula de recomendação do produto;Data Science Workspace;tópicos populares;fórmulas;pré-criar fórmula
solution: Experience Platform
title: Receita de recomendação de produto
topic: overview
description: A fórmula do Recommendations Product permite fornecer recomendações personalizadas de produtos, adaptadas às necessidades e interesses do cliente. Com um modelo de previsão preciso, o histórico de compras de um cliente pode fornecer a você informações sobre quais produtos eles podem estar interessados.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 2%

---


# Fórmula de recomendação de produto

A fórmula do Recommendations Product permite fornecer recomendações personalizadas de produtos, adaptadas às necessidades e interesses do cliente. Com um modelo de previsão preciso, o histórico de compras de um cliente pode fornecer a você informações sobre quais produtos eles podem estar interessados.

## Para quem esta receita foi construída?

Na atualidade, um retalhista pode oferta de uma grande quantidade de produtos, dando aos seus clientes uma série de opções que podem também dificultar a procura dos seus clientes. Devido a limitações de tempo e esforço, os clientes podem não encontrar o produto que desejam, resultando em compras com um alto nível de dissonância cognitiva ou nenhuma compra.

## O que esta receita faz?

A fórmula do Recommendations Product usa o aprendizado de máquina para analisar as interações de um cliente com produtos no passado e gerar uma lista personalizada de recomendações de produtos de forma rápida e fácil. Isso otimiza o processo de descoberta de produtos e elimina pesquisas longas, improdutivas e irrelevantes para seus clientes. Como resultado, a receita da Recommendations do produto pode melhorar a experiência geral de compra de um cliente, resultando em maior envolvimento e maior fidelidade à marca.

## Como começar?

Para começar, siga o tutorial do Adobe Experience Platform Lab (consulte o link Lab abaixo). Este tutorial mostrará como criar a receita do Produto Recommendations em um notebook de Júpiter seguindo o fluxo de trabalho [notebook para a fórmula](../jupyterlab/create-a-recipe.md) e implementando a fórmula em [!DNL Experience Platform] [!DNL Data Science Workspace].

* [Laboratório: Preveja o futuro com a área de trabalho da Data Science](https://expleague.azureedge.net/labs/L777/index.html)
* [Recursos do laboratório](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## Schema de dados

Esta fórmula usa schemas [XDM](../../xdm/schema/field-dictionary.md) personalizados para modelar os dados de entrada e saída:

### Schema de dados de entrada

| Nome do campo | Tipo |
--- | ---
| itemId | String |
| interventionType | String |
| carimbo de data e hora | String |
| userId | String |

### Schema de dados de saída

| Nome do campo | Tipo |
--- | ---
| recomendações | String |
| userId | Número inteiro |

## Algoritmo

A fórmula do Recommendations Product utiliza filtragem colaborativa para gerar uma lista personalizada de recomendações de produtos para seus clientes. A filtragem colaborativa, ao contrário de uma abordagem baseada em conteúdo, não exige informações sobre um produto específico, mas utiliza as preferências históricas do cliente em um conjunto de produtos. Esta técnica de recomendação avançada usa dois pressupostos simples:
* Há clientes com interesses semelhantes e eles podem ser agrupados comparando seus comportamentos de compra e navegação.
* É mais provável que um cliente esteja interessado em uma recomendação baseada em clientes semelhantes em termos de comportamento de compra e navegação.

Esse processo é dividido em duas etapas principais. Primeiro, defina um subconjunto de clientes semelhantes. Em seguida, dentro desse conjunto, identifique recursos semelhantes entre esses clientes para retornar uma recomendação para o cliente do público alvo.