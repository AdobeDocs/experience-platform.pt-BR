---
keywords: Experience Platform;receita de vendas de varejo;Ciência de dados Workspace;tópicos populares;receitas;receita de pré-compilação
solution: Experience Platform
title: Receita de vendas de varejo
description: A fórmula de Vendas de Varejo permite prever a previsão de vendas para todas as lojas pré-implantadas por um determinado período de tempo. Com um modelo de previsão preciso, a retailer seria capaz de encontrar a relação entre as políticas de demanda e de preços e tomar decisões de preços otimizadas para maximizar as vendas e a receita.
exl-id: ff01fcd1-fca6-4957-8470-a974fd1520aa
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 2%

---

# Receita de venda de varejo

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

A fórmula de Vendas de Varejo permite prever a previsão de vendas para todas as lojas pré-implantadas por um determinado período de tempo. Com um modelo de previsão preciso, a retailer seria capaz de encontrar a relação entre as políticas de demanda e de preços e tomar decisões de preços otimizadas para maximizar as vendas e a receita.

O documento a seguir responderá perguntas como:

* Para quem esta receita foi criada?
* O que esta receita faz?
* Como começar?

## Para quem esta receita foi criada?

Um retailer enfrenta muitos desafios para se manter competitivo no mercado atual. Sua marca busca aumentar as vendas anuais para sua marca de varejo, mas há muitas decisões a serem tomadas para minimizar seus custos operacionais. Demasiada oferta aumenta os custos de estoque, enquanto uma oferta muito pequena aumenta o risco de perder clientes para outras marcas. Você precisa pedir mais suprimentos para os próximos meses? Como você decide os preços ideais para seus produtos a fim de manter as metas de vendas semanais?

## O que esta receita faz?

A fórmula Previsão de vendas de varejo usa aprendizado de máquina para prever tendências de venda. A fórmula faz isso aproveitando a riqueza de dados históricos de varejo e o algoritmo de aprendizado de máquina regressor de reforço de gradiente personalizado para prever as vendas com uma semana de antecedência. O modelo utiliza o histórico de compras anteriores e assume como padrão os parâmetros de configuração predeterminados por nossos cientistas de dados para melhorar a precisão preditiva.

## Como começar?

Você pode começar seguindo este [tutorial](../jupyterlab/create-a-model.md).

Este tutorial abordará a criação da fórmula de vendas de varejo em um Jupyter Notebook e o uso do fluxo de trabalho notebook para fórmula para criar a fórmula no Adobe Experience Platform.

## Esquema de dados

Esta fórmula usa [esquemas XDM](../../xdm/schema/field-dictionary.md) para modelar os dados. O esquema usado para esta fórmula é mostrado abaixo:

| Nome do campo | Tipo |
| --- | --- |
| data | String |
| loja | Número inteiro |
| storeType | String |
| weeklySales | Número |
| storeSize | Número inteiro |
| temperatura | Número |
| regionalPreçoDoCombustível | Número |
| markdown | Número |
| cpi | Número |
| desemprego | Número |
| isHoliday | Booleano |


## Algoritmo

Primeiro, o conjunto de dados de treinamento no esquema *DSWRetailSales* é carregado. Daqui, o modelo é treinado usando um [algoritmo de regressor de reforço de gradiente](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html). O incentivo de gradiente usa a ideia de que alunos fracos (um que é pelo menos um pouco melhor do que o acaso aleatório) podem formar uma sucessão de alunos focados em melhorar as fraquezas do aluno anterior. Juntos, eles podem ser usados para criar um modelo preditivo poderoso.

O processo envolve três elementos: uma função de perda, um aluno fraco e um modelo aditivo.

A função de perda refere-se a uma medida de quão bom um modelo de previsão faz em termos de ser capaz de prever o resultado esperado - regressão dos quadrados mínimos é usada nesta fórmula.

No aumento de gradiente, uma árvore de decisão é usada como o aluno fraco. Normalmente, árvores com um número restrito de camadas, nós e divisões são usadas para garantir que o aluno permaneça fraco.

Por último, utiliza-se um modelo aditivo. Depois de calcular a perda com a função de perda, escolhe-se a árvore que reduz a perda e pondera-se para melhorar a modelagem das observações mais difíceis. A saída da árvore ponderada é então adicionada à sequência existente de árvores para melhorar a saída final do modelo - quantidade de vendas futuras .
