---
description: Saiba como usar a API de teste de destino baseada em arquivo para validar a configuração dos destinos baseados em arquivo criados por meio do Destination SDK.
title: API de teste de destino baseado em arquivo
exl-id: 2733fd00-af08-4763-a30e-a53ee56c0a19
source-git-commit: adf75720f3e13c066b5c244d6749dd0939865a6f
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# Visão geral da API de teste de destino baseado em arquivo

A API de teste de destino baseado em arquivo é um conjunto de endpoints que podem ser usados para validar a configuração dos destinos baseados em arquivo criados por meio do Destination SDK.

Recomendamos o uso dessas ferramentas para validar sua configuração antes de [enviar](../../guides/submit-destination.md) seu destino para revisão no Adobe.

Para obter os melhores resultados de teste, recomendamos usar essa API com base no diagrama de fluxo abaixo.

![Diagrama mostrando o fluxo de teste de destino recomendado](../../assets/testing-api/batch-destinations/file-based-testing-flow.png)

Consulte as seções abaixo para obter uma breve visão geral do que cada endpoint pode fazer.

## Gerar perfis de amostra {#generate-sample-profiles}

Use o ponto de extremidade de API `/sample-profiles` para gerar perfis de amostra com base no esquema de origem existente.

Os perfis de amostra podem ajudar você a entender a estrutura JSON de um perfil. Além disso, elas fornecem um padrão que pode ser personalizado com seus próprios dados de perfil para testes de destino adicionais.

Consulte a [documentação dedicada](file-based-sample-profile-generation-api.md) para saber como gerar perfis de amostra.

## Testar configuração de destino {#test-destination-configuration}

Use o ponto de extremidade de API `/testing/destinationInstance` para testar se o destino baseado em arquivo está configurado corretamente e verificar a integridade dos fluxos de dados para o destino configurado.

Você pode fazer solicitações ao ponto de extremidade de teste com ou sem adicionar [perfis de amostra](file-based-sample-profile-generation-api.md) à chamada. Se você não enviar nenhum perfil na solicitação, a API gerará um perfil de amostra automaticamente e o adicionará à solicitação.

Consulte a [documentação dedicada](file-based-destination-testing-api.md) para saber como testar sua configuração de destino com perfis de amostra.

## Exibir resultados detalhados da ativação {#view-detailed-activation-results}

Use o ponto de extremidade da API `/testing/destinationInstance` para exibir os detalhes completos dos resultados do teste de destino baseado em arquivo.

Este ponto de extremidade de API retorna o mesmo resultado que você obteria ao usar a [API de Serviço de Fluxo](../../../api/update-destination-dataflows.md) para monitorar fluxos de dados.

Consulte a [documentação dedicada](file-based-destination-results-api.md) para saber como exibir resultados detalhados da ativação.

## Renderizar campos de dados do cliente {#render-customer-data-fields}

Use o ponto de extremidade de API `/authoring/testing/template/render` para visualizar como seriam os [campos de dados do cliente](../../functionality/destination-configuration/customer-data-fields.md) modelados definidos na configuração de destino.

O endpoint da API gera valores aleatórios para os campos de dados do cliente e os retorna na resposta. Isso ajuda a validar a estrutura semântica dos campos de dados do cliente, como nomes de buckets ou caminhos de pastas.

Consulte a [documentação dedicada](file-based-render-template-api.md) para saber como gerar e visualizar valores para seus campos de dados de clientes.
