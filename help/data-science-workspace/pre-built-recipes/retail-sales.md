---
keywords: Experience Platform, receita de vendas de varejo, Data Science Workspace, tópicos populares, receitas, receita de pré-criação
solution: Experience Platform
title: Receita de Vendas de Varejo
topic-legacy: overview
description: A receita Vendas de Varejo permite prever a previsão de vendas para todas as lojas pré-implantadas por um determinado período. Com um modelo de previsão preciso, o varejista poderia encontrar a relação entre as políticas de demanda e de preços e tomar decisões otimizadas de preços para maximizar as vendas e a receita.
exl-id: ff01fcd1-fca6-4957-8470-a974fd1520aa
translation-type: tm+mt
source-git-commit: 441d7822f287fabf1b06cdf3f6982f9c910387a8
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 2%

---

# Receita de vendas de varejo

A receita Vendas de Varejo permite prever a previsão de vendas para todas as lojas pré-implantadas por um determinado período. Com um modelo de previsão preciso, o varejista poderia encontrar a relação entre as políticas de demanda e de preços e tomar decisões otimizadas de preços para maximizar as vendas e a receita.

O documento a seguir responderá perguntas como:
* Para quem esta receita foi criada?
* O que esta receita faz?
* Como começar?

## Para quem esta receita foi criada?

Um varejista enfrenta muitos desafios para se manter competitivo no mercado atual. Sua marca busca aumentar as vendas anuais para sua marca de varejo, mas há muitas decisões a serem tomadas para minimizar seus custos operacionais. Demasiada oferta aumenta os custos do inventário, ao mesmo tempo que a oferta diminui o risco de perder clientes para outras marcas. Você precisa pedir mais suprimento para os próximos meses? Como você decide qual é o preço ideal para seus produtos manter as metas semanais de vendas?

## O que esta receita faz?

A fórmula Previsão de Vendas de Varejo usa aprendizagem de máquina para prever tendências de vendas. A receita faz isso aproveitando a riqueza de dados históricos de varejo e o algoritmo de aprendizado de máquina personalizado de reforço de gradiente para prever vendas com uma semana de antecedência. O modelo utiliza o histórico de compras e os padrões anteriores para parâmetros de configuração predeterminados determinados pelos nossos cientistas de dados, a fim de melhorar a precisão preditiva.

## Como começar?

Você pode começar seguindo este [tutorial](../jupyterlab/create-a-recipe.md).

Este tutorial irá criar a receita de Vendas de varejo em um Bloco de Notas de Júpiter e usar o bloco de notas para receber fluxo de trabalho para criar a receita no Adobe Experience Platform.

## Schema de dados

Essa fórmula usa [esquemas XDM](../../xdm/schema/field-dictionary.md) para modelar os dados. O esquema usado para esta fórmula é mostrado abaixo:

| Nome do campo | Tipo |
| --- | --- |
| data | String |
| loja | Número inteiro |
| storeType | String |
| weeklySales | Número |
| storeSize | Número inteiro |
| temperatura | Número |
| regionalFuelPrice | Número |
| marcação | Número |
| cpi | Número |
| desemprego | Número |
| isHoliday | Booleano |


## Algoritmo

Primeiro, o conjunto de dados de treinamento no esquema *DSWRetailSales* é carregado. A partir daqui, o modelo é treinado usando um algoritmo [de regressão de reforço de gradiente](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html). A valorização de gradiente usa a ideia de que os aprendentes fracos (um que é pelo menos ligeiramente melhor do que o acaso aleatório) podem formar uma sucessão de aprendentes focados em melhorar as fraquezas do aluno anterior. Juntas, elas podem ser usadas para criar um modelo preditivo poderoso.

O processo envolve três elementos: uma função de perda, um aprendiz fraco e um modelo aditivo.

A função de perda refere-se a uma medida do desempenho de um modelo de previsão em termos de capacidade de prever o resultado esperado - pelo menos a regressão dos quadrados é utilizada nesta receita.

Na promoção de gradiente, uma árvore de decisão é usada como o aprendiz fraco. Normalmente, as árvores com um número restrito de camadas, nós e divisões são usadas para garantir que o aluno permaneça fraco.

Por último, é utilizado um modelo de aditivo. Depois de calcular a perda com a função de perda, a árvore que reduz a perda é escolhida e ponderada para melhorar a modelagem das observações mais difíceis. A produção da árvore ponderada é então adicionada à sequência de árvores existente para melhorar a produção final do modelo - quantidade de vendas futuras .
