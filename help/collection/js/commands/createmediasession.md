---
title: createMediaSession
description: Saiba como configurar o Web SDK para gerenciar sessões de mídia automaticamente
exl-id: abcb26f6-7249-4235-99eb-e4b9aeecff3e
source-git-commit: 60447ef6f881bf2a34f5502f2259328bf73d08c0
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 7%

---

# `createMediaSession`

O comando `createMediaSession` faz parte do componente `streamingMedia` do Web SDK. Você pode usar esse componente para coletar dados relacionados a sessões de mídia no seu site. Consulte a `streamingMedia` [documentação](configure/streamingmedia.md) para saber como configurar este componente.

Os dados coletados podem incluir informações sobre reprodução de mídia, pausas, conclusões e outros eventos relacionados. Depois de coletados, você pode enviar esses dados para o [Adobe Analytics para mídia de streaming](https://experienceleague.adobe.com/pt-br/docs/media-analytics/using/media-overview), para agregar métricas. Esse recurso fornece uma solução abrangente para rastrear e entender o comportamento de consumo de mídia no site.

Você pode criar sessões de mídia no Web SDK de duas maneiras:

* **Sessões de mídia rastreadas automaticamente** permitem que o Web SDK gerencie a expedição de eventos de ping de mídia para o [Adobe Analytics para mídia de streaming](https://experienceleague.adobe.com/pt-br/docs/media-analytics/using/media-overview). A frequência desses pings é determinada pelas definições de configuração do componente [streamingMedia](configure/streamingmedia.md).
* **Sessões de mídia rastreadas manualmente** dão a você mais controle sobre o envio de eventos de ping de sessão para o [Adobe Analytics para mídia de streaming](https://experienceleague.adobe.com/pt-br/docs/media-analytics/using/media-overview). Além disso, você pode armazenar o `sessionID` para sessões de mídia.

## Criar uma sessão de mídia rastreada automaticamente {#automatic}

Para começar a rastrear uma sessão de mídia automaticamente, chame o método `createMediaSession` com as opções descritas abaixo:

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
| `getPlayerDetails` | Função | Sim | Uma função que retorna os detalhes do reprodutor. Essa função de retorno de chamada será chamada pelo Web SDK antes de cada evento de mídia para o `playerId` fornecido. |
| `xdm.eventType` | Objeto | Não | O tipo de evento de mídia. Se não for fornecido, este campo será automaticamente definido como `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | Objeto | Sim | Contém propriedades de detalhes da sessão. Consulte [Esquema de coleção de mídia](/help/xdm/data-types/media-collection-details.md) para obter mais informações. |

## Criar uma sessão de mídia rastreada manualmente {#manual}

Para começar a rastrear uma sessão de mídia manualmente, chame o método `createMediaSession` com as opções descritas abaixo:

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
| `xdm.mediaCollection.sessionDetails` | Objeto | Sim | Contém propriedades de detalhes da sessão. Consulte [Esquema de coleção de mídia](/help/xdm/data-types/media-collection-details.md) para obter mais informações. |
| `xdm.mediaCollection.playhead` | Número inteiro | Sim | O indicador de reprodução atual. |
| `xdm.mediaCollection.qoeDataDetails` | Objeto | Não | A qualidade dos dados da experiência. Consulte a documentação do [esquema da Coleção de mídia](/help/xdm/data-types/media-collection-details.md) para obter mais informações. |

## Criar sessão de mídia usando a extensão de tag do Web SDK

A extensão de marca do Web SDK equivalente a este comando é o tipo de evento [**[!UICONTROL Session start]**](/help/tags/extensions/client/web-sdk/actions/send-media-event.md#session-start) na ação &#39;[!UICONTROL Send media event]&#39;.
