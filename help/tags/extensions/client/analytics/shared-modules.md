---
title: Módulos compartilhados para a extensão do Adobe Analytics
description: Saiba mais sobre os módulos de biblioteca compartilhada fornecidos pela extensão de tag do Adobe Analytics na Adobe Experience Platform.
exl-id: f1d7cb2b-0058-46f9-983c-079079e06057
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 100%

---

# Módulos compartilhados para a extensão do Adobe Analytics

A [extensão do Adobe Analytics](./overview.md) fornece dois [módulos compartilhados](../../../extension-dev/web/shared.md) diferentes que você pode integrar ao seu aplicativo de experiência. Esses módulos são abordados nas seções abaixo.

## [!DNL get-tracker]

Antes de enviar beacons, o Adobe Analytics deve inicializar o objeto de rastreamento. O processo de inicialização começa carregando o [AppMeasurement](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=pt-BR), seguido pela criação de um objeto de rastreador.

Você poderá acessar o objeto do rastreador depois que ele for totalmente inicializado usando o módulo compartilhado `get-tracker` da seguinte maneira:

```js
var getTracker = turbine.getSharedModule('adobe-analytics', 'get-tracker');

getTracker().then(function(tracker) {
  // Use tracker in some way
});
```

### Verificando se o Adobe Analytics foi instalado

É possível que o Adobe Analytics não tenha sido instalado ou incluído na mesma tag de biblioteca que a sua extensão. Por isso, é altamente recomendável que você verifique esse caso no seu código e lide com ele adequadamente. O seguinte JavaScript é um exemplo de como você pode implementar isso:

```js
var getTracker = turbine.getSharedModule('adobe-analytics', 'get-tracker');

if (getTracker) {
  getTracker().then(function(tracker) {
    // Use tracker in some way
  });
} else {
  turbine.logger.error("The Adobe Analytics extension is required for Extension XYZ to function properly.");
}
```

Se `getTracker` está `undefined`, a extensão do Adobe Analytics não existe na tag de biblioteca. Você pode personalizar a mensagem registrada para refletir com precisão qual funcionalidade poderá ser perdida se o Adobe Analytics não estiver instalado.


## [!DNL augment-tracker]

Depois que o objeto de rastreamento é inicializado, a próxima etapa do processo é a ampliação. Essa etapa permite que a extensão amplie o rastreador com o que for necessário antes que qualquer variável seja aplicada da configuração de extensão do Adobe Analytics ou antes que qualquer beacon seja enviado.

Além disso, a extensão tem a oportunidade de pausar o processo de inicialização do rastreador enquanto a extensão executa qualquer tarefa assíncrona própria, como buscar dados ou JavaScript de um servidor.

Você pode implementar o módulo `augment-tracker` da seguinte maneira:

```js
var augmentTracker = turbine.getSharedModule('adobe-analytics', 'augment-tracker');

augmentTracker(function(tracker) {
  // Augment tracker in some way
});
```

A função transmitida para `augmentTracker()` será chamada assim que a fase de aumento do processo de inicialização do rastreador for atingida.

Se sua extensão precisar concluir uma tarefa assíncrona antes de aumentar o rastreador, você poderá retornar uma promessa da sua função da seguinte maneira:

```js
var Promise = require('@adobe/reactor-promise');
var augmentTracker = turbine.getSharedModule('adobe-analytics', 'augment-tracker');

augmentTracker(function(tracker) {
  return new Promise(function(resolve) {
    // Augment the tracker object, then call resolve()
  });
});
```

Ao retornar uma promessa, sua extensão sinaliza ao Adobe Analytics que ela deve pausar o processo de inicialização do rastreador até que a promessa seja resolvida.

>[!WARNING]
>
>Seja prudente ao pausar o processo de inicialização do rastreador, pois ele pode atrasar o envio de beacons e, portanto, resultar em dados não coletados (por exemplo, se o usuário sair da página antes que o beacon seja enviado).
