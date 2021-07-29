---
title: Rastrear eventos usando o SDK da Web da Adobe Experience Platform
description: Saiba como rastrear eventos do SDK da Web da Adobe Experience Platform.
keywords: sendEvent; xdm; eventType; datasetId; sendBeacon; send Beacon; documentUnloading; document Unloading; onBeforeEventSend;
exl-id: 8b221cae-3490-44cb-af06-85be4f8d280a
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1451'
ht-degree: 0%

---

# Rastrear eventos

Para enviar dados do evento para o Adobe Experience Cloud, use o comando `sendEvent`. O comando `sendEvent` é a maneira principal de enviar dados para o [!DNL Experience Cloud] e recuperar conteúdo personalizado, identidades e destinos de público-alvo.

Os dados enviados para o Adobe Experience Cloud são divididos em duas categorias:

* Dados XDM
* Dados não XDM

## Envio de dados XDM

Os dados XDM são um objeto cujo conteúdo e estrutura correspondem a um esquema criado no Adobe Experience Platform. [Saiba mais sobre como criar um schema.](../../xdm/tutorials/create-schema-ui.md)

Quaisquer dados XDM que você deseja que façam parte de sua análise, personalização, públicos-alvo ou destinos devem ser enviados usando a opção `xdm`.


```javascript
alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

Pode passar algum tempo entre a execução do comando `sendEvent` e o envio dos dados para o servidor (por exemplo, se a biblioteca do SDK da Web não tiver sido totalmente carregada ou o consentimento ainda não tiver sido recebido). Se você pretende modificar qualquer parte do objeto `xdm` após executar o comando `sendEvent`, é altamente recomendável clonar o objeto `xdm` _antes de_ executar o comando `sendEvent`. Por exemplo:

```javascript
var clone = function(value) {
  return JSON.parse(JSON.stringify(value));
};

var dataLayer = {
  "commerce": {
    "order": {
      "purchaseID": "a8g784hjq1mnp3",
      "purchaseOrderNumber": "VAU3123",
      "currencyCode": "USD",
      "priceTotal": 999.98
    }
  }
};

alloy("sendEvent", {
  "xdm": clone(dataLayer)
});

