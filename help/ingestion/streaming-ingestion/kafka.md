---
keywords: Experience Platform; home; tópicos populares; kafka; conector kafka; Kafka;
solution: Experience Platform
title: Conector Kafka
topic: visão geral
description: O conector de fluxo para a Adobe Experience Platform é baseado no Apache Kafka Connect. Essa biblioteca pode ser usada para transmitir eventos JSON de tópicos do Kafka no seu data center diretamente para a Experience Platform em tempo real.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# [!DNL Kafka] conector para a Adobe Experience Platform

O conector de fluxo para a Adobe Experience Platform é baseado em [!DNL Apache Kafka Connect]. Essa biblioteca pode ser usada para transmitir eventos JSON de [!DNL Kafka] tópicos em seu data center diretamente para [!DNL Experience Platform] em tempo real.

O conector de fluxo é um conector de pia (unidirecional), fornecendo dados dos tópicos [!DNL Kafka] para um terminal registrado em [!DNL Experience Platform]. Para usar esse conector, você deve baixar a biblioteca, adicioná-la à implantação [!DNL Kafka] existente e configurar o(s) tópico(s) [!DNL Kafka] para o URL HTTP do Adobe Streaming. O código adicional é **não** necessário. O conector é compatível com os seguintes recursos:

- Coleta de dados autenticada
- Agrupamento de mensagens para reduzir chamadas de rede e aumentar a taxa de transferência

Para obter mais informações sobre o conector [!DNL Kafka], incluindo instruções sobre como configurar o conector, leia o [guia de introdução](https://github.com/adobe/experience-platform-streaming-connect). Para obter um workflow mais detalhado, leia o [guia do desenvolvedor](https://www.adobe.com/go/kafka-connector-developer-guide).