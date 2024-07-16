---
keywords: Experience Platform;página inicial;tópicos populares;conector kafka;kafka;;home;popular topics;kafka;kafka connector;Kafka;
solution: Experience Platform
title: Conector Kafka
description: O conector de fluxo do Adobe Experience Platform é baseado no Apache Kafka Connect. Essa biblioteca pode ser usada para transmitir eventos JSON de tópicos Kafka em seu data center diretamente para o Experience Platform em tempo real.
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# Conector [!DNL Kafka] para Adobe Experience Platform

O conector de fluxo do Adobe Experience Platform é baseado em [!DNL Apache Kafka Connect]. Esta biblioteca pode ser usada para transmitir eventos JSON de [!DNL Kafka] tópicos em seu data center diretamente para [!DNL Experience Platform] em tempo real.

O conector de fluxo é um conector de coletor (unidirecional), que fornece dados de tópicos [!DNL Kafka] para um ponto de extremidade registrado em [!DNL Experience Platform]. Para usar esse conector, você deve baixar a biblioteca, adicioná-la à implantação existente do [!DNL Kafka] e configurar o(s) [!DNL Kafka] tópico(s) para a URL HTTP de Streaming do Adobe. O código adicional é **não** necessário. O conector é compatível com os seguintes recursos:

- Coleta de dados autenticada
- Criação de lotes de mensagens para reduzir chamadas de rede e aumentar a taxa de transferência

Para obter mais informações sobre o conector [!DNL Kafka], incluindo instruções sobre como configurar o conector, leia o [guia de introdução](https://github.com/adobe/experience-platform-streaming-connect). Para obter um fluxo de trabalho mais detalhado, leia o [guia do desenvolvedor](https://www.adobe.com/go/kafka-connector-developer-guide).
