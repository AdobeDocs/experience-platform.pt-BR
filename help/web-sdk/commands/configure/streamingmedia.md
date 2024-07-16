---
title: streamingMedia
description: Configure o SDK da Web para coletar dados relacionados ao uso de mídia em suas propriedades da Web.
exl-id: f7733619-d35e-43eb-ac90-052717310c39
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 6%

---

# `streamingMedia`

O componente `streamingMedia` ajuda a coletar dados relacionados a sessões de mídia no site.

Os dados coletados podem incluir informações sobre reprodução de mídia, pausas, conclusões e outros eventos relacionados. Depois de coletados, é possível enviar esses dados para a Adobe Experience Platform e/ou Adobe Analytics para gerar relatórios. Esse recurso fornece uma solução abrangente para rastrear e entender o comportamento de consumo de mídia no site.

## Pré-requisitos {#prerequisites}

Para usar o componente `streamingMedia` do SDK da Web, você deve atender aos seguintes pré-requisitos:

* Verifique se você tem acesso ao Adobe Experience Platform e/ou Adobe Analytics.
* Você deve usar o SDK da Web versão 2.20.0 ou posterior. Consulte a [visão geral de instalação do SDK da Web](../../install/overview.md) para saber como instalar a versão mais recente.
* Habilite a opção **[[!UICONTROL Media Analytics]](../../../datastreams/configure.md#advanced-options)** para a sequência de dados que você está usando.
* Certifique-se de que o esquema usado pelo fluxo de dados inclua os campos de esquema Coleção de mídia.
* Configure o recurso Mídia de Streaming na configuração do SDK da Web, conforme mostrado nesta página, por meio da [extensão de tag](#tag-extension) ou da [biblioteca JavaScript](#library).

## Configurar mídia de transmissão usando a extensão de tag do SDK da Web {#tag-extension}

Para configurar a transmissão de mídia na extensão de tag do SDK da Web, siga as etapas abaixo.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e clique em **[!UICONTROL Configurar]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Defina as configurações de **[!UICONTROL Mídia de streaming]** conforme descrito na [página de configuração da extensão de marca do SDK da Web](../../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#media-collection).

## Configurar mídia de transmissão usando a biblioteca JavaScript do SDK da Web {#library}

Para configurar a transmissão de mídia no SDK da Web, use as propriedades descritas abaixo.

Ao chamar o comando `configure`, adicione o objeto `streamingMedia`.

```js
alloy("configure", {
    streamingMedia: {
        channel: "video channel",
        playerName: "test player",
        appVersion: "Media Analytics with Web SDK 2.20.0",
        mainPingInterval: 10,
        adPingInterval: 10
    }
});
```

| Propriedade | Tipo | Obrigatório | Descrição |
|---------|----------|---------|---------|
| `channel` | String | Sim | O nome do canal onde ocorre a coleção de mídia de transmissão. Exemplo: `Video channel`. |
| `playerName` | String | Sim | O nome do media player. |
| `appVersion` | String | Não | A versão do aplicativo do reprodutor de mídia. |
| `mainPingInterval` | Número inteiro | Não | Frequência de pings para o conteúdo principal, em segundos. O valor padrão é `10`. Os valores podem variar de `10` a `50` segundos.  Se nenhum valor for especificado, o valor padrão será usado ao usar [sessões rastreadas automaticamente](../createmediasession.md#automatic). |
| `adPingInterval` | Número inteiro | Não | Frequência de pings para conteúdo de anúncio, em segundos. O valor padrão é `10`. Os valores podem variar de `1` a `10` segundos. Se nenhum valor for especificado, o valor padrão será usado ao usar [sessões rastreadas automaticamente](../createmediasession.md#automatic). |
