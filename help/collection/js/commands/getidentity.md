---
title: getIdentity
description: Obter a identidade de um visitante sem enviar dados do evento.
exl-id: 28b99f62-14c4-4e52-a5c7-9f6fe9852a87
source-git-commit: aea46e3804d315c1237fc853540771f1b5c2b767
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 2%

---

# `getIdentity`

Quando você executa o comando [`sendEvent`](sendevent/overview.md), o Web SDK obtém automaticamente a identidade do visitante, se uma ainda não estiver presente. O comando `getIdentity` permite obter uma ID de visitante sem enviar dados do evento. Se você precisar de chamadas separadas para gerar uma ID de visitante e enviar dados, poderá usar esse comando.

O comando `getIdentity` passa pelo seguinte fluxo para recuperar o `ECID`.

1. Você usa o Web SDK para chamar `getIdentity` ou [`appendIdentityToUrl`](appendidentitytourl.md).
1. O Web SDK aguarda que as informações de consentimento sejam fornecidas.
1. O Web SDK verifica se o namespace `ECID` foi solicitado na chamada. Por padrão, o namespace `ECID` é sempre incluído.
1. O Web SDK lê o cookie `kndctr` e retorna seu valor como `ECID`, se ele existir. Retorna apenas o valor `ECID`, mas não `regionId`.
1. Se o cookie de identidade `kndctr` não estiver definido ou o namespace `"CORE"` tiver sido solicitado, o Web SDK fará uma solicitação para a Edge Network.
1. O Edge Network retorna o `ECID` e o `regionId` (e o `CORE ID`, se solicitado).

Execute o comando `getIdentity` ao chamar a instância configurada do Web SDK. As seguintes opções estão disponíveis ao configurar este comando:

* **`namespaces`**: Uma matriz de namespaces. O valor padrão é `["ECID"]`. Outros valores compatíveis incluem:
   * `["CORE"]`
   * `["ECID","CORE"]`
   * `null`
   * `undefined`

  Você pode solicitar `"ECID"` e `"CORE ID"` ao mesmo tempo. Exemplo: `"namespaces": ["ECID","CORE"]`.

* **`edgeConfigOverrides`**: Um [objeto de substituição de configuração de sequência de dados](configure/edgeconfigoverrides.md).

```js
alloy("getIdentity",{
  // This command retrieves both ECID and CORE IDs
  "namespaces": ["ECID","CORE"] 
});
```

## Objeto de resposta

Se você decidir [manipular respostas](command-responses.md) com este comando, as seguintes propriedades estarão disponíveis no objeto de resposta:

* **`identity.ECID`**: uma string contendo a ECID do visitante.
* **`identity.CORE`**: uma cadeia de caracteres contendo a ID PRINCIPAL do visitante.
* **`edge.regionID`**: um número inteiro que representa a região do Edge Network que o navegador atinge ao adquirir uma identidade. É o mesmo que a dica de localização herdada do Audience Manager.

```js
// Get the visitor's ECID
alloy('getIdentity').then(result => {
  console.log(result.identity.ECID);
});
```

## Obter identidade usando a extensão de tag do Web SDK

A extensão de tag do Web SDK não oferece esse comando por meio da interface do usuário da extensão de tag. Use o editor de código personalizado usando a sintaxe da biblioteca do JavaScript.
