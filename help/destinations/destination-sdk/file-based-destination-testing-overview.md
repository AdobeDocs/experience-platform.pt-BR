---
description: A API de teste de destino baseada em arquivo é uma coleção de endpoints que você pode usar para validar a configuração de destinos com base em arquivo criados pelo Destination SDK.
title: API de teste de destino baseada em arquivo
source-git-commit: d2d362f4b61e04fc2fa4d9cd9db70ed94a850642
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# API de teste de destino baseada em arquivo

## Visão geral {#overview}

A API de teste de destino baseada em arquivo é um conjunto de endpoints que você pode usar para validar a configuração de destinos com base em arquivo criados pelo Destination SDK.

Recomendamos usar essas ferramentas para validar sua configuração antes de [submissão](submit-destination.md) seu destino para análise no Adobe.

Para obter os melhores resultados de teste, recomendamos usar essa API com base no diagrama de fluxo abaixo.

![Diagrama que mostra o fluxo de ensaio de destino recomendado](assets/file-based-testing-flow.png)

Consulte as seções abaixo para obter uma breve visão geral do que cada endpoint pode fazer.

## Ponto de extremidade de geração de amostra {#sample-generation-endpoint}

Esse terminal ajuda a gerar perfis de amostra com base no esquema de origem existente.

Os perfis de amostra ajudam você a entender a estrutura JSON de um perfil. Além disso, elas fornecem um backbone que você pode personalizar com seus próprios dados de perfil, para testes de destino adicionais.

Consulte a [documentação dedicada](file-based-sample-profile-generation-api.md) para saber como gerar perfis de amostra.

## Ponto de extremidade do teste de configuração de destino {#destination-configuration-testing-endpoint}

Esse terminal ajuda a testar se o destino baseado em arquivo está configurado corretamente e verificar a integridade dos fluxos de dados para o destino configurado.

Você pode fazer solicitações ao endpoint de teste com ou sem adicionar [perfis de amostra](file-based-sample-profile-generation-api.md) à chamada . Se você não enviar perfis na solicitação, a API gera um perfil de amostra automaticamente e o adiciona à solicitação.

Consulte a [documentação dedicada](file-based-destination-testing-api.md) para saber como testar a configuração de destino com perfis de amostra.

## Ponto de extremidade dos resultados da ativação {#activation-results}

Esse ponto de extremidade ajuda você a visualizar os detalhes completos dos resultados de testes de destino baseados em arquivo.

Esse ponto de extremidade de API retorna o mesmo resultado que você obteria ao usar a variável [API de Serviço de Fluxo](../api/update-destination-dataflows.md) para monitorar os fluxos de dados.

Consulte a [documentação dedicada](file-based-destination-results-api.md) para saber como visualizar resultados detalhados da ativação.

## Ponto final de renderização de campos do cliente {#customer-fields-rendering-endpoint}

Esse endpoint ajuda a visualizar como o modelo [campos de dados do cliente](file-based-destination-configuration.md#customer-data-fields) definido na configuração de destino, seria parecido.

O endpoint gera valores aleatórios para os campos de dados do cliente e os retorna na resposta. Isso ajuda a validar a estrutura semântica dos campos de dados do cliente, como nomes de bucket ou caminhos de pasta.

Consulte a [documentação dedicada](file-based-render-template-api.md) para saber como visualizar resultados detalhados da ativação.