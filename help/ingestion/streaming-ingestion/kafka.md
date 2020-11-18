---
keywords: Experience Platform;home;popular topics;kafka;kafka connector;Kafka;
solution: Experience Platform
title: Conector Kafka
topic: overview
description: O conector de fluxo para Adobe Experience Platform é baseado no Apache Kafka Connect. Essa biblioteca pode ser usada para transmitir eventos JSON de tópicos Kafka em seu data center diretamente para Experience Platform em tempo real.
translation-type: tm+mt
source-git-commit: 7fc7f0e525d994904dc71b1eb7136f11c05d5672
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---


# [!DNL Kafka] conector para Adobe Experience Platform

O conector de fluxo para Adobe Experience Platform é baseado em [!DNL Apache Kafka Connect]. Essa biblioteca pode ser usada para transmitir eventos JSON de [!DNL Kafka] tópicos em seu data center diretamente para [!DNL Experience Platform] em tempo real.

O conector de fluxo é um conector de pia (unidirecional), que fornece dados de [!DNL Kafka] tópicos para um terminal registrado em [!DNL Experience Platform]. Para usar esse conector, você deve baixar a biblioteca, adicioná-la à sua [!DNL Kafka] implantação existente e configurar o(s) [!DNL Kafka] tópico(s) no URL HTTP de transmissão de Adobe. Código adicional **não** é necessário. O conector suporta os seguintes recursos:

- Coleta de dados autenticada
- Colocação de mensagens em lote para reduzir chamadas de rede e aumentar a throughput

Para obter mais informações sobre o [!DNL Kafka] conector, incluindo instruções sobre como configurar o conector, leia o guia [de](https://github.com/adobe/experience-platform-streaming-connect)introdução. Para obter um fluxo de trabalho mais detalhado, leia o guia [do](https://www.adobe.com/go/kafka-connector-developer-guide)desenvolvedor.