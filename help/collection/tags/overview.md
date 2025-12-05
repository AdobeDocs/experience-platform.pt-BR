---
title: Referência a objeto satélite
description: Saiba mais sobre o objeto _satellite do lado do cliente e as várias funções que você pode executar com ele nas tags.
exl-id: f8b31c23-409b-471e-bbbc-b8f24d254761
source-git-commit: 05bf3a8c92aa221af153b4ce9949f0fdfc3c86ab
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# `_satellite` referência do objeto

_Essas páginas descrevem como usar o objeto `_satellite`, que permite gerenciar e personalizar a lógica da tag usando o JavaScript. Consulte a [extensão de tag do Adobe Experience Platform Web SDK](/help/tags/extensions/client/web-sdk/overview.md) para obter detalhes sobre como configurar sua implementação na interface da Coleção de dados._

O objeto `_satellite` expõe vários pontos de entrada com suporte que ajudam você a interagir com a biblioteca de tags publicada no site. Todas as implantações de tag expõem `_satellite` se a tag do carregador for implementada corretamente. Existem vários casos de uso principais para esse objeto:

* Uso na biblioteca de tags em blocos de código personalizados, fornecendo acesso total à própria biblioteca de tags.
* Depuração da implementação implantada em qualquer ambiente (desenvolvimento, preparo ou produção)
* Implementação direta no seu site, fornecendo controle total sobre quando os eventos ou as regras de tag são acionados. Para novas implementações, a Adobe recomenda usar uma estratégia mais flexível, como a [Camada de dados de clientes Adobe](/help/tags/extensions/client/client-data-layer/overview.md).

>[!IMPORTANT]
>
>Se você chamar `_satellite` do código do site (por exemplo, `_satellite.track()`), **proteja todas as chamadas** para que o site não seja totalmente associado à biblioteca de marcas.
>
>Usar `_satellite` dentro do código personalizado de uma propriedade de tag ou localmente no console do navegador não requer proteção.

## Exemplos de uso comum

```js
// Read and write a temporary data element value (guarded)
if(window._satellite?.getVar && window._satellite?.setVar) {
  const region = _satellite.getVar('user_region');
  _satellite.setVar('promo_code', code);
}

// Manually trigger a rule configured in your tag property (guarded)
if (window._satellite?.track) {
  _satellite.track('cart_add', { sku: '123', qty: 2 });
}

// Local console debugging (guarding not needed)
_satellite.setDebug(true);
_satellite.logger.log('Rule evaluated');
```
