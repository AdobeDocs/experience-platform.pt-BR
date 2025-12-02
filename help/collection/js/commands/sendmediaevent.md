---
title: sendMediaEvent
description: Saiba como usar o comando sendMediaEvent para rastrear sessões de mídia no Web SDK.
exl-id: a38626fd-4810-40a0-8893-e98136634fac
source-git-commit: 364b9adc406f732ea5ba450730397c4ce1bf03cf
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# `sendMediaEvent`

O comando `sendMediaEvent` faz parte do componente `streamingMedia` do Web SDK. Você pode usar esse componente para coletar dados relacionados a sessões de mídia no seu site. Consulte a `streamingMedia` [documentação](configure/streamingmedia.md) para saber como configurar este componente.

Use o comando `sendMediaEvent` para rastrear reprodução de mídia, pausas, conclusões, atualizações de estado do player e outros eventos relacionados.

O Web SDK pode lidar com eventos de mídia com base no tipo de rastreamento de sessão de mídia:

* **Manipulação de eventos para sessões rastreadas automaticamente**. Nesse modo, não é necessário passar o `sessionID` para o evento de mídia nem para o valor do indicador de reprodução. O Web SDK lidará com isso para você, com base na ID do player fornecida e na função de retorno de chamada `getPlayerDetails` fornecida ao iniciar a sessão de mídia.
* **Manipulação de eventos para sessões rastreadas manualmente**. Neste modo, você precisa passar o `sessionID` para o evento de mídia, juntamente com o valor do indicador de reprodução (valor inteiro). Você também pode transmitir os detalhes dos dados de Qualidade da experiência, se necessário.

## Lidar com eventos de mídia por tipo {#handle-by-type}

Selecione as guias abaixo para ver exemplos de manipulação de tipo de evento para cada tipo de evento e método de rastreamento de sessão (automático ou manual).

### Reproduzir {#play}

O tipo de evento `media.play` é usado para monitorar quando a reprodução de mídia começa. Esse evento deve ser enviado quando o reprodutor muda o estado para &quot;reproduzindo&quot; a partir de outro estado. Outros estados a partir dos quais o reprodutor passa para &quot;reproduzindo&quot; incluem &quot;buffering&quot;, a retomada do usuário de &quot;pausado&quot;, o reprodutor se recuperando de um erro ou reprodução automática.

>[!BEGINTABS]

>[!TAB Rastreamento automático de sessão]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.play"
    }
});
```

>[!TAB Rastreamento manual de sessão]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.play",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]

### Pause {#pause}

O tipo de evento `media.pauseStart` é usado para rastrear quando uma reprodução de mídia é pausada. Este evento deve ser enviado quando o usuário pressiona **[!UICONTROL Pause]**. Não há um tipo de evento de retomada. Uma retomada é inferida quando você envia um evento `media.play` após um `media.pauseStart`.

>[!BEGINTABS]

>[!TAB Rastreamento automático de sessão]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.pauseStart"
    }
});
```

>[!TAB Rastreamento manual de sessão]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.pauseStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]

### Erro {#error}

O tipo de evento `media.error` é usado para monitorar quando ocorre um erro durante a reprodução de mídia. Esse evento deve ser enviado quando ocorrer um erro.

>[!BEGINTABS]

>[!TAB Rastreamento automático de sessão]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.error",
        mediaCollection: {
            errorDetails: {
                name: "network-error",
                source: "player"
            }
        }
    }
});
```

>[!TAB Rastreamento manual de sessão]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.error",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                errorDetails: {
                    name: "network-error",
                    source: "player"
                }
            }
        }
    });
});
```

>[!ENDTABS]

### Início de ad break {#ad-break-start}

O tipo de evento `media.adBreakStart` é usado para rastrear o início de um ad break. Esse evento deve ser enviado quando um ad break é iniciado.

>[!BEGINTABS]

>[!TAB Rastreamento automático de sessão]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adBreakStart",
        mediaCollection: {
            advertisingPodDetails: {
                friendlyName: "Mid-roll",
                offset: 0,
                index: 1
            }
        }
    }
});
```

>[!TAB Rastreamento manual de sessão]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adBreakStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                advertisingPodDetails: {
                    friendlyName: "Mid-roll",
                    offset: 0,
                    index: 1
                }
            }
        }
    });
});
```

