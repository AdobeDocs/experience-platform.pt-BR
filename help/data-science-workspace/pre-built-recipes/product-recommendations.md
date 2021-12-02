---
keywords: Experience Platform, receita de recomendação do produto, Data Science Workspace, tópicos populares, receitas, receita de pré-criação
solution: Experience Platform
title: Receita de recomendação do produto
topic-legacy: overview
description: A fórmula do Recommendations do produto permite fornecer recomendações personalizadas de produtos, adaptadas às necessidades e interesses do cliente. Com um modelo de previsão preciso, o histórico de compras de um cliente pode fornecer informações sobre quais produtos eles podem estar interessados.
exl-id: 508d55af-c33b-4f1d-b1b6-f00ed5d12bf9
source-git-commit: 38c493e6306e493f4ef5caf90509bda6f4d80023
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 3%

---

# Fórmula de recomendação do produto

A fórmula do Recommendations do produto permite fornecer recomendações personalizadas de produtos, adaptadas às necessidades e interesses do cliente. Com um modelo de previsão preciso, o histórico de compras de um cliente pode fornecer informações sobre quais produtos eles podem estar interessados.

## Para quem esta receita foi criada?

Na atualidade, um retalhista pode oferecer uma infinidade de produtos, dando aos seus clientes muitas opções que também podem dificultar a pesquisa dos seus clientes. Devido a restrições de tempo e esforço, os clientes podem não encontrar o produto desejado, resultando em compras com alto nível de dissonância cognitiva ou nenhuma compra.

## O que esta receita faz?

A fórmula do Recommendations do produto usa o aprendizado de máquina para analisar as interações de um cliente com produtos no passado e gerar uma lista personalizada de recomendações de produtos de forma rápida e fácil. Isso otimiza o processo de descoberta de produtos e elimina pesquisas longas, improdutivas e irrelevantes para seus clientes. Como resultado, a receita do Recommendations do produto pode melhorar a experiência geral de compra de um cliente, resultando em maior engajamento e maior fidelidade à marca.

## Como começar?

Você pode começar seguindo o tutorial do Adobe Experience Platform Lab (consulte o link Lab abaixo). Este tutorial mostrará como criar a receita do Recommendations do produto em um notebook Júpiter seguindo o [notebook para receita](../jupyterlab/create-a-model.md) e implementar a receita em [!DNL Experience Platform] [!DNL Data Science Workspace].

* [Laboratório: Preveja o futuro com o Data Science Workspace](https://expleague.azureedge.net/labs/L777/index.html)
* [Recursos do laboratório](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## Schema de dados

Esta fórmula usa personalizado [Esquemas XDM](../../xdm/schema/field-dictionary.md) para modelar os dados de entrada e saída:

### Schema de dados de entrada

| Nome do campo | Tipo |
| --- | --- |
| itemId | String |
| interactionType | String |
| carimbo de data e hora | String |
| userId | String |

### Esquema de dados de saída

| Nome do campo | Tipo |
| --- | --- |
| recomendações | String |
| userId | Número inteiro |

## Algoritmo

A fórmula do Recommendations do produto utiliza uma filtragem colaborativa para gerar uma lista personalizada de recomendações de produto para seus clientes. A filtragem colaborativa, diferente de uma abordagem baseada em conteúdo, não requer informações sobre um produto específico, mas utiliza as preferências históricas de um cliente em um conjunto de produtos. Essa poderosa técnica de recomendação usa duas suposições simples:
* Há clientes com interesses semelhantes e eles podem ser agrupados comparando seus comportamentos de compra e navegação.
* É mais provável que um cliente esteja interessado em uma recomendação com base em clientes semelhantes em termos de comportamento de compra e navegação.

Esse processo é dividido em duas etapas principais. Primeiro, defina um subconjunto de clientes semelhantes. Em seguida, dentro desse conjunto, identifique recursos semelhantes entre esses clientes para retornar uma recomendação para o cliente alvo.
