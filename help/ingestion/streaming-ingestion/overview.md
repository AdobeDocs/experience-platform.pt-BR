---
keywords: Experience Platform;home;popular topics;ingestão;ingested data;streaming;overview;streaming ingestão;latência;streaming latency;streaming latency;
solution: Experience Platform
title: Visão geral da ingestão de streaming do Adobe Experience Platform
topic: overview
description: A ingestão de streaming para Adobe Experience Platform fornece aos usuários um método para enviar dados de dispositivos cliente e servidor para o Experience Platform em tempo real.
translation-type: tm+mt
source-git-commit: 2dbd92efbd992b70f4f750b09e9d2e0626e71315
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 3%

---


# Visão geral da assimilação de transmissão

A ingestão de streaming para Adobe Experience Platform fornece aos usuários um método para enviar dados de dispositivos cliente e servidor para [!DNL Experience Platform] em tempo real.

## O que você pode fazer com a ingestão de streaming?

A Adobe Experience Platform permite que você direcione experiências coordenadas, consistentes e relevantes gerando um [!DNL Real-time Customer Profile] para cada um de seus clientes individuais. A inclusão de streaming desempenha um papel fundamental na criação desses perfis, permitindo que você forneça [!DNL Profile] dados para [!DNL Data Lake] com a menor latência possível.

O vídeo a seguir foi criado para ajudar a compreender a ingestão de streaming e descreve os conceitos acima.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Registros de perfil de fluxo e [!DNL ExperienceEvents]

Com a ingestão de streaming, os usuários podem transmitir registros de perfis e [!DNL ExperienceEvents] para [!DNL Platform] em segundos para ajudar a impulsionar a personalização em tempo real. Todos os dados enviados para as APIs de ingestão de streaming são automaticamente persistentes em [!DNL Data Lake].

Leia o [criar um guia de conexão de streaming](../tutorials/create-streaming-connection.md) para obter mais informações.

### Fluxo para conjuntos de dados

Quando estiver confiante de que seus dados estão limpos, você poderá ativar seus conjuntos de dados para [!DNL Real-time Customer Profile] e [!DNL Identity Service].

Para obter mais informações sobre como habilitar um conjunto de dados para [!DNL Profile] e [!DNL Identity Service], leia o [configure um guia de conjunto de dados](../../profile/tutorials/dataset-configuration.md).

## Qual é a latência esperada para a ingestão de streaming em [!DNL Platform]?

| Destino | Latência esperada |
| --------- | ---------------- |
| Perfil do cliente em tempo real | &lt; 1=&quot;&quot; minute=&quot;&quot;> |
| Data Lake | &lt; 60 minutos |

## Extensão da Adobe Experience Platform

Você pode usar a extensão Adobe Experience Platform para criar uma nova conexão de streaming. A extensão [!DNL Experience Platform] fornece ações para enviar beacons formatados em [!DNL Experience Data Model] (XDM) para ingestão em tempo real em [!DNL Experience Platform]. Visite a documentação [Extensão do Experience Platform](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) para obter mais informações.