---
title: getIdentity
description: Obter a identidade de um visitante sem enviar dados do evento.
source-git-commit: 90493d179e620604337bda96cb3b7f5401ca4a81
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 2%

---

# `getIdentity`

A variável `getIdentity` permite obter uma ID de visitante sem enviar dados do evento. Quando você executa o `sendEvent` , o SDK da Web obtém automaticamente a identidade do visitante se ainda não houver uma.

Se você precisar de chamadas separadas para gerar uma ID de visitante e enviar dados, poderá usar esse comando.

## Obter identidade usando a extensão de tag do SDK da Web

A extensão de tag do SDK da Web não oferece esse comando por meio da interface do usuário da extensão de tag. Use o editor de código personalizado usando a sintaxe da biblioteca JavaScript.

## Obter identidade usando a biblioteca JavaScript do SDK da Web

Execute o `getIdentity` ao chamar a instância configurada do SDK da Web. As seguintes opções estão disponíveis ao configurar este comando:

* **`namespaces`**: uma matriz de namespaces. O valor padrão é `["ECID"]`. Os valores válidos incluem `["ECID"]`, `null`ou `undefined`.
* **`edgeConfigOverrides`**: Um [objeto de substituição da configuração da sequência de dados](datastream-overrides.md).

```js
alloy("getIdentity",{
  "namespaces": ["ECID"]
});
```

## Objeto de resposta

Se você decidir [lidar com respostas](command-responses.md) com esse comando, as seguintes propriedades estão disponíveis no objeto de resposta:

* **`identity.ECID`**: uma string que contém a ECID do visitante.
* **`edge.regionID`**: um número inteiro que representa a região da Rede de borda que o navegador atinge ao adquirir uma identidade. É o mesmo que a dica de localização do Audience Manager herdado.
