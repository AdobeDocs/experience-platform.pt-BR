---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conector Kafka
topic: overview
translation-type: tm+mt
source-git-commit: f80b2e1d787d1f8d9fe8ac306422aa7744a69cd3

---


# Conector Kafka para Adobe Experience Platform

O conector de fluxo para a Adobe Experience Platform é baseado no Apache Kafka Connect. Essa biblioteca pode ser usada para transmitir eventos JSON de tópicos Kafka em seu data center diretamente para a plataforma Experience em tempo real.

O conector de fluxo é um conector de pia (unidirecional), que fornece dados dos tópicos da Kafka para um terminal registrado na plataforma Experience. Para usar esse conector, você deve baixar a biblioteca, adicioná-la à implantação do Kafka existente e configurar os tópicos do Kafka para o URL HTTP de transmissão da Adobe. Código adicional **não** é necessário. O conector suporta os seguintes recursos:

- Coleta de dados autenticada
- Colocação de mensagens em lote para reduzir chamadas de rede e aumentar a throughput

Para obter mais informações sobre o conector Kafka, incluindo instruções sobre como configurar o conector, leia o guia [de](https://github.com/adobe/experience-platform-streaming-connect)introdução. Para obter um fluxo de trabalho mais detalhado, leia o guia [do](https://github.com/adobe/experience-platform-streaming-connect/blob/master/DEVELOPER_GUIDE.md)desenvolvedor.