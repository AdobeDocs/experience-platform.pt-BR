---
keywords: Experience Platform;retail sales recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Fórmula de vendas de varejo
topic: overview
translation-type: tm+mt
source-git-commit: e08460bc76d79920bbc12c7665a1416d69993f34
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 2%

---


# Fórmula de vendas de varejo

A receita de Vendas de Varejo permite prever a previsão de vendas para todas as lojas semeadas por um determinado período. Com um modelo preciso de previsão, o varejista poderia encontrar a relação entre as políticas de demanda e de preços e tomar decisões otimizadas de preços para maximizar as vendas e a receita.

O documento a seguir responderá perguntas como:
* Para quem esta receita foi construída?
* O que esta receita faz?
* Como começar?

## Para quem esta receita foi construída?

Um varejista enfrenta muitos desafios para se manter competitivo no mercado atual. Sua marca busca impulsionar as vendas anuais para sua marca de varejo, mas há muitas decisões a serem tomadas para minimizar seus custos operacionais. O excesso de suprimento aumenta os custos de inventário enquanto o suprimento insuficiente aumenta o risco de perder clientes para outras marcas. Você precisa pedir mais suprimento para os próximos meses? Como você decide o preço ideal para seus produtos para manter as metas semanais de vendas?

## O que esta receita faz?

A receita de Previsão de Vendas de Varejo usa o aprendizado da máquina para prever tendências de venda. A receita faz isso aproveitando a riqueza dos dados históricos de varejo e do gradiente personalizado aumentando o regressivo ou o algoritmo de aprendizado de máquina para prever vendas uma semana antes. O modelo utiliza o histórico de compras e o padrão para parâmetros de configuração predeterminados determinados determinados pelos nossos Cientistas de Dados para melhorar a precisão preditiva.

## Como começar?

Você pode começar seguindo este [tutorial](../jupyterlab/create-a-recipe.md).

Este tutorial vai além da criação da receita de vendas de varejo em um notebook de Júpiter e do fluxo de trabalho do notebook para a receita para criar a receita no Adobe Experience Platform.

## schema de dados

Essa fórmula usa schemas [](../../xdm/schema/field-dictionary.md) XDM para modelar os dados. O schema usado para esta fórmula é mostrado abaixo:

| Nome do campo | Tipo |
--- | ---
| date | String |
| loja | Número inteiro |
| storeType | String |
| weekSales | Número |
| storeSize | Número inteiro |
| temperatura | Número |
| regionalFuelPrice | Número |
| redução | Número |
| cpi | Número |
| desemprego | Número |
| isHoliday | Booleano |


## Algoritmo

Primeiro, o conjunto de dados de treinamento no schema *DSWRetailSales* é carregado. Daqui, o modelo é treinado usando um algoritmo [de regressor de](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html)gradiente. O aumento de gradiente usa a ideia de que os alunos fracos (que é pelo menos um pouco melhor que o acaso aleatório) podem formar uma sucessão de alunos focados em melhorar as fraquezas do aluno anterior. Juntos, eles podem ser usados para criar um modelo preditivo poderoso.

O processo envolve três elementos: uma função de perda, um aluno fraco e um modelo aditivo.

A função de perda refere-se a uma medida da qualidade de um modelo de previsão em termos de capacidade de prever o resultado esperado - a regressão dos quadrados é utilizada nesta fórmula.

Na ampliação de gradiente, uma árvore decisória é usada como o aluno fraco. Normalmente, as árvores com um número restrito de camadas, nós e divisões são usadas para garantir que o aluno permaneça fraco.

Por último, é utilizado um modelo aditivo. Depois de calcular a perda com a função de perda, a árvore que reduz a perda é escolhida e ponderada para melhorar a modelagem das observações mais difíceis. A produção da árvore ponderada é então adicionada à sequência de árvores existente para melhorar a produção final do modelo - quantidade de vendas futuras.