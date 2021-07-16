---
title: Módulos compartilhados para a extensão do Adobe Analytics
description: Saiba mais sobre os módulos de biblioteca compartilhada fornecidos pela extensão de tag do Adobe Analytics no Adobe Experience Platform.
source-git-commit: 8dfb7bdc16d0654ee1d76dc5f5af50938b122d33
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 78%

---

# Módulos compartilhados para a extensão do Adobe Analytics

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

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

É possível que o Adobe Analytics não tenha sido instalado ou incluído na mesma biblioteca de tags que sua extensão. Por isso, é altamente recomendável que você verifique esse caso no seu código e lide com ele adequadamente. O seguinte JavaScript é um exemplo de como você pode implementar isso:

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

Se `getTracker` for `undefined`, a extensão Adobe Analytics não existirá na biblioteca de tags. Você pode personalizar a mensagem registrada para refletir com precisão qual funcionalidade poderá ser perdida se o Adobe Analytics não estiver instalado.


## [!DNL augment-tracker]

Depois que o objeto de rastreamento é inicializado, a próxima etapa do processo é a ampliação. Essa etapa permite que sua extensão aumente o rastreador com o que for necessário antes que qualquer variável tenha sido aplicada a partir da configuração da extensão do Adobe Analytics ou antes que qualquer beacons tenha sido enviado.

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
