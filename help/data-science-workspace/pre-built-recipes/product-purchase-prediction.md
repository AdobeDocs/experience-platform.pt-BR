---
keywords: Experience Platform;receita de compra do produto;Data Science Workspace;tópicos populares;receitas;pré-criar fórmula
solution: Experience Platform
title: Receita de Previsão de Compra do Produto
description: 'A fórmula Previsão de compra do produto permite prever a probabilidade de um determinado tipo de evento de compra do cliente: uma compra de produto, por exemplo.'
exl-id: 66a45629-33a3-4081-8dbd-b864983b8f57
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 5%

---

# Receita de previsão de compra de produto

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

A fórmula Previsão de compra do produto permite prever a probabilidade de um determinado tipo de evento de compra do cliente: uma compra de produto, por exemplo.

![](../images/pre-built-recipes/ppp_bigpicture.png)

O documento a seguir responderá perguntas como:

* Para quem esta receita foi criada?
* O que esta receita faz?

## Para quem esta receita foi criada?

Sua marca busca aumentar as vendas trimestrais para sua linha de produtos por meio de promoções eficazes e direcionadas para seus clientes. No entanto, nem todos os clientes são iguais e você quer o seu dinheiro no valor. A quem você direciona? Quais de seus clientes têm maior probabilidade de responder sem achar sua promoção intrusiva? Como você personaliza suas promoções para cada cliente? Em quais canais você deve confiar e quando enviar promoções?

## O que esta receita faz?

A fórmula de Previsão de compra do produto usa o aprendizado de máquina para prever o comportamento de compra do cliente. Ela faz isso aplicando um classificador de floresta aleatória personalizado e um Experience Data Model (XDM) de duas camadas para prever a probabilidade de um evento de compra. O modelo utiliza dados de entrada incorporando informações de perfil do cliente e histórico de compras anteriores, além de assumir como padrão parâmetros de configuração predeterminados por nossos cientistas de dados para melhorar a precisão preditiva.

## Esquema de dados

Esta fórmula usa [esquemas XDM](../../xdm/home.md) para modelar os dados. O esquema usado para esta fórmula é mostrado abaixo:

| Nome do campo | Tipo |
| --- | --- |
| userId | String |
| genderRatio | Número |
| ageY | Número |
| ageM | Número |
| optinEmail | Booleano |
| optinMobile | Booleano |
| optinAddress | Booleano |
| criado | Número inteiro |
| totalOrders | Número |
| totalItems | Número |
| orderDate1 | Número |
| shippingDate1 | Número |
| totalPrice1 | Número |
| imposto1 | Número |
| orderDate2 | Número |
| shippingDate2 | Número |
| totalPrice2 | Número |


## Algoritmo

Primeiro, o conjunto de dados de treinamento no esquema *ProductPrediction* é carregado. Aqui, o modelo é treinado usando um [classificador aleatório de floresta](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html). Classificador de floresta aleatória é um tipo de algoritmo conjunto que se refere a um algoritmo que combina vários algoritmos para obter melhor desempenho preditivo. A ideia por trás do algoritmo é que o classificador de floresta aleatória constrói várias árvores de decisão e as mescla para criar uma previsão mais precisa e estável.

Esse processo começa com a criação de um conjunto de árvores de decisão que seleciona aleatoriamente subconjuntos de dados de treinamento. Depois, é feita a média dos resultados de cada árvore decisória.
