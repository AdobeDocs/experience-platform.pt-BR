---
title: Criar uma conexão de base de armazenamento na nuvem do Google usando a API do serviço de fluxo
description: Saiba como conectar o Adobe Experience Platform a uma conta de Armazenamento na nuvem do Google usando a API do serviço de fluxo.
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
source-git-commit: 3636b785d82fa2e49f76825650e6159be119f8b4
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# Criar um [!DNL Google Cloud Storage] conexão básica usando o [!DNL Flow Service] API

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial guiará você pelas etapas para criar uma conexão básica para [!DNL Google Cloud Storage] usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Origens](../../../../home.md): [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando o [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem as informações adicionais que você precisará saber para se conectar com êxito a uma conta do Google Cloud Storage usando o [!DNL Flow Service] API.

### Coletar credenciais necessárias

A fim de [!DNL Flow Service] para se conectar com o seu [!DNL Google Cloud Storage] você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `accessKeyId` | Uma sequência de 61 caracteres alfanuméricos usada para autenticar seu [!DNL Google Cloud Storage] para a Platform. |
| `secretAccessKey` | Uma string de 40 caracteres codificada em base 64 usada para autenticar seu [!DNL Google Cloud Storage] para a Platform. |
| `bucketName` | O nome do seu [!DNL Google Cloud Storage] balde. Você deve especificar um nome de bucket se quiser fornecer acesso a uma subpasta específica no armazenamento na nuvem. |
| `folderPath` | O caminho para a pasta à qual você deseja fornecer acesso. |

Para obter mais informações sobre esses valores, consulte [Chaves HMAC do Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guia. Para obter etapas sobre como gerar sua própria ID da chave de acesso e chave de acesso secreta, consulte o [[!DNL Google Cloud Storage] visão geral](../../../../connectors/cloud-storage/google-cloud-storage.md).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e sua ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar um ID de conexão base, faça uma solicitação POST ao `/connections` ao fornecer sua [!DNL Google Cloud Storage] credenciais de autenticação como parte dos parâmetros de solicitação.

>[!TIP]
>
>Durante essa etapa, também é possível designar as subpastas às quais sua conta terá acesso definindo o nome do bucket e o caminho para a subpasta.

**Formato da API**

```http
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão básica para [!DNL Google Cloud Storage]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google Cloud Storage connection",
      "description": "Connector for Google Cloud Storage",
      "auth": {
          "specName": "Basic Authentication for google-cloud",
          "params": {
              "accessKeyId": "accessKeyId",
              "secretAccessKey": "secretAccessKey",
              "bucketName": "acme-google-cloud-bucket",
              "folderPath": "/acme/customers/sales"
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
| `auth.params.bucketName` | O nome do seu [!DNL Google Cloud Storage] balde. Você deve especificar um nome de bucket se quiser fornecer acesso a uma subpasta específica no armazenamento na nuvem. |
| `auth.params.folderPath` | O caminho para a pasta à qual você deseja fornecer acesso. |
| `connectionSpec.id` | A variável [!DNL Google Cloud Storage] ID da especificação de conexão: `32e8f412-cdf7-464c-9885-78184cb113fd` |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar os dados de armazenamento na nuvem no próximo tutorial.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou um [!DNL Google Cloud Storage] Uma conexão usando APIs e uma ID exclusiva foi obtida como parte do corpo da resposta. Você pode usar essa ID de conexão para [explorar armazenamentos em nuvem usando a API do Serviço de fluxo](../../explore/cloud-storage.md).
