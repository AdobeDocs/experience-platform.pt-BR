---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Ponto de extremidade da API de consentimento
topic-legacy: developer guide
description: Saiba como gerenciar solicitações de consentimento do cliente para aplicativos Experience Cloud usando a API do Privacy Service.
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 1%

---

# Ponto de extremidade de consentimento

Determinadas regulamentações exigem consentimento explícito do cliente para que seus dados pessoais possam ser coletados. O endpoint `/consent` na API [!DNL Privacy Service] permite processar as solicitações de consentimento do cliente e integrá-las ao workflow de privacidade.

Antes de usar este guia, consulte a seção [introdução](./getting-started.md) para obter informações sobre os cabeçalhos de autenticação necessários apresentados na chamada de API de exemplo abaixo.

## Processar uma solicitação de consentimento do cliente

As solicitações de consentimento são processadas fazendo uma solicitação POST ao endpoint `/consent`.

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
| `optOutOfSale` | Quando definido como true, indica que os usuários fornecidos em `entities` desejam recusar a venda ou o compartilhamento de seus dados pessoais. |
| `entities` | Uma matriz de objetos que indica os usuários aos quais a solicitação de consentimento se aplica. Cada objeto contém um `namespace` e uma matriz de `values` para corresponder usuários individuais a esse namespace. |
| `nameSpace` | Cada objeto na matriz `entities` deve conter um dos [namespaces de identidade padrão](./appendix.md#standard-namespaces) reconhecidos pela API do Privacy Service. |
| `values` | Uma matriz de valores para cada usuário, correspondente ao `nameSpace` fornecido. |

>[!NOTE]
>
>Para obter mais informações sobre como determinar quais valores de identidade do cliente enviar para [!DNL Privacy Service], consulte o guia em [fornecendo dados de identidade](../identity-data.md).

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Accepted) sem carga, indicando que a solicitação foi aceita por [!DNL Privacy Service] e está em processamento.
