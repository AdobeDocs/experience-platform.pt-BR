---
title: Interagir com várias propriedades no SDK da Web da Adobe Experience Platform
description: Saiba como interagir com várias propriedades do SDK da Web do Experience Platform.
keywords: várias propriedades;configurar;sendEvent;edgeConfigId;orgId;
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Interagir com várias propriedades

Há casos em que você pode querer interagir com duas propriedades diferentes na mesma página. Esses casos incluem:

* Empresas que foram adquiridas e estão trabalhando na integração de seus sites
* Relacionamentos de compartilhamento de dados entre várias empresas
* Clientes que estão testando novas soluções de Adobe e não desejam interromper sua implementação existente

O SDK permite criar uma instância separada para cada propriedade adicionando outro nome à matriz no código base. O exemplo a seguir fornece dois nomes, `mycustomname1` e `mycustomname2`.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

Como resultado, o script cria duas instâncias do SDK. A função global para interagir com a primeira instância é chamada de `mycustomname1` e a função global para interagir com a segunda instância é nomeada `mycustomname2`.

Ao criar duas instâncias separadas, cada uma pode ser configurada para uma propriedade diferente. Qualquer comunicação ou persistência de dados que ocorra devido à interação com o `mycustomname1` é mantido isolado de `mycustomname2`.

Após o exemplo acima, você pode executar comandos usando cada uma das instâncias, da seguinte maneira:

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

Certifique-se de executar o `configure` para cada instância antes de executar outros comandos na mesma instância.

## Limitações

Para evitar conflitos com cookies, somente uma instância do Adobe Experience Platform [!DNL Web SDK] em uma página pode ter um determinado `edgeConfigId`. Da mesma forma, apenas uma instância do Adobe Experience Platform [!DNL Web SDK] pode ter um `orgId`.
