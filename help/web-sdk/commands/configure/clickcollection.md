---
title: clickCollection
description: Ajuste as configurações da coleção de cliques.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---


# `clickCollection`

A variável `clickCollection` O objeto contém várias variáveis que ajudam você a controlar os dados de link coletados automaticamente. Use essas variáveis quando quiser incluir ou excluir tipos de links da coleção de dados.

Exige [`clickCollectionEnabled`](clickcollectionenabled.md) para ser ativado.

Ele é compatível com o SDK da Web 2.25.0 ou posterior.

As seguintes variáveis estão disponíveis no `clickCollection` objeto:

* **`clickCollection.internalLinkEnabled`**: um booleano que determina se os links no domínio atual são rastreados automaticamente. Por exemplo, `https://example.com/index.html` para `https://example.com/product.html`.
* **`clickCollection.downloadLinkEnabled`**: um booliano que determina se a biblioteca rastreia links que se qualificam como downloads com base no [`downloadLinkQualifier`](downloadlinkqualifier.md) propriedade.
* **`clickCollection.externalLinkEnabled`**: um booleano que determina se os links para domínios externos são rastreados automaticamente. Por exemplo, `https://example.com` para `https://example.net`.
* **`clickCollection.eventGroupingEnabled`**: um booliano que determina se a biblioteca aguarda até a próxima página para enviar dados de rastreamento de link. Quando a próxima página for carregada, combine os dados de rastreamento de link com o evento de carregamento de página. Ativar essa opção reduz o número de eventos enviados para o Adobe. Se `internalLinkEnabled` estiver desativada, essa variável não fará nada.
* **`clickCollection.sessionStorageEnabled`**: um booleano que determina se os dados de rastreamento de link são armazenados no armazenamento da sessão, em vez de em variáveis locais. Se `internalLinkEnabled` ou `eventGroupingEnabled` estiverem desativados, essa variável não fará nada.

  O Adobe recomenda que essa variável seja ativada ao usar `eventGroupingEnabled`. Se `eventGroupingEnabled` está ativado enquanto `sessionStorageEnabled` estiver desativado, clicar em para uma nova página resultará na perda dos dados de rastreamento do link, pois não será preservado no armazenamento da sessão. Embora seja aceitável desativar o `sessionStorageEnabled` em aplicativos de página única, não é ideal para páginas que não sejam SPA.
* **`filterClickDetails`**: uma função de retorno de chamada que fornece controles completos sobre os dados de rastreamento de link coletados. Você pode usar essa função de retorno de chamada para alterar, ofuscar ou abortar o envio de dados de rastreamento de link. Essa chamada de retorno é útil quando você deseja omitir informações específicas, como informações de identificação pessoal em links.

## Clique nas configurações da coleção usando a extensão de tag do SDK da Web

Selecione o **[!UICONTROL Ativar a coleta de dados de cliques]** quando [configuração da extensão de tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Habilitar essa caixa de seleção revela as seguintes opções relacionadas à coleção de cliques:

* [!UICONTROL Links internos]
   * [!UICONTROL Ativar agrupamento de eventos]
   * [!UICONTROL Habilitar armazenamento de sessão]
* [!UICONTROL Links externos]
* [!UICONTROL Links de download]
* [!UICONTROL Propriedades de clique de filtro]

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e, em seguida, clique em **[!UICONTROL Configurar]** no [!UICONTROL Adobe Experience Platform Web SDK] cartão.
1. Role para baixo até [!UICONTROL Coleta de dados] e marque a caixa de seleção **[!UICONTROL Ativar a coleta de dados de cliques]**.
1. Selecione as configurações da coleção de cliques desejadas.
1. Clique em **[!UICONTROL Salvar]** e, em seguida, publique as alterações.

A variável [!UICONTROL Propriedades de clique de filtro] o retorno de chamada abre um editor de código personalizado que permite inserir o código desejado. No editor de código, você tem acesso às seguintes variáveis:

* **`content.clickedElement`**: o elemento DOM que foi clicado.
* **`content.pageName`**: o nome da página quando o clique aconteceu.
* **`content.linkName`**: o nome do link clicado.
* **`content.linkRegion`**: a região do link clicado.
* **`content.linkType`**: o tipo de link (saída, download ou outro).
* **`content.linkURL`**: o URL de destino do link clicado.
* **`return true`**: sai imediatamente do retorno de chamada com os valores de variável atuais.
* **`return false`**: saia imediatamente do retorno de chamada e cancele a coleta de dados.

Quaisquer variáveis definidas fora do `content` podem ser usados, mas não estão incluídos na carga útil enviada para o Adobe.

## Clique nas configurações da coleção usando a biblioteca JavaScript do SDK da Web

Defina as variáveis desejadas no `clickCollection` ao executar o [`configure`](overview.md) comando. Se não estiver definido, as configurações padrão para este objeto dependerão do valor de [`clickCollectionEnabled`](clickcollectionenabled.md).

* `internalLinkEnabled`: Corresponde `clickCollectionEnabled`
* `downloadLinkEnabled`: Corresponde `clickCollectionEnabled`
* `externalLinkEnabled`: Corresponde `clickCollectionEnabled`
* `eventGroupingEnabled`: O padrão é `false`; deve ser habilitado explicitamente
* `sessionStorageEnabled`: O padrão é `false`; deve ser habilitado explicitamente
* `filterClickDetails`: não contém uma função; deve ser explicitamente registrado

>[!TIP]
>O Adobe recomenda ativar `eventGroupingEnabled`, pois ajuda a reduzir o número de eventos que contam para o uso contratual.

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
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
