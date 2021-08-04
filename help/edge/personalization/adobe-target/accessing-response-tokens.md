---
title: Acessar tokens de resposta usando o SDK da Web da Adobe Experience Platform
description: Saiba como acessar tokens de resposta com o SDK da Web da Adobe Experience Platform.
keywords: personalização, target, adobe target, renderDecisões, sendEvent, decisionScopes, result.decisions, tokens de resposta;
source-git-commit: 4bddd9f23ae885468148d1592af219290d6fafd9
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# Acessar tokens de resposta

O conteúdo de personalização retornado do Adobe Target inclui [tokens de resposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), que são detalhes sobre a atividade, oferta, experiência, perfil do usuário, informações geográficas e muito mais. Esses detalhes podem ser compartilhados com ferramentas de terceiros ou usados para depuração. Os tokens de resposta podem ser configurados na interface do usuário do Adobe Target.

Para acessar qualquer conteúdo de personalização, forneça uma função de retorno de chamada ao enviar um evento. Esse retorno de chamada será chamado depois que o SDK receber uma resposta bem-sucedida do servidor. Seu retorno de chamada receberá um objeto `result`, que pode conter uma propriedade `propositions` contendo qualquer conteúdo de personalização retornado. Abaixo está um exemplo de como fornecer uma função de retorno de chamada.

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

Neste exemplo, `result.propositions`, se existir, é uma matriz contendo apresentações de personalização relacionadas ao evento. Consulte [Rendering personalization content](../rendering-personalization-content.md) para obter mais informações sobre o conteúdo de `result.propositions`.

Suponha que você queira coletar todos os nomes de atividades de todas as apresentações que foram renderizadas automaticamente pelo SDK da Web e enviá-las para um único array. Em seguida, você poderia enviar o único array para terceiros. Nesse caso:

1. Extraia apresentações do objeto `result`.
1. Faça o loop por cada proposta.
1. Determine se o SDK renderizou a proposta.
1. Em caso positivo, faça um loop por cada item na proposta.
1. Recupere o nome da atividade da propriedade `meta`, que é um objeto contendo tokens de resposta.
1. Encaminhe o nome da atividade para uma matriz.
1. Envie os nomes das atividades para terceiros.

Seu código seria o seguinte:

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    var activityNames = [];
    propositions.forEach(function(proposition) {
      if (proposition.renderAttempted) {
        proposition.items.forEach(function(item) {
          if (item.meta) {
            // item.meta contains the response tokens.
            var activityName = item.meta["activity.name"];
            // Ignore duplicates
            if (activityNames.indexOf(activityName) === -1) {
              activityNames.push(activityName);
            }
          }
        });
      }
    });
    // Now that activity names are in an array,
    // you can send them to a third party or use
    // them in some other way.
  });
```