>[!ENDTABS]

### Ad break concluído {#ad-break-complete}

O tipo de evento `media.adBreakComplete` é usado para monitorar quando um ad break é concluído. Esse evento deve ser enviado quando um ad break é concluído.

>[!BEGINTABS]

>[!TAB Rastreamento automático de sessão]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adBreakComplete"
    }
});
```

>[!TAB Rastreamento manual de sessão]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adBreakComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]

### Início do anúncio {#ad-start}

O tipo de evento `media.adStart` é usado para rastrear o início de um anúncio. Esse evento deve ser enviado quando um anúncio é iniciado.

>[!BEGINTABS]

>[!TAB Rastreamento automático de sessão]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adStart",
        mediaCollection: {
            advertisingDetails: {
                friendlyName: "Ad 1",
                name: "/uri-reference/001",
                length: 10,
                advertiser: "Adobe Marketing",
                campaignID: "Adobe Analytics",
                creativeID: "creativeID",
                creativeURL: "https://creativeurl.com",
                placementID: "placementID",
                siteID: "siteID",
                podPosition: 11,
                playerName: "HTML5 player"
            },
            customMetadata: [{
                    name: "myCustomValue3",
                    value: "c3"
                },
                {
                    name: "myCustomValue2",
                    value: "c2"
                },
                {
                    name: "myCustomValue1",
                    value: "c1"
                }
            ]
        }
    }
});
```

>[!TAB Rastreamento manual de sessão]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
        eventType: "media.adStart",
        mediaCollection: {
            playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
            sessionID,
            advertisingDetails: {
              friendlyName: "Ad 1",
              name: "/uri-reference/001",
              length: 10,
              advertiser: "Adobe Marketing",
              campaignID: "Adobe Analytics",
              creativeID: "creativeID",
              creativeURL: "https://creativeurl.com",
              placementID: "placementID",
              siteID: "siteID",
              podPosition: 11,
              playerName: "HTML5 player"
            },
            customMetadata: [
              {
                name: "myCustomValue3",
                value: "c3"
              },
              {
                name: "myCustomValue2",
                value: "c2"
              },
              {
                name: "myCustomValue1",
                value: "c1"
              }]
        }
        }
    });
});
```

>[!ENDTABS]

### Anúncio concluído {#ad-complete}

O tipo de evento `media.adComplete` é usado para monitorar quando um anúncio é concluído. Esse evento deve ser enviado quando um anúncio é concluído.

>[!BEGINTABS]

>[!TAB Rastreamento automático de sessão]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adComplete"
    }
});
```

>[!TAB Rastreamento manual de sessão]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]

### Ignorar anúncio {#ad-skip}

O tipo de evento `media.adSkip` é usado para monitorar quando um anúncio é ignorado. Esse evento deve ser enviado quando um anúncio é ignorado.

>[!BEGINTABS]

>[!TAB Rastreamento automático de sessão]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adSkip"
    }
});
```

>[!TAB Rastreamento manual de sessão]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adSkip",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]

### Início do capítulo {#chapter-start}

O tipo de evento `media.chapterStart` é usado para rastrear o início de um capítulo. Esse evento deve ser enviado quando um capítulo é iniciado.

>[!BEGINTABS]

>[!TAB Rastreamento automático de sessão]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterStart",
        mediaCollection: {
            chapterDetails: {
                friendlyName: "Chapter 1",
                position: 1,
                length: 10,
                index: 1,
                offset: 0
            },
            customMetadata: [{
                    name: "myCustomValue3",
                    value: "c3"
                },
                {
                    name: "myCustomValue2",
                    value: "c2"
                },
                {
                    name: "myCustomValue1",
                    value: "c1"
                }
            ]
        }
    }
});
```

>[!TAB Rastreamento manual de sessão]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                chapterDetails: {
                    friendlyName: "Chapter 1",
                    position: 1,
                    length: 10,
                    index: 1,
                    offset: 0
                },
                customMetadata: [{
                        name: "myCustomValue3",
                        value: "c3"
                    },
                    {
                        name: "myCustomValue2",
                        value: "c2"
                    },
                    {
                        name: "myCustomValue1",
                        value: "c1"
                    }
                ]
            }
        }
    });
});
```

>[!ENDTABS]

### Capítulo concluído {#chapter-complete}

O tipo de evento `media.chapterComplete` é usado para rastrear quando um capítulo é concluído. Esse evento deve ser enviado quando um capítulo é concluído.

>[!BEGINTABS]

>[!TAB Rastreamento automático de sessão]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterComplete"
    }
});
```

