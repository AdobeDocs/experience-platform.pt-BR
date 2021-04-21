---
keywords: Experience Platform, home, tópicos populares, assimilação de dados, dados assimilados, streaming, visão geral, assimilação de streaming, latência, latência de streaming;
solution: Experience Platform
title: Visão geral da assimilação de fluxo
topic-legacy: overview
description: A assimilação de streaming para Adobe Experience Platform fornece aos usuários um método para enviar dados de dispositivos cliente e do lado do servidor para o Experience Platform em tempo real.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 3%

---

# Visão geral da assimilação de streaming

A assimilação de streaming para Adobe Experience Platform fornece aos usuários um método para enviar dados de dispositivos cliente e do lado do servidor para [!DNL Experience Platform] em tempo real.

## O que você pode fazer com a ingestão de streaming?

O Adobe Experience Platform permite que você conduza experiências coordenadas, consistentes e relevantes, gerando um [!DNL Real-time Customer Profile] para cada um dos clientes individuais. A assimilação de streaming desempenha um papel importante na criação desses perfis, permitindo que você forneça [!DNL Profile] dados no [!DNL Data Lake] com o mínimo de latência possível.

O vídeo a seguir foi criado para ajudar a entender a assimilação de streaming e descreve os conceitos acima.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Registros de perfil de fluxo e [!DNL ExperienceEvents]

Com a assimilação de streaming, os usuários podem transmitir registros de perfil e [!DNL ExperienceEvents] para [!DNL Platform] em segundos para ajudar a impulsionar a personalização em tempo real. Todos os dados enviados para APIs de assimilação de streaming são automaticamente mantidos no [!DNL Data Lake].

Leia o [criar um guia de conexão de transmissão](../tutorials/create-streaming-connection.md) para obter mais informações.

### Fluxo para conjuntos de dados

Depois de ter certeza de que os dados estão limpos, é possível ativar os conjuntos de dados para [!DNL Real-time Customer Profile] e [!DNL Identity Service].

Para obter mais informações sobre como ativar um conjunto de dados para [!DNL Profile] e [!DNL Identity Service], leia o [configurar um guia de conjunto de dados](../../profile/tutorials/dataset-configuration.md).

## Qual é a latência esperada para a assimilação de streaming em [!DNL Platform]?

| Destino | Latência esperada |
| --------- | ---------------- |
| Perfil do cliente em tempo real | &lt; 1=&quot;&quot; minute=&quot;&quot;> |
| Data Lake | &lt; 60 minutos |

## Extensão da Adobe Experience Platform

Você pode usar a extensão Adobe Experience Platform para criar uma nova conexão de transmissão. A extensão [!DNL Experience Platform] fornece ações para enviar beacons formatados em [!DNL Experience Data Model] (XDM) para assimilação em tempo real em [!DNL Experience Platform]. Visite a documentação da [Extensão do Experience Platform](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) para obter mais informações.
