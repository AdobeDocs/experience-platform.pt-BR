---
title: Rastrear Eventos usando o Adobe Experience Platform Web SDK
seo-description: Saiba como rastrear eventos Adobe Experience Platform Web SDK.
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;send Beacon;documentUnloading;documento Unloading;onBeforeEventSend;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '1334'
ht-degree: 0%

---


# Rastrear eventos

Para enviar dados do evento para a Adobe Experience Cloud, use o comando `sendEvent`. O comando `sendEvent` é a principal maneira de enviar dados para [!DNL Experience Cloud] e recuperar conteúdo personalizado, identidades e destinos de audiência.

Os dados enviados à Adobe Experience Cloud são divididos em duas categorias:

* Dados XDM
* Dados não XDM (atualmente não suportados)

## Envio de dados XDM

Os dados XDM são um objeto cujo conteúdo e estrutura correspondem a um schema criado no Adobe Experience Platform. [Saiba mais sobre como criar um schema.](../../xdm/tutorials/create-schema-ui.md)

Todos os dados XDM que você deseja que façam parte de suas análises, personalização, audiências ou destinos devem ser enviados usando a opção `xdm`.


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

Pode passar algum tempo entre quando o comando `sendEvent` é executado e quando os dados são enviados para o servidor (por exemplo, se a biblioteca do SDK da Web não foi totalmente carregada ou o consentimento ainda não foi recebido). Se você pretende modificar qualquer parte do objeto `xdm` depois de executar o comando `sendEvent`, é altamente recomendável clonar o objeto `xdm` _antes de_ executar o comando `sendEvent`. Por exemplo:

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

