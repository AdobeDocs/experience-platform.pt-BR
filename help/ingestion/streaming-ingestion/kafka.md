---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conector Kafka
topic: overview
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# [!DNL Kafka] conector para Adobe Experience Platform

O conector de fluxo para Adobe Experience Platform é baseado em [!DNL Apache Kafka Connect]. Essa biblioteca pode ser usada para transmitir eventos JSON de [!DNL Kafka] tópicos em seu data center diretamente para [!DNL Experience Platform] em tempo real.

O conector de fluxo é um conector de pia (unidirecional), que fornece dados de [!DNL Kafka] tópicos para um terminal registrado em [!DNL Experience Platform]. Para usar esse conector, você deve baixar a biblioteca, adicioná-la à sua [!DNL Kafka] implantação existente e configurar o(s) [!DNL Kafka] tópico(s) no URL HTTP de transmissão de Adobe. Código adicional **não** é necessário. O conector suporta os seguintes recursos:

- Coleta de dados autenticada
- Colocação de mensagens em lote para reduzir chamadas de rede e aumentar a throughput

Para obter mais informações sobre o [!DNL Kafka] conector, incluindo instruções sobre como configurar o conector, leia o guia [de](https://github.com/adobe/experience-platform-streaming-connect)introdução. Para obter um fluxo de trabalho mais detalhado, leia o guia [do](https://github.com/adobe/experience-platform-streaming-connect/blob/master/DEVELOPER_GUIDE.md)desenvolvedor.