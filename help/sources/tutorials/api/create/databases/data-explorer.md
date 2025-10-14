---
keywords: Experience Platform;página inicial;tópicos populares;Azure Azure Data Explorer;Azure Data Explorer;Azure Data Explorer
solution: Experience Platform
title: Criar uma conexão básica do Azure Data Explorer usando a API do serviço de fluxo
type: Tutorial
description: Saiba como conectar o Azure Data Explorer ao Adobe Experience Platform usando a API do Serviço de Fluxo.
exl-id: 1b17bbb0-1f7b-4d89-a158-ad269e6edf30
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 4%

---

# Criar uma conexão de base [!DNL Azure Azure Data Explorer] usando a API [!DNL Flow Service]

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial guiará você pelas etapas para criar uma conexão básica para [!DNL Azure Data Explorer] usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).


## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Azure Data Explorer] usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL Azure Data Explorer], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `endpoint` | O ponto de extremidade do servidor [!DNL Azure Data Explorer]. |
| `database` | O nome do banco de dados [!DNL Azure Data Explorer]. |
| `tenant` | A ID de locatário exclusiva usada para conectar ao banco de dados [!DNL Azure Data Explorer]. |
| `servicePrincipalId` | A ID exclusiva da entidade de serviço usada para se conectar ao banco de dados [!DNL Azure Data Explorer]. |
| `servicePrincipalKey` | A chave da entidade de serviço exclusiva usada para se conectar ao banco de dados [!DNL Azure Data Explorer]. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Azure Data Explorer] é `0479cc14-7651-4354-b233-7480606c2ac3`. |

Para obter mais informações sobre a introdução, consulte este [[!DNL Azure Data Explorer] documento](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Experience Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer suas credenciais de autenticação [!DNL Azure Data Explorer] como parte dos parâmetros de solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Azure Data Explorer]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Azure Data Explorer connection",
        "description": "A connection for Azure Azure Data Explorer",
        "auth": {
            "specName": "Service Principal Based Authentication",
            "params": {
                    "endpoint": "{ENDPOINT}",
                    "database": "{DATABASE}",
                    "tenant": "{TENANT}",
                    "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                    "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
                }
        },
        "connectionSpec": {
            "id": "0479cc14-7651-4354-b233-7480606c2ac3",
            "version": "1.0"
        }
    }'
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `auth.params.endpoint` | O ponto de extremidade do servidor [!DNL Azure Data Explorer]. |
| `auth.params.database` | O nome do banco de dados [!DNL Azure Data Explorer]. |
| `auth.params.tenant` | A ID de locatário exclusiva usada para conectar ao banco de dados [!DNL Azure Data Explorer]. |
| `auth.params.servicePrincipalId` | A ID exclusiva da entidade de serviço usada para se conectar ao banco de dados [!DNL Azure Data Explorer]. |
| `auth.params.servicePrincipalKey` | A chave da entidade de serviço exclusiva usada para se conectar ao banco de dados [!DNL Azure Data Explorer]. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Azure Data Explorer]: `0479cc14-7651-4354-b233-7480606c2ac3`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## Próximas etapas

Seguindo este tutorial, você criou uma conexão de base [!DNL Azure Data Explorer] usando a API [!DNL Flow Service]. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando a API  [!DNL Flow Service] &#x200B;](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados do banco de dados para a Experience Platform usando a API  [!DNL Flow Service] &#x200B;](../../collect/database-nosql.md)
