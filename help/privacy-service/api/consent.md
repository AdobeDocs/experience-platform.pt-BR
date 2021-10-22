---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Ponto de extremidade da API de consentimento
topic-legacy: developer guide
description: Saiba como gerenciar solicitações de consentimento do cliente para aplicativos Experience Cloud usando a API do Privacy Service.
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 3%

---

# Ponto de extremidade de consentimento

Determinadas regulamentações exigem consentimento explícito do cliente para que seus dados pessoais possam ser coletados. O `/consent` endpoint no [!DNL Privacy Service] A API permite processar solicitações de consentimento do cliente e integrá-las ao seu fluxo de trabalho de privacidade.

Antes de usar este guia, consulte o [introdução](./getting-started.md) guia para obter informações sobre os cabeçalhos de autenticação necessários apresentados na chamada de API de exemplo abaixo.

## Processar uma solicitação de consentimento do cliente

As solicitações de consentimento são processadas fazendo uma solicitação POST para o `/consent` endpoint .

**Formato da API**

```http
POST /consent
```

**Solicitação**

A solicitação a seguir cria um novo trabalho de consentimento para as IDs de usuário fornecidas no `entities` matriz.

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
| `optOutOfSale` | Quando definido como true, indica que os usuários fornecidos em `entities` Desejam recusar a venda ou o compartilhamento de seus dados pessoais. |
| `entities` | Uma matriz de objetos que indica os usuários aos quais a solicitação de consentimento se aplica. Cada objeto contém um `namespace` e uma matriz de `values` para corresponder usuários individuais com esse namespace. |
| `nameSpace` | Cada objeto na variável `entities` a matriz deve conter um dos [namespaces de identidade padrão](./appendix.md#standard-namespaces) reconhecido pela API do Privacy Service. |
| `values` | Uma matriz de valores para cada usuário, correspondendo ao valor fornecido `nameSpace`. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Para obter mais informações sobre como determinar para quais valores de identidade do cliente enviar [!DNL Privacy Service], consulte o guia em [fornecimento de dados de identidade](../identity-data.md).

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) sem carga, indicando que a solicitação foi aceita por [!DNL Privacy Service] e está em transformação.
