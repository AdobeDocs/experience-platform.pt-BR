---
keywords: Experience Platform, home, tópicos populares, Azure, blob do azure, blob, Blob
solution: Experience Platform
title: Criar uma conexão de fonte de blob do Azure usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform ao Azure Blob usando a API do Serviço de Fluxo.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 2%

---

# Crie uma conexão de origem [!DNL Azure Blob] usando a API [!DNL Flow Service]

Este tutorial usa a [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) para guiá-lo pelas etapas para conectar [!DNL Azure Blob] (a seguir, &quot;Blob&quot;) ao Adobe Experience Platform.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para criar com êxito uma conexão de origem [!DNL Blob] usando a API [!DNL Flow Service].

### Obter credenciais necessárias

Para que [!DNL Flow Service] se conecte ao armazenamento [!DNL Blob], você deve fornecer valores para a seguinte propriedade de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | Uma string que contém as informações de autorização necessárias para autenticar [!DNL Blob] no Experience Platform. O padrão da string de conexão [!DNL Blob] é: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Para obter mais informações sobre cadeias de conexão, consulte este documento [!DNL Blob] em [configurar cadeias de conexão](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | O URI da assinatura de acesso compartilhado que você pode usar como um tipo de autenticação alternativo para conectar sua conta [!DNL Blob]. O padrão de URI SAS [!DNL Blob] é: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Para obter mais informações, consulte este documento [!DNL Blob] em [URIs de assinatura de acesso compartilhado](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `connectionSpec.id` | O identificador exclusivo necessário para criar uma conexão. A ID de especificação de conexão para [!DNL Blob] é: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

### Lendo exemplos de chamadas de API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas do Experience Platform.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para APIs da plataforma, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API do Experience Platform, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos no Experience Platform, incluindo aqueles pertencentes a [!DNL Flow Service], são isolados para sandboxes virtuais específicas. Todas as solicitações para APIs da plataforma exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* `Content-Type: application/json`

## Criar uma conexão

Uma conexão especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão é necessária por conta [!DNL Blob], pois pode ser usada para criar vários fluxos de dados para trazer dados diferentes.

### Criar uma conexão [!DNL Blob] usando a autenticação baseada em cadeia de conexão

Para criar uma conexão [!DNL Blob] usando a autenticação baseada em string de conexão, faça uma solicitação de POST para a API [!DNL Flow Service], fornecendo o [!DNL Blob] `connectionString`.

**Formato da API**

```http
POST /connections
```

**Solicitação**

Para criar uma conexão [!DNL Blob], a ID de especificação de conexão exclusiva deve ser fornecida como parte da solicitação POST. A ID de especificação de conexão para [!DNL Blob] é `4c10e202-c428-4796-9208-5f1f5732b1cf`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Blob connection using connectionString",
        "description": "Azure Blob connection using connectionString",
        "auth": {
            "specName": "ConnectionString",
            "params": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}"
            }
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.connectionString` | A string de conexão necessária para acessar dados no armazenamento do Blob. O padrão da string de conexão Blob é: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | A ID de especificação da conexão de armazenamento Blob é: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seu armazenamento no próximo tutorial.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

### Criar uma conexão [!DNL Blob] usando o URI da assinatura de acesso compartilhado

Um URI de assinatura de acesso compartilhado (SAS) permite autorização delegada segura para sua conta [!DNL Blob]. Você pode usar a SAS para criar credenciais de autenticação com diferentes graus de acesso, já que uma autenticação baseada em SAS permite definir permissões, datas de início e expiração, bem como provisões para recursos específicos.

Para criar uma conexão [!DNL Blob] usando o URI da assinatura de acesso compartilhado, faça uma solicitação de POST para a API [!DNL Flow Service], fornecendo valores para seu [!DNL Blob] `sasUri`.

**Formato da API**

```http
POST /connections
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Blob source connection using SAS URI",
        "description": "Azure Blob source connection using SAS URI",
        "auth": {
            "specName": "SasURIAuthentication",
            "params": {
                "sasUri": "https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>"
            }
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.connectionString` | O URI SAS necessário para acessar dados em seu armazenamento [!DNL Blob]. O padrão de URI SAS [!DNL Blob] é: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`. |
| `connectionSpec.id` | A ID da especificação de conexão de armazenamento [!DNL Blob] é: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seu armazenamento no próximo tutorial.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão [!DNL Blob] usando APIs e uma ID exclusiva foi obtida como parte do corpo da resposta. Você pode usar essa ID de conexão para [explorar armazenamentos em nuvem usando a API do Serviço de Fluxo](../../explore/cloud-storage.md) ou [assimilar dados do Parquet usando a API do Serviço de Fluxo](../../cloud-storage-parquet.md).
