---
keywords: Experience Platform;página inicial;tópicos populares;Azure Data Lake Storage Gen2;azure data lake storage;;home;popular topics;Azure Data Lake Storage Gen2;azure data lake storage;Azure
solution: Experience Platform
title: Criar uma conexão básica Gen2 de armazenamento do Azure Data Lake usando a API do serviço de fluxo
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform ao Azure Data Lake Storage Gen2 usando a API do Serviço de Fluxo.
exl-id: cad5e2a0-e27c-4130-9ad8-888352c92f04
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 4%

---

# Criar uma conexão de base [!DNL Azure Data Lake Storage Gen2] usando a API [!DNL Flow Service]

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial guiará você pelas etapas para criar uma conexão básica para [!DNL Azure Data Lake Storage Gen2] (doravante chamada de &quot;ADLS Gen2&quot;) usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para criar com êxito uma conexão de origem ADLS Gen2 usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Para que [!DNL Flow Service] se conecte ao ADLS Gen2, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `url` | O endpoint para ADLS Gen2. O padrão do ponto de extremidade é: `https://<accountname>.dfs.core.windows.net`. |
| `servicePrincipalId` | A ID do cliente do aplicativo. |
| `servicePrincipalKey` | A chave do aplicativo. |
| `tenant` | As informações de locatário que contêm seu aplicativo. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID de especificação de conexão para ADLS Gen2 é: `b3ba5556-48be-44b7-8b85-ff2b69b46dc4`. |

Para obter mais informações sobre esses valores, consulte [este documento do ADLS Gen2](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Experience Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` enquanto fornece suas credenciais de autenticação ADLS Gen2 como parte dos parâmetros de solicitação.

**Formato da API**

```http
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para o ADLS Gen2:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.url` | O endpoint do URL da sua conta ADLS Gen2. |
| `auth.params.servicePrincipalId` | A ID da entidade de serviço da sua conta ADLS Gen2. |
| `auth.params.servicePrincipalKey` | A chave da entidade de serviço da sua conta ADLS Gen2. |
| `auth.params.tenant` | As informações de locatário da sua conta ADLS Gen2. |
| `connectionSpec.id` | A ID de especificação da conexão ADLS Gen2: `b3ba5556-48be-44b7-8b85-ff2b69b46dc41`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## Próximas etapas

Seguindo este tutorial, você criou uma conexão ADLS Gen2 usando APIs e uma ID exclusiva foi obtida como parte do corpo da resposta. Você pode usar esta ID de conexão para [explorar armazenamentos em nuvem usando a API de Serviço de Fluxo](../../explore/cloud-storage.md).
