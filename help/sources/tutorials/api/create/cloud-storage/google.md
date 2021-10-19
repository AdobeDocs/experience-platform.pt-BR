---
keywords: Experience Platform, home, tópicos populares, Google Cloud Storage, armazenamento na nuvem do google, google, Google
solution: Experience Platform
title: Criar uma conexão base de armazenamento da Google Cloud usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform a uma conta do Google Cloud Storage usando a API do Serviço de fluxo.
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
source-git-commit: 13bd1254dfe89004465174a7532b4f6aaef54c09
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 2%

---

# Crie um [!DNL Google Cloud Storage] conexão básica usando o [!DNL Flow Service] API

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para [!DNL Google Cloud Storage] usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a uma conta do Google Cloud Storage usando o [!DNL Flow Service] API.

### Obter credenciais necessárias

Para [!DNL Flow Service] para se conectar com seu [!DNL Google Cloud Storage] , você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `accessKeyId` | Uma sequência de 61 caracteres alfanuméricos usada para autenticar o [!DNL Google Cloud Storage] para a Platform. |
| `secretAccessKey` | Uma string codificada em 40 caracteres, base e 64, usada para autenticar seu [!DNL Google Cloud Storage] para a Platform. |

Para obter mais informações sobre esses valores, consulte o [Chaves HMAC do Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guia. Para obter etapas sobre como gerar sua própria ID de chave de acesso e chave de acesso secreta, consulte [[!DNL Google Cloud Storage] visão geral](../../../../connectors/cloud-storage/google-cloud-storage.md).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../../../landing/api-guide.md).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST para a variável `/connections` endpoint enquanto fornece seu [!DNL Google Cloud Storage] credenciais de autenticação como parte dos parâmetros da solicitação.

**Formato da API**

```http
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Google Cloud Storage]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google Cloud Storage connection",
        "description": "Connector for Google Cloud Storage",
        "auth": {
            "specName": "Basic Authentication for google-cloud",
            "params": {
                "accessKeyId": "accessKeyId",
                "secretAccessKey": "secretAccessKey"
            }
        },
        "connectionSpec": {
            "id": "32e8f412-cdf7-464c-9885-78184cb113fd",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.accessKeyId` | A ID da chave de acesso associada à [!DNL Google Cloud Storage] conta. |
| `auth.params.secretAccessKey` | A chave de acesso secreta associada à [!DNL Google Cloud Storage] conta. |
| `connectionSpec.id` | O [!DNL Google Cloud Storage] ID de especificação de conexão: `32e8f412-cdf7-464c-9885-78184cb113fd` |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados de armazenamento em nuvem no próximo tutorial.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou um [!DNL Google Cloud Storage] conexão usando APIs e uma ID exclusiva foi obtida como parte do corpo da resposta. Você pode usar essa ID de conexão para [explorar armazenamentos em nuvem usando a API do Serviço de fluxo](../../explore/cloud-storage.md).
