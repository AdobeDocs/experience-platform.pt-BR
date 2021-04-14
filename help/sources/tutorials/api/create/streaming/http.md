---
keywords: Experience Platform, home, tópicos populares, conexão de transmissão, criar conexão de transmissão, guia de api, tutorial, criar uma conexão de transmissão, assimilação de transmissão, ingestão;
solution: Experience Platform
title: Criar uma conexão de transmissão usando a API
topic: tutorial
type: Tutorial
description: Este tutorial ajudará você a começar a usar APIs de assimilação de streaming, parte das APIs do serviço de assimilação de dados da Adobe Experience Platform.
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
translation-type: tm+mt
source-git-commit: 69abc982c4a820b850096d83761552ca526bca29
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 2%

---


# Criação de uma conexão de transmissão usando a API

O Serviço de fluxo é usado para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a API [!DNL Flow Service] para orientá-lo pelas etapas para criar uma conexão de transmissão usando a API do Serviço de fluxo.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md): O quadro normalizado pelo qual  [!DNL Platform] organiza os dados de experiência.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para as APIs de assimilação de streaming.

### Lendo exemplos de chamadas de API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo aqueles pertencentes a [!DNL Flow Service], são isolados para sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte a [documentação de visão geral da sandbox](../../../../../sandboxes/home.md).

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Criar uma conexão

Uma conexão especifica a fonte e contém as informações necessárias para tornar o fluxo compatível com as APIs de assimilação de streaming. Ao criar uma conexão, você tem a opção de criar uma conexão não autenticada e autenticada.

### Conexão não autenticada

As conexões não autenticadas são a conexão de transmissão padrão que pode ser criada quando você deseja transmitir dados na Plataforma.

**Formato da API**

```http
POST /flowservice/connections
```

**Solicitação**

Para criar uma conexão de transmissão, a ID do provedor e a ID de especificação de conexão devem ser fornecidas como parte da solicitação do POST. A ID do provedor é `521eee4d-8cbe-4906-bb48-fb6bd4450033` e a ID da especificação da conexão é `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

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
| `auth.params.sourceId` | A ID da conexão de transmissão que você deseja criar. |
| `auth.params.dataType` | O tipo de dados para a conexão de transmissão. Esse valor deve ser `xdm`. |
| `auth.params.name` | O nome da conexão de transmissão que deseja criar. |
| `connectionSpec.id` | A especificação de conexão `id` para conexões de transmissão. |

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

As conexões autenticadas devem ser usadas quando for necessário diferenciar entre registros provenientes de fontes confiáveis e não confiáveis. Os usuários que desejam enviar informações com informações de identificação pessoal (PII) devem criar uma conexão autenticada ao transmitir informações para a plataforma.

**Formato da API**

```http
POST /flowservice/connections
```

**Solicitação**

Para criar uma conexão de transmissão, a ID do provedor e a ID de especificação de conexão devem ser fornecidas como parte da solicitação do POST. A ID do provedor é `521eee4d-8cbe-4906-bb48-fb6bd4450033` e a ID da especificação da conexão é `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

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
| `auth.params.sourceId` | A ID da conexão de transmissão que você deseja criar. |
| `auth.params.dataType` | O tipo de dados para a conexão de transmissão. Esse valor deve ser `xdm`. |
| `auth.params.name` | O nome da conexão de transmissão que deseja criar. |
| `auth.params.authenticationRequired` | O parâmetro que especifica a conexão de transmissão criada |
| `connectionSpec.id` | A especificação de conexão `id` para conexões de transmissão. |

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

## Obter URL de ponto de extremidade de fluxo

Com a conexão criada, agora é possível recuperar o URL do terminal de transmissão.

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

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre a conexão solicitada. O URL do ponto de extremidade de transmissão é criado automaticamente com a conexão e pode ser recuperado usando o valor `inletUrl` .

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

Ao seguir este tutorial, você criou uma conexão HTTP de transmissão, permitindo usar o endpoint de transmissão para assimilar dados na plataforma. Para obter instruções para criar uma conexão de transmissão na interface do usuário, leia o [tutorial de conexão de transmissão](../../../ui/create/streaming/http.md).

Para saber como transmitir dados para a Platform, leia o tutorial em [dados da série de tempo de transmissão](../../../../../ingestion/tutorials/streaming-time-series-data.md) ou o tutorial em [dados de registro de transmissão](../../../../../ingestion/tutorials/streaming-record-data.md).

## Apêndice

Esta seção fornece informações complementares sobre como criar conexões de transmissão usando a API.

### Envio de mensagens para uma conexão de transmissão autenticada

Se uma conexão de transmissão tiver a autenticação ativada, o cliente deverá adicionar o cabeçalho `Authorization` à solicitação.

Se o cabeçalho `Authorization` não estiver presente ou um token de acesso inválido/expirado for enviado, uma resposta HTTP 401 Não autorizado será retornada, com uma resposta semelhante como abaixo:

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
