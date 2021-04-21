---
keywords: Experience Platform, home, tópicos populares, Azure Data Lake Storage Gen2, armazenamento de dados azure no lago, Azure
solution: Experience Platform
title: Criar uma conexão de origem Gen2 do Armazenamento do Azure Data Lake usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform ao Azure Data Lake Storage Gen2 usando a API do Serviço de Fluxo.
exl-id: cad5e2a0-e27c-4130-9ad8-888352c92f04
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 1%

---

# Crie uma conexão de origem [!DNL Azure] Data Lake Storage Gen2 usando a API [!DNL Flow Service]

[!DNL Flow Service] O é usado para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a API [!DNL Flow Service] para orientá-lo pelas etapas para se conectar [!DNL Experience Platform] a [!DNL Azure] Data Lake Storage Gen2 (a seguir chamado &quot;ADLS Gen2&quot;).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md):  [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes, além de fornecer a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para criar com êxito uma conexão de origem ADLS Gen2 usando a API [!DNL Flow Service].

### Obter credenciais necessárias

Para que [!DNL Flow Service] se conecte ao ADLS Gen2, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `url` | O URL do endereço. |
| `servicePrincipalId` | A ID de cliente do aplicativo. |
| `servicePrincipalKey` | A chave do aplicativo. |
| `tenant` | As informações do locatário que contêm seu aplicativo. |

Para obter mais informações sobre esses valores, consulte [este documento ADLS Gen2](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

### Lendo exemplos de chamadas de API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo aqueles pertencentes a [!DNL Flow Service], são isolados para sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* `Content-Type: application/json`

## Criar uma conexão

Uma conexão especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão é necessária por conta ADLS Gen2, pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```http
POST /connections
```

**Solicitação**

Para criar uma conexão ADLS-Gen2, a ID de especificação de conexão exclusiva deve ser fornecida como parte da solicitação POST. A ID de especificação de conexão para ADLS-Gen2 é `0ed90a81-07f4-4586-8190-b40eccef1c5a`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "adls-gen2",
        "description": "Connection for adls-gen2",
        "auth": {
            "specName": "Basic Authentication for adls-gen2",
            "params": {
                "url": "{URL}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
                "tenant": "{TENANT}"
            }
        },
        "connectionSpec": {
            "id": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.url` | O endpoint do URL para sua conta ADLS Gen2. |
| `auth.params.servicePrincipalId` | A ID principal de serviço da sua conta ADLS Gen2. |
| `auth.params.servicePrincipalKey` | A chave principal de serviço da sua conta ADLS Gen2. |
| `auth.params.tenant` | As informações do locatário de sua conta ADLS Gen2. |
| `connectionSpec.id` | A ID de especificação de conexão ADLS Gen2: `0ed90a81-07f4-4586-8190-b40eccef1c5a1`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar o armazenamento em nuvem na próxima etapa.

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão ADLS Gen2 usando APIs e uma ID exclusiva foi obtida como parte do corpo da resposta. Você pode usar essa ID de conexão para [explorar armazenamentos em nuvem usando a API do Serviço de Fluxo](../../explore/cloud-storage.md) ou [assimilar dados do Parquet usando a API do Serviço de Fluxo](../../cloud-storage-parquet.md).
