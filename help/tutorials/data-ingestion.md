---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tutoriais de ingestão de dados
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---


# Ingressar dados em [!DNL Experience Platform]

O Adobe Experience Platform reúne dados de várias fontes para ajudar os profissionais de marketing a entender melhor o comportamento de seus clientes. O Adobe [!DNL Experience Platform Data Ingestion] representa os vários métodos pelos quais [!DNL Platform] ingere dados dessas fontes, bem como como como esses dados são persistentes no Data Lake para uso em downstream [!DNL Platform services]. [!DNL Data Ingestion] inclui a ingestão em lote, a ingestão em fluxo contínuo e a ingestão por meio de conectores de origem. Para saber mais, leia a visão geral [da Ingestão de](../ingestion/home.md) dados ou vá diretamente para a documentação [](../sources/home.md)Fontes.

## Criar um conector de origem na interface do usuário e na API

Os conectores de origem permitem que você ingira dados de várias fontes, onde eles podem ser rotulados, estruturados e aprimorados usando [!DNL Platform services]. Para começar a criar um conector de origem, consulte a visão geral [das](../sources/home.md)fontes.

## Dados do lote de assimilação

O Adobe Experience Platform permite importar facilmente dados para [!DNL Platform] como arquivos em lote. Exemplos de dados a serem ingeridos podem incluir dados de perfil de um arquivo simples em um sistema CRM (como um arquivo parquet) ou dados que estejam em conformidade com um schema conhecido [!DNL Experience Data Model] (XDM) no Registro do Schema. Para começar, visite os dados de [ingestão no tutorial](../ingestion/tutorials/ingest-batch-data.md)da Platform.

## Mapear um arquivo CSV para um Schema XDM

Para assimilar dados CSV no Adobe Experience Platform, os dados devem ser mapeados para um schema [!DNL Experience Data Model] (XDM). Para obter etapas que mostram como mapear um arquivo CSV para um schema XDM usando a interface do [!DNL Experience Platform] usuário, siga o [mapeamento de um arquivo CSV para um tutorial](../ingestion/tutorials/map-a-csv-file.md)de schema XDM.

## Criar uma conexão de streaming

Para que os dados de streaming de start sejam enviados para [!DNL Experience Platform], é necessário primeiro solicitar um terminal HTTP. Você tem a opção de configurar esse terminal para impor um comportamento autenticado. Isso pode ser feito usando a interface do [!DNL Platform] usuário ou [!DNL Experience Platform] as APIs. Para saber mais, siga os tutoriais para [criar uma conexão de streaming usando a interface do usuário](../ingestion/tutorials/create-streaming-connection-ui.md) ou [criar uma conexão de streaming usando APIs](../ingestion/tutorials/create-streaming-connection.md).

## Criar uma conexão de streaming autenticada

A coleta de dados autenticada permite que serviços de Adobe Experience Platform, como [!DNL Real-time Customer Profile] e [!DNL Identity], diferenciem entre registros provenientes de fontes confiáveis e fontes não confiáveis. Para começar, siga o tutorial para [criar uma conexão](../ingestion/tutorials/create-authenticated-streaming-connection.md)de streaming autenticada.

## Dados de registro de fluxo e de série cronológica

Com um conjunto de dados e conexões em vapor instaladas, é possível transmitir dados de registro ou de série de tempo para [!DNL Platform]. Para começar a streaming de dados de registro, siga os dados de registro de [fluxo no tutorial](../ingestion/tutorials/streaming-record-data.md)do Platform. Para começar a transmitir dados de séries de tempo, siga os dados de séries de tempo de [fluxo para o Platform](../ingestion/tutorials/streaming-time-series-data.md).

## Transmitir várias mensagens em uma única solicitação HTTP

Ao transmitir dados para o Adobe Experience Platform, fazer várias chamadas HTTP pode ser caro. Por exemplo, em vez de criar 200 solicitações HTTP com cargas de 1 KB, é muito mais eficiente criar 1 solicitação HTTP com 200 mensagens de 1 KB cada, com uma única carga de 200 KB. Quando usado corretamente, agrupar várias mensagens em uma única solicitação é uma excelente maneira de otimizar os dados que estão sendo enviados para [!DNL Experience Platform]. Para saber como enviar várias mensagens para [!DNL Experience Platform] dentro de uma única solicitação HTTP usando a ingestão de streaming, siga o tutorial [de](../ingestion/tutorials/streaming-multiple-messages.md)envio de várias mensagens.



