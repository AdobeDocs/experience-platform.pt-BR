---
description: A API de teste de destino baseado em arquivo é uma coleção de endpoints que podem ser usados para validar a configuração dos destinos baseados em arquivo criados por meio do Destination SDK.
title: API de teste de destino baseado em arquivo
exl-id: 2733fd00-af08-4763-a30e-a53ee56c0a19
source-git-commit: 44e056407f5089c927752f00cc6bf173d7640b83
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# API de teste de destino baseado em arquivo

## Visão geral {#overview}

A API de teste de destino baseado em arquivo é um conjunto de endpoints que podem ser usados para validar a configuração dos destinos baseados em arquivo criados por meio do Destination SDK.

Recomendamos o uso dessas ferramentas para validar a configuração antes de [enviando](submit-destination.md) seu destino para revisão no Adobe.

Para obter os melhores resultados de teste, recomendamos usar essa API com base no diagrama de fluxo abaixo.

![Diagrama que mostra o fluxo de teste de destino recomendado](assets/file-based-testing-flow.png)

Consulte as seções abaixo para obter uma breve visão geral do que cada endpoint pode fazer.

## Gerar perfis de amostra {#generate-sample-profiles}

Use o `/sample-profiles` Endpoint da API para gerar perfis de amostra com base no esquema de origem existente.

Os perfis de amostra podem ajudar você a entender a estrutura JSON de um perfil. Além disso, elas fornecem um padrão que pode ser personalizado com seus próprios dados de perfil para testes de destino adicionais.

Consulte a [documentação dedicada](file-based-sample-profile-generation-api.md) para saber como gerar perfis de amostra.

## Testar configuração de destino {#test-destination-configuration}

Use o `/testing/destinationInstance` Endpoint da API para testar se o destino baseado em arquivo está configurado corretamente e verificar a integridade dos fluxos de dados para o destino configurado.

Você pode fazer solicitações para o endpoint de teste com ou sem adicionar [perfis de amostra](file-based-sample-profile-generation-api.md) à chamada. Se você não enviar nenhum perfil na solicitação, a API gerará um perfil de amostra automaticamente e o adicionará à solicitação.

Consulte a [documentação dedicada](file-based-destination-testing-api.md) para saber como testar sua configuração de destino com perfis de amostra.

## Exibir resultados detalhados da ativação {#view-detailed-activation-results}

Use o `/testing/destinationInstance` O endpoint da API permite exibir os detalhes completos dos resultados do teste de destino com base em arquivo.

Esse ponto de extremidade de API retorna o mesmo resultado que você obteria ao usar o [API do serviço de fluxo](../api/update-destination-dataflows.md) para monitorar fluxos de dados.

Consulte a [documentação dedicada](file-based-destination-results-api.md) para saber como exibir resultados detalhados da ativação.

## Renderizar campos de dados do cliente {#render-customer-data-fields}

Use o `/authoring/testing/template/render` Endpoint da API para visualizar como o modelo foi [campos de dados do cliente](file-based-destination-configuration.md#customer-data-fields) definido na configuração de destino seria semelhante a.

O endpoint da API gera valores aleatórios para os campos de dados do cliente e os retorna na resposta. Isso ajuda a validar a estrutura semântica dos campos de dados do cliente, como nomes de buckets ou caminhos de pastas.

Consulte a [documentação dedicada](file-based-render-template-api.md) para saber como gerar e visualizar valores para os campos de dados do cliente.
