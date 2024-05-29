---
title: sendMediaEvent
description: Saiba como usar o comando sendMediaEvent para rastrear sessões de mídia no SDK da Web.
source-git-commit: 83d3de67e7680369dc890f58b16d9668058e221c
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---


# `sendMediaEvent`

A variável `sendMediaEvent` faz parte do SDK da Web `streamingMedia` componente. Você pode usar esse componente para coletar dados relacionados a sessões de mídia no seu site. Consulte a `streamingMedia` [documentação](configure/streamingmedia.md) para saber como configurar esse componente.

Use o `sendMediaEvent` comando para rastrear reproduções de mídia, pausas, conclusões, atualizações de estado do player e outros eventos relacionados.

O SDK da Web pode lidar com eventos de mídia com base no tipo de rastreamento de sessão de mídia:

* **Manipulação de eventos para sessões rastreadas automaticamente**. Nesse modo, não é necessário passar a variável `sessionID` ao evento de mídia ou ao valor do indicador de reprodução. O SDK da Web lidará com isso para você, com base na ID do player fornecida e na variável `getPlayerDetails` função de retorno de chamada fornecida ao iniciar a sessão de mídia.
* **Manipulação de eventos para sessões rastreadas manualmente**. Nesse modo, você precisa passar a variável `sessionID` ao evento de mídia, juntamente com o valor do indicador de reprodução (valor inteiro). Você também pode transmitir os detalhes dos dados de Qualidade da experiência, se necessário.

## Lidar com eventos de mídia por tipo {#handle-by-type}

Selecione as guias abaixo para ver exemplos de manipulação de tipo de evento para cada tipo de evento e método de rastreamento de sessão (automático ou manual).


### Reproduzir {#play}

A variável `media.play` o tipo de evento é usado para rastrear o início da reprodução de mídia. Esse evento deve ser enviado quando o reprodutor muda o estado para &quot;reproduzindo&quot; a partir de outro estado. Outros estados a partir dos quais o reprodutor passa para &quot;reproduzindo&quot; incluem &quot;buffering&quot;, a retomada do usuário de &quot;pausado&quot;, o reprodutor se recuperando de um erro ou reprodução automática.

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

>[!TAB Rastreamento manual da sessão]

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


### Pausar {#pause}

A variável `media.pauseStart` O tipo de evento é usado para rastrear quando uma reprodução de mídia é pausada. Esse evento deve ser enviado quando o usuário pressionar **[!UICONTROL Pausar]**. Não há um tipo de evento de retomada. Um currículo é inferido quando você envia um `media.play` evento depois de um `media.pauseStart`.

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

>[!TAB Rastreamento manual da sessão]

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

A variável `media.error` o tipo de evento é usado para rastrear quando ocorre um erro durante a reprodução da mídia. Esse evento deve ser enviado quando ocorrer um erro.

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

>[!TAB Rastreamento manual da sessão]

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

A variável `media.adBreakStart` o tipo de evento é usado para rastrear o início de um ad break. Esse evento deve ser enviado quando um ad break é iniciado.

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

>[!TAB Rastreamento manual da sessão]

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

A variável `media.adBreakComplete` o tipo de evento é usado para rastrear quando um ad break é concluído. Esse evento deve ser enviado quando um ad break é concluído.

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

>[!TAB Rastreamento manual da sessão]

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

A variável `media.adStart` O tipo de evento é usado para rastrear o início de um anúncio. Esse evento deve ser enviado quando um anúncio é iniciado.

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

>[!TAB Rastreamento manual da sessão]

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

A variável `media.adComplete` tipo de evento é usado para rastrear quando um anúncio é concluído. Esse evento deve ser enviado quando um anúncio é concluído.

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

>[!TAB Rastreamento manual da sessão]

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

A variável `media.adSkip` o tipo de evento é usado para rastrear quando um anúncio é ignorado. Esse evento deve ser enviado quando um anúncio é ignorado.

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

>[!TAB Rastreamento manual da sessão]

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

A variável `media.chapterStart` o tipo de evento é usado para rastrear o início de um capítulo. Esse evento deve ser enviado quando um capítulo é iniciado.

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

>[!TAB Rastreamento manual da sessão]

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

A variável `media.chapterComplete` tipo de evento é usado para rastrear quando um capítulo é concluído. Esse evento deve ser enviado quando um capítulo é concluído.

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

>[!TAB Rastreamento manual da sessão]

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

A variável `media.chapterSkip` tipo de evento é usado para rastrear quando um capítulo é ignorado. Este evento deve ser enviado quando um capítulo é ignorado.

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

>[!TAB Rastreamento manual da sessão]

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

A variável `media.bufferStart` o tipo de evento é usado para rastrear o início do buffering. Esse evento deve ser enviado quando o buffering é iniciado. Não há `bufferResume` tipo de evento. A `bufferResume` é inferido quando você envia um evento de reprodução após `bufferStart`.

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

>[!TAB Rastreamento manual da sessão]

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

A variável `media.bitrateChange` tipo de evento é usado para rastrear quando a taxa de bits muda. Esse evento deve ser enviado quando a taxa de bits for alterada.

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

>[!TAB Rastreamento manual da sessão]

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

A variável `media.stateUpdate` o tipo de evento é usado para rastrear quando o estado do player é alterado. Esse evento deve ser enviado quando o estado do player for alterado.

>[!BEGINTABS]

>[!TAB Rastreamento automático de sessão]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.stateUpdate",
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

>[!TAB Rastreamento manual da sessão]

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

A variável `media.sessionEnd` O tipo de evento é usado para notificar o back-end do Media Analytics para fechar imediatamente a sessão quando o usuário abandona a visualização do conteúdo e é improvável que retorne.

Se você não enviar um `sessionEnd` Uma sessão abandonada sofrerá tempo limite depois que nenhum evento for recebido por 10 minutos ou quando nenhum movimento do indicador de reprodução ocorrer por 30 minutos. A sessão é excluída automaticamente.

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

>[!TAB Rastreamento manual da sessão]

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

A variável `media.sessionComplete` O tipo de evento é usado para rastrear quando uma sessão de mídia é concluída. Esse evento deve ser enviado quando o fim do conteúdo principal é atingido.

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

>[!TAB Rastreamento manual da sessão]

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



