---
keywords: Experience Platform;home;populares tópicos
solution: Experience Platform
title: Ponto de extremidade da API de consentimento
topic: developer guide
description: Saiba como gerenciar solicitações de consentimento do cliente para aplicativos Experience Cloud usando a API Privacy Service.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 1%

---


# Ponto de extremidade de consentimento

Determinadas regulamentações exigem o consentimento explícito do cliente antes que seus dados pessoais possam ser coletados. O endpoint `/consent` na API [!DNL Privacy Service] permite processar solicitações de consentimento do cliente e integrá-las ao seu fluxo de trabalho de privacidade.

Antes de usar este guia, consulte a seção [getting started](./getting-started.md) para obter informações sobre os cabeçalhos de autenticação necessários apresentados na chamada de API de exemplo abaixo.

## Processar uma solicitação de consentimento do cliente

As solicitações de consentimento são processadas fazendo uma solicitação POST para o terminal `/consent`.

**Formato da API**

```http
POST /consent
```

**Solicitação**

A solicitação a seguir cria um novo trabalho de consentimento para as IDs de usuário fornecidas na matriz `entities`.

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
| `optOutOfSale` | Quando definido como true, indica que os usuários fornecidos em `entities` desejam excluir a venda ou compartilhar seus dados pessoais. |
| `entities` | Uma matriz de objetos que indica aos usuários aos quais a solicitação de consentimento se aplica. Cada objeto contém um `namespace` e uma matriz de `values` para corresponder usuários individuais a essa namespace. |
| `nameSpace` | Cada objeto na matriz `entities` deve conter uma das [namespaces de identidade padrão](./appendix.md#standard-namespaces) reconhecidas pela API Privacy Service. |
| `values` | Uma matriz de valores para cada usuário, correspondente ao `nameSpace` fornecido. |

>[!NOTE]
>
>Para obter mais informações sobre como determinar quais valores de identidade do cliente enviar para [!DNL Privacy Service], consulte o guia em [fornecendo dados de identidade](../identity-data.md).

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) sem carga, indicando que a solicitação foi aceita por [!DNL Privacy Service] e está sendo processada.