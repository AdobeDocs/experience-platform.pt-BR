---
title: Rastrear eventos usando o SDK da Web da Adobe Experience Platform
description: Saiba como rastrear eventos do Adobe Experience Platform Web SDK.
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;send Beacon;documentUnloading;document Unloading;onBeforeEventSend;
exl-id: 8b221cae-3490-44cb-af06-85be4f8d280a
source-git-commit: a6948e3744aa754eda22831a7e68b847eb904e76
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 1%

---

# Rastrear eventos

Para enviar dados do evento para o Adobe Experience Cloud, use o `sendEvent` comando. A variável `sendEvent` é a principal maneira de enviar dados para o [!DNL Experience Cloud]e para recuperar conteúdo personalizado, identidades e destinos de público-alvo.

Os dados enviados para o Adobe Experience Cloud se encaixam em duas categorias:

* Dados XDM
* Dados não XDM

## Envio de dados XDM

Os dados XDM são um objeto cujo conteúdo e estrutura correspondem a um esquema criado no Adobe Experience Platform. [Saiba mais sobre como criar um esquema.](../../xdm/tutorials/create-schema-ui.md)

Quaisquer dados XDM que você deseja que façam parte de sua análise, personalização, públicos ou destinos devem ser enviados usando o `xdm` opção.


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

Pode decorrer algum tempo entre o momento em que a `sendEvent` é executado e quando os dados são enviados ao servidor (por exemplo, se a biblioteca do SDK da Web não tiver sido totalmente carregada ou se o consentimento ainda não tiver sido recebido). Se você pretende modificar qualquer parte da variável `xdm` após executar o `sendEvent` , é altamente recomendável que você clone o `xdm` objeto _antes_ execução da `sendEvent` comando. Por exemplo:

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

