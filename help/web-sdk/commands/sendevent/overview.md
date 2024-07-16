---
title: sendEvent
description: Envie dados para o Edge Network Adobe Experience Platform.
exl-id: 83de368d-78d4-4e28-aadd-afaea1ca091d
source-git-commit: 9ea7b678f5cfa19c7fd1e3ba6633cdeed4084b18
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# `sendEvent`

O comando `sendEvent` é a principal maneira de enviar dados para o Adobe, para recuperar conteúdo personalizado, identidades e destinos de público-alvo. Use o objeto [`xdm`](xdm.md) para enviar dados que mapeiam para o esquema do Adobe Experience Platform. Use o objeto [`data`](data.md) para enviar dados não XDM. Você pode usar o mapeador de sequência de dados para alinhar dados nesse objeto a campos de esquema.

## Enviar dados do evento usando a extensão de tag do SDK da Web

O envio de dados de eventos é executado como uma ação em uma regra na interface das tags da Coleção de dados da Adobe Experience Platform.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Regras]** e selecione a regra desejada.
1. Em [!UICONTROL Ações], selecione uma ação existente ou crie uma ação.
1. Defina o campo suspenso [!UICONTROL Extensão] como **[!UICONTROL Adobe Experience Platform Web SDK]** e defina o [!UICONTROL Tipo de Ação] como **[!UICONTROL Enviar evento]**.
1. Defina os campos desejados, clique em **[!UICONTROL Manter alterações]** e execute o fluxo de trabalho de publicação.

## Enviar dados do evento usando a biblioteca JavaScript do SDK da Web

Execute o comando `sendEvent` ao chamar a instância configurada do SDK da Web. Chame o comando [`configure`](../configure/overview.md) antes de chamar o comando `sendEvent`.

```js
alloy("sendEvent", {
  "data": dataObject,
  "documentUnloading": false,
  "edgeConfigOverrides": { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  "renderDecisions": true,
  "type": "commerce.purchases",
  "xdm": adobeDataLayer.getState(reference)
});
```

## Objeto de resposta

Se você decidir [manipular respostas](../command-responses.md) com este comando, as seguintes propriedades estarão disponíveis no objeto de resposta:

* **`propositions`**: Uma matriz de propostas retornadas pelo Edge Network. As propostas que são renderizadas automaticamente incluem o sinalizador `renderAttempted` definido como `true`.
* **`inferences`**: uma matriz de objetos de inferência, que contém informações de aprendizado de máquina sobre este usuário.
* **`destinations`**: Uma matriz de objetos de destino retornada pelo Edge Network.
