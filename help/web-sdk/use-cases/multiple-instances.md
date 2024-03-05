---
title: Usar várias instâncias do SDK da Web
description: Saiba como interagir com várias propriedades do SDK da Web do Experience Platform.
keywords: várias propriedades;configurar;sendEvent;edgeConfigId;orgId;
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Usar várias instâncias do SDK da Web

Há casos em que você pode querer interagir com duas propriedades diferentes na mesma página. Esses casos incluem:

* Empresas que foram adquiridas e estão trabalhando na integração de seus sites
* Relacionamentos de compartilhamento de dados entre várias empresas
* Clientes que estão testando novas soluções de Adobe e não desejam interromper sua implementação existente

O SDK permite criar uma instância separada para cada propriedade adicionando outro nome à matriz no código base. O exemplo a seguir fornece dois nomes, `titanium` e `copper`.

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["titanium", "copper"]);
</script>
<script src="alloy.js" async></script>
```

Como resultado, o script cria duas instâncias do SDK. A função global para interagir com a primeira instância é chamada de `titanium` e a função global para interagir com a segunda instância é nomeada `copper`.

Ao criar duas instâncias separadas, cada uma pode ser configurada para uma propriedade diferente. Qualquer comunicação ou persistência de dados que ocorra devido à interação com o `titanium` é mantido isolado de `copper`.

Seguindo o exemplo acima, você pode executar comandos usando cada instância:

```javascript
titanium("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

titanium("sendEvent", {
  "data": {
    "key": "value"
  }
});

copper("configure", {
  "edgeConfigId": "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  "orgId": "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

copper("sendEvent", {
  "data": {
    "key": "value"
  }
});
```

Certifique-se de executar o `configure` para cada instância antes de executar outros comandos na mesma instância.

>[!IMPORTANT]
>
>Para evitar conflitos com cookies, cada instância do SDK da Web deve ter sua própria `edgeConfigId` e seu próprio e exclusivo `orgId`.
