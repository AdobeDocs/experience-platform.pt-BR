---
title: Interagir com várias propriedades
seo-title: Adobe Experience Platform Web SDK Interagindo com várias propriedades
description: Saiba como interagir com várias propriedades do SDK da Web da Experience Platform
seo-description: Saiba como interagir com várias propriedades do SDK da Web da Experience Platform
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Interagindo com várias propriedades

>[!IMPORTANT]
>
>O SDK da Web da plataforma Adobe Experience está atualmente em beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

Há alguns casos em que você pode interagir com duas propriedades diferentes na mesma página. Dentre eles:

* Empresas que foram adquiridas e estão trabalhando na integração de seus sites
* Relações de compartilhamento de dados entre várias empresas
* Clientes que estão testando novas soluções da Adobe e não querem interromper a implementação existente

O SDK permite que você crie uma instância separada para cada propriedade adicionando outro nome à matriz no código base. No exemplo a seguir, fornecemos dois nomes, `mycustomname1` e `mycustomname2`.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

Como resultado, o script cria duas instâncias do SDK. A função global para interagir com a primeira instância é nomeada `mycustomname1` e a função global para interagir com a segunda instância é nomeada `mycustomname2`.

Ao criar duas instâncias separadas, cada uma pode ser configurada para uma propriedade diferente. Qualquer comunicação ou persistência de dados que ocorre devido à interação com `mycustomname1` é mantida isolada de `mycustomname2` e vice-versa.

A seguir ao exemplo acima, você pode executar comandos usando cada uma das instâncias, como segue:

```javascript
mycustomname1("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

mycustomname1("event", {
  "data": {
    "key": "value"
  }
});

mycustomname2("configure", {
  "configId": "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  "orgId": "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

mycustomname2("event", {
  "data": {
    "key": "value"
  }
});
```

Certifique-se de executar o `configure` comando para cada instância antes de executar outros comandos na mesma instância.

## Limitações

Para evitar conflitos com cookies, somente uma instância do SDK da Web da plataforma Adobe Experience em uma página pode ter um particular `configId`.  Da mesma forma, somente uma instância do SDK da Web da Adobe Experience Platform pode ter um particular `orgId`.
