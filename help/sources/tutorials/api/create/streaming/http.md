---
keywords: Experience Platform;home;popular topics;conexão de transmissão;criar conexão de transmissão;guia de API;tutorial;criar uma conexão de transmissão;ingestão de transmissão;;home;popular topics;streaming connection;create streaming connection;api guide;tutorial;create a streaming connection;streaming ingestion;ingestão;ingestão;
solution: Experience Platform
title: Criar uma conexão de fluxo usando a API
topic: tutorial
type: Tutorial
description: Este tutorial o ajudará a começar a usar APIs de ingestão de streaming, parte das APIs do Adobe Experience Platform Data Ingestion Service.
translation-type: tm+mt
source-git-commit: 5932d63820dd0e50acccd18573746061232e099e
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 2%

---


# Criação de uma conexão de streaming usando a API

O Serviço de fluxo é usado para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a API [!DNL Flow Service] para guiá-lo pelas etapas para criar uma conexão de streaming usando a API de Serviço de Fluxo.

## Introdução

Este guia exige uma compreensão prática dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md): O quadro normalizado através do qual  [!DNL Platform] organiza os dados da experiência.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil unificado e de consumidor em tempo real, com base em dados agregados de várias fontes.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para as APIs de ingestão de streaming.

### Lendo chamadas de exemplo da API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção em [como ler chamadas de API de exemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo os pertencentes a [!DNL Flow Service], são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a [documentação de visão geral da caixa de proteção](../../../../../sandboxes/home.md).

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Criar uma conexão

Uma conexão especifica a fonte e contém as informações necessárias para tornar o fluxo compatível com as APIs de ingestão de streaming. Ao criar uma conexão, você tem a opção de criar uma conexão não autenticada e autenticada.

### Conexão não autenticada

As conexões não autenticadas são a conexão de streaming padrão que você pode criar quando quiser transmitir dados na Plataforma.

**Formato da API**

```http
POST /flowservice/connections
```

**Solicitação**

Para criar uma conexão de fluxo contínuo, a ID do provedor e a ID da especificação da conexão devem ser fornecidas como parte da solicitação do POST. A ID do provedor é `521eee4d-8cbe-4906-bb48-fb6bd4450033` e a ID da especificação da conexão é `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection"
         }
     }
 }
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.sourceId` | A ID da conexão de streaming que você deseja criar. |
| `auth.params.dataType` | O tipo de dados para a conexão de streaming. Esse valor deve ser `xdm`. |
| `auth.params.name` | O nome da conexão de streaming que você deseja criar. |
| `connectionSpec.id` | A especificação de conexão `id` para conexões de streaming. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 com detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`).

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | O `id` da conexão recém-criada. Isso será chamado de `{CONNECTION_ID}`. |
| `etag` | Um identificador atribuído à conexão, especificando a revisão da conexão. |

### Conexão autenticada

As conexões autenticadas devem ser usadas quando for necessário diferenciar entre registros provenientes de fontes confiáveis e não confiáveis. Os usuários que desejam enviar informações com PII (Personally Identifier Information, Informações pessoais identificáveis) devem criar uma conexão autenticada ao transmitir as informações à plataforma.

**Formato da API**

```http
POST /flowservice/connections
```

**Solicitação**

Para criar uma conexão de fluxo contínuo, a ID do provedor e a ID da especificação da conexão devem ser fornecidas como parte da solicitação do POST. A ID do provedor é `521eee4d-8cbe-4906-bb48-fb6bd4450033` e a ID da especificação da conexão é `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection",
             "authenticationRequired": true
         }
     }
 }
```


| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.sourceId` | A ID da conexão de streaming que você deseja criar. |
| `auth.params.dataType` | O tipo de dados para a conexão de streaming. Esse valor deve ser `xdm`. |
| `auth.params.name` | O nome da conexão de streaming que você deseja criar. |
| `auth.params.authenticationRequired` | O parâmetro que especifica a conexão de streaming criada |
| `connectionSpec.id` | A especificação de conexão `id` para conexões de streaming. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 com detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`).

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | O `id` da conexão recém-criada. Isso será chamado de `{CONNECTION_ID}`. |
| `etag` | Um identificador atribuído à conexão, especificando a revisão da conexão. |

## Obter URL de ponto de extremidade de streaming

Com a conexão criada, agora é possível recuperar o URL do ponto de extremidade de streaming.

**Formato da API**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{CONNECTION_ID}` | O valor `id` da conexão criada anteriormente. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre a conexão solicitada. O URL do ponto de extremidade de streaming é criado automaticamente com a conexão e pode ser recuperado usando o valor `inletUrl`.

```json
{
    "items": [
        {
            "createdAt": 1583971856947,
            "updatedAt": 1583971856947,
            "createdBy": "{API_KEY}",
            "updatedBy": "{API_KEY}",
            "createdClient": "{USER_ID}",
            "updatedClient": "{USER_ID}",
            "id": "77a05521-91d6-451c-a055-2191d6851c34",
            "name": "Another new sample connection (Experience Event)",
            "description": "Sample description",
            "connectionSpec": {
                "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Streaming Connection",
                "params": {
                    "sourceId": "Sample connection (ExperienceEvent)",
                    "inletUrl": "https://dcs.adobedc.net/collection/a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "inletId": "a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "dataType": "xdm",
                    "name": "Sample connection (ExperienceEvent)"
                }
            },
            "version": "\"56008aee-0000-0200-0000-5e697e150000\"",
            "etag": "\"56008aee-0000-0200-0000-5e697e150000\""
        }
    ]
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão HTTP de streaming, permitindo que você use o terminal de streaming para assimilar dados na Plataforma. Para obter instruções sobre como criar uma conexão de streaming na interface do usuário, leia o tutorial [criação de uma conexão de streaming](../../../ui/create/streaming/http.md).

Para saber como transmitir dados para a Plataforma, leia o tutorial em [streaming time series data](../../../../../ingestion/tutorials/streaming-time-series-data.md) ou o tutorial em [streaming record data](../../../../../ingestion/tutorials/streaming-record-data.md).

## Apêndice

Esta seção fornece informações complementares sobre a criação de conexões de fluxo contínuo usando a API.

### Envio de mensagens para uma conexão de streaming autenticada

Se uma conexão de streaming tiver a autenticação ativada, o cliente será solicitado a adicionar o cabeçalho `Authorization` à solicitação.

Se o cabeçalho `Authorization` não estiver presente, ou um token de acesso inválido/expirado for enviado, uma resposta HTTP 401 Não autorizado será retornada, com uma resposta semelhante como a seguir:

**Resposta**

```json
{
    "type": "https://ns.adobe.com/adobecloud/problem/data-collection-service-authorization",
    "status": "401",
    "title": "Authorization",
    "report": {
        "message": "[id] Ims service token is empty"
    }
}
```
