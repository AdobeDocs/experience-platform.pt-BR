---
title: Mesclagem de dados de evento
seo-title: Mesclagem de dados de evento do SDK da Web do Adobe Experience Platform
description: Saiba como unir os dados do evento SDK da Web da Experience Platform
seo-description: Saiba como unir os dados do evento SDK da Web da Experience Platform
translation-type: tm+mt
source-git-commit: 4bff4b20ccc1913151aa1783d5123ffbb141a7d0
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---


# Mesclagem de dados de evento

>[!IMPORTANT]
>
>Esse recurso ainda está em desenvolvimento e, portanto, nem todas as soluções poderão unir esses dados.

Às vezes, nem todos os dados estão disponíveis quando um evento ocorre. Talvez você queira capturar os dados _que_ possui para que não sejam perdidos se, por exemplo, o usuário fechar o navegador. Por outro lado, você também pode incluir quaisquer dados que estarão disponíveis posteriormente.

Nesses casos, é possível unir dados a eventos anteriores, passando `eventMergeId` como uma opção para `event` comandos da seguinte maneira:

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
  "eventMergeId": "ABC123"
});

// Time passes and more data becomes available

alloy("sendEvent", {
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

Ao transmitir o mesmo valor de ID de mesclagem de evento para ambos os comandos de evento neste exemplo, os dados no segundo comando de evento são aumentados para dados enviados anteriormente no primeiro comando de evento. Um registro para cada comando de evento é criado na plataforma Experience Data, mas durante o relatórios os registros são unidos usando a ID de mesclagem do evento e aparecem como um único evento.

Se você estiver enviando dados sobre um determinado evento para provedores de terceiros, também poderá incluir a mesma ID de mesclagem de evento com esses dados. Posteriormente, se você optar por importar os dados de terceiros para a Adobe Experience Platform, a ID de mesclagem do evento será usada para unir todos os dados coletados como resultado do evento discreto que ocorreu em sua página da Web.

## Geração de uma ID de mesclagem de evento

O valor da ID de mesclagem do evento pode ser qualquer sequência escolhida, mas lembre-se de que todos os eventos enviados usando a mesma ID são reportados como um único evento, portanto, tenha cuidado para aplicar a exclusividade quando os eventos não devem ser mesclados. Se você deseja que o SDK gere uma ID exclusiva de mesclagem de evento em seu nome (seguindo a especificação [amplamente adotada do](https://www.ietf.org/rfc/rfc4122.txt)UID v4), use o `createEventMergeId` comando para fazer isso.

Como em todos os comandos, uma promessa é retornada porque você pode executar o comando antes que o SDK termine de carregar. A promessa será resolvida com uma ID exclusiva de mesclagem de evento assim que possível. Você pode esperar que a promessa seja resolvida antes de enviar dados para o servidor da seguinte forma:

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
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
    "mergeId": results.eventMergeId
  });
});

// Time passes and more data becomes available

eventMergeIdPromise.then(function(results) {
  alloy("sendEvent", {
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
    "mergeId": results.eventMergeId
  });
});
```

Siga este mesmo padrão se desejar acessar a ID de mesclagem do evento por outros motivos (por exemplo, para enviá-la para um provedor de terceiros):

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
  // send event merge ID to a third-party provider
  console.log(results.eventMergeId);
});
```

## Observação sobre o formato XDM

Dentro do comando evento, o objeto `mergeId` é adicionado à `xdm` carga.  Se desejado, o formulário `mergeId` pode ser enviado como parte da opção xdm, como segue:

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
    },
    "eventMergeId": "ABC123"
  }
});
```
