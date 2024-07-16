---
title: getIdentity
description: Obter a identidade de um visitante sem enviar dados do evento.
exl-id: 28b99f62-14c4-4e52-a5c7-9f6fe9852a87
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 2%

---

# `getIdentity`

O comando `getIdentity` permite obter uma ID de visitante sem enviar dados do evento. Quando você executa o comando `sendEvent`, o SDK da Web obtém automaticamente a identidade do visitante, se uma ainda não estiver presente.

Se você precisar de chamadas separadas para gerar uma ID de visitante e enviar dados, poderá usar esse comando.

## Obter identidade usando a extensão de tag do SDK da Web

A extensão de tag do SDK da Web não oferece esse comando por meio da interface do usuário da extensão de tag. Use o editor de código personalizado usando a sintaxe da biblioteca do JavaScript.

## Obter identidade usando a biblioteca JavaScript do SDK da Web

Execute o comando `getIdentity` ao chamar a instância configurada do SDK da Web. As seguintes opções estão disponíveis ao configurar este comando:

* **`namespaces`**: Uma matriz de namespaces. O valor padrão é `["ECID"]`. Os valores válidos incluem `["ECID"]`, `null` ou `undefined`.
* **`edgeConfigOverrides`**: Um [objeto de substituição de configuração de sequência de dados](datastream-overrides.md).

```js
alloy("getIdentity",{
  "namespaces": ["ECID"]
});
```

## Objeto de resposta

Se você decidir [manipular respostas](command-responses.md) com este comando, as seguintes propriedades estarão disponíveis no objeto de resposta:

* **`identity.ECID`**: uma string contendo a ECID do visitante.
* **`edge.regionID`**: um número inteiro que representa a região do Edge Network que o navegador atingiu ao adquirir uma identidade. É o mesmo que a dica de localização do Audience Manager herdado.
