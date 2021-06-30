---
keywords: Experience Platform, home, tópicos populares, Data Explorer do Azure, Data Explorer do Azure, Data Explorer do Azure
solution: Experience Platform
title: Criar uma Conexão Base de Datas Explorer do Azure usando a API do Serviço de Fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Azure Data Explorer ao Adobe Experience Platform usando a API do Serviço de Fluxo.
exl-id: 1b17bbb0-1f7b-4d89-a158-ad269e6edf30
source-git-commit: 5fb5f0ce8bd03ba037c6901305ba17f8939eb9ce
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 1%

---

# Crie uma conexão base [!DNL Azure Azure Data Explorer] usando a API [!DNL Flow Service]

>[!NOTE]
>
>O conector [!DNL Azure Azure Data Explorer] está em beta. Consulte a [Visão geral das Fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para [!DNL Azure Data Explore] usando a [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).


## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md):  [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes, além de fornecer a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a [!DNL Azure Data Explorer] usando a API [!DNL Flow Service].

### Obter credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL Azure Data Explorer], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `endpoint` | O endpoint do servidor [!DNL Azure Data Explorer]. |
| `database` | O nome do banco de dados [!DNL Azure Data Explorer]. |
| `tenant` | A ID de locatário exclusiva usada para se conectar ao banco de dados [!DNL Azure Data Explorer]. |
| `servicePrincipalId` | A ID da entidade de serviço exclusiva usada para se conectar ao banco de dados [!DNL Azure Data Explorer]. |
| `servicePrincipalKey` | A chave principal de serviço exclusiva usada para se conectar ao banco de dados [!DNL Azure Data Explorer]. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. A ID de especificação de conexão para [!DNL Azure Data Explorer] é `0479cc14-7651-4354-b233-7480606c2ac3`. |

Para obter mais informações sobre a introdução, consulte este [[!DNL Azure Data Explorer] documento](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia sobre como [começar a usar APIs da plataforma](../../../../../landing/api-guide.md).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST ao endpoint `/connections`, fornecendo as credenciais de autenticação [!DNL Azure Data Explorer] como parte dos parâmetros da solicitação.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.endpoint` | O endpoint do servidor [!DNL Azure Data Explorer]. |
| `auth.params.database` | O nome do banco de dados [!DNL Azure Data Explorer]. |
| `auth.params.tenant` | A ID de locatário exclusiva usada para se conectar ao banco de dados [!DNL Azure Data Explorer]. |
| `auth.params.servicePrincipalId` | A ID da entidade de serviço exclusiva usada para se conectar ao banco de dados [!DNL Azure Data Explorer]. |
| `auth.params.servicePrincipalKey` | A chave principal de serviço exclusiva usada para se conectar ao banco de dados [!DNL Azure Data Explorer]. |
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

Ao seguir este tutorial, você criou uma conexão [!DNL Azure Data Explorer] usando a API [!DNL Flow Service] e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial à medida que aprende a [explorar bancos de dados usando a API do Serviço de Fluxo](../../explore/database-nosql.md).
