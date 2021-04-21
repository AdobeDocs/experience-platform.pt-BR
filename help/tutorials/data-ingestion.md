---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Tutoriais de assimilação de dados
topic-legacy: tutorial
type: Tutorial
description: A Assimilação de dados inclui a ingestão em lote, a assimilação de streaming e a assimilação usando conectores de origem.
exl-id: 51627acf-e90b-4911-aa54-4a59f3b6a8f9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 4%

---

# Assimilar dados em [!DNL Experience Platform]

A Adobe Experience Platform reúne dados de várias fontes para ajudar os profissionais de marketing a entender melhor o comportamento de seus clientes. Adobe [!DNL Experience Platform Data Ingestion] representa os vários métodos pelos quais [!DNL Platform] assimila dados dessas fontes, bem como como esses dados são mantidos no Data Lake para uso em downstream [!DNL Platform services]. [!DNL Data Ingestion] inclui assimilação em lote, assimilação de streaming e assimilação usando conectores de origem. Para saber mais, leia a [Visão geral da assimilação de dados](../ingestion/home.md) ou prossiga diretamente para a [Documentação de fontes](../sources/home.md).

## Criar uma conexão de origem na interface do usuário e na API

Os conectores de origem permitem assimilar dados de várias fontes, onde eles podem ser rotulados, estruturados e aprimorados usando [!DNL Platform services]. Para começar a criar um conector de origem, consulte a [visão geral das fontes](../sources/home.md).

## Assimilar dados em lote

O Adobe Experience Platform permite importar facilmente dados para [!DNL Platform] como arquivos em lote. Os exemplos de dados a serem assimilados podem incluir dados de perfil de um arquivo simples em um sistema CRM (como um arquivo Parquet) ou dados que estejam em conformidade com um esquema [!DNL Experience Data Model] (XDM) conhecido no Registro de Esquema. Para começar, visite os [dados de assimilação no tutorial da plataforma](../ingestion/tutorials/ingest-batch-data.md).

## Mapear um arquivo CSV para um esquema XDM

Para assimilar dados CSV no Adobe Experience Platform, os dados devem ser mapeados para um esquema [!DNL Experience Data Model] (XDM). Para etapas que mostram como mapear um arquivo CSV para um esquema XDM usando a interface do usuário [!DNL Experience Platform], siga o [mapear um arquivo CSV para um tutorial de esquema XDM](../ingestion/tutorials/map-a-csv-file.md).

## Criar uma conexão de transmissão

Para iniciar o streaming de dados em [!DNL Experience Platform], primeiro solicite um endpoint HTTP. Você tem a opção de configurar esse ponto de extremidade para impor o comportamento autenticado. Isso pode ser feito usando a interface do usuário [!DNL Platform] ou [!DNL Experience Platform] APIs. Para saber mais, siga os tutoriais para [criar uma conexão de transmissão usando a interface do usuário](../ingestion/tutorials/create-streaming-connection-ui.md) ou [criar uma conexão de transmissão usando APIs](../ingestion/tutorials/create-streaming-connection.md).

## Criar uma conexão de transmissão autenticada

A Coleta de dados autenticada permite que os serviços da Adobe Experience Platform, como [!DNL Real-time Customer Profile] e [!DNL Identity], diferenciem entre registros provenientes de fontes confiáveis e fontes não confiáveis. Para começar, siga o tutorial para [criar uma conexão de transmissão autenticada](../ingestion/tutorials/create-authenticated-streaming-connection.md).

## Registros de fluxo e dados da série cronológica

Com um conjunto de dados e conexões de steaming no lugar, é possível transmitir dados de registro ou de série de tempo em [!DNL Platform]. Para iniciar o streaming de dados de registro, siga os [dados de registro de fluxo no tutorial da plataforma](../ingestion/tutorials/streaming-record-data.md). Para começar a transmitir dados da série de tempo, siga os [dados da série de tempo de fluxo para a Plataforma](../ingestion/tutorials/streaming-time-series-data.md).

## Transmitir várias mensagens em uma única solicitação HTTP

Ao transmitir dados para o Adobe Experience Platform, fazer várias chamadas HTTP pode ser caro. Por exemplo, em vez de criar 200 solicitações HTTP com cargas de 1 KB, é muito mais eficiente criar 1 solicitação HTTP com 200 mensagens de 1 KB cada, com uma única carga de 200 KB. Quando usado corretamente, agrupar várias mensagens em uma única solicitação é uma excelente maneira de otimizar os dados que estão sendo enviados para [!DNL Experience Platform]. Para saber como enviar várias mensagens para [!DNL Experience Platform] em uma única solicitação HTTP usando assimilação de streaming, siga o [tutorial de envio de várias mensagens](../ingestion/tutorials/streaming-multiple-messages.md).
