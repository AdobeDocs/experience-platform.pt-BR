---
title: Conjuntos de dados derivados
description: Os conjuntos de dados derivados fornecem um meio conveniente de gerar conjuntos de dados de sua escolha que podem ser atualizados em qualquer cadência regular e, opcionalmente, publicados nos dados do Perfil do cliente em tempo real. Este documento fornece uma visão geral de como usar o Serviço de consulta para criar conjuntos de dados derivados para usar com os dados do seu Perfil.
exl-id: 5d52b268-e2a3-411c-8242-3aa32e759937
source-git-commit: 7364da23c261d83681af605047a7cd7539f4a83f
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# Conjuntos de dados derivados

O recurso de conjuntos de dados derivados fornece um meio conveniente de gerar conjuntos de dados de sua escolha a partir de outras informações disponíveis no data lake. Esses conjuntos de dados podem ser atualizados em qualquer cadência regular e, opcionalmente, publicados nos dados do Perfil do cliente em tempo real. Os conjuntos de dados derivados atendem à necessidade de criar conjuntos de dados complexos, como decis, percentis e quartis, em vez de conjuntos mais simples, como máximo, contagem e média. Esses conjuntos de dados podem ser calculados especificamente para um usuário individual ou para uma entidade de negócios. Isso permite derivar conjuntos de dados que podem ser diretamente certificados para um identificador, como endereços de email, IDs de dispositivo e números de telefone, além de derivar conjuntos de dados que são indiretamente associados a esse usuário ou perfil de negócios.

Os conjuntos de dados derivados são necessários para uma variedade de casos de uso quando os dados estão sendo analisados no data lake. Esses dados podem ser marcados para uso no Perfil do cliente em tempo real e usados em casos de uso downstream, como a criação de públicos-alvo altamente focados. Alguns casos de uso em potencial para esse recurso podem incluir:

* Identificação dos 10% mais baixos de assinantes com base na audiência por canal. Isso permitiria que os profissionais de marketing segmentassem um público específico e vendessem um novo pacote de assinantes.
* Identificação de um público-alvo que está no top 10% dos panfletos com base no total de milhas percorridas e tem o status &quot;Panfleto&quot;. Esse público-alvo pode ser usado para direcionar seletivamente a venda de uma nova oferta de cartão de crédito.
* Determine a taxa de churn com base na assinatura.
* Identificando o 1% superior da renda familiar em uma província ou estado, e fornecendo uma medida do número de indivíduos que saem desse grupo coletivo nos últimos &quot;n&quot; meses.

## Conjuntos de dados complexos derivados

Para criar uma classificação com base em uma ou mais métricas (como receita, duração da visualização e assim por diante) em uma dimensão específica (categoria), são necessários conjuntos de dados derivados complexos. Decis, quartis e percentis permitem flexibilidade e precisão ao classificar dados com conjuntos de dados derivados.

Um decil é um método de dividir um conjunto de dados classificados em 10 partes iguais. Quando os dados são divididos em decis, uma classificação de decis é atribuída a cada linha no conjunto de dados. Isso permite que os dados sejam classificados em ordem decrescente ou crescente.

Uma classificação decimal organiza os dados em ordem do mais baixo para o mais alto e é feita em uma escala de 1 a 10, onde cada número sucessivo corresponde a um aumento de 10 pontos percentuais.

Os intervalos de decis representam o número de grupos classificados e são usados para atribuir uma classificação a uma dimensão (categoria) no conjunto de dados. O bucket pode ser um número ou uma expressão que é avaliada como um valor inteiro positivo para cada partição. Os buckets não devem ter um valor nulo.

Quartis são usados para dividir a distribuição por quatro e percentis por 100.

## Conjuntos de dados derivados analíticos

O Serviço de consulta fornece funções integradas, como sessão e último contato, entre outras, que você pode aplicar a qualquer dado de série temporal para gerar conjuntos de dados derivados relacionados a negócios. Você tem a opção de basear esses conjuntos de dados derivados analíticos em uma ou mais identidades e, opcionalmente, publicar os dados no Perfil do cliente em tempo real, se necessário.

Alguns possíveis casos de uso para esse tipo de atributo derivado podem incluir:

* Rastreamento de produtos verificados durante uma sessão de usuário que estavam indisponíveis.
* Rastrear métricas populares, como tamanho, cor ou categoria do produto, dos produtos que estão sendo pesquisados ou comprados.
* Rastrear a origem da plataforma que levou a uma pesquisa ou compra do produto.
* Rastreamento do item pesquisado mais recentemente por uma identidade.
* Métricas de rastreamento, como número médio de itens em um carrinho, abandono de carrinho ou frequência média de compra.

## Outros conjuntos de dados derivados

Você também pode calcular métricas comerciais como um atributo derivado e usá-las em conjunto com conjuntos de dados simples, como um código postal, ou uma métrica agregada, como a contagem total. Por exemplo, uma contagem total com base em uma cidade ou província ou uma contagem total com base em uma categoria comercial e uma cidade/província.

## Próximas etapas e casos de uso

Ao ler este documento, você entende melhor como os conjuntos de dados derivados do Serviço de consulta facilitam casos de uso complexos para maximizar a utilidade dos seus dados. Em seguida, leia a [caso de uso de atributo derivado baseado em decil](../../use-cases/deciles-use-case.md) para ver como esse recurso é aplicado em um cenário real.
