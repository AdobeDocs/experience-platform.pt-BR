---
keywords: Experience Platform, home, tópicos populares, assimilação de dados, dados assimilados, streaming, visão geral, assimilação de streaming, latência, latência de streaming;
solution: Experience Platform
title: Visão geral da assimilação de fluxo
topic-legacy: overview
description: A assimilação de streaming para Adobe Experience Platform fornece aos usuários um método para enviar dados de dispositivos cliente e do lado do servidor para o Experience Platform em tempo real.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: 968f2635330fb0fa8a55b17b30bd8557f7d70335
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 2%

---

# Visão geral da assimilação de streaming

A assimilação de streaming para Adobe Experience Platform fornece aos usuários um método para enviar dados de dispositivos cliente e do lado do servidor para o [!DNL Experience Platform] em tempo real.

## O que você pode fazer com a ingestão de streaming?

O Adobe Experience Platform permite que você conduza experiências coordenadas, consistentes e relevantes, gerando uma [!DNL Real-time Customer Profile] para cada um dos clientes individuais. A assimilação de streaming tem um papel importante na criação desses perfis, permitindo que você forneça [!DNL Profile] dados no [!DNL Data Lake] com o mínimo de latência possível.

O vídeo a seguir foi criado para ajudar a entender a assimilação de streaming e descreve os conceitos acima.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Registros de perfil de fluxo e [!DNL ExperienceEvents]

Com a assimilação de streaming, os usuários podem transmitir registros de perfil e [!DNL ExperienceEvents] para [!DNL Platform] em segundos para ajudar a impulsionar a personalização em tempo real. Todos os dados enviados para as APIs de assimilação de streaming são automaticamente mantidos na variável [!DNL Data Lake].

Leia o [criar um guia de conexão de transmissão](../tutorials/create-streaming-connection.md) para obter mais informações.

### Fluxo para conjuntos de dados

Depois de ter certeza de que os dados estão limpos, é possível ativar os conjuntos de dados para [!DNL Real-time Customer Profile] e [!DNL Identity Service].

Para obter mais informações sobre como ativar um conjunto de dados para [!DNL Profile] e [!DNL Identity Service]Por favor leia o [configurar um guia de conjunto de dados](../../profile/tutorials/dataset-configuration.md).

## Qual é a latência esperada para a assimilação de streaming em [!DNL Platform]?

| Destino | Latência esperada |
| --------- | ---------------- |
| Perfil do cliente em tempo real | &lt; 15 minutos, no percentil 95 |
| Data Lake | &lt; 60 minutos |

## Orientação de solicitação por segundos (RPS) sobre assimilação de streaming

A tabela abaixo exibe orientações sobre os limites de solicitação por segundos para a assimilação de streaming.

| Limite de RPS | Notas |
| --- | --- |
| 1000 solicitações por segundo | Eles podem conter várias mensagens ao usar `/collection/batch` endpoint . |
| 10000 mensagens individuais por segundo | As mensagens podem ser agrupadas em menos solicitações reais ao usar a variável `/collection/batch` endpoint . |

>[!IMPORTANT]
>
>O limite imposto se torna **60 pedidos por minuto** ao usar a validação síncrona como se destina a fins de depuração.

## Extensão da Adobe Experience Platform

Você pode usar a extensão Adobe Experience Platform para criar uma nova conexão de transmissão. O [!DNL Experience Platform] fornece ações para enviar beacons formatados em [!DNL Experience Data Model] (XDM) para ingestão em tempo real para [!DNL Experience Platform]. Visite o [Extensão Experience Platform](../../tags/extensions/web/sdk/overview.md) documentação para obter mais informações.