>[!TAB Rastreamento manual de sessão]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]

### Capítulo ignorado {#chapter-skip}

O tipo de evento `media.chapterSkip` é usado para rastrear quando um capítulo é ignorado. Este evento deve ser enviado quando um capítulo é ignorado.

>[!BEGINTABS]

>[!TAB Rastreamento automático de sessão]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterSkip"
    }
});
```

>[!TAB Rastreamento manual de sessão]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterSkip",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]

### Início do buffer {#buffer-start}

O tipo de evento `media.bufferStart` é usado para rastrear quando o buffering é iniciado. Esse evento deve ser enviado quando o buffering é iniciado. Não há um tipo de evento `bufferResume`. Um `bufferResume` é inferido quando você envia um evento de reprodução após `bufferStart`.

>[!BEGINTABS]

>[!TAB Rastreamento automático de sessão]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.bufferStart"
    }
});
```

>[!TAB Rastreamento manual de sessão]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.bufferStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]

### Alteração da taxa de bits {#bitrate-change}

O tipo de evento `media.bitrateChange` é usado para monitorar quando a taxa de bits muda. Esse evento deve ser enviado quando a taxa de bits for alterada.

>[!BEGINTABS]

>[!TAB Rastreamento automático de sessão]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.bitrateChange",
        mediaCollection: {
            qoeDataDetails: {
                framesPerSecond: 1,
                bitrate: 35000,
                droppedFrames: 30,
                timeToStart: 1364
            }
        }
    }
});
```

>[!TAB Rastreamento manual de sessão]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.bitrateChange",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                qoeDataDetails: {
                    bitrate: 35000,
                    droppedFrames: 30,
                    timeToStart: 1364
                }
            }
        }
    });
});
```

>[!ENDTABS]

### Atualizações de estado {#state-updates}

O tipo de evento `media.statesUpdate` é usado para rastrear quando o estado do player é alterado. Esse evento deve ser enviado quando o estado do player for alterado.

>[!BEGINTABS]

>[!TAB Rastreamento automático de sessão]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.statesUpdate",
        mediaCollection: {
            statesStart: [{
                    name: "mute"
                },
                {
                    name: "pictureInPicture"
                }
            ],
            statesEnd: [{
                name: "fullScreen"
            }]
        }
    }
});
```

>[!TAB Rastreamento manual de sessão]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.stateUpdate",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                statesStart: [{
                        name: "mute"
                    },
                    {
                        name: "pictureInPicture"
                    }
                ],
                statesEnd: [{
                    name: "fullScreen"
                }]
            }
        }
    });
});
```

>[!ENDTABS]

### Fim da sessão {#session-end}

O tipo de evento `media.sessionEnd` é usado para notificar o back-end do Media Analytics para fechar imediatamente a sessão quando o usuário abandonar a visualização do conteúdo e for improvável que retorne.

Se você não enviar um evento `sessionEnd`, uma sessão abandonada sofrerá tempo limite depois que nenhum evento for recebido por 10 minutos ou quando nenhum movimento do indicador de reprodução ocorrer por 30 minutos. A sessão é excluída automaticamente.

>[!BEGINTABS]

>[!TAB Rastreamento automático de sessão]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.sessionEnd"
    }
});
```

>[!TAB Rastreamento manual de sessão]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.sessionEnd",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]

### Sessão concluída {#session-complete}

O tipo de evento `media.sessionComplete` é usado para monitorar quando uma sessão de mídia é concluída. Esse evento deve ser enviado quando o fim do conteúdo principal é atingido.

>[!BEGINTABS]

>[!TAB Rastreamento automático de sessão]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.sessionComplete"
    }
});
```

>[!TAB Rastreamento manual de sessão]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.sessionComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]

## Enviar evento de mídia usando a extensão de tag do Web SDK

A extensão de tag do Web SDK equivalente a este comando é a ação [**[!UICONTROL Send media event]**](/help/tags/extensions/client/web-sdk/actions/send-media-event.md).
