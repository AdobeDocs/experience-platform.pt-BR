---
title: applyResponse
description: Use uma resposta do Edge Network para inicializar o Web SDK.
exl-id: 0653b8f7-33f0-43a1-97f5-59a51270f660
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# `applyResponse`

O comando `applyResponse` permite executar várias ações com base em uma resposta do Edge Network. Normalmente, é usado em implantações híbridas, nas quais o servidor faz uma chamada inicial para o Edge Network. Esse comando recebe a resposta dessa chamada e inicializa o Web SDK no navegador.

Execute o comando `applyResponse` ao chamar a instância configurada do Web SDK. O objeto que contém opções de configuração é compatível com os seguintes campos:

* **`renderDecisions`**: um booleano que força o Web SDK a renderizar qualquer conteúdo personalizado que esteja qualificado para renderização automática. Idêntico a [`renderDecisions`](sendevent/renderdecisions.md) no comando [`sendEvent`](sendevent/overview.md).
* **`responseHeaders`**: um mapa de nomes de cabeçalho de cadeia de caracteres para valores de cabeçalho de cadeia de caracteres.
* **`responseBody`**: Obrigatório. Um corpo de resposta JSON da chamada do servidor para o Edge Network.
* **`personalization.sendDisplayEvent`**: um booleano que opera de forma idêntica a [`personalization.sendDisplayEvent`](sendevent/personalization.md) no comando `sendEvent`.

```js
alloy("applyResponse",{
  "renderDecisions": true,
  "responseHeaders": {},
  "responseBody": {},
  "personalization": {
    "sendDisplayEvent": true
  }
});
```

## Objeto de resposta

Se você decidir [manipular respostas](command-responses.md) com este comando, as seguintes propriedades estarão disponíveis no objeto de resposta:

* **`propositions`**: Uma matriz de propostas retornadas pela Edge Network. As propostas que são renderizadas automaticamente incluem o sinalizador `renderAttempted` definido como `true`.
* **`inferences`**: uma matriz de objetos de inferência, que contém informações de aprendizado de máquina sobre este usuário.
* **`destinations`**: Uma matriz de objetos de destino retornada pela Edge Network.

## Aplicar resposta usando a extensão de tag do Web SDK

A extensão de tag do Web SDK equivalente a este comando é a ação [**[!UICONTROL Apply response]**](/help/tags/extensions/client/web-sdk/actions/apply-response.md).
