---
title: clickCollection
description: Ajuste as configurações da coleção de cliques.
exl-id: 5a128b4a-4727-4415-87b4-4ae87a7e1750
source-git-commit: 46c8748e9ab972705b8283c174c285e571acb2ed
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# `clickCollection`

O objeto `clickCollection` contém várias variáveis que ajudam você a controlar os dados de link coletados automaticamente. Use essas variáveis quando quiser incluir ou excluir tipos de links da coleção de dados. Ele é compatível com o Web SDK versões 2.25.0 ou posteriores.

Essa variável exige todos os itens a seguir:

* [`clickCollectionEnabled`](clickcollectionenabled.md) deve ser habilitado.
* Se você usar `clickCollection.filterClickDetails`, o método obsoleto [`onBeforeLinkClickSend`](onbeforelinkclicksend.md) deverá estar vazio.
* A carga do evento deve conter um valor em `xdm.web.webPageDetails.name` em algum momento da visita do visitante.

Se sua implementação não atender a todos os requisitos acima, esse objeto não fará nada.

As seguintes propriedades estão disponíveis no objeto `clickCollection`:

| Propriedade | Tipo | Descrição |
| --- | --- | --- |
| **`internalLinkEnabled`** | `boolean` | Determina se os links no domínio atual são rastreados automaticamente. Por exemplo, de `https://example.com/index.html` a `https://example.com/product.html` seria considerado um link interno. |
| **`downloadLinkEnabled`** | `boolean` | Determina se a biblioteca rastreia links qualificados como downloads com base na propriedade [`downloadLinkQualifier`](downloadlinkqualifier.md). |
| **`externalLinkEnabled`** | `boolean` | Determina se os links para domínios externos são rastreados automaticamente. Por exemplo, de `https://example.com` a `https://example.net` seria considerado um link externo. |
| **`eventGroupingEnabled`** | `boolean` | Determina se a biblioteca aguarda até o próximo evento &quot;Exibição de página&quot; para enviar dados de rastreamento de link. A biblioteca considera um evento uma &quot;visualização de página&quot; quando os seguintes elementos são incluídos na carga:<ul><li>`xdm.web.webPageDetails.name` contém um valor de cadeia de caracteres</li><li>`xdm.web.webPageDetails.pageViews.value` é maior que `0`</li></ul>Quando o evento &quot;exibição de página&quot; é carregado, a biblioteca combina os dados de rastreamento de link armazenados com o restante dos dados nesse evento. Ativar essa opção reduz o número total de eventos enviados para o Adobe. Se `internalLinkEnabled` estiver desabilitado, essa variável não fará nada. |
| **`sessionStorageEnabled`** | `boolean` | Determina se os dados de rastreamento de link são armazenados no armazenamento da sessão em vez de em variáveis locais. Se `internalLinkEnabled` ou `eventGroupingEnabled` estiverem desabilitados, essa variável não fará nada.<br>A Adobe recomenda habilitar essa variável ao usar `eventGroupingEnabled` fora dos aplicativos de página única. Se `eventGroupingEnabled` estiver habilitado enquanto `sessionStorageEnabled` estiver desabilitado, clicar em uma nova página resultará na perda de dados de rastreamento de link, pois não será preservado no armazenamento da sessão. Como os aplicativos de página única normalmente não navegam para uma nova página, o armazenamento de sessão não é necessário para páginas de SPA. |
| **`filterClickDetails`** | `function` | Uma função de retorno de chamada que fornece controles completos sobre os dados de rastreamento de link coletados. Você pode usar essa função de retorno de chamada para alterar, ofuscar ou abortar o envio de dados de rastreamento de link. Essa chamada de retorno é útil quando você deseja omitir informações específicas, como informações de identificação pessoal em links. |

Se você não definir este objeto no comando [`configure`](overview.md), as configurações padrão para este objeto dependerão do valor de [`clickCollectionEnabled`](clickcollectionenabled.md):

* `internalLinkEnabled`: Corresponde a `clickCollectionEnabled`
* `downloadLinkEnabled`: Corresponde a `clickCollectionEnabled`
* `externalLinkEnabled`: Corresponde a `clickCollectionEnabled`
* `eventGroupingEnabled`: o padrão é `false`; deve ser habilitado explicitamente
* `sessionStorageEnabled`: o padrão é `false`; deve ser habilitado explicitamente
* `filterClickDetails`: Não contém uma função; deve ser explicitamente registrado

>[!TIP]
>
>A Adobe recomenda habilitar `eventGroupingEnabled` quando `internalLinkEnabled` estiver habilitado, pois isso reduz o número de eventos que contam para o uso contratual.

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

## Configurar a coleção de cliques para a extensão de tag do Web SDK

Essas configurações podem ser definidas na extensão de marca do Web SDK usando [as configurações da coleção de dados](/help/tags/extensions/client/web-sdk/configure/data-collection.md).
