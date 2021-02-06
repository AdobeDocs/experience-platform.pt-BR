---
keywords: Experience Platform;casa;tópicos populares;kafka;conector kafka;Kafka;
solution: Experience Platform
title: Conector Kafka
topic: overview
description: O conector de fluxo para Adobe Experience Platform é baseado no Apache Kafka Connect. Essa biblioteca pode ser usada para transmitir eventos JSON de tópicos Kafka em seu data center diretamente para Experience Platform em tempo real.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# [!DNL Kafka] conector para Adobe Experience Platform

O conector de fluxo para Adobe Experience Platform é baseado em [!DNL Apache Kafka Connect]. Essa biblioteca pode ser usada para transmitir eventos JSON de [!DNL Kafka] tópicos em seu data center diretamente para [!DNL Experience Platform] em tempo real.

O conector de fluxo é um conector de dissipador (unidirecional), que fornece dados de [!DNL Kafka] tópicos para um terminal registrado em [!DNL Experience Platform]. Para usar esse conector, você deve baixar a biblioteca, adicioná-la à sua implantação [!DNL Kafka] existente e configurar o(s) tópico(s) [!DNL Kafka] para o URL HTTP Adobe Streaming. O código adicional é **não** necessário. O conector suporta os seguintes recursos:

- Coleta de dados autenticada
- Colocação de mensagens em lote para reduzir chamadas de rede e aumentar a throughput

Para obter mais informações sobre o conector [!DNL Kafka], incluindo instruções sobre como configurar o conector, leia o [guia de introdução](https://github.com/adobe/experience-platform-streaming-connect). Para obter um fluxo de trabalho mais detalhado, leia o [guia do desenvolvedor](https://www.adobe.com/go/kafka-connector-developer-guide).