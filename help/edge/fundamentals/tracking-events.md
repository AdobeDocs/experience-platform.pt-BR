---
title: Rastreamento de eventos
seo-title: Rastreamento de eventos SDK da Web Adobe Experience Platform
description: Saiba como rastrear eventos SDK da Web do Experience Platform
seo-description: Saiba como rastrear eventos SDK da Web do Experience Platform
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---


# Rastreamento de eventos

Para enviar dados do evento para a Adobe Experience Cloud, use o `sendEvent` comando. O `sendEvent` comando é a principal maneira de enviar dados para o [!DNL Experience Cloud]e recuperar conteúdo personalizado, identidades e destinos de audiência.

Os dados enviados para a Adobe Experience Cloud são divididos em duas categorias:

* Dados XDM
* Dados não XDM (atualmente não suportados)

## Envio de dados XDM

Os dados XDM são um objeto cujo conteúdo e estrutura correspondem a um schema que você criou no Adobe Experience Platform. [Saiba mais sobre como criar um schema.](../../xdm/tutorials/create-schema-ui.md)

Todos os dados XDM que você deseja que façam parte de suas análises, personalização, audiências ou destinos devem ser enviados usando a `xdm` opção.

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

>[!NOTE]
>Há um limite de 32 KB nos dados que podem ser enviados em cada evento no campo XDM.

### Envio de dados não XDM

Atualmente, não há suporte para o envio de dados que não correspondem a um schema XDM. O suporte está planejado para uma data futura.

### Configuração `eventType`

Em um evento de experiência XDM, há um `eventType` campo. Isso mantém o tipo de evento principal do registro. Isso pode ser passado como parte da `xdm` opção.

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

Como alternativa, o comando `eventType` pode ser passado para o evento usando a `type` opção. Em segundo plano, isso é adicionado aos dados XDM. Ter a opção `type` como uma permite que você defina mais facilmente a carga `eventType` sem precisar modificar a carga do XDM.

```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

## Uso da API sendBeacon

Pode ser complicado enviar dados de evento antes que o usuário da página da Web tenha saído. Se a solicitação demorar muito, o navegador pode cancelar a solicitação. Alguns navegadores implementaram uma API padrão da Web chamada `sendBeacon` para permitir que os dados sejam coletados com mais facilidade durante esse período. Ao usar `sendBeacon`, o navegador faz a solicitação da Web no contexto de navegação global. Isso significa que o navegador faz a solicitação de beacon em segundo plano e não segura na navegação da página. Para informar o Adobe Experience Platform [!DNL Web SDK] a usar `sendBeacon`, adicione a opção `"documentUnloading": true` ao comando evento.  Exemplo:

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

Os navegadores impuseram limites para a quantidade de dados que pode ser enviada com `sendBeacon` uma só vez. Em muitos navegadores, o limite é de 64K. Se o navegador rejeitar o evento porque a carga é muito grande, o Adobe Experience Platform [!DNL Web SDK] voltará a usar seu método de transporte normal (por exemplo, busca).

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

## Modificação global de eventos {#modifying-events-globally}

Se quiser adicionar, remover ou modificar campos do evento globalmente, você pode configurar um `onBeforeEventSend` retorno de chamada.  Esse retorno de chamada é chamado sempre que um evento é enviado.  Esse retorno de chamada é passado em um objeto de evento com um `xdm` campo.  Modifique `event.xdm` para alterar os dados enviados no evento.

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
2. Valores coletados automaticamente.  (Consulte Informações [](../reference/automatic-information.md)Automáticas.)
3. As alterações feitas no `onBeforeEventSend` retorno de chamada.

Se o `onBeforeEventSend` retorno de chamada gerar uma exceção, o evento ainda será enviado; no entanto, nenhuma das alterações feitas no retorno de chamada é aplicada ao evento final.

## Erros acionáveis potenciais

Ao enviar um evento, um erro pode ser emitido se os dados enviados forem muito grandes (mais de 32 KB para a solicitação completa). Nesse caso, é necessário reduzir a quantidade de dados que está sendo enviada.

Quando a depuração está ativada, o servidor valida sincronicamente os dados do evento que estão sendo enviados em relação ao schema XDM configurado. Se os dados não corresponderem ao schema, os detalhes sobre a incompatibilidade serão retornados do servidor e um erro será lançado. Nesse caso, modifique os dados para que correspondam ao schema. Quando a depuração não está ativada, o servidor valida os dados de forma assíncrona e, portanto, nenhum erro correspondente é emitido.
