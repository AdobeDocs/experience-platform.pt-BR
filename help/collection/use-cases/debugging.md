---
title: Métodos de depuração
description: Saiba como alternar recursos de depuração no Web SDK.
keywords: depurando sdk da web;depurando;comando de depuração;setDebug;debugEnabled;depurar
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: aea46e3804d315c1237fc853540771f1b5c2b767
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Métodos de depuração

Quando a depuração está ativada, o Web SDK envia mensagens para o console do navegador que podem ser úteis na depuração da implementação. Ela também permite ver mensagens de [`_satellite.logger`](../tags/logger.md) se você usar marcas como método de implementação. A depuração é importante quando você deseja entender como o SDK se comporta de acordo com as regras e os elementos de dados estabelecidos.

A depuração está desativada por padrão, mas pode ser ativada de quatro maneiras diferentes. Você pode usar qualquer combinação desses métodos para ativar ou desativar a depuração mais conveniente para o fluxo de trabalho de desenvolvimento.

## Usar `debugEnabled` no comando `configure`

Defina o booleano `debugEnabled` como verdadeiro ao configurar a extensão. Normalmente, essa opção é usada para ambientes de desenvolvimento, pois permite a depuração para todos que visitam qualquer página do site:

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  debugEnabled: true
});
```

Consulte [`debugEnabled`](../js/commands/configure/debugenabled.md) para obter mais informações.

## Usar o comando `setDebug`

De modo semelhante ao booleano acima, esse comando permite a depuração em todos os visitantes da página.

```js
alloy("setDebug", {"enabled": true});
```

Consulte o comando [`setDebug`](../js/commands/setdebug.md) para obter mais informações.

## Definir um parâmetro da cadeia de caracteres de consulta

Você pode habilitar a depuração adicionando a cadeia de consulta `?alloy_debug=true` ao final de qualquer URL. Por exemplo:

`http://example.com/?alloy_debug=true`

Esse método se aplica somente ao computador local, permitindo depurar sites de produção sem ativar a depuração para todos. Habilitar a depuração dessa maneira permanece ativo durante o restante da sessão de navegação ou até que você a desabilite.

## Usar o Adobe Experience Platform Debugger

O Adobe Experience Platform Debugger é uma ferramenta poderosa que examina as páginas da Web e ajuda a depurar a implementação dos produtos da Experience Cloud. Você pode ativar a depuração na guia de configuração da seção AEP Web SDK.

![Habilitar depurador](../js/assets/enable-debugging.png)

Consulte [visão geral do Adobe Experience Platform Debugger](/help/debugger/home.md) para obter mais informações.
