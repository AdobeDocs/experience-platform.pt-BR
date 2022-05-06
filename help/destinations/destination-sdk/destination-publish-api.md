---
description: Esta página lista e descreve todas as operações da API que podem ser realizadas usando o endpoint da API `/authoring/destination/publish`.
title: Publicar operações de endpoint da API de destinos
exl-id: 0564a132-42f4-478c-9197-9b051acf093c
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 5%

---

# Publicar operações da API de ponto de extremidade de Destinos {#publish-destination}

>[!IMPORTANT]
>
>**Ponto de extremidade da API**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Esta página lista e descreve todas as operações de API que você pode executar usando o `/authoring/destinations/publish` Ponto de extremidade da API.

Após configurar e testar seu destino, você pode enviá-lo ao Adobe para análise e publicação. Ler [Enviar para revisão de um destino criado no Destination SDK](./submit-destination.md) para todas as outras etapas, é necessário fazer parte do processo de envio do destino.

Use o endpoint da API de destinos de publicação para enviar uma solicitação de publicação quando:

* Como parceiro de Destination SDK, você deseja disponibilizar o destino produzido em todas as organizações de Experience Platform para que todos os clientes de Experience Platform possam usá-lo;
* Você deseja disponibilizar o destino personalizado em sua própria organização do Experience Platform, em todas as sandboxes.
* Você faz *qualquer atualização* nas suas configurações. As atualizações de configuração são refletidas no destino somente após enviar uma nova solicitação de publicação, que é aprovada pela equipe do Experience Platform.

## Introdução às operações da API de publicação de destino {#get-started}

Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com sucesso, incluindo como obter a permissão de criação de destino necessária e os cabeçalhos necessários.

## Enviar uma configuração de destino para publicação {#create}

Você pode enviar uma configuração de destino para publicação fazendo uma solicitação de POST para a `/authoring/destinations/publish` endpoint .

**Formato da API**

```http
POST /authoring/destinations/publish
```

**Solicitação**

A solicitação a seguir envia um destino para publicação, em todas as organizações configuradas pelos parâmetros fornecidos no payload. A carga abaixo inclui todos os parâmetros aceitos pela `/authoring/destinations/publish` endpoint .

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"ALL"
}
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `destinationId` | String | A ID de destino da configuração de destino que você está enviando para publicação. Obtenha a ID de destino de uma configuração de destino usando o [referência da API de configuração de destino](./destination-configuration-api.md#retrieve-list). |
| `destinationAccess` | String | Use `ALL` para que seu destino apareça no catálogo para todos os clientes do Experience Platform. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 com detalhes da solicitação de publicação de destino.

## Listar solicitações de publicação de destino {#retrieve-list}

Você pode recuperar uma lista de todos os destinos enviados para publicação da sua Organização IMS fazendo uma solicitação de GET para a `/authoring/destinations/publish` endpoint .

**Formato da API**

```http
GET /authoring/destinations/publish
```

**Solicitação**

A solicitação a seguir recupera a lista de destinos enviados para publicação aos quais você tem acesso, com base na Organização IMS e na configuração da sandbox.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A resposta a seguir retorna o status HTTP 200 com uma lista de destinos enviados para publicação aos quais você tem acesso, com base na IMS Organization ID e no nome da sandbox usados. One `configId` corresponde à solicitação de publicação para um destino.

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"123cs780-ce29-434f-921e-4ed6ec2a6c35",
         "allowedOrgs": [
            "*"
         ],    
         "status":"PUBLISHED",
         "destinationType": "PUBLIC",
         "publishedDate":"1630617746"
      }
   ]
}
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `destinationId` | String | A ID de destino da configuração de destino que você enviou para publicação. |
| `publishDetailsList.configId` | String | A ID exclusiva da solicitação de publicação de destino para o destino enviado. |
| `publishDetailsList.allowedOrgs` | String | Retorna as organizações Experience Platform para as quais o destino está disponível. <br> <ul><li> Para `"destinationType": "PUBLIC"`, esse parâmetro retorna `"*"`, o que significa que o destino está disponível para todas as organizações Experience Platform.</li><li> Para `"destinationType": "DEV"`, esse parâmetro retorna a ID da organização usada para criar e testar o destino.</li></ul> |
| `publishDetailsList.status` | String | O status da solicitação de publicação de destino. Os valores possíveis são `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. Destinos com o valor `PUBLISHED` são ativos e podem ser usados por clientes do Experience Platform. |
| `publishDetailsList.destinationType` | String | O tipo de destino. Os valores podem ser `DEV` e `PUBLIC`. `DEV` corresponde ao destino em sua organização Experience Platform. `PUBLIC` corresponde ao destino enviado para publicação. Pense nessas duas opções em termos de Git, onde a variável `DEV` A versão representa a ramificação de criação local e a variável `PUBLIC` representa a ramificação principal remota. |
| `publishDetailsList.publishedDate` | String | A data em que o destino foi enviado para publicação, em época. |

{style=&quot;table-layout:auto&quot;}

## Obter o status de uma solicitação de publicação de destino específica {#get}

Você pode recuperar informações detalhadas sobre uma solicitação de publicação de destino específica fazendo uma solicitação de GET para a `/authoring/destinations/publish` e fornecer a ID do destino para o qual você deseja recuperar o status de publicação.

**Formato da API**

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{DESTINATION_ID}` | A ID do destino para o qual você deseja recuperar o status de publicação. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish/1230e5e4-4ab8-4655-ae1e-a6296b30f2ec \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre a solicitação de publicação de destino especificada.

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"ab41387c0-4772-4709-a3ce-6d5fee654520",
         "allowedOrgs":[
            "716543205DB85F7F0A495E5B@AdobeOrg"
         ],
         "status":"TEST",
         "destinationType":"DEV"
      },
      {
         "configId":"cd568c67-f25e-47e4-b9a2-d79297a20b27",
         "allowedOrgs":[
            "*"
         ],
         "status":"DEPRECATED",
         "destinationType":"PUBLIC",
         "publishedDate":1630525501009
      },
      {
         "configId":"ef6f07154-09bc-4bee-8baf-828ea9c92fba",
         "allowedOrgs":[
            "*"
         ],
         "status":"PUBLISHED",
         "destinationType":"PUBLIC",
         "publishedDate":1630531586002
      }
   ]
}
```

## Tratamento de erros da API

Os pontos de extremidade da API do Destination SDK seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](../../landing/troubleshooting.md#api-status-codes) e [erros do cabeçalho da solicitação](../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas

Após a leitura deste documento, você agora sabe como enviar uma solicitação de publicação para o seu destino. A equipe da Adobe Experience Platform verificará sua solicitação de publicação e retornará a você com cinco dias úteis.
