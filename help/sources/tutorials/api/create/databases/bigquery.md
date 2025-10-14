---
title: Conecte O Google BigQuery Ao Experience Platform Usando A API Do Serviço De Fluxo
description: Saiba como conectar o Adobe Experience Platform ao Google BigQuery usando a API de serviço de fluxo.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 2%

---

# Conectar o [!DNL Google BigQuery] ao Experience Platform usando a API [!DNL Flow Service]

>[!IMPORTANT]
>
>A origem [!DNL Google BigQuery] está disponível no catálogo de origens para usuários que compraram o Real-Time Customer Data Platform Ultimate.

Leia este guia para saber como conectar seu banco de dados do [!DNL Google BigQuery] ao Adobe Experience Platform usando a [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

### Coletar credenciais necessárias

Leia o [[!DNL Google BigQuery] guia de autenticação](../../../../connectors/databases/bigquery.md#prerequisites) para obter as etapas detalhadas sobre como recuperar suas credenciais do [!DNL Google BigQuery].

## Conectar [!DNL Google BigQuery] ao Experience Platform no Azure {#azure}

Leia as etapas abaixo para obter informações sobre como conectar sua origem do [!DNL Google BigQuery] à Experience Platform no Azure.

### Criar uma conexão base para [!DNL Google BigQuery] no Experience Platform no Azure {#azure-base}

Uma conexão base retém informações entre sua origem e a Experience Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer suas credenciais de autenticação [!DNL Google BigQuery] como parte dos parâmetros de solicitação.

**Formato da API**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB Usar autenticação básica]

+++Solicitação

A solicitação a seguir cria uma conexão base para [!DNL Google BigQuery] usando autenticação básica.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery connection with basic authentication",
        "description": "Google BigQuery connection with basic authentication",
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
| `auth.params.project` | A ID do projeto [!DNL Google BigQuery] padrão a ser consultado. contra. |
| `auth.params.clientId` | O valor de ID usado para gerar o token de atualização. |
| `auth.params.clientSecret` | O valor do cliente usado para gerar o token de atualização. |
| `auth.params.refreshToken` | O token de atualização obtido de [!DNL Google] usado para autorizar o acesso a [!DNL Google BigQuery]. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Google BigQuery]: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

+++

+++Resposta

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

+++

>[!TAB Usar autenticação de serviço]


+++Solicitação

A solicitação a seguir cria uma conexão base para [!DNL Google BigQuery] usando autenticação de serviço:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google BigQuery base connection with service account",
      "description": "Google BigQuery connection with service account",
      "auth": {
          "specName": "Service Authentication",
          "params": {
                  "projectId": "{PROJECT_ID}",
                  "keyFileContent": "{KEY_FILE_CONTENT},
                  "largeResultsDataSetId": "{LARGE_RESULTS_DATASET_ID}"
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
| `auth.params.projectId` | A ID do projeto [!DNL Google BigQuery] padrão a ser consultado. contra. |
| `auth.params.keyFileContent` | O arquivo de chave usado para autenticar a conta de serviço. Você deve codificar o conteúdo do arquivo de chave em [!DNL Base64]. |
| `auth.params.largeResultsDataSetId` | (Opcional) A ID do conjunto de dados [!DNL Google BigQuery] pré-criada que é necessária para habilitar o suporte para grandes conjuntos de resultados. |

+++

+++Resposta

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

+++

>[!ENDTABS]

## Conectar o [!DNL Google BigQuery] ao Experience Platform no Amazon Web Services (AWS) {#aws}

Leia as etapas abaixo para obter informações sobre como conectar o banco de dados do [!DNL Google BigQuery] ao Experience Platform no AWS.

### Criar uma conexão base para [!DNL Google BigQuery] no Experience Platform no AWS

>[!AVAILABILITY]
>
>Esta seção se aplica às implementações do Experience Platform em execução no Amazon Web Services (AWS). O Experience Platform em execução no AWS está disponível atualmente para um número limitado de clientes. Para saber mais sobre a infraestrutura do Experience Platform compatível, consulte a [visão geral da nuvem múltipla do Experience Platform](../../../../../landing/multi-cloud.md).

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão básica para conectar [!DNL Google BigQuery] ao Experience Platform no AWS.

+++Selecione para exibir o exemplo

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google BigQuery base connection on AWS",
      "description": "Google BigQuery base connection on AWS",
      "auth": {
          "specName": "Service Authentication",
          "params": {
                  "projectId": "{PROJECT_ID}",
                  "keyFileContent": "{KEY_FILE_CONTENT},
                  "datasetId": "{DATASET_ID}"
      },
      "connectionSpec": {
          "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `auth.params.projectId` | A ID do projeto [!DNL Google BigQuery] padrão a ser consultado. contra. |
| `auth.params.keyFileContent` | O arquivo de chave usado para autenticar a conta de serviço. Você deve codificar o conteúdo do arquivo de chave em [!DNL Base64]. |
| `auth.params.datasetId` | A ID do conjunto de dados que corresponde à sua origem [!DNL Google BigQuery]. Essa ID representa onde as tabelas de dados estão localizadas. |

+++

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seu armazenamento no próximo tutorial.

+++Selecione para exibir o exemplo

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

+++

## Próximas etapas

Seguindo este tutorial, você criou uma conexão de base [!DNL Google BigQuery] usando a API [!DNL Flow Service]. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando a API  [!DNL Flow Service] &#x200B;](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados do banco de dados para a Experience Platform usando a API  [!DNL Flow Service] &#x200B;](../../collect/database-nosql.md)
