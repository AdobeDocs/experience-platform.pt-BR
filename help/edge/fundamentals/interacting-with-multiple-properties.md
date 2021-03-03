---
title: Interagir com várias propriedades no SDK da Web da Adobe Experience Platform
description: Saiba como interagir com várias propriedades do SDK da Web da Experience Platform.
keywords: várias propriedades; configurar; sendEvent; edgeConfigId; orgId;
translation-type: tm+mt
source-git-commit: b865b7fb940ca2d5f8b44f71eb58e62e3473f52d
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Interagir com várias propriedades

Há determinados casos em que você pode interagir com duas propriedades diferentes na mesma página. Esses casos incluem:

* Empresas que foram adquiridas e estão trabalhando na integração de seus sites
* Relações de compartilhamento de dados entre várias empresas
* Clientes que estão testando novas soluções da Adobe e não desejam interromper a implementação existente

O SDK permite criar uma instância separada para cada propriedade, adicionando outro nome à matriz no código base. O exemplo a seguir fornece dois nomes, `mycustomname1` e `mycustomname2`.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

Como resultado, o script cria duas instâncias do SDK. A função global para interagir com a primeira instância é chamada de `mycustomname1` e a função global para interagir com a segunda instância é chamada de `mycustomname2`.

Ao criar duas instâncias separadas, cada uma pode ser configurada para uma propriedade diferente. Qualquer comunicação ou persistência de dados que ocorre devido à interação com `mycustomname1` é mantida isolada de `mycustomname2`.

A seguir ao exemplo acima, você pode executar comandos usando cada uma das instâncias, da seguinte maneira:

```javascript
mycustomname1("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

mycustomname1("sendEvent", {
  "data": {
    "key": "value"
  }
});

mycustomname2("configure", {
  "edgeConfigId": "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  "orgId": "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

mycustomname2("sendEvent", {
  "data": {
    "key": "value"
  }
});
```

Certifique-se de executar o comando `configure` para cada instância antes de executar outros comandos na mesma instância.

## Limitações

Para evitar conflitos com cookies, somente uma instância da Adobe Experience Platform [!DNL Web SDK] em uma página pode ter um `edgeConfigId` específico. Da mesma forma, somente uma instância da Adobe Experience Platform [!DNL Web SDK] pode ter um `orgId` específico.