// This change will not be reflected in the data sent to the 
// server for the prior sendEvent command.
dataLayer.commerce = null;
```

Neste exemplo, a camada de dados é clonada serializando-a para JSON e depois desserializando-a. Em seguida, o resultado clonado é transmitido ao comando `sendEvent`. Isso garante que o comando `sendEvent` tenha um instantâneo da camada de dados como existia quando o comando `sendEvent` foi executado, de modo que modificações posteriores no objeto da camada de dados original não sejam refletidas nos dados enviados para o servidor. Se você estiver usando uma camada de dados orientada por eventos, a clonagem de seus dados provavelmente já será manipulada automaticamente. Por exemplo, se estiver usando a [Camada de dados do cliente do Adobe](https://github.com/adobe/adobe-client-data-layer/wiki), o método `getState()` fornecerá um instantâneo computado e clonado de todas as alterações anteriores. Isso também é feito para você automaticamente se estiver usando a extensão de tag Adobe Experience Platform Web SDK.

>[!NOTE]
>
>Há um limite de 32 KB nos dados que podem ser enviados em cada evento no campo XDM.


## Envio de dados não XDM

Os dados que não correspondem a um esquema XDM devem ser enviados usando a opção `data` do comando `sendEvent`. Esse recurso é compatível com versões 2.5.0 e posteriores do SDK da Web.

Isso é útil se você precisar atualizar um perfil do Adobe Target ou enviar atributos do Recommendations do Target. [Leia mais sobre esses recursos do Target.](../personalization/adobe-target/target-overview.md#single-profile-update)

No futuro, você poderá enviar a camada de dados completa sob a opção `data` e mapeá-la para o lado do servidor XDM.

**Como enviar atributos do Perfil e do Recommendations para o Adobe Target:**

```javascript
alloy("sendEvent", {
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30,
        "entity.id" : "123",
        "entity.genre" : "Drama"
      }
    }
  }
});
```


### Configuração `eventType` {#event-types}

Em um evento de experiência XDM, há um campo opcional `eventType`. Isso mantém o tipo de evento principal para o registro. Definir um tipo de evento pode ajudar você a diferenciar os diferentes eventos que serão enviados. O XDM fornece vários tipos de evento predefinidos que podem ser usados ou você sempre cria seus próprios tipos de evento personalizados para seus casos de uso. Abaixo está uma lista de todos os tipos de evento predefinidos fornecidos pelo XDM. [Leia mais no repositório público XDM](https://github.com/adobe/xdm/blob/master/docs/reference/behaviors/time-series.schema.md#xdmeventtype-known-values).


| **Tipo de evento:** | **Definição:** |
| ---------------------------------- | ------------ |
| advertising.completes | Indica se um ativo de mídia cronometrado foi observado até o fim - não significa necessariamente que o visualizador assistiu a todo o vídeo; o visualizador poderia ter ignorado com antecedência |
| advertising.timePlayed | Descreve o tempo gasto por um usuário em um ativo de mídia programado específico |
| advertising.federated | Indica se um evento de experiência foi criado por meio da federação de dados (compartilhamento de dados entre clientes) |
| advertising.clicks | Ações de clique em um anúncio |
| advertising.conversions | Uma(s) ação(ões) predefinida(s) do cliente que aciona um evento para avaliação de desempenho |
| advertising.firstQuartiles | Um anúncio de vídeo digital foi reproduzido por 25% de sua duração em velocidade normal |
| advertising.impressions | Impressão(ões) de um anúncio para um usuário final com o potencial de ser visualizado |
| advertising.midpoints | Um anúncio de vídeo digital foi reproduzido por 50% de sua duração em velocidade normal |
| advertising.starts | Um anúncio de vídeo digital começou a ser reproduzido |
| advertising.thirdQuartiles | Um anúncio de vídeo digital foi reproduzido por 75% de sua duração em velocidade normal |
| web.webpagedetails.pageViews | Ocorreram exibições de uma página da Web |
| web.webinteraction.linkClicks | Ocorreu um clique de um link da Web |
| commerce.checkouts | Uma ação durante um processo de finalização de uma lista de produtos, pode haver mais de um evento de finalização se houver várias etapas em um processo de finalização. Se houver várias etapas, as informações de tempo do evento e a página ou experiência referenciada serão usadas para identificar a etapa que os eventos individuais representam em ordem |
| commerce.productListAdds | Adição de um produto à lista de produtos. Exemplo: um produto é adicionado ao carrinho de compras |
| commerce.productListOpens | Inicializações de uma nova lista de produtos. Exemplo de criação de um carrinho de compras |
| commerce.productListRemovals | Remoção(ões) de uma entrada de produto de uma lista de produtos. Exemplo: um produto é removido de um carrinho de compras |
| commerce.productListReopens | Uma lista de produtos que não estava mais acessível (abandonada) foi reativada pelo usuário. Exemplo por meio de uma atividade de re-marketing |
| commerce.productListViews | Ocorreu a(s) exibição(s) de uma lista de produtos |
| commerce.productViews | Ocorreram exibições de um produto |
| commerce.purchases | Um pedido foi aceito. A compra é a única ação necessária em uma conversão de comércio. A compra deve ter uma lista de produtos referenciada |
| commerce.saveForLaters | A lista de produtos é salva para uso futuro. Exemplo de uma lista de desejos de produto |
| delivery.feedback | Eventos de feedback para um delivery. Exemplo de eventos de feedback para um delivery de email |


Esses tipos de evento serão mostrados em uma lista suspensa se você estiver usando a extensão de tag ou sempre puder transmiti-los sem tags. Eles podem ser transmitidos como parte da opção `xdm` .


```javascript
alloy("sendEvent", {
  "xdm": {
    "eventType": "commerce.purchases",
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

Como alternativa, o `eventType` pode ser passado para o comando event usando a opção `type`. Em segundo plano, isso é adicionado aos dados XDM. Ter o `type` como uma opção permite definir mais facilmente o `eventType` sem precisar modificar a carga do XDM.


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### Substituição da ID do conjunto de dados

Em alguns casos de uso, você pode enviar um evento para um conjunto de dados diferente daquele configurado na interface do usuário de configuração. Para isso, é necessário definir a opção `datasetId` no comando `sendEvent`:


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### Adição de informações de identidade

As informações de identidade personalizadas também podem ser adicionadas ao evento. Consulte [Recuperando Experience Cloud ID](../identity/overview.md).

## Uso da API sendBeacon

Pode ser complicado enviar dados de evento antes que o usuário da página da Web tenha saído. Se a solicitação demorar muito, o navegador pode cancelar a solicitação. Alguns navegadores implementaram uma API padrão da Web chamada `sendBeacon` para permitir que os dados sejam coletados com mais facilidade durante esse período. Ao usar `sendBeacon`, o navegador faz a solicitação da Web no contexto de navegação global. Isso significa que o navegador faz a solicitação de beacon em segundo plano e não segura a navegação da página. Para dizer ao Adobe Experience Platform [!DNL Web SDK] para usar `sendBeacon`, adicione a opção `"documentUnloading": true` ao comando event.  Exemplo:


```javascript
alloy("sendEvent", {
  "documentUnloading": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

Os navegadores impuseram limites para a quantidade de dados que pode ser enviada com `sendBeacon` de uma vez. Em muitos navegadores, o limite é de 64 K. Se o navegador rejeitar o evento porque a carga é muito grande, o Adobe Experience Platform [!DNL Web SDK] voltará a usar seu método de transporte normal (por exemplo, busca).

## Lidar com respostas de eventos

Se quiser lidar com uma resposta de um evento, você poderá ser notificado de um sucesso ou falha da seguinte maneira:


```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(results) {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

## Modificação global de eventos {#modifying-events-globally}

Se quiser adicionar, remover ou modificar campos do evento globalmente, você pode configurar um retorno de chamada `onBeforeEventSend`.  Esse retorno de chamada é chamado sempre que um evento é enviado.  Esse retorno de chamada é passado em um objeto de evento com um campo `xdm`.  Modifique `content.xdm` para alterar os dados enviados com o evento.


```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(content) {
    // Change existing values
    content.xdm.web.webPageDetails.URL = xdm.web.webPageDetails.URL.toLowerCase();
    // Remove existing values
    delete content.xdm.web.webReferrer.URL;
    // Or add new values
    content.xdm._adb3lettersandnumbers.mycustomkey = "value";
  }
});
```

`xdm` são definidos nesta ordem:

1. Valores passados como opções para o comando de evento `alloy("sendEvent", { xdm: ... });`
2. Valores coletados automaticamente.  (Consulte [Informações Automáticas](../data-collection/automatic-information.md).)
3. As alterações feitas no retorno de chamada `onBeforeEventSend`.

Algumas observações sobre o retorno de chamada `onBeforeEventSend`:

* O XDM do evento pode ser modificado durante o retorno de chamada. Depois que a chamada de retorno for retornada, todos os campos e valores modificados de
os objetos content.xdm e content.data são enviados com o evento .

   ```javascript
   onBeforeEventSend: function(content){
     //sets a query parameter in XDM
     const queryString = window.location.search;
     const urlParams = new URLSearchParams(queryString);
     content.xdm.marketing.trackingCode = urlParams.get('cid')
   }
   ```

* Se o retorno de chamada gerar uma exceção, o processamento do evento será interrompido e o evento não será enviado.
* Se o retorno de chamada retornar o valor booleano de `false`, o processamento de evento será interrompido,
sem um erro e o evento não é enviado. Esse mecanismo permite que determinados eventos sejam facilmente ignorados por
examinando os dados do evento e retornando `false` se o evento não deve ser enviado.

   >[!NOTE]
   >Deve-se tomar cuidado para evitar retornar &quot;false&quot; no primeiro evento em uma página. Retornar false no primeiro evento pode afetar negativamente a personalização.

```javascript
   onBeforeEventSend: function(content) {
     // ignores events from bots
     if (MyBotDetector.isABot()) {
       return false;
     }
   }
```

Qualquer valor de retorno diferente do booleano `false` permitirá que o evento processe e envie após o retorno de chamada.

* Os eventos podem ser filtrados examinando o tipo de evento (Consulte [Tipos de evento](#event-types).):

```javascript
    onBeforeEventSend: function(content) {  
      // augments XDM if link click event is to a partner website
      if (
        content.xdm.eventType === "web.webinteraction.linkClicks" &&
        content.xdm.web.webInteraction.URL ===
          "http://example.com/partner-page.html"
      ) {
        content.xdm.partnerWebsiteClick = true;
      }
   }
```

## Possíveis erros acionáveis

Ao enviar um evento, um erro pode ser lançado se os dados que estão sendo enviados forem muito grandes (mais de 32 KB para a solicitação completa). Nesse caso, é necessário reduzir a quantidade de dados que estão sendo enviados.
