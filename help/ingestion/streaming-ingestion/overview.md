---
keywords: Experience Platform;home;popular topics;data ingestion;ingested data;streaming
solution: Experience Platform
title: Visão geral da ingestão de streaming do Adobe Experience Platform
topic: overview
description: A ingestão de streaming para Adobe Experience Platform fornece aos usuários um método para enviar dados de dispositivos cliente e servidor para o Experience Platform em tempo real.
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 3%

---


# Visão geral da assimilação de transmissão

A ingestão de streaming para Adobe Experience Platform fornece aos usuários um método para enviar dados de dispositivos cliente e servidor para [!DNL Experience Platform] em tempo real.

## O que você pode fazer com a ingestão de streaming?

A Adobe Experience Platform permite que você direcione experiências coordenadas, consistentes e relevantes, gerando um [!DNL Real-time Customer Profile] para cada um de seus clientes individuais. A inclusão de streaming desempenha um papel fundamental na criação desses perfis, permitindo que você forneça [!DNL Profile] dados para o [!DNL Data Lake] com o mínimo de latência possível.

O vídeo a seguir foi criado para ajudar a compreender a ingestão de streaming e descreve os conceitos acima.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Registros de perfil de fluxo e [!DNL ExperienceEvents]

Com a ingestão de streaming, os usuários podem transmitir registros de perfis [!DNL ExperienceEvents] e até [!DNL Platform] segundos para ajudar a impulsionar a personalização em tempo real. Todos os dados enviados para APIs de ingestão de streaming são automaticamente persistentes no [!DNL Data Lake].

Leia o guia [de](../tutorials/create-streaming-connection.md) criação de conexão de streaming para obter mais informações.

### Fluxo para conjuntos de dados

Quando estiver confiante de que seus dados estão limpos, você poderá ativar seus conjuntos de dados para [!DNL Real-time Customer Profile] e [!DNL Identity Service].

Para obter mais informações sobre como habilitar um conjunto de dados para [!DNL Profile] e [!DNL Identity Service], leia o guia [](../../profile/tutorials/dataset-configuration.md)configurar um conjunto de dados.

## What is the expected latency for streaming ingestion on [!DNL Platform]?

| Destino | Latência esperada |
| --------- | ---------------- |
| Perfil do cliente em tempo real | &lt; 1 minuto |
| Data Lake | &lt; 60 minutos |

## Extensão da Adobe Experience Platform

Você pode usar a extensão Adobe Experience Platform para criar uma nova conexão de streaming. A [!DNL Experience Platform] extensão fornece ações para enviar beacons formatados em [!DNL Experience Data Model] (XDM) para ingestão em tempo real [!DNL Experience Platform]. Visite a documentação da Extensão [do](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) Experience Platform para obter mais informações.