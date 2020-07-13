---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visão geral de ingestão de transmissão de Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 3f1c3c77a0755a3e305da0fb8a234be0f0ee1863
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 3%

---


# Visão geral da assimilação de transmissão

A ingestão de transmissão para o Adobe Experience Platform fornece aos usuários um método para enviar dados de dispositivos cliente e servidor para o Experience Platform em tempo real.

## O que você pode fazer com a ingestão de streaming?

O Adobe Experience Platform permite que você direcione experiências coordenadas, consistentes e relevantes gerando um Perfil de cliente em tempo real para cada um de seus clientes individuais. A ingestão de streaming desempenha um papel fundamental na criação desses perfis, permitindo que você forneça dados de Perfis no Data Lake com o mínimo de latência possível.

O vídeo a seguir foi criado para ajudar a compreender a ingestão de streaming e descreve os conceitos acima.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Registros de perfil de fluxo e ExperienceEvents

Com a ingestão de streaming, os usuários podem transmitir registros de perfis e ExperienceEvents para a Platform em segundos para ajudar a impulsionar a personalização em tempo real. Todos os dados enviados para APIs de ingestão de fluxo contínuo são automaticamente persistentes no Data Lake.

Leia o guia [de](../tutorials/create-streaming-connection.md) criação de conexão de streaming para obter mais informações.

### Fluxo para conjuntos de dados

Quando estiver confiante de que seus dados estão limpos, você poderá ativar seus conjuntos de dados para o Perfil do cliente em tempo real e o Serviço de identidade.

Para obter mais informações sobre como habilitar um conjunto de dados para o Perfil e o Serviço de identidade, leia o guia [de](../../profile/tutorials/dataset-configuration.md)configuração de um conjunto de dados.

## Qual é a latência esperada para a ingestão de streaming no Platform?

| Destino | Latência esperada |
| --------- | ---------------- |
| Perfil do cliente em tempo real | &lt; 1 minuto |
| Data Lake | &lt; 60 minutos |

## Extensão da Adobe Experience Platform

Você pode usar a extensão Adobe Experience Platform para criar uma nova conexão de streaming. A extensão Experience Platform fornece ações para enviar beacons formatados no Modelo de dados de experiência (XDM) para ingestão em tempo real ao Experience Platform. Visite a documentação da Extensão [do](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) Experience Platform para obter mais informações.