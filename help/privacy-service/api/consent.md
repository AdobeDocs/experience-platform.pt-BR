---
keywords: Experience Platform;página inicial;tópicos populares
solution: Experience Platform
title: Endpoint da API de consentimento
description: Saiba como gerenciar solicitações de consentimento do cliente para aplicativos Experience Cloud usando a API Privacy Service.
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 2%

---

# Endpoint de consentimento

Certos regulamentos exigem o consentimento explícito do cliente antes que seus dados pessoais possam ser coletados. A variável `/consent` endpoint na variável [!DNL Privacy Service] A API permite processar solicitações de consentimento do cliente e integrá-las ao seu fluxo de trabalho de privacidade.

Antes de usar este guia, consulte o [introdução](./getting-started.md) guia para obter informações sobre os cabeçalhos de autenticação necessários apresentados na chamada de API de exemplo abaixo.

## Processar uma solicitação de consentimento do cliente

As solicitações de consentimento são processadas fazendo uma solicitação POST ao `/consent` terminal.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `optOutOfSale` | Quando definido como verdadeiro, indica que os usuários fornecidos em `entities` recusar a venda ou a partilha dos seus dados pessoais. |
| `entities` | Uma matriz de objetos que indica os usuários aos quais a solicitação de consentimento se aplica. Cada objeto contém um `namespace` e uma série de `values` para corresponder usuários individuais a esse namespace. |
| `nameSpace` | Cada objeto no `entities` a matriz deve conter um dos [namespaces de identidade padrão](./appendix.md#standard-namespaces) reconhecido pela API Privacy Service. |
| `values` | Uma matriz de valores para cada usuário, correspondente à variável fornecida `nameSpace`. |

{style="table-layout:auto"}

>[!NOTE]
>
>Para obter mais informações sobre como determinar para quais valores de identidade do cliente enviar [!DNL Privacy Service], consulte o guia sobre [fornecimento de dados de identidade](../identity-data.md).

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) sem carga, indicando que a solicitação foi aceita por [!DNL Privacy Service] e está em processamento.
