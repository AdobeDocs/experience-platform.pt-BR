---
keywords: Experience Platform, visão geral, atendimento ao cliente, tópicos populares, visão geral do atendimento ao cliente
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Visão geral do Customer AI
topic-legacy: Customer AI Overview
description: o Customer AI é usado para gerar pontuações de propensão personalizadas, como churn e conversão para perfis individuais em escala. Isso é feito sem precisar transformar as necessidades de negócios em um problema de aprendizado de máquina, escolher um algoritmo, treinar ou implantar.
landing-page-description: o Customer AI é usado para gerar pontuações de propensão personalizadas, como churn e conversão para perfis individuais em escala.
exl-id: 3e668103-e2a2-4ce6-a40a-8029a6aaa8dd
source-git-commit: 6c0e001419dc78d4ff87bebd0604c7add07b635f
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 26%

---


# Visão geral do Customer AI

A Customer AI, como parte dos Serviços inteligentes, fornece aos profissionais de marketing o poder de gerar previsões de clientes a nível individual com explicações.

Com a ajuda de fatores influentes, a IA do cliente pode informar o que um cliente deve fazer e por quê. Além disso, os profissionais de marketing podem se beneficiar das previsões e insights da IA do cliente para personalizar as experiências do cliente, disponibilizando as ofertas e mensagens mais apropriadas.

## Noções básicas sobre o Customer AI

o Customer AI é usado para gerar pontuações de propensão personalizadas, como churn e conversão para perfis individuais em escala. Isso é feito sem precisar transformar as necessidades de negócios em um problema de aprendizado de máquina, escolher um algoritmo, treinar ou implantar.

O Customer AI foi criado para:

- Forneça modelos de propensão do cliente de alta precisão para segmentação e definição de metas mais fortes.
- Ajuda para entender os fatores influentes e a probabilidade por trás de determinados comportamentos do cliente.
- Forneça opções personalizáveis para os casos de uso e dados exclusivos de sua empresa.
- Melhore o Perfil do cliente em tempo real com pontuações de propensão do cliente, como churn e conversão.
- Aprimore os perfis do cliente com fatores influentes para pontuações de propensão.
- Crie segmentos de clientes com base em fatores influentes e pontuações de propensão.

O cliente não foi criado para:

- A API do cliente não deve ser usada para prever preços dinâmicos ou o ponto de preço no qual o cliente fará uma compra.
- O Customer AI não pode determinar se a oferta aumentará a probabilidade do cliente comprar um item. Embora você possa decidir enviar ofertas de desconto com base em pontuações de propensão, não é necessariamente a melhor maneira de converter esses clientes.
- O Customer AI não é uma ferramenta de recomendações do produto. Se você tiver milhares de SKUs, não use o Customer AI como proxy para uma solução de recomendações de produto real, como [!DNL Adobe Target].
- O Customer AI não pode prever em qual estágio da Jornada de compra o cliente está, por exemplo, se ele estiver em estágios de &quot;consciência&quot;, &quot;consideração&quot;, &quot;compra&quot; ou &quot;retenção&quot;.
- Não use o Customer AI para determinar os clientes que provavelmente comprarão um lançamento de produto no futuro. Isso requer que alguns eventos de sucesso estejam presentes no passado para que a API do cliente treine com sucesso o algoritmo de aprendizado de máquina em seus dados.

O vídeo a seguir foi criado para oferecer suporte à compreensão da API do cliente.

>[!VIDEO](https://video.tv.adobe.com/v/32664?learn=on&quality=12)

## Como funciona

O Customer AI funciona analisando os dados existentes do Evento de experiência do consumidor para prever pontuações de abandono ou propensão de conversão. O Adobe sabe que a definição de churn e conversão não é uniforme em todos os casos de uso e, por esse motivo, você tem a capacidade de definir metas personalizadas como um conjunto de condições. Você pode configurar a meta prevista, desde que o evento de interesse esteja presente nos dados de entrada do Evento de experiência do consumidor.

## Próximas etapas

Você pode começar seguindo a [introdução](./getting-started.md) guia. Este guia aborda a configuração de todos os pré-requisitos necessários para o Customer AI. Se você já tiver todas as suas credenciais e dados prontos, visite  [configuração de uma instância do Customer AI](./user-guide/configure.md). Ela fornece etapas para usar a API do cliente.
