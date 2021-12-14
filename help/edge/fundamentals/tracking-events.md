---
title: Rastrear eventos usando o SDK da Web da Adobe Experience Platform
description: Saiba como rastrear eventos do SDK da Web da Adobe Experience Platform.
keywords: sendEvent; xdm; eventType; datasetId; sendBeacon; send Beacon; documentUnloading; document Unloading; onBeforeEventSend;
exl-id: 8b221cae-3490-44cb-af06-85be4f8d280a
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 1%

---

# Rastrear eventos

Para enviar dados do evento para o Adobe Experience Cloud, use a variável `sendEvent` comando. O `sendEvent` é a principal maneira de enviar dados para o [!DNL Experience Cloud]e para recuperar conteúdo personalizado, identidades e destinos de público-alvo.

Os dados enviados para o Adobe Experience Cloud são divididos em duas categorias:

* Dados XDM
* Dados não XDM

## Envio de dados XDM

Os dados XDM são um objeto cujo conteúdo e estrutura correspondem a um esquema criado no Adobe Experience Platform. [Saiba mais sobre como criar um schema.](../../xdm/tutorials/create-schema-ui.md)

Quaisquer dados XDM que você deseja que façam parte de sua análise, personalização, públicos-alvo ou destinos devem ser enviados usando a variável `xdm` opção.


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

Algum tempo pode passar entre quando a função `sendEvent` é executado e quando os dados são enviados para o servidor (por exemplo, se a biblioteca do SDK da Web não tiver sido totalmente carregada ou o consentimento ainda não tiver sido recebido). Se você pretende modificar qualquer parte da variável `xdm` após executar o `sendEvent` é altamente recomendável clonar o `xdm` objeto _before_ executar o `sendEvent` comando. Por exemplo:

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

