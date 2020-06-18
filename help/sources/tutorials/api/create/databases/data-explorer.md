---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector do Azure Data Explorer usando a API do Serviço de Fluxo
topic: overview
translation-type: tm+mt
source-git-commit: e4ed6ae3ee668cd0db741bd07d2fb7be593db4c9
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 1%

---


# Criar um conector do Azure Data Explorer usando a API do Serviço de Fluxo

>[!NOTE]
>O conector do Azure Data Explorer está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

O Serviço de fluxo é usado para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a API de Serviço de Fluxo para guiá-lo pelas etapas para conectar o Azure Data Explorer (a seguir denominado &quot;Data Explorer&quot;) ao Experience Platform.

## Introdução

Este guia exige uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, ao mesmo tempo em que lhe fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços Platform.
* [Caixas de proteção](../../../../../sandboxes/home.md): O Experience Platform fornece caixas de proteção virtuais que particionam uma única instância do Platform em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao Data Explorer usando a API de Serviço de Fluxo.

### Reunir credenciais obrigatórias

Para que o Serviço de Fluxo se conecte ao Data Explorer, é necessário fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `endpoint` | O terminal do servidor do Data Explorer. |
| `database` | O nome do banco de dados do Data Explorer. |
| `tenant` | A ID de locatário exclusiva usada para conectar-se ao banco de dados do Data Explorer. |
| `servicePrincipalId` | A ID de principal de serviço exclusiva usada para conectar-se ao banco de dados do Data Explorer. |
| `servicePrincipalKey` | A chave principal de serviço exclusiva usada para conectar-se ao banco de dados do Data Explorer. |
| `connectionSpec.id` | O identificador exclusivo necessário para criar uma conexão. A ID da especificação de conexão para o Data Explorer é `0479cc14-7651-4354-b233-7480606c2ac3`. |

Para obter mais informações sobre como começar, consulte [este documento](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad)do Data Explorer.

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de solução de problemas do Experience Platform.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para as APIs da Platform, você deve primeiro concluir o tutorial [de](../../../../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API de Experience Platform, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos no Experience Platform, incluindo os pertencentes ao Serviço de Fluxo, são isolados para caixas de proteção virtuais específicas. Todas as solicitações às APIs do Platform exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

## Criar uma conexão

Uma conexão especifica uma fonte e contém suas credenciais para essa fonte. Somente um conector é necessário por conta do Data Explorer, pois pode ser usado para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```http
POST /connections
```

**Solicitação**

Para criar uma conexão com o Data Explorer, sua ID exclusiva de especificação de conexão deve ser fornecida como parte da solicitação POST. A ID da especificação de conexão para o Data Explorer é `0479cc14-7651-4354-b233-7480606c2ac3`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Data Explorer connection",
        "description": "A connection for Azure Data Explorer",
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
| `auth.params.endpoint` | O terminal do servidor do Data Explorer. |
| `auth.params.database` | O nome do banco de dados do Data Explorer. |
| `auth.params.tenant` | A ID de locatário exclusiva usada para conectar-se ao banco de dados do Data Explorer. |
| `auth.params.servicePrincipalId` | A ID de principal de serviço exclusiva usada para conectar-se ao banco de dados do Data Explorer. |
| `auth.params.servicePrincipalKey` | A chave principal de serviço exclusiva usada para conectar-se ao banco de dados do Data Explorer. |
| `connectionSpec.id` | A ID de especificação da conexão do Data Explorer: `0479cc14-7651-4354-b233-7480606c2ac3`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão com o Data Explorer usando a API de Serviço de Fluxo e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial à medida que aprende a [explorar bancos de dados usando a API](../../explore/database-nosql.md)do Serviço de Fluxo.
