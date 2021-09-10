---
description: Esta página lista e descreve todas as operações da API que podem ser realizadas usando o endpoint da API `/authoring/destination/publish`.
title: Publicar operações de endpoint da API de destinos
exl-id: 0564a132-42f4-478c-9197-9b051acf093c
source-git-commit: 9be8636b02a15c8f16499172289413bc8fb5b6f0
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 5%

---

# Publicar operações da API de ponto de extremidade de Destinos {#publish-destination}

>[!IMPORTANT]
>
>**Ponto de extremidade** da API:  `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Esta página lista e descreve todas as operações de API que podem ser executadas usando o endpoint da API `/authoring/destinations/publish`.

Após configurar e testar seu destino, você pode enviá-lo ao Adobe para análise e publicação.

Use o endpoint da API de destinos de publicação para enviar uma solicitação de publicação quando:
* Como parceiro de SDK de destino, você deseja disponibilizar o destino produzido em todas as organizações do Experience Platform para que todos os clientes do Experience Platform usem;
* Você deseja disponibilizar o destino personalizado em sua própria organização do Experience Platform, em todas as sandboxes.

## Introdução às operações da API de publicação de destino {#get-started}

Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com êxito, incluindo como obter a permissão de criação de destino necessária e os cabeçalhos necessários.

## Enviar uma configuração de destino para publicação {#create}

É possível enviar uma configuração de destino para publicação, fazendo uma solicitação de POST ao endpoint `/authoring/destinations/publish`.

**Formato da API**


```http
POST /authoring/destinations/publish
```

**Solicitação**

A solicitação a seguir envia um destino para publicação, em todas as organizações configuradas pelos parâmetros fornecidos no payload. A carga abaixo inclui todos os parâmetros aceitos pelo ponto de extremidade `/authoring/destinations/publish`.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"LIMITED",
   "allowedOrgs":[
      "xyz@AdobeOrg",
      "lmn@AdobeOrg"
   ]
}
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `destinationId` | String | A ID de destino da configuração de destino que você está enviando para publicação. Obtenha a ID de destino de uma configuração de destino usando a [referência da API de configuração de destino](./destination-configuration-api.md#retrieve-list). |
| `destinationAccess` | String | `ALL` ou `LIMITED`. Especifique se deseja que seu destino apareça no catálogo para todos os clientes do Experience Platform ou apenas para determinadas organizações. <br> **Observação**: Se você usar  `LIMITED`, o destino será publicado somente para sua organização do Experience Platform. Se desejar publicar o destino em um subconjunto de organizações do Experience Platform para fins de teste do cliente, entre em contato com o suporte ao Adobe. |
| `allowedOrgs` | String | Se você usar `"destinationAccess":"LIMITED"`, especifique as organizações de Experience Platform para as quais o destino estará disponível. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 com detalhes da solicitação de publicação de destino.

## Listar solicitações de publicação de destino {#retrieve-list}

Você pode recuperar uma lista de todos os destinos enviados para publicação da Organização IMS fazendo uma solicitação de GET para o endpoint `/authoring/destinations/publish`.

**Formato da API**


```http
GET /authoring/destinations/publish
```

**Solicitação**

A solicitação a seguir recuperará a lista de destinos enviados para publicação aos quais você tem acesso, com base na Organização IMS e na configuração da sandbox.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A resposta a seguir retorna o status HTTP 200 com uma lista de destinos enviados para publicação aos quais você tem acesso, com base na IMS Organization ID e no nome da sandbox usados. Um `configId` corresponde à solicitação de publicação para um destino.

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"string",
         "allowedOrgs":[
            "xyz@AdobeOrg",
            "lmn@AdobeOrg"
         ],
         "status":"TEST",
         "publishedDate":"1630617746"
      }
   ]
}
    
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `destinationId` | String | A ID de destino da configuração de destino que você enviou para publicação. |
| `publishDetailsList.configId` | String | A ID exclusiva da solicitação de publicação de destino para o destino enviado. |
| `publishDetailsList.allowedOrgs` | String | Retorna as organizações Experience Platform para as quais o destino deve estar disponível. |
| `publishDetailsList.status` | String | O status da solicitação de publicação de destino. Os valores possíveis são `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. |
| `publishDetailsList.publishedDate` | String | A data em que o destino foi enviado para publicação, em época. |

{style=&quot;table-layout:auto&quot;}

## Atualizar uma solicitação de publicação de destino existente {#update}

Você pode atualizar as organizações permitidas em uma solicitação de publicação de destino existente, fazendo uma solicitação de PUT ao endpoint `/authoring/destinations/publish` e fornecendo a ID do destino para o qual deseja atualizar as organizações permitidas. No corpo da chamada , forneça as organizações permitidas atualizadas.

**Formato da API**


```http
PUT /authoring/destinations/publish/{DESTINATION_ID}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{DESTINATION_ID}` | A ID do destino para o qual você deseja atualizar a solicitação de publicação. |

**Solicitação**

A solicitação a seguir atualiza uma solicitação de publicação de destino existente, configurada pelos parâmetros fornecidos no payload. Na chamada de exemplo abaixo, estamos atualizando as organizações permitidas.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/publish/1230e5e4-4ab8-4655-ae1e-a6296b30f2ec \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"LIMITED",
   "allowedOrgs":[
      "abc@AdobeOrg",
      "def@AdobeOrg"
   ]
}
```

## Obter o status de uma solicitação de publicação de destino específica {#get}

Você pode recuperar informações detalhadas sobre uma solicitação de publicação de destino específica fazendo uma solicitação de GET para o endpoint `/authoring/destinations/publish` e fornecendo a ID do destino para o qual deseja recuperar o status de publicação.

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
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
         "configId":"string",
         "allowedOrgs":[
            "xyz@AdobeOrg",
            "lmn@AdobeOrg"
         ],
         "status":"TEST",
         "publishedDate":"string"
      }
   ]
}
```

## Tratamento de erros da API

Os pontos de extremidade da API do SDK de destino seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) e [erros do cabeçalho da solicitação](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas

Após a leitura deste documento, você agora sabe como enviar uma solicitação de publicação para o seu destino. A equipe da Adobe Experience Platform verificará sua solicitação de publicação e retornará a você com cinco dias úteis.
