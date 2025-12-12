---
title: Tipos de evento para extensões da Web
description: Saiba como definir um módulo de biblioteca do tipo evento para uma extensão da Web no Adobe Experience Platform.
exl-id: dbdd1c88-5c54-46be-9824-2f15cce3d160
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 71%

---

# Tipos de evento para extensões da Web

Em uma regra de tag, um evento é uma atividade que deve ocorrer para que uma regra seja acionada. Como exemplo, uma extensão da Web pode fornecer um tipo de evento de &quot;gesto&quot; que observa a ocorrência de determinado gesto de toque ou mouse. Quando o gesto ocorre, a lógica do evento aciona a regra.

Um módulo de biblioteca do tipo de evento é projetado para detectar quando uma atividade ocorre e, em seguida, chamar uma função para acionar uma regra associada. O evento que está sendo detectado é personalizável. Por exemplo, o pode detectar quando um usuário faz um determinado gesto, rola rapidamente ou interage com algo.

Este documento aborda como definir tipos de evento para uma extensão da Web no Adobe Experience Platform.

>[!NOTE]
>
>Este documento supõe que você esteja familiarizado com os módulos de biblioteca e como eles são integrados nas extensões da Web. Consulte a visão geral na [formatação de módulo de biblioteca](./format.md) para obter uma introdução à sua implementação antes de retornar a este guia.

Os tipos de evento são definidos por extensões e geralmente consistem no seguinte:

1. Uma [visualização](./views.md) mostrada na interface do usuário do Experience Platform e na interface da Coleção de dados que permite que os usuários modifiquem as configurações para o evento.
2. Um módulo de biblioteca emitido na biblioteca de tempo de execução de tag para interpretar as configurações e observar a ocorrência de determinada atividade.

`module.exports` aceite tanto o `settings` quanto os parâmetros `trigger`. Isso permite a personalização do tipo de evento.

```js
module.exports = function(settings, trigger) { … };
```

| Parâmetro | Descrição |
| --- | --- |
| `settings` | Um objeto que contém quaisquer configurações que o usuário definiu na visualização do tipo de evento. Você tem controle total sobre o que vai para esse objeto. |
| `trigger` | Uma função que o módulo deve chamar sempre que a regra deve ser acionada. Há uma relação individualizada entre um objeto `settings`, uma função `trigger` e uma regra. Significa que a função de acionamento recebida para uma regra não pode ser usada para acionar uma regra diferente. |

>[!NOTE]
>
>A função exportada será chamada uma vez para cada regra configurada para usar seu tipo de evento.

Usando a atividade de cinco segundos decorridos como exemplo, após cinco segundos, a atividade ocorre e a regra é acionada. O módulo será semelhante ao deste exemplo.

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, 5000);
};
```

Se você quiser que a duração seja configurável pelo usuário do Adobe Experience Platform, será necessária a opção para inserir e salvar uma duração no objeto de configurações. O objeto pode ser semelhante a:

```js
{
  "duration": 25000
}
```

Para operar com a duração definida pelo usuário, o módulo precisaria ser atualizado para incluir tal recurso.

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, settings.duration);
};
```

## Transmissão de dados do evento contextuais

Quando uma regra é acionada, geralmente é útil fornecer detalhes adicionais sobre o evento que ocorreu. Os usuários que criam regras podem considerar essas informações úteis para alcançar determinado comportamento. Por exemplo, vamos supor que um profissional de marketing deseje criar uma regra na qual um beacon de análise é enviado sempre que o usuário desliza o dedo pela tela. A extensão teria que fornecer um tipo de evento `swipe` para que o profissional de marketing pudesse usar esse tipo de evento para acionar a regra apropriada. Supondo que o profissional de marketing pretendesse incluir o ângulo no qual o deslizamento ocorreu no beacon, isso seria difícil de fazer sem fornecer informações adicionais. Para fornecer mais informações sobre o evento que ocorreu, passe um objeto ao chamar a função `trigger`. Por exemplo:

```js
trigger({
  swipeAngle: 90 // the value would be the detected angle
});
```

Assim, o profissional de marketing poderia usar esse valor em um beacon de análise especificando o valor `%event.swipeAngle%` em um campo de texto. Ele também pode acessar `event.swipeAngle` em outros contextos (como uma ação de código personalizada). É possível incluir outros tipos de informações opcionais do evento que possam ser úteis para um profissional de marketing da mesma maneira.

### [!DNL nativeEvent]

Se o seu tipo de evento for baseado em um evento nativo (por exemplo, se a extensão tiver fornecido um tipo de evento) `click`, recomenda-se definir a propriedade `nativeEvent` conforme segue.

```js
trigger({
  nativeEvent: nativeEvent // the value would be the underlying native event
});
```

Isso pode ser útil para profissionais de marketing que tentam acessar qualquer informação do evento nativo, como coordenadas de cursor.

### [!DNL element]

Se houver uma forte relação entre um elemento e o evento que ocorreu, será recomendável definir a propriedade `element` para o nó DOM do elemento. Por exemplo, vamos supor que a extensão forneça um tipo de evento `click` e que você autorize os profissionais de marketing a configurá-lo de modo que só seja acionado se um elemento com a ID de `herobanner` for selecionado. Nesse caso, se o usuário selecionar o banner hero, será recomendável chamar `trigger` e definir `element` para o nó DOM do banner hero.

```js
trigger({
  element: element // the value would be the DOM node
});
```

## Respeitar a ordem das regras

As tags oferecem aos usuários a capacidade de solicitar regras. Por exemplo, um usuário pode criar duas regras que usam o tipo de evento de alteração de orientação e personalizar a ordem em que as regras são acionadas. Vamos supor que o usuário do Adobe Experience Platform especifique um valor de ordem de `2` para o evento de alteração de orientação na Regra A e um valor de ordem de `1` para o evento de alteração de orientação na Regra B. Isso indica que, quando a orientação mudar em um dispositivo móvel, a Regra B deverá ser acionada antes da Regra A (regras com valores de ordem mais baixa são acionadas primeiro).

Como mencionado anteriormente, a função exportada em nosso módulo de evento será chamada uma vez para cada regra configurada para usar nosso tipo de evento. Cada vez que a função exportada é chamada, ela recebe uma função exclusiva `trigger` vinculada a uma regra específica. No cenário descrito, nossa função exportada será chamada uma vez com uma função `trigger` vinculada à Regra B e, em seguida, novamente com uma função `trigger` vinculada à Regra A. A Regra B aparece primeiro porque o usuário lhe deu um valor de ordem menor que a Regra A. Quando nosso módulo de biblioteca detecta uma alteração de orientação, é importante chamar as funções `trigger` na mesma ordem em que foram fornecidas ao módulo da biblioteca.

No código de exemplo abaixo, observe que quando uma alteração de orientação é detectada, as funções de acionamento são chamadas na mesma ordem em que foram fornecidas à função exportada:

```js
var triggers = [];

window.addEventListener('orientationchange', function() {
  triggers.forEach(function(trigger) {
    trigger();
  });
});

module.exports = function(settings, trigger) {
  triggers.push(trigger);
};
```

Isso garante que a ordem especificada pelo usuário seja mantida.

Uma implementação incorreta chamaria as funções de acionamento em uma ordem diferente:

```js
var triggers = [];

window.addEventListener('orientationchange', function() {
  for (var i = triggers.length - 1; i >= 0; i--) {
    triggers[i]();
  }
});

module.exports = function(settings, trigger) {
  triggers.push(trigger);
};
```

As práticas de programação natural mantêm a ordem correta, mas é importante estar ciente das implicações e realizar o desenvolvimento adequadamente.
