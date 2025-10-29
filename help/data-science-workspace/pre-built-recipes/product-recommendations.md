---
keywords: Experience Platform;receita de recomendação do produto;Data Science Workspace;tópicos populares;receitas;pré-criar fórmula
solution: Experience Platform
title: Receita de recomendação do produto
description: A fórmula Recomendações de produto permite fornecer recomendações de produto personalizadas, personalizadas de acordo com as necessidades e os interesses do cliente. Insight Com um modelo de previsão preciso, o histórico de compras de um cliente pode fornecer a você informações sobre quais produtos ele pode estar interessado.
exl-id: 508d55af-c33b-4f1d-b1b6-f00ed5d12bf9
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 2%

---

# Receita de recomendação do produto

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

A fórmula Recomendações de produto permite fornecer recomendações de produto personalizadas, personalizadas de acordo com as necessidades e os interesses do cliente. Insight Com um modelo de previsão preciso, o histórico de compras de um cliente pode fornecer a você informações sobre quais produtos ele pode estar interessado.

## Para quem esta receita foi criada?

Nos dias de hoje, uma retailer pode oferecer uma variedade de produtos, proporcionando aos clientes muitas opções que também podem atrapalhar a pesquisa. Devido a restrições de tempo e esforço, os clientes podem não encontrar o produto que desejam, resultando em compras com um alto nível de dissonância cognitiva ou nenhuma compra.

## O que esta receita faz?

A fórmula Recomendações de produto usa o aprendizado de máquina para analisar as interações de um cliente com produtos no passado e gerar uma lista personalizada de recomendações de produto de forma rápida e fácil. Isso otimiza o processo de detecção de produtos e elimina pesquisas longas, improdutivas e irrelevantes para seus clientes. Como resultado, a fórmula de Recomendações de produto pode melhorar a experiência geral de compra de um cliente, resultando em maior engajamento e maior fidelidade à marca.

## Como começar?

Você pode começar seguindo o tutorial do Adobe Experience Platform Lab (consulte o link Lab abaixo). Este tutorial mostrará como criar a fórmula do Product Recommendations em um Jupyter Notebook seguindo o fluxo de trabalho [bloco de anotações para a fórmula](../jupyterlab/create-a-model.md) e implementando a fórmula em [!DNL Experience Platform] [!DNL Data Science Workspace].

* [Laboratório: Preveja o futuro com o Data Science Workspace](https://expleague.azureedge.net/labs/L777/index.html)
* [Recursos do laboratório](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## Esquema de dados

Esta fórmula usa [esquemas XDM](../../xdm/schema/field-dictionary.md) personalizados para modelar os dados de entrada e saída:

### Esquema de dados de entrada

| Nome do campo | Tipo |
| --- | --- |
| itemId | String |
| interactionType | String |
| carimbo de data e hora | String |
| userId | String |

### Esquema de dados de saída

| Nome do campo | Tipo |
| --- | --- |
| recommendations | String |
| userId | Número inteiro |

## Algoritmo

A fórmula Recomendações de produto utiliza filtragem colaborativa para gerar uma lista personalizada de recomendações de produto para seus clientes. A filtragem colaborativa, ao contrário de uma abordagem baseada em conteúdo, não requer informações sobre um produto específico, mas utiliza as preferências históricas de um cliente em um conjunto de produtos. Essa eficiente técnica de recomendação usa duas suposições simples:

* Existem clientes com interesses semelhantes, que podem ser agrupados ao comparar seus comportamentos de compra e de navegação.
* É mais provável que um cliente esteja interessado em uma recomendação baseada em clientes semelhantes em termos de comportamento de compra e navegação.

Esse processo é dividido em duas etapas principais. Primeiro, defina um subconjunto de clientes semelhantes. Em seguida, dentro desse conjunto, identifique recursos semelhantes entre esses clientes para retornar uma recomendação para o cliente-alvo.
