---
title: Conectar o Armazenamento Azure Blob ao Experience Platform usando a API do Serviço de fluxo
description: Saiba como conectar o Adobe Experience Platform ao Azure Blob usando a API do Serviço de fluxo.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: 8e932a25026bef2b785cfddfb8b668b1dd47eb0d
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 3%

---

# Conectar o [!DNL Azure Blob Storage] ao Experience Platform usando a API

Leia este guia para saber como conectar sua conta do [!DNL Azure Blobg Storage] à Adobe Experience Platform usando a [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

### Coletar credenciais necessárias

Leia a [[!DNL Azure Blob Storage] visão geral](../../../../connectors/cloud-storage/blob.md#authentication) para obter informações sobre autenticação.

## Conectar sua conta do [!DNL Azure Blob Storage] à Experience Platform {#connect}

Leia as etapas abaixo para obter informações sobre como conectar sua conta do [!DNL Azure Blob Storage] à Experience Platform.

### Criar uma conexão básica

>[!NOTE]
>
>Depois de criada, você não pode alterar o tipo de autenticação de uma conexão de base [!DNL Azure Blob Storage]. Para alterar o tipo de autenticação, você deve criar uma nova conexão base.

Uma conexão básica vincula sua origem ao Experience Platform, armazenando detalhes de autenticação, status da conexão e uma ID exclusiva. Use essa ID para procurar arquivos de origem e identificar itens específicos a serem assimilados, incluindo seus tipos de dados e formatos.

Você pode conectar sua conta do [!DNL Azure Blob Storage] à Experience Platform usando estes tipos de autenticação:

* **Autenticação da chave da conta**: usa a chave de acesso da conta de armazenamento para autenticar e conectar-se à sua conta do [!DNL Azure Blob Storage].
* **Assinatura de acesso compartilhado (SAS)**: usa um URI SAS para fornecer acesso delegado e limitado por tempo aos recursos da sua conta [!DNL Azure Blob Storage].
* **Autenticação baseada na entidade de serviço**: usa uma entidade de serviço do Azure Ative Diretory (AAD) (ID de cliente e segredo) para autenticar com segurança em sua conta de Armazenamento de Blobs do Azure.

**Formato da API**

```https
POST /connections
```

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` e forneça suas credenciais de autenticação como parte dos parâmetros de solicitação.

>[!BEGINTABS]

>[!TAB Autenticação da chave da conta]

Para usar a autenticação de chave de conta, forneça valores para `connectionString`, `container` e `folderPath`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage connection using connectingString",
    "description": "Azure Blob Storage connection using connectionString",
    "auth": {
      "specName": "ConnectionString",
      "params": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| Parâmetro | Descrição |
| --- | --- |
| `connectionString` | A cadeia de conexão da sua conta [!DNL Azure Blob Storage]. O padrão da cadeia de conexão é: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY};EndpointSuffix=core.windows.net`. |
| `container` | O nome do container [!DNL Azure Blob Storage] onde seus arquivos de dados são armazenados. |
| `folderPath` | O caminho dentro do container especificado onde seus arquivos estão localizados. |
| `connectionSpec.id` | A ID de especificação da conexão da origem [!DNL Azure Blob Storage]. Esta ID foi corrigida como: `4c10e202-c428-4796-9208-5f1f5732b1cf`. |

>[!TAB Assinatura de acesso compartilhado]

Para usar assinatura de acesso compartilhado, forneça valores para o `sasUri`, `container` e `folderPath`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage source connection using SAS URI",
    "description": "Azure Blob Storage source connection using SAS URI",
    "auth": {
      "specName": "SAS URI Authentication",
      "params": {
        "sasUri": "https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| Parâmetro | Descrição |
| --- | --- |
| `sasUri` | O URI de assinatura de acesso compartilhado que você pode usar como um tipo de autenticação alternativo para conectar sua conta. O padrão do URI SAS é: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}`. |
| `container` | O nome do container [!DNL Azure Blob Storage] onde seus arquivos de dados são armazenados. |
| `folderPath` | O caminho dentro do container especificado onde seus arquivos estão localizados. |
| `connectionSpec.id` | A ID de especificação da conexão da origem [!DNL Azure Blob Storage]. Esta ID foi corrigida como: `4c10e202-c428-4796-9208-5f1f5732b1cf`. |

>[!TAB Autenticação baseada na entidade de serviço]

Para se conectar via autenticação baseada na entidade de serviço, forneça valores para: `serviceEndpoint`, `servicePrincipalId`, `servicePrincipalKey`, `accountKind`, `tenant`, `container` e `folderPath`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage source connection using service principal based authentication",
    "description": "Azure Blob Storage source connection using service principal based authentication",
    "auth": {
      "specName": "Service Principal Based Authentication",
      "params": {
        "serviceEndpoint": "{SERVICE_ENDPOINT}",
        "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
        "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
        "accountKind": "{ACCOUNT_KIND}",
        "tenant": "{TENANT}",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| Parâmetro | Descrição |
| --- | --- |
| `serviceEndpoint` | A URL do ponto de extremidade da sua conta [!DNL Azure Blob Storage]. Normalmente no formato: `https://{ACCOUNT_NAME}.blob.core.windows.net`. |
| `servicePrincipalId` | A ID do cliente/aplicativo da entidade de serviço do Azure Ative Diretory (AAD) usada para autenticação. |
| `servicePrincipalKey` | O segredo do cliente ou a senha associada à entidade de serviço do Azure. |
| `accountKind` | O tipo da sua conta [!DNL Azure Blob Storage]. Valores comuns incluem `Storage` (finalidade geral V1), `StorageV2` (finalidade geral V2), `BlobStorage` e `BlockBlobStorage`. |
| `tenant` | A ID do locatário do Azure Ative Diretory (AAD) em que a entidade de serviço está registrada. |
| `container` | O nome do container [!DNL Azure Blob Storage] onde seus arquivos de dados são armazenados. |
| `folderPath` | O caminho dentro do container especificado onde seus arquivos estão localizados. |
| `connectionSpec.id` | A ID de especificação da conexão da origem [!DNL Azure Blob Storage]. Esta ID foi corrigida como: `4c10e202-c428-4796-9208-5f1f5732b1cf`. |

>[!ENDTABS]

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```



## Próximas etapas

Seguindo este tutorial, você criou uma conexão [!DNL Blob] usando APIs e uma ID exclusiva foi obtida como parte do corpo da resposta. Você pode usar esta ID de conexão para [explorar armazenamentos em nuvem usando a API de Serviço de Fluxo](../../explore/cloud-storage.md).
