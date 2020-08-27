---
keywords: Experience Platform;product purchase recipe;Data Science Workspace;popular topics;recipes;pre build recipe
solution: Experience Platform
title: Fórmula de compra do produto
topic: overview
description: A fórmula Predição de compra de produto permite prever a probabilidade de um determinado tipo de evento de compra do cliente - uma compra de produto, por exemplo.
translation-type: tm+mt
source-git-commit: 7615476c4b728b451638f51cfaa8e8f3b432d659
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 7%

---


# Fórmula de compra do produto

## Visão geral

A fórmula Predição de compra de produto permite prever a probabilidade de um determinado tipo de evento de compra do cliente - uma compra de produto, por exemplo.

![](../images/pre-built-recipes/ppp_bigpicture.png)

O documento a seguir responderá perguntas como:
* Para quem esta receita foi construída?
* O que esta receita faz?

## Para quem esta receita foi construída?

Sua marca busca impulsionar as vendas trimestrais para sua linha de produtos através de promoções eficazes e direcionadas aos seus clientes. No entanto, nem todos os clientes são iguais e você quer o seu dinheiro. Quem você público alvo? Quais de seus clientes têm maior probabilidade de responder sem achar sua promoção intrusiva? Como você personaliza suas promoções para cada cliente? Em que canais você deve confiar e quando deve enviar promoções?

## O que esta receita faz?

A fórmula Predição de compra de produto utiliza o aprendizado da máquina para prever o comportamento de compra do cliente. Isso é feito aplicando um classificador de floresta aleatório personalizado e um XDM (Modelo de Dados de Experiência em Duas camadas) para prever a probabilidade de um evento de compra. O modelo utiliza dados de entrada que incorporam informações de perfil do cliente e histórico de compras passadas, além de padrões para parâmetros de configuração predeterminados determinados determinados pelos nossos Cientistas de Dados para aprimorar a precisão preditiva.

## Schema de dados

Essa fórmula usa schemas [](../../xdm/home.md) XDM para modelar os dados. O schema usado para esta fórmula é mostrado abaixo:

| Nome do campo | Tipo |
--- | ---
| userId | String |
| genderRatio | Número |
| ageY | Número |
| ageM | Número |
| optinEmail | Booleano |
| optinMobile | Booleano |
| optinAddress | Booleano |
| criado | Número inteiro |
| totalOrder | Número |
| totalItems | Número |
| orderDate1 | Número |
| shippingDate1 | Número |
| totalPrice1 | Número |
| tax1 | Número |
| orderDate2 | Número |
| shippingDate2 | Número |
| totalPrice2 | Número |


## Algoritmo

Primeiro, o conjunto de dados de treinamento no schema *ProductPredição* é carregado. Daqui, o modelo é treinado com um classificador [de floresta](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html)aleatório. Classificador de floresta aleatória é um tipo de algoritmo agrupado que se refere a um algoritmo que combina vários algoritmos para obter melhor desempenho preditivo. A ideia por trás do algoritmo é que o classificador aleatório de floresta constrói várias árvores de decisão e as mescla para criar uma previsão mais precisa e estável.

Esse processo se start com a criação de um conjunto de árvores de decisão que seleciona aleatoriamente subconjuntos de dados de treinamento. Depois é feita a média dos resultados de cada árvore decisória.