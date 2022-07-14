---
title: Atributos derivados
description: Os atributos derivados fornecem um meio conveniente de gerar atributos de sua escolha que podem ser atualizados a qualquer ritmo e publicados opcionalmente nos dados do Perfil do cliente em tempo real. Este documento fornece uma visão geral de como usar o Serviço de query para criar atributos derivados para usar com os dados do perfil.
hide: true
hidefromtoc: true
exl-id: 5d52b268-e2a3-411c-8242-3aa32e759937
source-git-commit: ae11d6f622c42d08373b7454ef920a80abaf2425
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Atributos derivados

O recurso de atributos derivados fornece um meio conveniente de gerar atributos de sua escolha a partir de outras informações disponíveis no lago de dados. Esses atributos podem ser atualizados a qualquer ritmo regular e, como opção, publicados nos dados do Perfil do cliente em tempo real. Atributos derivados atendem à necessidade de criar atributos complexos, como decílio, percentil e quartil, em vez de atributos mais simples, como máximo, contagem e média. Esses atributos podem ser calculados especificamente para um usuário individual ou para uma entidade comercial. Isso permite derivar atributos que podem ser diretamente creditados a um identificador, como endereços de email, IDs de dispositivo e números de telefone, e também derivar atributos que estão indiretamente associados a esse usuário ou perfil de negócios.

Atributos derivados são necessários para uma variedade de casos de uso quando os dados estão sendo analisados no lago de dados. Esses dados podem ser marcados para uso no Perfil do cliente em tempo real e usados em casos de uso downstream, como a criação de públicos-alvo altamente focados. Alguns casos de uso potenciais para esse recurso podem incluir:

* Identificação dos 10% mais baixos de assinantes com base na visualização por canal. Isso permitiria que os profissionais de marketing direcionassem um público-alvo específico e vendessem um novo pacote de assinantes.
* Identificação de um público que está no top 10% dos panfletos com base em suas milhas totais viajadas e tem status de &quot;panfleto&quot;. Este público-alvo poderia ser usado para direcionar seletivamente a venda de uma nova oferta de cartão de crédito.
* Determine a taxa de churn com base na assinatura.
* Identificar os 1% mais elevados do rendimento familiar numa província ou estado e fornecer uma medida do número de indivíduos que se mudaram para fora desse grupo coletivo nos últimos &quot;n&quot; meses.

## Atributos derivados complexos

Para criar uma classificação com base em uma ou mais métricas (como receita, duração da visualização e assim por diante) em uma dimensão específica (categoria), são necessários atributos derivados complexos. Deciles, quartis e percentis permitem flexibilidade e precisão ao classificar dados com atributos derivados.

Um decile é um método de dividir um conjunto de dados classificados em 10 partes iguais. Quando os dados são divididos em decodificações, uma classificação de decil é atribuída a cada linha no conjunto de dados. Isso permite que os dados sejam classificados em ordem decrescente ou crescente.

Uma classificação decile organiza os dados em ordem do mais baixo para o mais alto e é feita em uma escala de 1 a 10, onde cada número sucessivo corresponde a um aumento de 10 pontos percentuais.

Os buckets do decile representam o número de grupos classificados e são usados para atribuir uma classificação a uma dimensão (categoria) no conjunto de dados. O bucket pode ser um número ou uma expressão que resulta em um valor inteiro positivo para cada partição. Os buckets não devem ter um valor nulo.

Os quartis são usados para dividir a distribuição por quatro e percentis por 100.

## Atributos derivados analíticos

O Serviço de Consulta fornece funções integradas como sessão e último contato, entre outras, que você pode aplicar a qualquer dado de série de tempo para gerar atributos derivados relacionados a negócios. Você tem a opção de basear esses atributos derivados analíticos em uma ou mais identidades e, opcionalmente, publicar os dados no Perfil do cliente em tempo real, se necessário.

Alguns casos de uso potenciais para esse tipo de atributo derivado podem incluir:

* Rastreamento de produtos examinados durante uma sessão de usuário que estavam em falta.
* Rastreamento de métricas populares, como tamanho, cor ou categoria de produto dos produtos que estão sendo navegados ou comprados.
* Rastrear a fonte da plataforma que levou a uma compra ou navegação do produto.
* Rastreamento do item navegado mais recentemente por uma identidade.
* Métricas de rastreamento como o número médio de itens em um carrinho, abandono do carrinho ou frequência média de compra.

## Outros atributos derivados

Também é possível calcular métricas de negócios como um atributo derivado e usá-las junto com atributos simples, como código postal ou uma métrica agregada, como a contagem total. Por exemplo, uma contagem total com base em uma cidade ou província, ou contagem total com base em uma categoria de negócios e uma cidade/província.

## Próximas etapas e casos de uso

Ao ler este documento, você tem uma melhor compreensão de como os atributos derivados do Serviço de query facilitam casos de uso complexos para maximizar o utilitário dos seus dados. Em seguida, você deve ler o [caso de uso de atributo derivado com base em decil](./deciles-use-case.md) para ver como esse recurso é aplicado em um cenário real.
