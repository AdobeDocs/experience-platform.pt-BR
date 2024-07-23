---
title: clickCollection
description: Ajuste as configurações da coleção de cliques.
exl-id: 5a128b4a-4727-4415-87b4-4ae87a7e1750
source-git-commit: d3be2a9e75514023a7732a1c3460f8695ef02e68
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# `clickCollection`

O objeto `clickCollection` contém várias variáveis que ajudam você a controlar os dados de link coletados automaticamente. Use essas variáveis quando quiser incluir ou excluir tipos de links da coleção de dados.

É necessário que [`clickCollectionEnabled`](clickcollectionenabled.md) esteja habilitado.

Ele é compatível com o SDK da Web 2.25.0 ou posterior.

As seguintes variáveis estão disponíveis no objeto `clickCollection`:

* **`clickCollection.internalLinkEnabled`**: um booleano que determina se os links no domínio atual são acompanhados automaticamente. Por exemplo, de `https://example.com/index.html` a `https://example.com/product.html`.
* **`clickCollection.downloadLinkEnabled`**: um booleano que determina se a biblioteca rastreia links que se qualificam como downloads com base na propriedade [`downloadLinkQualifier`](downloadlinkqualifier.md).
* **`clickCollection.externalLinkEnabled`**: um booleano que determina se os links para domínios externos são rastreados automaticamente. Por exemplo, de `https://example.com` a `https://example.net`.
* **`clickCollection.eventGroupingEnabled`**: um booliano que determina se a biblioteca aguarda até a próxima página para enviar dados de rastreamento de link. Quando a próxima página for carregada, combine os dados de rastreamento de link com o evento de carregamento de página. Ativar essa opção reduz o número de eventos enviados para o Adobe. Se `internalLinkEnabled` estiver desabilitado, essa variável não fará nada.
* **`clickCollection.sessionStorageEnabled`**: um booliano que determina se os dados de rastreamento de link são armazenados no armazenamento da sessão em vez de em variáveis locais. Se `internalLinkEnabled` ou `eventGroupingEnabled` estiverem desabilitados, essa variável não fará nada.

  A Adobe recomenda que essa variável seja ativada ao usar o `eventGroupingEnabled` fora dos aplicativos de página única. Se `eventGroupingEnabled` estiver habilitado enquanto `sessionStorageEnabled` estiver desabilitado, clicar em uma nova página resultará na perda de dados de rastreamento de link, pois não será preservado no armazenamento da sessão. Como os aplicativos de página única normalmente não navegam para uma nova página, o armazenamento de sessão não é necessário para páginas SPA.
* **`filterClickDetails`**: uma função de retorno de chamada que fornece controles completos sobre os dados de rastreamento de link coletados. Você pode usar essa função de retorno de chamada para alterar, ofuscar ou abortar o envio de dados de rastreamento de link. Essa chamada de retorno é útil quando você deseja omitir informações específicas, como informações de identificação pessoal em links.

## Clique nas configurações da coleção usando a extensão de tag do SDK da Web

Selecione qualquer uma das seguintes opções ao [configurar a extensão de marca](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md):

* [!UICONTROL Coletar links internos]
   * [!UICONTROL Opções de agrupamento de eventos]:
      * [!UICONTROL Nenhum agrupamento de eventos]
      * [!UICONTROL Agrupamento de eventos usando o armazenamento de sessão]
      * [!UICONTROL Agrupamento de eventos usando objeto local]
* [!UICONTROL Coletar links externos]
* [!UICONTROL Coletar links de download]
* [!UICONTROL Propriedades de clique do filtro]

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e clique em **[!UICONTROL Configurar]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Role para baixo até a seção [!UICONTROL Coleção de dados] e selecione as configurações de coleção de cliques desejadas.
1. Clique em **[!UICONTROL Salvar]** e publique suas alterações.

O retorno de chamada [!UICONTROL Propriedades de clique de filtro] abre um editor de código personalizado que permite inserir o código desejado. No editor de código, você tem acesso às seguintes variáveis:

* **`content.clickedElement`**: o elemento DOM que foi clicado.
* **`content.pageName`**: O nome da página quando o clique ocorreu.
* **`content.linkName`**: o nome do link clicado.
* **`content.linkRegion`**: A região do link clicado.
* **`content.linkType`**: O tipo de link (saída, download ou outro).
* **`content.linkURL`**: a URL de destino do link clicado.
* **`return true`**: Saia imediatamente do retorno de chamada com os valores de variável atuais.
* **`return false`**: Saia imediatamente do retorno de chamada e cancele a coleta de dados.

Qualquer variável definida fora de `content` pode ser usada, mas não está incluída na carga enviada para o Adobe.

## Clique nas configurações da coleção usando a biblioteca JavaScript do SDK da Web

Defina as variáveis desejadas no objeto `clickCollection` ao executar o comando [`configure`](overview.md). Se não for definido, as configurações padrão para este objeto dependerão do valor de [`clickCollectionEnabled`](clickcollectionenabled.md).

* `internalLinkEnabled`: Corresponde a `clickCollectionEnabled`
* `downloadLinkEnabled`: Corresponde a `clickCollectionEnabled`
* `externalLinkEnabled`: Corresponde a `clickCollectionEnabled`
* `eventGroupingEnabled`: o padrão é `false`; deve ser habilitado explicitamente
* `sessionStorageEnabled`: o padrão é `false`; deve ser habilitado explicitamente
* `filterClickDetails`: Não contém uma função; deve ser explicitamente registrado

>[!TIP]
>A Adobe recomenda habilitar `eventGroupingEnabled` quando `internalLinkEnabled` estiver habilitado, pois reduz o número de eventos que contam para o uso contratual.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  clickCollection: {
    internalLinkEnabled: true,
    downloadLinkEnabled: true,
    externalLinkEnabled: true,
    eventGroupingEnabled: true,
    sessionStorageEnabled: true,
    filterClickDetails: function(content) {
      // If the link is a clickable telephone number, anonymize it
      if(content.linkUrl?.includes("tel:")) {
        content.linkName = content.linkUrl = "Phone number";
      }
      // If the link is an email address, anonymize it
      if(content.linkUrl?.includes("mailto:")) {
        content.linkName = content.linkUrl = "Email address";
      }
    }
  }
});
```
