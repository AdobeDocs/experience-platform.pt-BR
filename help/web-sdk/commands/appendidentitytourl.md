---
title: appendIdentityToUrl
description: Ofereça experiências personalizadas com mais precisão entre aplicativos, Web e domínios.
exl-id: 09dd03bd-66d8-4d53-bda8-84fc4caadea6
source-git-commit: 153c5bae42c027c25a38a8b63070249d1b1a8f01
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# `appendIdentityToUrl`

O comando `appendIdentityToUrl` permite adicionar um identificador de usuário à URL como uma cadeia de caracteres de consulta. Essa ação permite que você carregue a identidade de um visitante entre domínios, evitando contagens de visitantes duplicadas para conjuntos de dados que incluem domínios ou canais. Ele está disponível nas versões 2.11.0 ou posteriores do SDK da Web.

A cadeia de consulta gerada e anexada à URL é `adobe_mc`. Se o SDK da Web não puder encontrar uma ECID, ele chamará o ponto de extremidade `/acquire` para gerar uma.

>[!NOTE]
>
>Se o consentimento não tiver sido fornecido, o URL desse método será retornado inalterado. Este comando é executado imediatamente; ele não espera por uma atualização de consentimento.

## Anexar identidade ao URL usando a extensão SDK da Web {#extension}

Anexar uma identidade a um URL é executado como uma ação em uma regra na interface das tags da Coleção de dados da Adobe Experience Platform.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Regras]** e selecione a regra desejada.
1. Em [!UICONTROL Ações], selecione uma ação existente ou crie uma ação.
1. Defina o campo suspenso [!UICONTROL Extensão] como **[!UICONTROL Adobe Experience Platform Web SDK]** e defina o [!UICONTROL Tipo de Ação] como **[!UICONTROL Redirecionar com identidade]**.
1. Clique em **[!UICONTROL Manter alterações]** e execute o fluxo de trabalho de publicação.

Normalmente, esse comando é usado com uma regra específica que ouve cliques e verifica domínios desejados.

+++Critérios de evento da regra

Acionado quando um tag de âncora com uma propriedade `href` é clicado.

* **[!UICONTROL Extensão]**: principal
* **[!UICONTROL Tipo de evento]**: clique
* **[!UICONTROL Quando o usuário clicar em]**: elementos específicos
* **[!UICONTROL Elementos correspondentes ao seletor de CSS]**: `a[href]`

![Evento de regra](../assets/id-sharing-event-configuration.png)

+++

Condição +++Regra

Aciona somente nos domínios desejados.

* **[!UICONTROL Tipo lógico]**: regular
* **[!UICONTROL Extensão]**: principal
* **[!UICONTROL Tipo de Condição]**: Comparação de Valores
* **[!UICONTROL Operando Esquerdo]**: `%this.hostname%`
* **[!UICONTROL Operador]**: Corresponde a Regex
* **[!UICONTROL Operando Direito]**: uma expressão regular que corresponde aos domínios desejados. Por exemplo, `adobe.com$|behance.com$`

![Condição de regra](../assets/id-sharing-condition-configuration.png)

+++

Ação +++Regra

Anexe a identidade ao URL.

* **[!UICONTROL Extensão]**: Adobe Experience Platform Web SDK
* **[!UICONTROL Tipo de ação]**: redirecionar com identidade

![Ação da regra](../assets/id-sharing-action-configuration.png)

+++

## Anexar identidade ao URL usando a biblioteca JavaScript do SDK da Web

Execute o comando `appendIdentityToUrl` com uma URL como parâmetro. O método retorna um URL com o identificador anexado como uma string de consulta.

```js
alloy("appendIdentityToUrl",document.location);
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
  alloy("appendIdentityToUrl", {url: anchor.href}).then(result => {document.location = result.url;});
});
```

## Objeto de resposta

Se você decidir [manipular respostas](command-responses.md) com este comando, o objeto de resposta conterá **`url`**, a nova URL com informações de identidade adicionada como parâmetro de sequência de consulta.
