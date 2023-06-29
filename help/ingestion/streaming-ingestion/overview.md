---
keywords: Experience Platform;página inicial;tópicos populares;assimilação de dados;dados assimilados;streaming;visão geral;assimilação de streaming;latência;latência de streaming;
solution: Experience Platform
title: Visão geral da assimilação de fluxo
description: A assimilação de streaming para o Adobe Experience Platform fornece aos usuários um método para enviar dados de dispositivos cliente e do lado do servidor para o Experience Platform em tempo real.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: 12bd4c6c1993afc438b75a3e5163ebe2fe8a8dd0
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 4%

---

# Visão geral da ingestão de streaming

A assimilação de streaming para o Adobe Experience Platform fornece aos usuários um método para enviar dados de dispositivos no lado do cliente e do servidor para o [!DNL Experience Platform] em tempo real.

## O que você pode fazer com a assimilação por transmissão?

O Adobe Experience Platform permite gerar experiências coordenadas, consistentes e relevantes por meio da geração de [!DNL Real-Time Customer Profile] para cada cliente individual. A assimilação de streaming desempenha um papel fundamental na criação desses perfis, permitindo que você forneça [!DNL Profile] dados na [!DNL Data Lake] com a menor latência possível.

O vídeo a seguir foi projetado para ajudar a entender a assimilação de streaming e descreve os conceitos acima.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Registros de perfil de fluxo e [!DNL ExperienceEvents]

Com a assimilação por transmissão, os usuários podem transmitir registros de perfil e [!DNL ExperienceEvents] para [!DNL Platform] em segundos para ajudar a impulsionar a personalização em tempo real. Todos os dados enviados para as APIs de assimilação por transmissão são mantidos automaticamente na [!DNL Data Lake].

Leia as [criar um guia de conexão de streaming](../tutorials/create-streaming-connection.md) para obter mais informações.

### Transmitir para conjuntos de dados

Depois de ter certeza de que os dados estão limpos, você poderá ativar os conjuntos de dados para [!DNL Real-Time Customer Profile] e [!DNL Identity Service].

Para obter mais informações sobre como habilitar um conjunto de dados para [!DNL Profile] e [!DNL Identity Service], leia o [configurar um guia de conjunto de dados](../../profile/tutorials/dataset-configuration.md).

## Qual é a latência esperada para assimilação por transmissão no [!DNL Platform]?

| Destino | Latência esperada |
| --------- | ---------------- |
| Perfil do cliente em tempo real | &lt; 1 minuto |
| Data Lake | &lt; 60 minutos |

## Orientação de solicitação por segundos (RPS) sobre assimilação de streaming

A tabela abaixo exibe orientações sobre os limites de solicitação por segundos para assimilação de streaming.

| Limite de RPS | Notas |
| --- | --- |
| 1000 solicitações por segundo | Eles podem conter várias mensagens ao usar `/collection/batch` terminal. |
| 10000 mensagens individuais por segundo | As mensagens podem ser agrupadas em menos solicitações reais ao usar o `/collection/batch` terminal. |

>[!IMPORTANT]
>
>O limite imposto torna-se **60 solicitações por minuto** ao usar a validação síncrona como pretendida para fins de depuração.

## Extensão da Adobe Experience Platform

Você pode usar a extensão Adobe Experience Platform para criar uma nova conexão de transmissão. A variável [!DNL Experience Platform] A extensão fornece ações para enviar beacons formatados em [!DNL Experience Data Model] (XDM) para assimilação em tempo real em [!DNL Experience Platform]. Visite o [Extensão do Experience Platform](../../tags/extensions/client/web-sdk/overview.md) para obter mais informações.
