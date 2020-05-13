---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Consentimento
topic: developer guide
translation-type: tm+mt
source-git-commit: a3178ab54a7ab5eacd6c5f605b8bd894779f9e85
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 1%

---


# Consentimento

Determinados regulamentos exigem consentimento explícito do cliente antes que seus dados pessoais possam ser coletados. O `/consent` terminal na API Privacy Service permite processar solicitações de consentimento do cliente e integrá-las ao seu fluxo de trabalho de privacidade.

Antes de usar este guia, consulte a seção [Introdução](./getting-started.md) para obter informações sobre os cabeçalhos de autenticação necessários apresentados na chamada de API de exemplo abaixo.

## Processar uma solicitação de consentimento do cliente

As solicitações de consentimento são processadas fazendo uma solicitação POST para o `/consent` ponto de extremidade.

**Formato da API**

```http
POST /consent
```

**Solicitação**

A solicitação a seguir cria um novo trabalho de consentimento para as IDs de usuário fornecidas no `entities` storage.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/consent \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
        "optOutOfSale": true,
        "entities": [
          {
            "nameSpace": "email",
            "values": [
              "dsmith@acme.com",
              "ajones@acme.com"
            ]
          },
          {
            "nameSpace": "ECID",
            "values": [
              "443636576799758681021090721276"
            ]
          }
        ]
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `optOutOfSale` | Quando definido como true, indica que os usuários fornecidos desejam `entities` recusar a venda ou compartilhar seus dados pessoais. |
| `entities` | Uma matriz de objetos que indica aos usuários aos quais a solicitação de consentimento se aplica. Cada objeto contém um `namespace` e uma matriz de `values` para corresponder usuários individuais a essa namespace. |
| `nameSpace` | Cada objeto na `entities` matriz deve conter uma das namespaces [de identidade](./appendix.md#standard-namespaces) padrão reconhecidas pela API do Privacy Service. |
| `values` | Uma matriz de valores para cada usuário, correspondente ao fornecido `nameSpace`. |

>[!NOTE] Para obter mais informações sobre como determinar quais valores de identidade de cliente enviar para o Privacy Service, consulte o guia sobre como [fornecer dados](../identity-data.md)de identidade.

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) sem carga, indicando que a solicitação foi aceita pelo Privacy Service e está sendo processada.