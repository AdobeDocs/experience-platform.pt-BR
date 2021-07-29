---
title: Depuração no SDK da Web da Adobe Experience Platform
description: Saiba como alternar recursos de depuração no SDK da Web do Experience Platform.
keywords: depurar o sdk da web, depurar, configurar, comando configurar, comando depurar, edgeConfigId, setDebug, debugEnabled, depurar;
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# Depuração

Quando a depuração está ativada, o SDK gera mensagens para o console do navegador que podem ser úteis na depuração da implementação e na compreensão de como o SDK está se comportando. A depuração também resulta em uma validação síncrona do lado do servidor dos dados coletados com o esquema configurado.

A depuração é desativada por padrão, mas pode ser ativada de três maneiras diferentes:

* `configure` comando
* `setDebug` comando
* parâmetro da string de consulta

## Alternar a depuração com o comando Configurar

Ao configurar o SDK usando o comando `configure`, ative a depuração definindo a opção `debugEnabled` como `true`.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!TIP]
>
>Isso permite a depuração de todos os usuários da página da Web, em vez de somente seu navegador pessoal.

## Alternar a depuração com o comando Depurar

Alterne a depuração com um comando `debug` separado da seguinte maneira:

```javascript
alloy("setDebug", {
  "enabled": true
});
```

Se preferir não alterar o código na sua página da Web ou não quiser que as mensagens de registro sejam produzidas para todos os usuários do seu site, isso é particularmente útil, pois você pode executar o comando `debug` no console JavaScript do seu navegador a qualquer momento.

## Alternar a depuração com um parâmetro da string de consulta

Alterne a depuração definindo um parâmetro da sequência de consulta `alloy_debug` para `true` ou `false` da seguinte maneira:

```HTTP
http://example.com/?alloy_debug=true
```

Semelhante ao comando `debug` , se você preferir não alterar o código na sua página da Web ou não quiser que as mensagens de registro sejam produzidas para todos os usuários do seu site, isso é particularmente útil, pois você pode definir o parâmetro da cadeia de caracteres de consulta ao carregar a página da Web em seu navegador.

## Prioridade e duração

Quando a depuração é definida pelo comando `debug` ou parâmetro da string de consulta, ela substitui qualquer opção `debug` definida no comando `configure`. Nesses dois casos, a depuração também permanece ativada durante a sessão. Em outras palavras, se você ativar a depuração usando o comando debug ou parâmetro da string de consulta, ela permanecerá ativada até um dos seguintes:

* O fim da sessão
* Execute o comando `debug`
* Você define o parâmetro da string de consulta novamente

## Recuperando informações da biblioteca

Geralmente, é útil acessar alguns dos detalhes por trás da biblioteca que você carregou em seu site. Para fazer isso, execute o comando `getLibraryInfo` da seguinte maneira:

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
});
```

Atualmente, o objeto `libraryInfo` fornecido contém as seguintes propriedades:

* `version` Esta é a versão da biblioteca carregada. Por exemplo, se a versão da biblioteca que está sendo carregada fosse 1.0.0, o valor seria `1.0.0`. Quando a biblioteca é executada dentro da extensão da tag (chamada de &quot;AEP Web SDK&quot;), a versão é a versão da biblioteca e a versão da extensão da tag é unida com um sinal &quot;+&quot;. Por exemplo, se a versão da biblioteca fosse 1.0.0 e a versão da extensão de tag fosse 1.2.0, o valor seria `1.0.0+1.2.0`.
