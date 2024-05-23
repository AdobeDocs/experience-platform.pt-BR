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

A variável `sendEvent` O comando é a principal maneira de enviar dados para o Adobe, para recuperar conteúdo personalizado, identidades e destinos de público-alvo. Use o [`xdm`](xdm.md) para enviar dados que mapeiam para o esquema do Adobe Experience Platform. Use o [`data`](data.md) objeto para enviar dados não XDM. Você pode usar o mapeador de sequência de dados para alinhar dados nesse objeto a campos de esquema.

## Enviar dados do evento usando a extensão de tag do SDK da Web

O envio de dados de eventos é executado como uma ação em uma regra na interface das tags da Coleção de dados da Adobe Experience Platform.

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Regras]** e selecione a regra desejada.
1. Em [!UICONTROL Ações], selecione uma ação existente ou crie uma ação.
1. Defina o [!UICONTROL Extensão] campo suspenso até **[!UICONTROL Adobe Experience Platform Web SDK]** e defina o [!UICONTROL Tipo de ação] para **[!UICONTROL Enviar evento]**.
1. Defina os campos desejados, clique em **[!UICONTROL Manter alterações]**, em seguida, execute o fluxo de trabalho de publicação.

## Enviar dados do evento usando a biblioteca JavaScript do SDK da Web

Execute o `sendEvent` ao chamar a instância configurada do SDK da Web. Certifique-se de chamar o [`configure`](../configure/overview.md) antes de chamar o `sendEvent` comando.

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

Se você decidir [lidar com respostas](../command-responses.md) com esse comando, as seguintes propriedades estão disponíveis no objeto de resposta:

* **`propositions`**: uma matriz de propostas retornadas pelo Edge Network. As apresentações renderizadas automaticamente incluem o sinalizador `renderAttempted` definir como `true`.
* **`inferences`**: uma matriz de objetos de inferência, que contém informações de aprendizado de máquina sobre este usuário.
* **`destinations`**: uma matriz de objetos de destino retornados pelo Edge Network.
