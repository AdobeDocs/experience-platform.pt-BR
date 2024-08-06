---
keywords: Experience Platform;receita de recomendação do produto;Data Science Workspace;tópicos populares;receitas;pré-criar fórmula
solution: Experience Platform
title: Receita de recomendação do produto
description: A fórmula Recommendations de produto permite que você forneça recomendações de produto personalizadas, personalizadas para as necessidades e os interesses do seu cliente. Com um modelo de previsão preciso, o histórico de compras de um cliente pode fornecer insight sobre quais produtos eles podem estar interessados.
exl-id: 508d55af-c33b-4f1d-b1b6-f00ed5d12bf9
source-git-commit: 923c6f2deb4d1199cfc5dc9dc4ca7b4da154aaaa
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 2%

---

# recomendação fórmula do produto

>[!NOTE]
>
>O Área de trabalho de ciência de dados não está mais disponível para compra.
>
>Esta documentação destina-se a clientes existentes com direitos anteriores à Data Science Área de trabalho.

O recomendações fórmula do produto permite que você forneça recomendações personalizadas de produtos adaptadas às necessidades e interesses de seus clientes. Com um modelo de previsão preciso, o histórico de compras de um cliente pode fornecer insight sobre quais produtos eles podem estar interessados.

## Para quem este fórmula construído?

Nos dias modernos, um varejista pode oferta uma multidão de produtos, dando aos seus clientes muitas opções que também podem dificultar o pesquisa dos clientes. Devido a restrições de tempo e esforço, os clientes podem não encontrar o produto que desejam, resultando em compras com um alto nível de dissonância cognitiva ou nenhuma compra.

## O que esta receita faz?

A fórmula Recommendations de produto usa aprendizagem de máquina para analisar as interações de um cliente com produtos no passado e gerar uma lista personalizada de recomendações de produtos de forma rápida e fácil. Isso otimiza o processo de detecção de produtos e elimina pesquisas longas, improdutivas e irrelevantes para seus clientes. Como resultado, a fórmula do Recommendations de produto pode melhorar a experiência geral de compra do cliente, resultando em maior engajamento e maior fidelidade à marca.

## Como começar?

Você pode começar seguindo o Adobe Experience Platform Lab tutorial (consulte Lab link abaixo). Esta tutorial mostrará como criar o Recomendações fórmula de Produto em um Notebook Jupyter seguindo o [notebook para fórmula](../jupyterlab/create-a-model.md) fluxo de Trabalho e implementando o fórmula em [!DNL Experience Platform] [!DNL Data Science Workspace].

* [Lab: prever o futuro com o Área de trabalho de ciência de dados](https://expleague.azureedge.net/labs/L777/index.html)
* [Recursos do Lab](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## schema de dados

Essa fórmula usa esquemas](../../xdm/schema/field-dictionary.md) XDM personalizados [para modelar os dados de entrada e saída:

### schema de dados de entrada

| Nome do campo | Tipo |
| --- | --- |
| itemId | String |
| interactionType | String |
| carimbo de data e hora | String |
| id do usuário | String |

### schema de dados do Output

| Nome do campo | Tipo |
| --- | --- |
| recommendations | String |
| id do usuário | Número inteiro |

## Algoritmo

O recomendações fórmula utiliza filtros colaborativos para gerar uma lista personalizada de recomendações de produtos para seus clientes. A filtragem colaborativa, ao contrário de uma abordagem baseada em conteúdo, não requer informações sobre um produto específico, mas sim usa as preferências históricas de um cliente em um conjunto de produtos. Esta poderosa técnica de recomendação usa duas suposições simples:
* Há clientes com interesses semelhantes e podem ser agrupados por meio da comparação de seus comportamentos de compra e navegação.
* É mais provável que um cliente esteja interessado em uma recomendação baseada em clientes semelhantes em termos de comportamento de compra e navegação.

Esse processo é dividido em duas etapas principais. Primeiro, defina um subconjunto de clientes semelhantes. Em seguida, dentro desse conjunto, identifique recursos semelhantes entre esses clientes para retornar uma recomendação para o cliente-alvo.
