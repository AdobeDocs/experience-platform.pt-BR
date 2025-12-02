---
title: getMediaAnalyticsTracker
description: Saiba como criar um objeto do Rastreador do Media Analytics e usá-lo para rastrear eventos de mídia.
exl-id: ae968da8-7763-4b2a-a716-3014ba0d270d
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 2%

---

# `getMediaAnalyticsTracker`

Este comando do Web SDK recupera um Media Analytics Tracker. Você pode usar este comando para criar uma instância de objeto e, em seguida, usar as mesmas APIs que as fornecidas pela [biblioteca Media JS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html), rastrear eventos de mídia.

O comando `getMediaAnalyticsTracker` retorna a API herdada do Media Analytics.

| Nome do método | Descrição | Sintaxe |
|---|---|---|
| `getInstance` | Cria uma instância de mídia para rastrear a sessão de reprodução. | `Media.getInstance()` |
| `createMediaObject` | Cria um objeto contendo informações de mídia. Retorna o objeto vazio se parâmetros inválidos forem transmitidos. | `Media.createMediaObject(name, id, length, streamType, mediaType)` |
| `createAdBreakObject` | Cria um objeto contendo informações adbreak. Retorna o objeto vazio se parâmetros inválidos forem transmitidos. | `Media.createAdBreakObject(name, position, startTime)` |
| `createAdObject` | Cria um objeto contendo informações de anúncios. Retorna o objeto vazio se parâmetros inválidos forem transmitidos. | `Media.createAdObject(name, id, position, length)` |
| `createChapterObject` | Cria um objeto contendo informações do capítulo. Retorna o objeto vazio se parâmetros inválidos forem transmitidos. | `Media.createChapterObject(name, position, length, startTime)` |
| `createStateObject` | Cria um objeto contendo informações de estado. Retorna o objeto vazio se parâmetros inválidos forem transmitidos. | `Media.createStateObject(name)` |
| `createQoEObject` | Cria um objeto contendo informações de QoE. Retorna o objeto vazio se parâmetros inválidos forem transmitidos. | `Media.createQoEObject(bitrate, startupTime, fps, droppedFrames)` |

## Métodos de instância

| Nome do método | Descrição | Sintaxe |
|---|---|---|
| `trackSessionStart` | Rastreie a intenção de iniciar a reprodução. Isso inicia uma sessão de rastreamento na instância do rastreador de mídia. | `trackerInstance.trackSessionStart(mediaInfo, contextData)` |
| `trackPlay` | Rastrear a reprodução ou retomar a mídia após uma pausa anterior. | `trackerInstance.trackPlay()` |
| `trackPause` | Rastrear pausa de mídia. | `trackerInstance.trackPause()` |
| `trackComplete` | Rastreamento de mídia concluído. Chame esse método somente quando a mídia tiver sido completamente visualizada. | `trackerInstance.trackComplete()` |
| `trackSessionEnd` | Rastrear o final de uma sessão de exibição. Chame esse método mesmo se o usuário não visualizar a mídia até o fim. | `trackerInstance.trackSessionEnd()` |
| `trackError` | Rastreie um erro que ocorreu durante a reprodução da mídia. | `trackerInstance.trackError("errorId")` |
| `trackEvent` | Rastrear um evento personalizado. | `trackerInstance.trackEvent(event, info, contextData)` |
| `updatePlayhead` | Atualize a posição do indicador de reprodução. | `trackerInstance.updatePlayhead(playhead)` |
| `updateQoEObject` | Atualize a qualidade da experiência. | `trackerInstance.updateQoEObject(qoe)` |

## Constantes

| Nome da constante | Descrição | Valor |
|---|---|---|
| `MediaType` | Tipo de mídia | `Video`, `Audio` |
| `StreamType` | Tipo de fluxo | `VOD`, `Live`, `Linear`, `Podcast`, `Audiobook`, `AOD` |
| `VideoMetadataKeys` | Isso define as chaves de metadados padrão para fluxos de vídeo | `Show`, `Season`, `Episode`, `AssetId`, `Genre`, `FirstAirDate`, `FirstDigitalDate`, `Rating`, `Originator`, `Network`, `ShowType`, `AdLoad`, `MVPD`, `Authorized`, `DayPart`, `Feed`, `StreamFormat` |
| `AudioMetadataKeys` | Isso define as chaves de metadados padrão para fluxos de áudio. | `Artist`, `Album`, `Label`, `Author`, `Station`, `Publisher` |
| `AdMetadataKeys` | Isso define as chaves de metadados padrão para anúncios. | `Advertiser`, `CampaignId`, `CreativeId`, `PlacementId`, `SiteId`, `CreativeUrl` |
| `Event` | Isso define o tipo de evento de rastreamento. | `AdBreakStart`, `AdBreakComplete`, `AdStart`, `AdComplete`, `AdSkip`, `ChapterStart`, `ChapterComplete`, `ChapterSkip`, `SeekStart`, `SeekComplete`, `BufferStart`, `BufferComplete`, `BitrateChange`, `StateStart`, `StateEnd` |
| `PlayerState` | Isso define valores padrão para rastrear o estado do player. | `FullScreen`, `ClosedCaption`, `Mute`, `PictureInPicture`, `InFocus` |

## Obter o rastreador do Media Analytics usando a extensão de tag da Web SDK

O equivalente da extensão de tag do Web SDK desse comando é a ação [**[!UICONTROL Get Media Analytics tracker]**](/help/tags/extensions/client/web-sdk/actions/get-media-analytics-tracker.md).
