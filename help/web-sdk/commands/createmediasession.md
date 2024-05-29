---
title: createMediaSession
description: Saiba como configurar o SDK da Web para gerenciar sessões de mídia automaticamente
source-git-commit: 83d3de67e7680369dc890f58b16d9668058e221c
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 7%

---


# `createMediaSession`

A variável `createMediaSession` faz parte do SDK da Web `streamingMedia` componente. Você pode usar esse componente para coletar dados relacionados a sessões de mídia no seu site. Consulte a `streamingMedia` [documentação](configure/streamingmedia.md) para saber como configurar esse componente.

Os dados coletados podem incluir informações sobre reprodução de mídia, pausas, conclusões e outros eventos relacionados. Depois de coletados, você pode enviar esses dados para [Adobe Analytics para mídia de streaming](https://experienceleague.adobe.com/en/docs/media-analytics/using/media-overview?lang=pt-BR), para agregar métricas. Esse recurso fornece uma solução abrangente para rastrear e entender o comportamento de consumo de mídia no site.

Você pode criar sessões de mídia no SDK da Web de duas maneiras:

* [Sessões de mídia rastreadas automaticamente](#automatic) permitir que o SDK da Web gerencie a expedição de eventos de ping de mídia para [Adobe Analytics para mídia de streaming](https://experienceleague.adobe.com/en/docs/media-analytics/using/media-overview?lang=pt-BR). A frequência desses pings é determinada pelas definições de configuração do [streamingMedia](configure/streamingmedia.md) componente.
* [Sessões de mídia rastreadas manualmente](#manual) fornecer mais controle sobre o envio de eventos de ping de sessão para [Adobe Analytics para mídia de streaming](https://experienceleague.adobe.com/en/docs/media-analytics/using/media-overview?lang=pt-BR). Além disso, você pode armazenar o `sessionID` para sessões de mídia.

## Criar uma sessão de mídia rastreada automaticamente {#automatic}

Para começar a rastrear uma sessão de mídia automaticamente, chame o `createMediaSession` com as opções descritas abaixo:

```javascript
    alloy("createMediaSession", {
        playerId: "movie-test",
        getPlayerDetails: () => {
            return {
                playhead: document.getElementById("movie-test").currentTime,
                qoeDataDetails: {
                    bitrate: 1000,
                    startupTime: 1000,
                    fps: 30,
                    droppedFrames: 10
                }
            };
        },
        xdm: {
            eventType: "media.sessionStart",
            mediaCollection: {
                sessionDetails: {
                    ...
                }
            }
        }
    });
```

| Propriedade | Tipo | Obrigatório | Descrição |
|---------|----------|---------|---------|
| `playerId` | String | Sim | A ID do reprodutor, um identificador exclusivo que representa a sessão de mídia. |
| `getPlayerDetails` | Função | Sim | Uma função que retorna os detalhes do reprodutor. Essa função de retorno de chamada será chamada pelo SDK da Web antes de cada evento de mídia da `playerId` fornecidos. |
| `xdm.eventType ` | Objeto | Não | O tipo de evento de mídia. Se não for fornecido, será automaticamente definido como `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | Objeto | Sim | O objeto de detalhes da sessão. A variável `sessionDetails` o objeto deve conter as propriedades dos detalhes da sessão. Consulte a [Esquema de coleção de mídia](../../xdm/data-types/media-collection-details.md) para obter mais informações. |


## Criar uma sessão de mídia rastreada manualmente {#manual}

Para começar a rastrear uma sessão de mídia manualmente, chame o `createMediaSession` com as opções descritas abaixo:

```javascript
const sessionPromise = alloy("createMediaSession", {
    xdm: {
        eventType: "media.sessionStart",
        mediaCollection: {
            playhead: 0,
            sessionDetails: {
                ...
            },
            qoeDataDetails: {
                bitrate: 1000,
                startupTime: 1000,
                fps: 30,
                droppedFrames: 10
            }
        }
    }
});
```

| Propriedade | Tipo | Obrigatório | Descrição |
|---------|----------|---------|---------|
| `xdm.eventType` | Objeto | Não | O tipo de evento de mídia. Se não for fornecido, será automaticamente definido como `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | Objeto | Sim | O objeto de detalhes da sessão. A variável `sessionDetails` o objeto deve conter as propriedades dos detalhes da sessão. Consulte a [Esquema de coleção de mídia](../../xdm/data-types/media-collection-details.md) para obter mais informações. |
| `xdm.mediaCollection.playhead` | Número inteiro | Sim | O indicador de reprodução atual. |
| `xdm.mediaCollection.qoeDataDetails` | Objeto | Não | A qualidade dos dados da experiência. Consulte a [Esquema de coleção de mídia](../../xdm/data-types/media-collection-details.md) para obter mais informações. |