Neste exemplo, a camada de dados é clonada serializando-a para JSON e depois desserializando-a. Em seguida, o resultado clonado é passado para o `sendEvent` comando. Isso garante que a variável `sendEvent` tem um instantâneo da camada de dados como existia quando a `sendEvent` foi executado para que modificações posteriores no objeto da camada de dados original não sejam refletidas nos dados enviados para o servidor. Se você estiver usando uma camada de dados orientada por eventos, a clonagem de seus dados provavelmente já será manipulada automaticamente. Por exemplo, se você estiver usando a variável [Camada de dados do cliente Adobe](https://github.com/adobe/adobe-client-data-layer/wiki), o `getState()` O método oferece um instantâneo computado e clonado de todas as alterações anteriores. Isso também é feito para você automaticamente se estiver usando a extensão de tag Adobe Experience Platform Web SDK.

>[!NOTE]
>
>Há um limite de 32 KB nos dados que podem ser enviados em cada evento no campo XDM.


## Envio de dados não XDM

Os dados que não correspondem a um esquema XDM devem ser enviados usando o `data` da `sendEvent` comando. Esse recurso é compatível com versões 2.5.0 e posteriores do SDK da Web.

Isso é útil se você precisar atualizar um perfil do Adobe Target ou enviar atributos do Recommendations do Target. [Leia mais sobre esses recursos do Target.](../personalization/adobe-target/target-overview.md#single-profile-update)

No futuro, você poderá enviar a camada de dados completa sob a `data` e mapeie-a para o lado do servidor XDM.

**Como enviar atributos do Perfil e do Recommendations para o Adobe Target:**

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

Nos esquemas XDM ExperienceEvent, há uma opção opcional `eventType` campo. Isso mantém o tipo de evento principal para o registro. Definir um tipo de evento pode ajudar você a diferenciar os diferentes eventos que serão enviados. O XDM fornece vários tipos de evento predefinidos que podem ser usados ou você sempre cria seus próprios tipos de evento personalizados para seus casos de uso. Consulte a documentação do XDM para obter uma [lista de todos os tipos de evento predefinidos](../../xdm/classes/experienceevent.md#eventType).

Esses tipos de evento serão mostrados em uma lista suspensa se você estiver usando a extensão de tag ou sempre puder transmiti-los sem tags. Eles podem ser transmitidos como parte do `xdm` opção.


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

Como alternativa, a variável `eventType` pode ser transmitido para o comando event usando o `type` opção. Em segundo plano, isso é adicionado aos dados XDM. Tendo em conta `type` como uma opção, permite definir com mais facilidade a variável `eventType` sem precisar modificar a carga do XDM.


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### Substituição da ID do conjunto de dados

Em alguns casos de uso, você pode enviar um evento para um conjunto de dados diferente daquele configurado na interface do usuário de configuração. Para isso, é necessário definir a variável `datasetId` na `sendEvent` comando:


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### Adição de informações de identidade

As informações de identidade personalizadas também podem ser adicionadas ao evento. Consulte [Recuperar Experience Cloud ID](../identity/overview.md).

## Uso da API sendBeacon

Pode ser complicado enviar dados de evento antes que o usuário da página da Web tenha saído. Se a solicitação demorar muito, o navegador pode cancelar a solicitação. Alguns navegadores implementaram uma API padrão da Web chamada `sendBeacon` para permitir que os dados sejam coletados com mais facilidade durante esse período. Ao usar `sendBeacon`, o navegador faz a solicitação da Web no contexto de navegação global. Isso significa que o navegador faz a solicitação de beacon em segundo plano e não segura a navegação da página. Para dizer à Adobe Experience Platform [!DNL Web SDK] para usar `sendBeacon`, adicione a opção `"documentUnloading": true` para o comando event.  Exemplo:


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

Os navegadores impuseram limites para a quantidade de dados que pode ser enviada com `sendBeacon` de uma vez. Em muitos navegadores, o limite é de 64 K. Se o navegador rejeitar o evento porque a carga é muito grande, o Adobe Experience Platform [!DNL Web SDK] volta ao uso de seu método de transporte normal (por exemplo, busca).

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
}).then(function(result) {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```


### O `result` objeto

O `sendEvent` retorna uma promessa resolvida com um `result` objeto. O `result` O objeto contém as seguintes propriedades:

**propositions**: A Personalização oferece as ofertas para as quais o visitante se qualificou. [Saiba mais sobre propostas.](../personalization/rendering-personalization-content.md#manually-rendering-content)

**decisões**: Essa propriedade está obsoleta. Em vez disso, use `propositions`.

**destinos**: Segmentos do Adobe Experience Platform que podem ser compartilhados com plataformas de personalização externas, sistemas de gerenciamento de conteúdo, servidores de anúncios e outros aplicativos que estão sendo executados em sites do cliente. [Saiba mais sobre destinos.](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=en)

>[!WARNING]
>
>`destinations` está atualmente em Beta. A documentação e a funcionalidade estão sujeitas a alterações.

**inferências**: Insights de aprendizado de máquina em tempo real. [Saiba mais sobre o Aprendizado de máquina em tempo real.](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/real-time-machine-learning/home.html?lang=en)

>[!WARNING]
>
>`inferences` está atualmente em Beta. A documentação e a funcionalidade estão sujeitas a alterações.



## Modificação global de eventos {#modifying-events-globally}

Se quiser adicionar, remover ou modificar campos do evento globalmente, você pode configurar um `onBeforeEventSend` retorno de chamada.  Esse retorno de chamada é chamado sempre que um evento é enviado.  Esse retorno de chamada é passado em um objeto de evento com um `xdm` campo.  Modificar `content.xdm` para alterar os dados enviados com o evento.


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

1. Valores passados como opções para o comando event `alloy("sendEvent", { xdm: ... });`
2. Valores coletados automaticamente.  (Consulte [Informações automáticas](../data-collection/automatic-information.md).)
3. As alterações feitas no `onBeforeEventSend` retorno de chamada.

Algumas observações sobre o `onBeforeEventSend` retorno de chamada:

* O XDM do evento pode ser modificado durante o retorno de chamada. Depois que a chamada de retorno for retornada, todos os campos e valores modificados dos objetos content.xdm e content.data serão enviados com o evento .

   ```javascript
   onBeforeEventSend: function(content){
     //sets a query parameter in XDM
     const queryString = window.location.search;
     const urlParams = new URLSearchParams(queryString);
     content.xdm.marketing.trackingCode = urlParams.get('cid')
   }
   ```

* Se o retorno de chamada gerar uma exceção, o processamento do evento será interrompido e o evento não será enviado.
* Se o retorno de chamada retornar o valor booleano de `false`, o processamento de eventos é interrompido, sem um erro, e o evento não é enviado. Esse mecanismo permite que determinados eventos sejam facilmente ignorados ao examinar os dados do evento e retornar `false` se o evento não deve ser enviado.

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

Qualquer valor de retorno diferente de booleano `false` permitirá que o evento processe e envie após o retorno de chamada.

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
