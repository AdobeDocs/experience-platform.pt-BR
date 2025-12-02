---
title: appendIdentityToUrl
description: Ofereça experiências personalizadas com mais precisão entre aplicativos, Web e domínios.
exl-id: 09dd03bd-66d8-4d53-bda8-84fc4caadea6
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# `appendIdentityToUrl`

O comando `appendIdentityToUrl` permite adicionar um identificador de usuário à URL como uma cadeia de caracteres de consulta. Essa ação permite que você carregue a identidade de um visitante entre domínios, evitando contagens de visitantes duplicadas para conjuntos de dados que incluem domínios ou canais. Ele está disponível nas versões 2.11.0 ou posteriores do Web SDK.

A cadeia de consulta gerada e anexada à URL é `adobe_mc`. Se o Web SDK não puder encontrar uma ECID, ele chamará o ponto de extremidade `/acquire` para gerar uma.

>[!NOTE]
>
>Se o consentimento não tiver sido fornecido, o URL desse método será retornado inalterado. Este comando é executado imediatamente; ele não espera por uma atualização de consentimento.

Execute o comando `appendIdentityToUrl` com uma URL como parâmetro. O método retorna um URL com o identificador anexado como uma string de consulta.

```js
alloy("appendIdentityToUrl",
  {
    url: document.location.href
  }
);
```

Você pode adicionar um ouvinte de eventos para todos os cliques recebidos na página e verificar se o URL corresponde a algum domínio desejado. Se isso acontecer, anexe a identidade ao URL e redirecione o usuário.

```js
document.addEventListener("click", event => {
  // Check if the click was a link
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) return;

  // Check if the link points to the desired domain
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith(".adobe.com") && !url.hostname.endsWith(".behance.com")) return;

  // Append the identity to the URL, then direct the user to the URL
  event.preventDefault();
  alloy("appendIdentityToUrl", {url: anchor.href}).then(result => { window.open(result.url, anchor.target || "_self"); });
});
```

Este comando dá suporte ao objeto [`edgeConfigOverrides`](configure/edgeconfigoverrides.md).

## Objeto de resposta

Ao [manipular respostas](command-responses.md) com este comando, o objeto de resposta contém **`url`**, a nova URL com informações de identidade adicionada como parâmetro de cadeia de caracteres de consulta.

## Anexar identidade ao URL usando a extensão de tag do Web SDK

A extensão de marca do Web SDK equivalente a este comando é a ação [Redirecionar com identidade](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md).
