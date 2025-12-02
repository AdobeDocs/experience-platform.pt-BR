---
title: Usar várias instâncias do Web SDK
description: Saiba como interagir com várias propriedades do Experience Platform Web SDK.
keywords: várias propriedades
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: 2c60ebdebd706ed7b5beb2438ae83665b6b6e47a
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# Usar várias instâncias do Web SDK

Há casos em que você pode querer interagir com duas propriedades diferentes na mesma página. Esses casos incluem:

* Empresas que foram adquiridas e estão trabalhando na integração de seus sites
* Relacionamentos de compartilhamento de dados entre várias empresas
* Clientes que estão testando novas soluções da Adobe e não desejam interromper sua implementação existente

O SDK permite criar uma ocorrência separada para cada propriedade adicionando outro nome à matriz no código base. O exemplo a seguir fornece dois nomes, `titanium` e `copper`.

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["titanium", "copper"]);
</script>
<script src="alloy.js" async></script>
```

Como resultado, o script cria duas instâncias da SDK. A função global para interagir com a primeira instância é nomeada `titanium` e a função global para interagir com a segunda instância é nomeada `copper`.

Ao criar duas instâncias separadas, cada uma pode ser configurada para uma propriedade diferente. Qualquer comunicação ou persistência de dados que ocorra devido à interação com `titanium` é mantida isolada de `copper`.

Seguindo o exemplo acima, você pode executar comandos usando cada instância:

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

Certifique-se de executar o comando `configure` para cada instância antes de executar outros comandos na mesma instância.

>[!IMPORTANT]
>
>Para evitar conflitos com cookies, cada instância do Web SDK deve ter sua própria `datastreamId` exclusiva e sua própria `orgId` exclusiva.
