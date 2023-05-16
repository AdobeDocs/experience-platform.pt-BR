---
description: Saiba como usar a API de teste de destino baseada em arquivo para validar a configuração de destinos com base em arquivo criada pelo Destination SDK.
title: API de teste de destino baseada em arquivo
exl-id: 2733fd00-af08-4763-a30e-a53ee56c0a19
source-git-commit: adf75720f3e13c066b5c244d6749dd0939865a6f
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# Visão geral da API de teste de destino baseada em arquivo

A API de teste de destino baseada em arquivo é um conjunto de endpoints que você pode usar para validar a configuração de destinos com base em arquivo criados pelo Destination SDK.

Recomendamos usar essas ferramentas para validar sua configuração antes de [submissão](../../guides/submit-destination.md) seu destino para análise no Adobe.

Para obter os melhores resultados de teste, recomendamos usar essa API com base no diagrama de fluxo abaixo.

![Diagrama que mostra o fluxo de ensaio de destino recomendado](../../assets/testing-api/batch-destinations/file-based-testing-flow.png)

Consulte as seções abaixo para obter uma breve visão geral do que cada endpoint pode fazer.

## Gerar perfis de amostra {#generate-sample-profiles}

Use o `/sample-profiles` Ponto de extremidade da API para gerar perfis de amostra com base no esquema de origem existente.

Os perfis de amostra podem ajudar você a entender a estrutura JSON de um perfil. Além disso, elas fornecem um padrão que você pode personalizar com seus próprios dados de perfil, para testes de destino adicionais.

Consulte a [documentação dedicada](file-based-sample-profile-generation-api.md) para saber como gerar perfis de amostra.

## Testar configuração de destino {#test-destination-configuration}

Use o `/testing/destinationInstance` Ponto de extremidade de API para testar se o destino baseado em arquivo está configurado corretamente e verificar a integridade dos fluxos de dados para o destino configurado.

Você pode fazer solicitações ao endpoint de teste com ou sem adicionar [perfis de amostra](file-based-sample-profile-generation-api.md) à chamada . Se você não enviar perfis na solicitação, a API gera um perfil de amostra automaticamente e o adiciona à solicitação.

Consulte a [documentação dedicada](file-based-destination-testing-api.md) para saber como testar a configuração de destino com perfis de amostra.

## Exibir resultados detalhados da ativação {#view-detailed-activation-results}

Use o `/testing/destinationInstance` endpoint da API para visualizar os detalhes completos dos resultados de teste de destino com base em arquivo.

Esse ponto de extremidade de API retorna o mesmo resultado que você obteria ao usar a variável [API de Serviço de Fluxo](../../../api/update-destination-dataflows.md) para monitorar os fluxos de dados.

Consulte a [documentação dedicada](file-based-destination-results-api.md) para saber como visualizar resultados detalhados da ativação.

## Renderizar campos de dados do cliente {#render-customer-data-fields}

Use o `/authoring/testing/template/render` endpoint da API para visualizar como o modelo foi [campos de dados do cliente](../../functionality/destination-configuration/customer-data-fields.md) definido na configuração de destino, seria parecido.

O endpoint da API gera valores aleatórios para os campos de dados do cliente e os retorna na resposta. Isso ajuda a validar a estrutura semântica dos campos de dados do cliente, como nomes de bucket ou caminhos de pasta.

Consulte a [documentação dedicada](file-based-render-template-api.md) para saber como gerar e visualizar valores para os campos de dados do cliente.
