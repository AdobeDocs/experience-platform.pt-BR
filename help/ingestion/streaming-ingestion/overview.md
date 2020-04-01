---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visão geral sobre a ingestão de streaming da plataforma Adobe Experience
topic: overview
translation-type: tm+mt
source-git-commit: a570a7a3d905c4618d80f56f01747cced1d124e8

---


# Visão geral da assimilação de transmissão

A inclusão de transmissão contínua para a plataforma Adobe Experience fornece aos usuários um método para enviar dados de dispositivos cliente e servidor para a plataforma Experience em tempo real.

## O que você pode fazer com a ingestão de streaming?

A plataforma Adobe Experience permite que você direcione experiências coordenadas, consistentes e relevantes, gerando um Perfil de cliente em tempo real para cada um de seus clientes individuais. A ingestão de streaming desempenha um papel fundamental na criação desses perfis, permitindo que você forneça dados de Perfis no Data Lake com o mínimo de latência possível.

### Registros de perfil de fluxo e ExperienceEvents

Com a ingestão de streaming, os usuários podem transmitir registros de perfis e ExperienceEvents à plataforma em segundos para ajudar a impulsionar a personalização em tempo real. Todos os dados enviados para APIs de ingestão de fluxo contínuo são automaticamente persistentes no Data Lake.

Leia o guia [de](../tutorials/create-streaming-connection.md) criação de conexão de streaming para obter mais informações.

### Fluxo para conjuntos de dados

Quando estiver confiante de que seus dados estão limpos, você poderá ativar seus conjuntos de dados para o Perfil do cliente em tempo real e o Serviço de identidade.

Para obter mais informações sobre como habilitar um conjunto de dados para o Perfil e o Serviço de identidade, leia o guia [de](../../profile/tutorials/dataset-configuration.md)configuração de um conjunto de dados.

## Qual é a latência esperada para a ingestão de streaming na plataforma?

| Destino | Latência esperada |
| --------- | ---------------- |
| Perfil do cliente em tempo real | &lt; 1 minuto |
| Data Lake | &lt; 60 minutos |

## Extensão da Adobe Experience Platform

Você pode usar a extensão da plataforma Adobe Experience para criar uma nova conexão de streaming. A extensão da plataforma de experiência fornece ações para enviar beacons formatados no Modelo de dados de experiência (XDM) para ingestão em tempo real à plataforma de experiência. Visite a documentação [Experience Platform Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) para obter mais informações.