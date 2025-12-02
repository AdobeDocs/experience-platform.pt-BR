---
title: streamingMedia
description: Configure o Web SDK para coletar dados relacionados ao uso de mídia em suas propriedades da Web.
exl-id: f7733619-d35e-43eb-ac90-052717310c39
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 8%

---

# `streamingMedia`

O componente `streamingMedia` ajuda a coletar dados relacionados a sessões de mídia no site.

Os dados coletados podem incluir informações sobre reprodução de mídia, pausas, conclusões e outros eventos relacionados. Depois de coletados, é possível enviar esses dados para o Adobe Experience Platform ou Adobe Analytics para gerar relatórios. Esse recurso fornece uma solução abrangente para rastrear e entender o comportamento de consumo de mídia no site.

## Pré-requisitos

Para usar o componente `streamingMedia` do Web SDK, você deve atender aos seguintes pré-requisitos:

* Verifique se você tem acesso ao Adobe Experience Platform ou Adobe Analytics.
* Você deve usar o Web SDK versão 2.20.0 ou posterior. Consulte a [visão geral da instalação do Web SDK](../../install/overview.md) para saber como instalar a versão mais recente.
* Habilite a opção **[[!UICONTROL Media Analytics]](/help/datastreams/configure.md#advanced-options)** para a sequência de dados que você está usando.
* Certifique-se de que o esquema usado pelo fluxo de dados inclua os campos de esquema Coleção de mídia.
* Configure o recurso Mídia de transmissão no Web SDK, conforme mostrado nesta página.

Ao chamar o comando `configure`, adicione o objeto `streamingMedia`.

```js
alloy("configure", {
    streamingMedia: {
        channel: "Video channel",
        playerName: "Example player",
        appVersion: "Media Analytics with Web SDK 2.20.0",
        mainPingInterval: 10,
        adPingInterval: 10
    }
});
```

| Propriedade | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| **`channel`** | String | Sim | O nome do canal onde ocorre a coleção de mídia de transmissão. Exemplo: `Video channel`. |
| **`playerName`** | String | Sim | O nome do media player. |
| **`appVersion`** | String | Não | A versão do aplicativo do reprodutor de mídia. |
| **`mainPingInterval`** | Número inteiro | Não | Frequência de pings para o conteúdo principal, em segundos. O valor padrão é `10`. Os valores podem variar de `10` a `50` segundos.  Se nenhum valor for especificado, o valor padrão será usado ao usar [sessões rastreadas automaticamente](../createmediasession.md#automatic). |
| **`adPingInterval`** | Número inteiro | Não | Frequência de pings para conteúdo de anúncio, em segundos. O valor padrão é `10`. Os valores podem variar de `1` a `10` segundos. Se nenhum valor for especificado, o valor padrão será usado ao usar [sessões rastreadas automaticamente](../createmediasession.md#automatic). |

## Configuração de mídia de transmissão usando a extensão de tag do Web SDK

Essas configurações podem ser definidas na extensão de marca do Web SDK usando [as configurações de mídia de streaming](/help/tags/extensions/client/web-sdk/configure/streaming-media.md).
