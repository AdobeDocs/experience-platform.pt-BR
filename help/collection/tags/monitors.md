---
title: _monitores
description: Adicione ouvintes de eventos para depurar a implementação da tag.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 1%

---

# `_monitors`

O objeto `_satellite._monitors` permite criar ouvintes de eventos e executar um código personalizado quando a biblioteca detecta uma regra acionada. Seu uso principal é auxiliar na depuração da implementação para garantir que as regras sejam acionadas corretamente.

>[!IMPORTANT]
>
>Este objeto é somente para fins de depuração. Não vincule a lógica de produção a esse objeto. A disponibilidade de propriedades ou nomes nesse objeto pode ser alterada pela Adobe a qualquer momento.

```ts
_satellite._monitors?: {
  ruleTriggered(event: { rule: Rule }): void;
  ruleCompleted(event: { rule: Rule }): void;
  ruleConditionFailed(event: { rule: Rule; condition: Condition }): void;
}[];
```

Você pode acompanhar os seguintes tipos de evento:

## `ruleTriggered`

Essa função de retorno de chamada é acionada quando um evento aciona uma regra antes que as condições e ações da regra tenham sido processadas. Se esta função disparar, `ruleCompleted` ou `ruleConditionFailed` dispara logo depois (mutuamente exclusivo).

## `ruleCompleted`

A função de retorno de chamada `ruleCompleted` é acionada após `ruleTriggered` quando os critérios de condição da regra são bem-sucedidos e todas as ações da regra são executadas.

## `ruleConditionFailed`

A função de retorno de chamada `ruleConditionFailed` é acionada após `ruleTriggered` quando pelo menos uma das condições da regra falhar.

## objeto `Rule`

Cada função de retorno de chamada expõe um objeto `Rule` que fornece informações sobre a própria regra.

```ts
type Rule = {
  id: string;
  name: string;
  events: Event[]; // Rule-specific events
  conditions: Condition[]; // Rule-specific conditions
  actions: Action[]; // Rule-specific actions
}
```

| Nome | Tipo | Descrição |
|---|---|---|
| **`id`** | `string` | O identificador exclusivo da regra. |
| **`name`** | `string` | O nome amigável da regra. |
| **`events`** | `Event[]` | Uma matriz de eventos configurada para acionar a regra. |
| **`conditions`** | `Condition[]` | Uma matriz de condições configuradas para acionar a regra. |
| **`actions`** | `Action[]` | Uma matriz de ações configuradas para serem executadas quando a regra for acionada. |

## Exemplo

Adicione o seguinte trecho de código à HTML na tag `<head>` antes de chamar o carregador da biblioteca de tags:

```html
<script>
  window._satellite ??= {};
  window._satellite._monitors ??= [];
  window._satellite._monitors.push({
    ruleTriggered(event) { console.log('Rule triggered', event.rule);},
    ruleCompleted(event) { console.log('Rule completed', event.rule);},
    ruleConditionFailed(event) { console.log('Rule condition failed', event.rule, event.condition);}
  });
</script>
<script src="https://assets.adobedtm.com/.../launch-EN...js" async></script>
```

Como a biblioteca de marcas ainda não foi carregada neste ponto da página, o objeto `_satellite` inicial será criado e uma matriz em `_satellite._monitors` será inicializada. O script então adiciona um objeto de monitor a essa matriz.

Considere as seguintes dicas ao usar monitores:

* Observe que essas mensagens de depuração usam `console.log` em vez de [`_satellite.logger`](logger.md), pois os ganchos são criados antes do carregamento da biblioteca de marcas.
* Embora o exemplo de código inclua todas as três funções de retorno de chamada, elas não são campos obrigatórios. Você pode incluir apenas os ganchos desejados ao depurar regras no site.
* Vários monitores são permitidos, mesmo para os mesmos eventos. Se você usar vários monitores para um único evento, a ordem de chamada não será garantida.
* Certifique-se de criar `_monitors` _antes_ de carregar a biblioteca de marcas. Se você criar esses ganchos depois que a biblioteca for carregada, somente as regras que forem acionadas a partir desse ponto serão capturadas.
