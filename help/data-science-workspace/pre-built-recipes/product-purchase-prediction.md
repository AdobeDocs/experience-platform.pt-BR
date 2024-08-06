---
keywords: Experience Platform;receita de compra do produto;Data Science Workspace;tópicos populares;receitas;pré-criar fórmula
solution: Experience Platform
title: Receita de Previsão de Compra do Produto
description: 'A fórmula Previsão de compra do produto permite prever a probabilidade de um determinado tipo de evento de compra do cliente: uma compra de produto, por exemplo.'
exl-id: 66a45629-33a3-4081-8dbd-b864983b8f57
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 5%

---

# Receita de previsão de compra de produto

>[!NOTE]
>
>O Área de trabalho de ciência de dados não está mais disponível para compra.
>
>Esta documentação destina-se a clientes existentes com direitos anteriores à Data Science Área de trabalho.

A fórmula de Previsão de compra de produtos permite que você preveja a probabilidade de determinado tipo de evento de compra do cliente - uma compra de produto para instância.

![](../images/pre-built-recipes/ppp_bigpicture.png)

A seguinte documento responderá a perguntas como:
* Para quem este fórmula construído?
* O que isso fórmula faz?

## Para quem esta receita foi criada?

Sua marca busca aumentar as vendas trimestrais para sua linha de produtos por meio de promoções eficazes e direcionadas para seus clientes. No entanto, nem todos os clientes são iguais e você quer o seu dinheiro no valor. A quem você direciona? Quais de seus clientes têm maior probabilidade de responder sem achar sua promoção intrusiva? Como você personaliza suas promoções para cada cliente? Em quais canais você deve confiar e quando enviar promoções?

## O que isso fórmula faz?

O fórmula de Previsão de compra de produtos utiliza o aprendizado de máquina para prever o comportamento de compra do cliente. Ele faz isso aplicando um classificador random forest personalizado e um XDM (Experience Data Model) de dois níveis para prever a probabilidade de um evento de compra. O modelo usa dados de entrada incorporando informações de perfil do cliente e histórico de compras anteriores e o padrão para parâmetros de configuração pré-determinados determinados por nossos Cientistas de Dados para aumentar a precisão preditiva.

## schema de dados

Essa fórmula usa esquemas [](../../xdm/home.md) XDM para modelar os dados. A schema usada para esta fórmula é mostrada abaixo:

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
| tax1 | Número |
| orderDate2 | Número |
| shippingDate2 | Número |
| totalPrice2 | Número |


## Algoritmo

Primeiro, a treinamento conjunto de dados no *ProductPrediction* schema é carregada. A partir daqui, o modelo é treinado usando um [classificador](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html) random forest. Random forest classifier é um tipo de algoritmo conjunto que se refere a um algoritmo que combina vários algoritmos para obter um desempenho preditivo melhorado. A ideia por trás do algoritmo é que o classificador random forest constrói várias árvores de decisão e as une para criar uma previsão mais precisa e estável.

Esse processo começa com a criação de um conjunto de árvores de decisão que seleciona aleatoriamente subconjuntos de dados de treinamento. Depois, é feita a média dos resultados de cada árvore decisória.
