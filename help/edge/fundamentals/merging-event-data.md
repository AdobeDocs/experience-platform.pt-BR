---
title: Mesclagem de dados de evento
seo-title: Mesclagem de dados de evento do SDK da Web do Adobe Experience Platform
description: Saiba como unir os dados de eventos do SDK da Web da Experience Platform
seo-description: Saiba como unir os dados de eventos do SDK da Web da Experience Platform
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Mesclando dados de eventos

>[!IMPORTANT]
>
>O SDK da Web da plataforma Adobe Experience está atualmente em beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

Às vezes, nem todos os dados estão disponíveis quando um evento ocorre. Talvez você queira capturar os dados _que_ possui para que não sejam perdidos se, por exemplo, o usuário fechar o navegador. Por outro lado, você também pode incluir quaisquer dados que estarão disponíveis posteriormente.

Nesses casos, é possível unir dados a eventos anteriores transmitindo `eventMergeId` como uma opção para `event` comandos da seguinte maneira:

```javascript
alloy("event", {
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
  "eventMergeId": "ABC123"
});

// Time passes and more data becomes available

alloy("event", {
  "xdm": {
    "commerce": {
      "order": {
        "payments": [
          {
            "transactionID": "TR426941",
            "paymentAmount": 999.98,
            "paymentType": "credit_card",
            "currencyCode": "USD"
          }
        ]
      }
    }
  }
  "eventMergeId": "ABC123"
});
```

Ao transmitir o mesmo valor de ID de mesclagem de eventos para ambos os comandos de evento neste exemplo, os dados no segundo comando de evento são aumentados para dados enviados anteriormente no primeiro comando de evento. Um registro para cada comando de evento é criado na Plataforma de dados de experiência, mas durante o relatório os registros são unidos usando a ID de mesclagem de evento e exibidos como um único evento.

Se você estiver enviando dados sobre um evento específico para provedores de terceiros, também poderá incluir a mesma ID de mesclagem de evento com esses dados. Posteriormente, se você optar por importar os dados de terceiros para a Adobe Experience Platform, a ID de mesclagem do evento será usada para unir todos os dados coletados como resultado do evento discreto que ocorreu em sua página da Web.

## Geração de uma ID de mesclagem de evento

O valor da ID de mesclagem do evento pode ser qualquer sequência escolhida, mas lembre-se de que todos os eventos enviados usando a mesma ID são reportados como um único evento. Portanto, tenha cuidado para aplicar a exclusividade quando os eventos não devem ser mesclados. Se você desejar que o SDK gere uma ID exclusiva de mesclagem de evento em seu nome (seguindo a especificação [amplamente adotada do](https://www.ietf.org/rfc/rfc4122.txt)UID v4), use o `createEventMergeId` comando para fazer isso.

Como em todos os comandos, uma promessa é retornada porque você pode executar o comando antes que o SDK termine de carregar. A promessa será resolvida com uma ID exclusiva de mesclagem de eventos assim que possível. Você pode esperar que a promessa seja resolvida antes de enviar dados para o servidor da seguinte forma:

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(eventMergeId) {
  alloy("event", {
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
    "mergeId": eventMergeId
  });
});

// Time passes and more data becomes available

eventMergeIdPromise.then(function(eventMergeId) {
  alloy("event", {
    "xdm": {
      "commerce": {
        "order": {
          "payments": [
            {
              "transactionID": "TR426941",
              "paymentAmount": 999.98,
              "paymentType": "credit_card",
              "currencyCode": "USD"
            }
          ]
        }
      }
    }
    "mergeId": eventMergeId
  });
});
```

Siga este mesmo padrão se desejar acessar a ID de mesclagem do evento por outros motivos (por exemplo, para enviá-la para um provedor de terceiros):

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(eventMergeId) {
  // send event merge ID to a third-party provider
  console.log(eventMergeId);
});
```

## Observação sobre o formato XDM

Dentro do comando event, o evento `mergeId` é realmente adicionado à `xdm` carga.  Se desejado, o formulário `mergeId` pode ser enviado como parte da opção xdm, como segue:

```javascript
alloy("event", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    },
    "eventMergeId": "ABC123"
  }
});
```
