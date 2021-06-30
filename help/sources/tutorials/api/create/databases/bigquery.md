---
keywords: Experience Platform, home, tópicos populares, bigquery, Google, Google, BigQuery do Google
solution: Experience Platform
title: Criar uma conexão básica do Google BigQuery usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform ao Google BigQuery usando a API de Serviço de Fluxo.
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: e8c6620a6d2447a577bd56192030ff4353c62c62
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 1%

---

# Crie uma conexão base [!DNL Google BigQuery] usando a API [!DNL Flow Service]

>[!NOTE]
>
>O conector [!DNL Google BigQuery] está em beta. Consulte a [Visão geral das Fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para [!DNL Google BigQuery] (a seguir chamada &quot;[!DNL BigQuery]&quot;) usando a [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md):  [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes, além de fornecer a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a [!DNL BigQuery] usando a API [!DNL Flow Service].

### Obter credenciais necessárias

Para que [!DNL Flow Service] se conecte [!DNL BigQuery] à Plataforma, você deve fornecer os seguintes valores de autenticação OAuth 2.0:

| Credencial | Descrição |
| ---------- | ----------- |
| `project` | A ID do projeto [!DNL BigQuery] padrão para o qual consultar. |
| `clientID` | O valor da ID usado para gerar o token de atualização. |
| `clientSecret` | O valor secreto usado para gerar o token de atualização. |
| `refreshToken` | O token de atualização obtido de [!DNL Google] usado para autorizar o acesso a [!DNL BigQuery]. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. A ID de especificação de conexão para [!DNL BigQuery] é: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

Para obter mais informações sobre esses valores, consulte este [[!DNL BigQuery] documento](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia sobre como [começar a usar APIs da plataforma](../../../../../landing/api-guide.md).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST ao endpoint `/connections`, fornecendo as credenciais de autenticação [!DNL BigQuery] como parte dos parâmetros da solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL BigQuery]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery connection",
        "description": "Google BigQuery connection",
        "auth": {
            "specName": "Basic Authentication",
            "type": "OAuth2.0",
            "params": {
                    "project": "{PROJECT}",
                    "clientId": "{CLIENT_ID},
                    "clientSecret": "{CLIENT_SECRET}",
                    "refreshToken": "{REFRESH_TOKEN}"
                }
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `auth.params.project` | A ID do projeto padrão [!DNL BigQuery] a ser consultado. contra. |
| `auth.params.clientId` | O valor da ID usado para gerar o token de atualização. |
| `auth.params.clientSecret` | O valor do cliente usado para gerar o token de atualização. |
| `auth.params.refreshToken` | O token de atualização obtido de [!DNL Google] usado para autorizar o acesso a [!DNL BigQuery]. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Google BigQuery]: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão [!DNL BigQuery] usando a API [!DNL Flow Service] e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID de conexão no próximo tutorial à medida que aprende a [explorar bancos de dados ou sistemas NoSQL usando a API do Serviço de Fluxo](../../explore/database-nosql.md).
