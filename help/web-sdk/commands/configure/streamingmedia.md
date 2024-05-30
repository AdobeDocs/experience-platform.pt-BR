---
title: streamingMedia
description: Configure o SDK da Web para coletar dados relacionados ao uso de mídia em suas propriedades da Web.
source-git-commit: c0cb244221215f78f9ef13d8a54a8799ab15df6c
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 6%

---


# `streamingMedia`

A variável `streamingMedia` O componente ajuda a coletar dados relacionados a sessões de mídia no site.

Os dados coletados podem incluir informações sobre reprodução de mídia, pausas, conclusões e outros eventos relacionados. Depois de coletados, é possível enviar esses dados para a Adobe Experience Platform e/ou Adobe Analytics para gerar relatórios. Esse recurso fornece uma solução abrangente para rastrear e entender o comportamento de consumo de mídia no site.

## Pré-requisitos {#prerequisites}

Para usar o `streamingMedia` do SDK da Web, você deve atender aos seguintes pré-requisitos:

* Verifique se você tem acesso ao Adobe Experience Platform e/ou Adobe Analytics.
* Você deve usar o SDK da Web versão 2.20.0 ou posterior. Consulte a [Visão geral de instalação do SDK da Web](../../install/overview.md) para saber como instalar a versão mais recente.
* Ativar o **[[!UICONTROL Media Analytics]](../../../datastreams/configure.md#advanced-options)** opção para a sequência de dados que você está usando.
* Certifique-se de que o esquema usado pelo fluxo de dados inclua os campos de esquema Coleção de mídia.
* Configure o recurso Mídia de transmissão na configuração do SDK da Web, conforme mostrado nesta página, por meio da [extensão de tag](#tag-extension) ou por meio da [Biblioteca JavaScript](#library).

## Configurar mídia de transmissão usando a extensão de tag do SDK da Web {#tag-extension}

Para configurar a transmissão de mídia na extensão de tag do SDK da Web, siga as etapas abaixo.

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e, em seguida, clique em **[!UICONTROL Configurar]** no [!UICONTROL Adobe Experience Platform Web SDK] cartão.
1. Configure o **[!UICONTROL Mídia de transmissão]** conforme descrito na seção [Página de configuração da extensão de tag do SDK da Web](../../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#media-collection).

## Configurar mídia de transmissão usando a biblioteca JavaScript do SDK da Web {#library}

Para configurar a transmissão de mídia no SDK da Web, use as propriedades descritas abaixo.

Ao chamar o `configure` adicione o `streamingMedia` objeto.

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
| `mainPingInterval` | Número inteiro | Não | Frequência de pings para o conteúdo principal, em segundos. O valor padrão é `10`. Os valores podem variar de `10` para `50` segundos.  Se nenhum valor for especificado, o valor padrão será usado ao usar [sessões rastreadas automaticamente](../createmediasession.md#automatic). |
| `adPingInterval` | Número inteiro | Não | Frequência de pings para conteúdo de anúncio, em segundos. O valor padrão é `10`. Os valores podem variar de `1` para `10` segundos. Se nenhum valor for especificado, o valor padrão será usado ao usar [sessões rastreadas automaticamente](../createmediasession.md#automatic). |
