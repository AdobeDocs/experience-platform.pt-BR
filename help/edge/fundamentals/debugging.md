---
title: Depuração
seo-title: Depuração do SDK da Web da Adobe Experience Platform
description: Saiba como alternar a depuração do SDK da Web da Experience Platform
seo-description: Saiba como alternar a depuração do SDK da Web da Experience Platform
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# Depuração (Beta)

>[!IMPORTANT]
>
>O SDK da Web da plataforma Adobe Experience está atualmente em beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

Quando a depuração está ativada, o SDK gera mensagens para o console do navegador que podem ser úteis na depuração da sua implementação e na compreensão de como o SDK está se comportando. A depuração também resulta em uma validação síncrona do lado do servidor dos dados que estão sendo coletados em relação ao esquema configurado.

A depuração está desativada por padrão, mas pode ser alternada de três maneiras diferentes:

* `configure` comando
* `debug` comando
* parâmetro da string de consulta

## Alternar a depuração com o comando Configurar

Ao configurar o SDK usando o `configure` comando, ative a depuração definindo a opção `debugEnabled` como `true`.

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!Hint]
>Isso permite a depuração para todos os usuários da página da Web, em vez de somente para seu navegador pessoal.

## Alternar a depuração com o comando Depurar

Alterne a depuração com um `debug` comando separado da seguinte maneira:

```javascript
alloy("debug", {
  "enabled": true
});
```

Se você preferir não alterar o código na sua página da Web ou não quiser que as mensagens de registro sejam produzidas para todos os usuários do seu site, isso é particularmente útil, pois você pode executar o `debug` comando no console JavaScript do seu navegador a qualquer momento.

## Alternar a depuração com um parâmetro da string de consulta

Alterne a depuração definindo um parâmetro de string de `alloy_debug` consulta para `true` ou `false` como segue:

```HTTP
http://example.com/?alloy_debug=true
```

Semelhante ao `debug` comando, se você preferir não alterar o código em sua página da Web ou não quiser que as mensagens de registro sejam produzidas para todos os usuários do seu site, isso é particularmente útil, pois você pode definir o parâmetro da string de consulta ao carregar a página da Web dentro do navegador.

## Prioridade e duração

Quando a depuração é definida pelo parâmetro da string de consulta ou `debug` comando, ela substitui qualquer `debug` opção definida no `configure` comando. Nesses dois casos, a depuração também permanece alternada durante a sessão. Em outras palavras, se você ativar a depuração usando o comando debug ou o parâmetro da string de consulta, ela permanecerá ativada até um dos seguintes:

* O fim da sessão
* Execute o `debug` comando
* Você define o parâmetro da string de consulta novamente
