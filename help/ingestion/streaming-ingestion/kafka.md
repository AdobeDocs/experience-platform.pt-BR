---
keywords: Experience Platform; home; tópicos populares; kafka; conector kafka; Kafka;
solution: Experience Platform
title: Conector Kafka
topic-legacy: overview
description: O conector de fluxo para Adobe Experience Platform é baseado no Apache Kafka Connect. Essa biblioteca pode ser usada para transmitir eventos JSON de tópicos Kafka no seu data center diretamente para o Experience Platform em tempo real.
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# [!DNL Kafka] conector para Adobe Experience Platform

O conector de fluxo para Adobe Experience Platform é baseado em [!DNL Apache Kafka Connect]. Essa biblioteca pode ser usada para transmitir eventos JSON de [!DNL Kafka] tópicos em seu data center diretamente para [!DNL Experience Platform] em tempo real.

O conector de fluxo é um conector de pia (unidirecional), fornecendo dados dos tópicos [!DNL Kafka] para um terminal registrado em [!DNL Experience Platform]. Para usar esse conector, você deve baixar a biblioteca, adicioná-la à implantação [!DNL Kafka] existente e configurar o(s) tópico(s) [!DNL Kafka] para o URL HTTP de transmissão do Adobe. O código adicional é **não** necessário. O conector é compatível com os seguintes recursos:

- Coleta de dados autenticada
- Agrupamento de mensagens para reduzir chamadas de rede e aumentar a taxa de transferência

Para obter mais informações sobre o conector [!DNL Kafka], incluindo instruções sobre como configurar o conector, leia o [guia de introdução](https://github.com/adobe/experience-platform-streaming-connect). Para obter um workflow mais detalhado, leia o [guia do desenvolvedor](https://www.adobe.com/go/kafka-connector-developer-guide).