Neste exemplo, a camada de dados é clonada serializando-a para JSON e, em seguida, desserializando-a. Em seguida, o resultado clonado é passado para o comando `sendEvent`. Isso garante que o comando `sendEvent` tenha um instantâneo da camada de dados como ela existia quando o comando `sendEvent` foi executado para que as modificações posteriores no objeto da camada de dados original não sejam refletidas nos dados enviados para o servidor. Se você estiver usando uma camada de dados orientada por evento, a clonagem dos dados provavelmente já será feita automaticamente. Por exemplo, se você estiver usando a [Camada de Dados do Cliente Adobe](https://github.com/adobe/adobe-client-data-layer/wiki), o método `getState()` fornecerá um instantâneo computado e clonado de todas as alterações anteriores. Isso também é feito para você automaticamente se você estiver usando a extensão AEP Web SDK Launch.

>[!NOTE]
>
>Há um limite de 32 KB nos dados que podem ser enviados em cada evento no campo XDM.

### Envio de dados não XDM

Atualmente, não há suporte para o envio de dados que não correspondem a um schema XDM. O suporte está planejado para uma data futura.

### Configuração `eventType`

Em um evento de experiência XDM, há um campo opcional `eventType`. Isso mantém o tipo de evento principal do registro. A configuração de um tipo de evento pode ajudá-lo a diferenciar entre os diferentes eventos que você enviará. O XDM fornece vários tipos de evento predefinidos que você pode usar ou você sempre cria seus próprios tipos de evento personalizados para seus casos de uso. Abaixo está uma lista de todos os tipos de evento predefinidos fornecidos pelo XDM. [Leia mais no acordo](https://github.com/adobe/xdm/blob/master/docs/reference/behaviors/time-series.schema.md#xdmeventtype-known-values) público XDM.


| **Tipo de evento:** | **Definição:** |
| ---------------------------------- | ------------ |
| advertising.completes | Indica se um ativo de mídia cronometrado foi observado até a conclusão - isso não significa necessariamente que o visualizador assistiu ao vídeo inteiro; o visualizador poderia ter ignorado na frente |
| advertising.timePlayed | Descreve a quantidade de tempo gasta por um usuário em um ativo de mídia cronometrado específico |
| advertising.federated | Indica se um evento de experiência foi criado por meio da federação de dados (compartilhamento de dados entre clientes) |
| advertising.clicks | Ações de clique em um anúncio |
| advertising.conversions | Uma ação(ões) predefinida(s) do cliente que aciona um evento para avaliação do desempenho |
| advertising.firstQuartiles | Um anúncio de vídeo digital tem uma duração de 25% em velocidade normal |
| advertising.impressions | Impressão(ões) de um anúncio para um usuário final com o potencial de ser visualizado |
| advertising.midpoints | Um anúncio de vídeo digital tem 50% de sua duração em velocidade normal |
| advertising.starts | Um anúncio de vídeo digital começou a ser reproduzido |
| advertising.thirdQuartiles | Um anúncio de vídeo digital tem uma duração de 75% em velocidade normal |
| web.webpagedetails.pageViews | Ocorreu(m) visualização(s) de uma página da Web |
| web.webinteraction.linkClicks | Ocorreu um clique de um link da Web |
| commerce.checkouts | Uma ação durante um processo de finalização de uma lista de produto, pode haver mais de um evento de finalização se houver várias etapas em um processo de finalização. Se houver várias etapas, as informações de hora do evento e a página ou experiência referenciada serão usadas para identificar a etapa representada pelos eventos individuais em ordem |
| commerce.productListAdds | Adição de um produto à lista do produto. Exemplo de um produto adicionado a um carrinho de compras |
| commerce.productListOpens | Inicializações de uma nova lista de produto. Exemplo de criação de um carrinho de compras |
| commerce.productListRemovals | Remoção(ões) de uma entrada de produto de uma lista de produto. Exemplo de um produto removido de um carrinho de compras |
| commerce.productListReopens | Uma lista de produto que não estava mais acessível (abandonada) foi reativada pelo usuário. Exemplo por meio de uma atividade de recomercialização |
| commerce.productListViews | Ocorreu(m) visualização(s) de uma lista de produto |
| commerce.productViews | Ocorreram visualizações de um produto |
| commerce.purchases | Um pedido foi aceito. A compra é a única ação necessária em uma conversão de comércio. A compra deve ter uma lista de produto referenciada |
| commerce.saveForLaters | A lista do produto é salva para uso futuro. Exemplo de uma lista de desejo de produto |
| delivery.feedback | Eventos de feedback para um delivery. Exemplo de eventos de feedback para um delivery de email |


Esses tipos de evento serão mostrados em uma lista suspensa se você estiver usando a extensão Adobe Experience Platform Launch ou você sempre poderá passá-los sem Experience Platform Launch. Eles podem ser transmitidos como parte da opção `xdm`.


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

Como alternativa, `eventType` pode ser passado para o comando evento usando a opção `type`. Em segundo plano, isso é adicionado aos dados XDM. Ter `type` como uma opção permite definir mais facilmente `eventType` sem precisar modificar a carga do XDM.


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### Substituição da ID do conjunto de dados

Em alguns casos de uso, talvez você queira enviar um evento para um conjunto de dados diferente daquele configurado na interface do usuário de configuração. Para isso, é necessário definir a opção `datasetId` no comando `sendEvent`:


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### Adicionar informações de identidade

As informações de identidade personalizadas também podem ser adicionadas ao evento. Consulte [Recuperando ID do Experience Cloud](../identity/overview.md).

## Uso da API sendBeacon

Pode ser complicado enviar dados de evento antes que o usuário da página da Web tenha saído. Se a solicitação demorar muito, o navegador pode cancelar a solicitação. Alguns navegadores implementaram uma API padrão da Web chamada `sendBeacon` para permitir que os dados sejam coletados mais facilmente durante esse período. Ao usar `sendBeacon`, o navegador faz a solicitação da Web no contexto de navegação global. Isso significa que o navegador faz a solicitação de beacon em segundo plano e não segura na navegação da página. Para solicitar que a Adobe Experience Platform [!DNL Web SDK] use `sendBeacon`, adicione a opção `"documentUnloading": true` ao comando evento.  Exemplo:


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

Os navegadores impuseram limites à quantidade de dados que pode ser enviada com `sendBeacon` de uma vez. Em muitos navegadores, o limite é de 64K. Se o navegador rejeita o evento porque a carga é muito grande, o Adobe Experience Platform [!DNL Web SDK] volta a usar seu método de transporte normal (por exemplo, busca).

## Tratamento de respostas de eventos

Se quiser lidar com uma resposta de um evento, você pode ser notificado de um sucesso ou falha da seguinte maneira:


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

## Modificando eventos globalmente {#modifying-events-globally}

Se quiser adicionar, remover ou modificar campos do evento globalmente, você pode configurar um retorno de chamada `onBeforeEventSend`.  Esse retorno de chamada é chamado sempre que um evento é enviado.  Esse retorno de chamada é passado em um objeto de evento com um campo `xdm`.  Modifique `event.xdm` para alterar os dados enviados no evento.


```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(event) {
    // Change existing values
    event.xdm.web.webPageDetails.URL = xdm.web.webPageDetails.URL.toLowerCase();
    // Remove existing values
    delete event.xdm.web.webReferrer.URL;
    // Or add new values
    event.xdm._adb3lettersandnumbers.mycustomkey = "value";
  }
});
```

`xdm` são definidos nesta ordem:

1. Valores passados como opções para o comando evento `alloy("sendEvent", { xdm: ... });`
2. Valores coletados automaticamente.  (Consulte [Informações Automáticas](../data-collection/automatic-information.md).)
3. As alterações feitas no retorno de chamada `onBeforeEventSend`.

Se o retorno de chamada `onBeforeEventSend` gerar uma exceção, o evento ainda será enviado; no entanto, nenhuma das alterações feitas no retorno de chamada é aplicada ao evento final.

## Erros acionáveis potenciais

Ao enviar um evento, um erro pode ser emitido se os dados enviados forem muito grandes (mais de 32 KB para a solicitação completa). Nesse caso, é necessário reduzir a quantidade de dados que está sendo enviada.

Quando a depuração está ativada, o servidor valida sincronicamente os dados do evento que estão sendo enviados em relação ao schema XDM configurado. Se os dados não corresponderem ao schema, os detalhes sobre a incompatibilidade serão retornados do servidor e um erro será lançado. Nesse caso, modifique os dados para que correspondam ao schema. Quando a depuração não está ativada, o servidor valida os dados de forma assíncrona e, portanto, nenhum erro correspondente é emitido.