Neste exemplo, a camada de dados é clonada serializando-a para JSON e, em seguida, desserializando-a. Em seguida, o resultado clonado é passado para o estado `sendEvent` comando. Isso garante que a `sendEvent` tem um instantâneo da camada de dados existente quando o `sendEvent` O comando foi executado para que modificações posteriores no objeto da camada de dados original não sejam refletidas nos dados enviados ao servidor. Se você estiver usando uma camada de dados orientada por eventos, a clonagem de seus dados provavelmente já será manipulada automaticamente. Por exemplo, se estiver usando a variável [Camada de dados de clientes Adobe](https://github.com/adobe/adobe-client-data-layer/wiki), o `getState()` fornece um instantâneo calculado e clonado de todas as alterações anteriores. Isso também é feito automaticamente se você estiver usando a extensão de tag do Adobe Experience Platform Web SDK.

>[!NOTE]
>
>Há um limite de 32 KB nos dados que podem ser enviados em cada evento no campo XDM.


## Envio de dados não XDM

Os dados que não correspondem a um esquema XDM devem ser enviados usando o `data` opção do `sendEvent` comando. Esse recurso é compatível com as versões 2.5.0 e posteriores do SDK da Web.

Isso é útil se você precisar atualizar um perfil do Adobe Target ou enviar atributos do Target Recommendations. [Leia mais sobre estes recursos do Target.](../personalization/adobe-target/target-overview.md#single-profile-update)

No futuro, você poderá enviar sua camada de dados completa no `data` e mapeá-lo para o lado do servidor XDM.

**Como enviar atributos de Perfil e Recommendations para o Adobe Target:**

```javascript
alloy("sendEvent", {
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30,
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```


### Configuração `eventType` {#event-types}

Nos esquemas XDM ExperienceEvent, há uma variável `eventType` campo. Contém o tipo de evento principal do registro. Definir um tipo de evento pode ajudar a diferenciar os eventos diferentes que você enviará. O XDM fornece vários tipos de evento predefinidos que você pode usar ou sempre criar seus próprios tipos de evento personalizados para seus casos de uso. Consulte a documentação do XDM para obter uma [lista de todos os tipos de evento predefinidos](../../xdm/classes/experienceevent.md#eventType).

Esses tipos de evento serão mostrados em uma lista suspensa se estiver usando a extensão de tag ou se você sempre puder passá-los sem tags. Eles podem ser transmitidos como parte da variável `xdm` opção.


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

Em alternativa, a `eventType` pode ser passado para o comando de evento usando o `type` opção. Em segundo plano, isso é adicionado aos dados XDM. Ter o `type` como opção permite definir com mais facilidade as `eventType` sem precisar modificar a carga XDM.


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### Substituição da ID do conjunto de dados

>[!IMPORTANT]
>
>A variável `datasetId` opção compatível com o `sendEvent` comando foi descontinuado. Para substituir uma ID de conjunto de dados, use [sobreposições de configuração](../datastreams/overrides.md) em vez disso.

Em alguns casos de uso, convém enviar um evento para um conjunto de dados diferente daquele configurado na interface do usuário de configuração. Para isso, é necessário definir o `datasetId` opção no `sendEvent` comando:



```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### Adição de informações de identidade

Informações de identidade personalizadas também podem ser adicionadas ao evento. Consulte [Recuperando ID do Experience Cloud](../identity/overview.md).

## Utilização da API sendBeacon

Pode ser complicado enviar dados do evento antes que o usuário da página da Web tenha saído. Se a solicitação demorar muito, o navegador pode cancelar a solicitação. Alguns navegadores implementaram uma API padrão da Web chamada `sendBeacon` para permitir que os dados sejam coletados mais facilmente durante esse período. Ao usar `sendBeacon`, o navegador faz a solicitação da web no contexto de navegação global. Isso significa que o navegador faz a solicitação de sinal em segundo plano e não mantém a navegação da página. Para informar ao Adobe Experience Platform [!DNL Web SDK] para usar `sendBeacon`, adicione a opção `"documentUnloading": true` para o comando do evento.  Exemplo:


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

Os navegadores impuseram limites à quantidade de dados que pode ser enviada com `sendBeacon` de uma só vez. Em muitos navegadores, o limite é de 64K. Se o navegador rejeitar o evento porque a carga é muito grande, o Adobe Experience Platform [!DNL Web SDK] O retorna ao uso do método de transporte normal (por exemplo, fetch).

## Manipulação de respostas de eventos

Se quiser lidar com uma resposta de um evento, você poderá ser notificado sobre sucesso ou falha da seguinte maneira:


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
}).then(function(result) {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```


### A variável `result` objeto

A variável `sendEvent` retorna uma promessa que é resolvida com uma `result` objeto. A variável `result` contém as seguintes propriedades:

**apresentações**: as ofertas de personalização para as quais o visitante se qualificou. [Saiba mais sobre apresentações.](../personalization/rendering-personalization-content.md#manually-rendering-content)

**decisões**: esta propriedade está obsoleta. Em vez disso, use `propositions`.

**destinos**: segmentos do Adobe Experience Platform que podem ser compartilhados com plataformas de personalização externas, sistemas de gerenciamento de conteúdo, servidores de anúncios e outros aplicativos que estão sendo executados nos sites do cliente. [Saiba mais sobre destinos.](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=en)

>[!WARNING]
>
>`destinations` O está atualmente na versão beta. A documentação e a funcionalidade estão sujeitas a alterações.

## Modificação global de eventos {#modifying-events-globally}

Se quiser adicionar, remover ou modificar campos do evento globalmente, você pode configurar um `onBeforeEventSend` retorno de chamada.  Essa chamada de retorno é chamada sempre que um evento é enviado.  Essa chamada de retorno é passada em um objeto de evento com um `xdm` campo.  Modificar `content.xdm` para alterar os dados enviados com o evento.


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

`xdm` os campos são definidos nesta ordem:

1. Valores passados como opções para o comando de evento `alloy("sendEvent", { xdm: ... });`
2. Valores coletados automaticamente.  (Consulte [Informações Automáticas](../data-collection/automatic-information.md).)
3. As alterações efetuadas no `onBeforeEventSend` retorno de chamada.

Algumas observações sobre `onBeforeEventSend` retorno de chamada:

* O XDM do evento pode ser modificado durante o retorno de chamada. Depois que o retorno de chamada é retornado, os campos e valores modificados dos objetos content.xdm e content.data são enviados com o evento.

   ```javascript
   onBeforeEventSend: function(content){
     //sets a query parameter in XDM
     const queryString = window.location.search;
     const urlParams = new URLSearchParams(queryString);
     content.xdm.marketing.trackingCode = urlParams.get('cid')
   }
   ```

* Se o retorno de chamada lançar uma exceção, o processamento do evento descontinuará e o evento não será enviado.
* Se o retorno de chamada retornar o valor booleano de `false`, o processamento do evento será interrompido, sem um erro, e o evento não será enviado. Esse mecanismo permite que determinados eventos sejam facilmente ignorados, examinando os dados do evento e retornando `false` caso o evento não deva ser enviado.

   >[!NOTE]
   >Tenha cuidado para evitar retornar falso no primeiro evento em uma página. Retornar false no primeiro evento pode afetar negativamente a personalização.

```javascript
   onBeforeEventSend: function(content) {
     // ignores events from bots
     if (MyBotDetector.isABot()) {
       return false;
     }
   }
```

Qualquer valor de retorno diferente do booleano `false` permitirá que o evento seja processado e enviado após o retorno de chamada.

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

Ao enviar um evento, pode ocorrer um erro se os dados enviados forem muito grandes (mais de 32 KB para a solicitação completa). Nesse caso, é necessário reduzir a quantidade de dados que está sendo enviada.
