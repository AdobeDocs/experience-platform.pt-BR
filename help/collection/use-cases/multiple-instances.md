---
title: Usar várias instâncias do Web SDK
description: Saiba como interagir com várias propriedades do Experience Platform Web SDK.
keywords: várias propriedades
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: 192739967e6b050bb04893ee7bab5119dd7f870c
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Usar várias instâncias do Web SDK

Há casos em que você pode querer interagir com duas propriedades diferentes na mesma página. Os cenários possíveis incluem:

* Empresas que foram adquiridas e estão trabalhando na integração de seus sites
* Relacionamentos de compartilhamento de dados entre várias empresas
* Clientes que estão testando novas soluções da Adobe e não desejam interromper sua implementação existente

O SDK permite criar uma instância separada para cada propriedade adicionando outro nome à matriz no [código base](../js/install/base-code.md). O exemplo a seguir fornece dois nomes, `titanium` e `copper`.

```html
<!-- Base code -->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["titanium", "copper"]);
</script>

<!-- Load the Web SDK (JavaScript library loader or Tags embed code) -->
<!-- <script src=".../alloy.min.js" async></script> -->
<!-- <script src=".../launch-<ENV>.min.js" async></script> -->
```

Como resultado, o script cria duas funções globais (`titanium` e `copper` no exemplo acima) que se tornam duas instâncias do SDK quando a biblioteca é inicializada. Cada instância mantém sua própria configuração e estado; qualquer comando que use `titanium` é mantido isolado de `copper`.

>[!TIP]
>
>Se estiver usando o código base com marcas, verifique se todos os nomes de instância definidos correspondem a todos os [nomes de instância do SDK](/help/tags/extensions/client/web-sdk/configure/general.md) ao configurar a extensão de marca.

Seguindo o exemplo do padrão de nomenclatura de `titanium` e `copper` como instâncias do Web SDK, você pode executar comandos independentemente:

```javascript
titanium("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

titanium("sendEvent", {
  data: {
    key: "value"
  }
});

copper("configure", {
  datastreamId: "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  orgId: "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

copper("sendEvent", {
  data: {
    key: "value"
  }
});
```

Certifique-se de executar o comando [`configure`](../js/commands/configure/overview.md) para cada instância antes de executar outros comandos na mesma instância.

>[!IMPORTANT]
>
>Para evitar conflitos com cookies, cada instância do Web SDK deve ter sua própria `datastreamId` exclusiva e sua própria `orgId` exclusiva.
