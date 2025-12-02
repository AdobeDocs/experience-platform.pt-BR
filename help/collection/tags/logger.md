---
title: logger
description: Informações de saída para o console do navegador durante a depuração.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 1%

---

# `logger`

O objeto `_satellite.logger` contém métodos que permitem gerar mensagens de diagnóstico ou informativas no console do navegador quando a [Depuração](../use-cases/debugging.md) está habilitada. Se a depuração não estiver habilitada, todas as chamadas do método `logger` não farão nada.

Esses métodos permitem que desenvolvedores, profissionais de marketing técnico e testadores vejam facilmente o que é acionado em uma propriedade de tag e quando. Como essas mensagens do console só aparecem quando a depuração está habilitada, você pode deixar `logger` mensagens nas implantações para produção sem afetar o console do navegador dos visitantes do site.

```ts
readonly _satellite.logger: {
  debug(...args: unknown[]): void;
  log(...args: unknown[]): void;
  info(...args: unknown[]): void;
  warn(...args: unknown[]): void;
  error(...args: unknown[]): void;
}
```

>[!TIP]
>
>As versões anteriores do objeto de marca usaram `_satellite.notify()`. A função `notify()` foi preterida em favor de `_satellite.logger`.

## Métodos

Todos os métodos `_satellite.logger` passam para seu método `console.*` do JavaScript correspondente quando a depuração está habilitada. A maioria dos argumentos ou objetos `console` tem suporte usando `_satellite.logger`:

| Método | Encaminha para | Usos recomendados |
|---|---|---|
| `_satellite.logger.debug()` | `console.debug()` | Diagnóstico detalhado; alguns navegadores podem exigir registro detalhado para visualizá-lo. |
| `_satellite.logger.log()` | `console.log()` | Mensagens gerais. |
| `_satellite.logger.info()` | `console.info()` | Eventos informativos de alto nível. |
| `_satellite.logger.warn()` | `console.warn()` | Problemas recuperáveis. A entrada do console está realçada em amarelo. |
| `_satellite.logger.error()` | `console.error()` | Falhas. A entrada do console é realçada em vermelho. A Adobe recomenda usar objetos `error` para pilhas. |

```js
// First enable debugging mode
_satellite.setDebug(true);

// Logs a debug message
_satellite.logger.debug('Verbose diagnostic event');

// Logs a generic message
_satellite.logger.log('Example');

// Logs an informational message with mixed arguments
_satellite.logger.info('Rule triggered', 42, { ruleId: 'R123' }, ['a', 'b']);

// Logs a warning message
_satellite.logger.warn('Data element does not contain a value');

// Logs an error message with stack
_satellite.logger.error(new Error('Required extension not found'));
```

## Saída do console

A biblioteca anexa o seguinte a todas as mensagens de saída do console:

* **🚀**: Ajuda a detectar facilmente quais mensagens de console se originam da implementação de tags.
* **\[Origem\]**: o nome da regra, ação, extensão ou elemento de dados de onde o log se originou. Se você chamar um método de agente de log fora de sua implementação (por exemplo, por meio do console do navegador), `[Custom Script]` será usado.
* **Saída de mensagem**: a saída de mensagem incluída ao invocar o método.

>[!NOTE]
>
>Os tokens de formatação do navegador como `%c`, `%s` e `%d` não são aplicados devido ao agente de log aplicar o prefixo `🚀 [Origin]`.
