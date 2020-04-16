---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tutoriais de ingestão de dados
topic: tutorial
translation-type: tm+mt
source-git-commit: e4da80338dbfbad70dfb3cf7df9fe589e949e788

---


# Ingressar dados na plataforma Experience

A Adobe Experience Platform reúne dados de várias fontes para ajudar os profissionais de marketing a entender melhor o comportamento de seus clientes. A ingestão de dados da plataforma Adobe Experience representa os vários métodos pelos quais a plataforma ingere dados dessas fontes, bem como como como esses dados são persistentes no Data Lake para uso pelos serviços da plataforma downstream. A ingestão de dados inclui a ingestão em lote, a ingestão em streaming e a ingestão usando conectores de origem. Para saber mais, leia a visão geral [da Ingestão de](../ingestion/home.md) dados ou vá diretamente para a documentação [](../sources/home.md)Fontes.

## Criar um conector de origem na interface do usuário e na API

Os conectores de origem permitem que você ingira dados de várias fontes, onde eles podem ser rotulados, estruturados e aprimorados usando os serviços da plataforma. Para começar a criar um conector de origem, consulte a visão geral [das](../sources/home.md)fontes.

## Dados do lote de assimilação

O Adobe Experience Platform permite importar facilmente dados para a Plataforma como arquivos em lote. Exemplos de dados a serem ingeridos podem incluir dados de perfil de um arquivo simples em um sistema CRM (como um arquivo parquet) ou dados que estejam em conformidade com um schema do Modelo de Dados de Experiência (XDM) conhecido no Registro do Schema. Para começar, visite os dados de [ingestão no tutorial](../ingestion/tutorials/ingest-batch-data.md)da plataforma.

## Mapear um arquivo CSV para um Schema XDM

Para assimilar dados CSV na Adobe Experience Platform, os dados devem ser mapeados para um schema do Experience Data Model (XDM). Para obter etapas que mostram como mapear um arquivo CSV para um schema XDM usando a interface do usuário da plataforma Experience, siga o [mapeamento de um arquivo CSV para um tutorial](../ingestion/tutorials/map-a-csv-file.md)de schema XDM.

## Criar uma conexão de streaming

Para start de dados de streaming para a plataforma Experience, é necessário primeiro criar uma conexão HTTP de streaming. Ao criar uma conexão de streaming, você precisa fornecer detalhes importantes, como a fonte de dados de streaming, e se pretende enviar dados de uma fonte confiável (autenticada) ou não confiável (não autenticada). Isso pode ser feito usando a interface do usuário da plataforma ou as APIs da plataforma de experiência. Para saber mais, siga os tutoriais para [criar uma conexão de streaming usando a interface do usuário](../ingestion/tutorials/create-streaming-connection-ui.md) ou [criar uma conexão de streaming usando APIs](../ingestion/tutorials/create-streaming-connection.md).

## Criar uma conexão de streaming autenticada

A coleta de dados autenticada permite que os serviços da Adobe Experience Platform, como Perfil e identidade do cliente em tempo real, diferenciem entre registros provenientes de fontes confiáveis e fontes não confiáveis. Para começar, siga o tutorial para [criar uma conexão](../ingestion/tutorials/create-authenticated-streaming-connection.md)de streaming autenticada.

## Dados de registro de fluxo e de série cronológica

Com um conjunto de dados e conexões em vapor ativadas, é possível transmitir dados de registro ou de série de tempo para a Plataforma. Para começar a streaming de dados de registro, siga os dados de registro de [fluxo no tutorial](../ingestion/tutorials/streaming-record-data.md)da plataforma. Para começar a transmitir dados de séries de tempo, siga os dados de séries de tempo de [fluxo para a Plataforma](../ingestion/tutorials/streaming-time-series-data.md).

## Transmitir várias mensagens em uma única solicitação HTTP

Ao transmitir dados para a Adobe Experience Platform, fazer várias chamadas HTTP pode ser caro. Por exemplo, em vez de criar 200 solicitações HTTP com cargas de 1 KB, é muito mais eficiente criar 1 solicitação HTTP com 200 mensagens de 1 KB cada, com uma única carga de 200 KB. Quando usado corretamente, agrupar várias mensagens em uma única solicitação é uma excelente maneira de otimizar os dados que estão sendo enviados para a plataforma Experience. Para saber como enviar várias mensagens para a Experience Platform em uma única solicitação HTTP usando a assimilação de streaming, siga o tutorial [de](../ingestion/tutorials/streaming-multiple-messages.md)envio de várias mensagens.



