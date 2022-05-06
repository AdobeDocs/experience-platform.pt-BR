---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, guia de api, serviço de query, contas do serviço de query, contas;
solution: Experience Platform
title: Endpoint da API de contas
topic-legacy: connection parameters
description: Você pode criar uma conta do Serviço de query para persistente .
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 5%

---

# Ponto de extremidade de contas

No Adobe Experience Platform Query Service, as contas são usadas para criar credenciais que não expiram e que você pode usar com clientes SQL externos. Você pode usar o `/accounts` endpoint na API do Serviço de query, que permite criar, recuperar, editar e excluir programaticamente suas contas de integração do Serviço de query (também conhecidas como uma conta técnica).

## Introdução

Os endpoints usados neste guia fazem parte da API do Serviço de query. Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com sucesso, incluindo cabeçalhos necessários e como ler chamadas de API de exemplo.

## Criar uma conta

Você pode criar uma conta de integração do Serviço de consulta, fazendo uma solicitação de POST para a `/accounts` endpoint .

**Formato da API**

```http
POST /accounts
```

**Solicitação**

A solicitação a seguir criará uma nova conta de integração do Serviço de query para sua organização IMS.

```shell
curl -X POST https://platform.adobe.io/data/foundation/queryauth/accounts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
{
    "accountName": "sampleName",
    "assignedToUser": "sample@example.com",
    "credential": "samplecredential",
    "description": "Sample description"
}'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `accountName` | **Obrigatório** O nome da conta de integração do Serviço de Consulta. |
| `assignedToUser` | **Obrigatório** A Adobe ID para a qual a conta de integração do Serviço de query será criada. |
| `credential` | *(Opcional)* A credencial usada para a integração do Serviço de query. Se não for especificado, o sistema gerará automaticamente uma credencial para você. |
| `description` | *(Opcional)* Uma descrição para a conta de integração do Serviço de query. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200, com detalhes da sua conta de integração do Serviço de Consulta recém-criada. Você pode usar esses detalhes de conta para conectar o Serviço de query com clientes externos.

```json
{
    "technicalAccountName": "2428A037-D963-47C2-A14D-CD816EFB0AA3@TECHACCT.ADOBE.COM",
    "technicalAccountId": "E09A0DFB5FDB25D90A494012",
    "credential": "samplecredential"
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `technicalAccountName` | O nome da sua conta de integração do Serviço de query. |
| `technicalAccountId` | A ID da sua conta de integração do Serviço de query. Isso junto com a variável `credential`, compõe sua senha para sua conta do . |
| `credential` | A credencial da conta de integração do Serviço de query. Isso junto com a variável `technicalAccountId`, compõe sua senha para sua conta do . |

## Atualizar uma conta

Você pode atualizar sua conta de integração do Serviço de query fazendo uma solicitação de PUT para o `/accounts` endpoint .

**Formato da API**

```http
POST /accounts/{ACCOUNT_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{ACCOUNT_ID}` | A ID da conta de integração do Serviço de query que você deseja atualizar. |

**Solicitação**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/queryauth/accounts/E09A0DFB5FDB25D90A494012 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
     "accountName": "Updated account name",
     "assignedToUser": "sampleuser2@adobe.com",
     "credential": "UpdatedCredential",
     "description": "Updated description"
 }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `accountName` | *(Opcional)* O nome atualizado da conta de integração do Serviço de Consulta. |
| `assignedToUser` | *(Opcional)* A Adobe ID atualizada à qual a conta de integração do Serviço de query está vinculada. |
| `credential` | *(Opcional)* A credencial atualizada para sua conta do Serviço de query. |
| `description` | *(Opcional)* A descrição atualizada da conta de integração do Serviço de Consulta. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações sobre sua conta de integração do Serviço de Consulta recém-atualizada.

```json
{
    "accountName": "Updated account name",
    "assignedToUser": "sampleuser2@adobe.com",
    "created": "2021-06-16T16:44:42.073Z",
    "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
    "credential": "UpdatedCredential",
    "description": "Updated description",
    "lastUpdated": "2021-08-03T23:47:46.588Z",
    "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
    "technicalAccountName": "2428A037-D963-47C2-A14D-CD816EFB0AA3@TECHACCT.ADOBE.COM",
    "technicalAccountId": "E09A0DFB5FDB25D90A494012"
}
```

## Listar todas as contas

Você pode recuperar uma lista de todas as contas de integração do Serviço de query fazendo uma solicitação do GET para a `/accounts` endpoint .

**Formato da API**

```http
GET /accounts
```

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/foundation/queryauth/accounts \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de todas as contas de integração do Serviço de query.

```json
{
    "accounts": [
        {
            "lastUpdated": "2021-06-16T18:07:49.581Z",
            "accountName": "Use for XQL testing of account creation",
            "description": "Local test",
            "assignedToUser": "platform-ui-automation@adobe.com",
            "technicalAccountName": "ADC7EB19-63B4-4B9F-A192-EBE3CD0C034E@TECHACCT.ADOBE.COM",
            "technicalAccountId": "38645A7360CA3DF30A49400F",
            "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "created": "2021-06-16T18:07:49.581Z",
            "active": true
        },
        {
            "lastUpdated": "2021-06-16T16:44:42.073Z",
            "accountName": "Use for XQL testing of account creation",
            "description": " ",
            "assignedToUser": "platform-ui-automation@adobe.com",
            "technicalAccountName": "66E91FDD-4733-45E2-A312-D87580CFA55D@TECHACCT.ADOBE.COM",
            "technicalAccountId": "392202E060CA2A770A49420A",
            "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "created": "2021-06-16T16:44:42.073Z",
            "active": true
        }
    ],
    "_page": {
        "count": 2,
        "next": "2021-06-16T16:44:42.073Z",
        "orderby": "-created",
        "property": "active==true",
        "start": "2021-06-16T18:07:49.581Z"
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/queryauth/accounts?orderby=-created&property=active==true&start=2021-06-16T16:44:42.073Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/queryauth/accounts?orderby=-created&property=active==true&start=2021-06-16T18:07:49.581Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

## Excluir uma conta

Você pode excluir sua conta de integração do Serviço de query fazendo uma solicitação de DELETE para a `/accounts` endpoint .

**Formato da API**

```http
DELETE /accounts/{ACCOUNT_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{ACCOUNT_ID}` | A ID da conta de integração do Serviço de Consulta que você deseja excluir. |

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/queryauth/accounts/E09A0DFB5FDB25D90A494012 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma mensagem informando que a conta foi excluída com êxito.

```json
{
    "result": "Success"
}
```
