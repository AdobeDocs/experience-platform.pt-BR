---
title: track()
description: Acione uma regra de chamada direta.
source-git-commit: a36e5af39f904370c1e97a9ee1badad7a2eac32e
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 2%

---

# `track()`

O método `_satellite.track()` permite acionar uma [Regra de chamada direta](/help/tags/extensions/client/core/overview.md#direct-call-event).

>[!IMPORTANT]
>
>A Adobe considera `_satellite.track()` um **método de implementação herdado**. Embora ainda seja totalmente compatível, a Adobe recomenda o uso de práticas de implementação mais modernas, como a [Camada de dados de clientes Adobe](/help/tags/extensions/client/client-data-layer/overview.md), que é a abordagem recomendada para novas implementações.
>
>Se você optar por usar `_satellite.track()` no site, **proteja todas as chamadas** para que o site não seja totalmente associado à biblioteca de tags. Se não for protegida, a remoção da propriedade da marca no futuro fará com que todas as referências ao objeto `_satellite` gerem erros.

```ts
_satellite.track(identifier: string, detail?: unknown ): void;
```

Quando você chama `_satellite.track()` usando o identificador configurado na interface de marcas, essa regra é acionada imediatamente. Chamar esse método atua somente como o evento da regra; as condições da regra ainda se aplicam antes de executar as ações da regra. Várias regras de chamada direta podem usar o mesmo identificador, permitindo acionar todas essas regras de uma só vez usando uma única chamada `_satellite.track()`. Cada regra acionada ainda verifica suas próprias condições antes de tomar uma ação, mesmo se várias regras compartilharem o mesmo identificador.

## Campos disponíveis

O método `_satellite.track()` dá suporte a dois argumentos:

| Nome | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| **`identifier`** | `string` | Sim | O identificador da regra de chamada direta. Defina esse identificador ao configurar a regra na interface do usuário de tags. |
| **`detail`** | `unknown` | Não | Uma carga opcional contendo as informações desejadas. Ao configurar uma regra, você pode acessar a carga usando `event.detail` (código personalizado) ou `%event.detail%` (campos de texto que oferecem suporte à notação de elemento de dados). |

```js
// Trigger rules with the identifier 'example'
if (window._satellite?.track) {
  _satellite.track('example');
}

// Trigger a direct call rule with an optional payload that your tag rule can use
_satellite.track('contact_submit', { name: 'John Doe' });
// When configuring the rule, access the payload field using:
// event.detail.name (custom code block) or
// %event.detail.name% (data element)
```
