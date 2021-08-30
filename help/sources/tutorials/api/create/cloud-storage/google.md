---
keywords: Experience Platform, home, tópicos populares, Armazenamento no Google Cloud, armazenamento na nuvem do google, google, Google
solution: Experience Platform
title: Criar uma conexão base de armazenamento do Google Cloud usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform a uma conta do Google Cloud Storage usando a API do Serviço de fluxo.
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 2%

---

# Crie uma conexão base [!DNL Google Cloud Storage] usando a API [!DNL Flow Service]

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para [!DNL Google Cloud Storage] usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md):  [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes, além de fornecer a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a uma conta do Google Cloud Storage usando a API [!DNL Flow Service].

### Obter credenciais necessárias

Para que [!DNL Flow Service] se conecte com sua conta [!DNL Google Cloud Storage], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `accessKeyId` | Uma sequência de 61 caracteres alfanuméricos usada para autenticar sua conta [!DNL Google Cloud Storage] para a Platform. |
| `secretAccessKey` | Uma sequência de 40 caracteres codificados na base de 64 caracteres usada para autenticar sua conta [!DNL Google Cloud Storage] para a Platform. |

Para obter mais informações sobre esses valores, consulte o guia [Google Cloud Storage HMAC keys](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) . Para obter etapas sobre como gerar sua própria ID de chave de acesso e chave de acesso secreta, consulte a [[!DNL Google Cloud Storage] visão geral](../../../../connectors/cloud-storage/google-cloud-storage.md).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia sobre como [começar a usar APIs da plataforma](../../../../../landing/api-guide.md).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST ao endpoint `/connections`, fornecendo as credenciais de autenticação [!DNL Google Cloud Storage] como parte dos parâmetros da solicitação.

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
| `auth.params.accessKeyId` | A ID da chave de acesso associada à sua conta [!DNL Google Cloud Storage]. |
| `auth.params.secretAccessKey` | A chave de acesso secreta associada à sua conta [!DNL Google Cloud Storage]. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Google Cloud Storage]: `32e8f412-cdf7-464c-9885-78184cb113fd` |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados de armazenamento em nuvem no próximo tutorial.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão [!DNL Google Cloud Storage] usando APIs e uma ID exclusiva foi obtida como parte do corpo da resposta. Você pode usar essa ID de conexão para [explorar armazenamentos em nuvem usando a API do Serviço de Fluxo](../../explore/cloud-storage.md) ou [assimilar dados do Parquet usando a API do Serviço de Fluxo](../../cloud-storage-parquet.md).
