---
description: Esta página exemplifica a chamada de API usada para recuperar detalhes sobre uma solicitação de publicação de destino por meio do Adobe Experience Platform Destination SDK.
title: Recuperar uma solicitação de publicação de destino
exl-id: fceef12d-a52c-4259-a91e-7af88b132800
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 2%

---

# Recuperar uma solicitação de publicação de destino

>[!IMPORTANT]
>
>Você só precisará usar esse endpoint de API se estiver enviando um destino produtizado (público), para ser usado por outros clientes do Experience Platform. Se você estiver criando um destino privado para uso próprio, não será necessário enviar formalmente o destino usando a API de publicação.

>[!IMPORTANT]
>
>**Ponto de extremidade de API**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Depois de configurar e testar seu destino, você pode enviá-lo ao Adobe para revisão e publicação. Leia [Enviar para revisão um destino criado em Destination SDK](../guides/submit-destination.md) para todas as outras etapas que você deve realizar como parte do processo de envio do destino.

Use o endpoint da API de destinos de publicação para enviar uma solicitação de publicação quando:

* Como parceiro de Destination SDK, você deseja disponibilizar seu destino produzido em todas as organizações de Experience Platform para que todos os clientes de Experience Platform usem;
* Você faz *quaisquer atualizações* para suas configurações. As atualizações de configuração são refletidas no destino somente após o envio de uma nova solicitação de publicação, que é aprovada pela equipe do Experience Platform.

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros suportados pelo Destination SDK fazem **distinção entre maiúsculas e minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações de API de publicação de destino {#get-started}

Antes de continuar, consulte o [guia de introdução](../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Listar solicitações de publicação de destino {#retrieve-list}

Você pode recuperar uma lista de todos os destinos enviados para publicação para sua Organização IMS fazendo uma solicitação GET para o ponto de extremidade `/authoring/destinations/publish`.

**Formato da API**

Use o formato de API a seguir para recuperar todas as solicitações de publicação da sua conta.

```http
GET /authoring/destinations/publish
```

Use o formato de API a seguir para recuperar uma solicitação de publicação específica, definida pelo parâmetro `{DESTINATION_ID}`.

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

**Solicitação**

As duas solicitações a seguir recuperam todas as solicitações de publicação para sua Organização IMS ou uma solicitação de publicação específica, dependendo se você passa o parâmetro `DESTINATION_ID` na solicitação.

Selecione cada guia abaixo para visualizar o conteúdo correspondente.

>[!BEGINTABS]

>[!TAB Recuperar todas as solicitações de publicação]

+++Solicitação

A solicitação a seguir recuperará a lista de solicitações de publicação que você enviou, com base em [!DNL IMS Org ID] e na configuração da sandbox.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Resposta

A resposta a seguir retorna o status HTTP 200 com uma lista de todos os destinos enviados para publicação aos quais você tem acesso, com base na ID da organização IMS e no nome da sandbox usados. Um `configId` corresponde à solicitação de publicação para um destino.

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

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `destinationId` | String | A ID de destino da configuração de destino enviada para publicação. |
| `publishDetailsList.configId` | String | A ID exclusiva da solicitação de publicação de destino para o destino enviado. |
| `publishDetailsList.allowedOrgs` | String | Retorna as organizações de Experience Platform para as quais o destino está disponível. <br> <ul><li> Para `"destinationType": "PUBLIC"`, esse parâmetro retorna `"*"`, o que significa que o destino está disponível para todas as organizações Experience Platform.</li><li> Para `"destinationType": "DEV"`, esse parâmetro retorna a ID da Organização da organização que você usou para criar e testar o destino.</li></ul> |
| `publishDetailsList.status` | String | O status da solicitação de publicação de destino. Os valores possíveis são `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. Destinos com o valor `PUBLISHED` estão ao vivo e podem ser usados por clientes do Experience Platform. |
| `publishDetailsList.destinationType` | String | O tipo de destino. Os valores podem ser `DEV` e `PUBLIC`. `DEV` corresponde ao destino em sua organização de Experience Platform. `PUBLIC` corresponde ao destino enviado para publicação. Pense nessas duas opções em termos do Git, onde a versão `DEV` representa sua ramificação de criação local e a versão `PUBLIC` representa a ramificação principal remota. |
| `publishDetailsList.publishedDate` | String | A data em que o destino foi enviado para publicação, em época. |

{style="table-layout:auto"}

+++

>[!TAB Recuperar uma solicitação de publicação específica]

+++Solicitação

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish/{DESTINATION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{DESTINATION_ID}` | A ID do destino para o qual você deseja recuperar o status de publicação. |

+++

+++Resposta

Se você passou um `DESTINATION_ID` na chamada da API, a resposta retorna o status HTTP 200 com informações detalhadas sobre a solicitação de publicação de destino especificada.

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
| `destinationId` | String | A ID de destino da configuração de destino enviada para publicação. |
| `publishDetailsList.configId` | String | A ID exclusiva da solicitação de publicação de destino para o destino enviado. |
| `publishDetailsList.allowedOrgs` | String | Retorna as organizações de Experience Platform para as quais o destino está disponível. <br> <ul><li> Para `"destinationType": "PUBLIC"`, esse parâmetro retorna `"*"`, o que significa que o destino está disponível para todas as organizações Experience Platform.</li><li> Para `"destinationType": "DEV"`, esse parâmetro retorna a ID da Organização da organização que você usou para criar e testar o destino.</li></ul> |
| `publishDetailsList.status` | String | O status da solicitação de publicação de destino. Os valores possíveis são `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. Destinos com o valor `PUBLISHED` estão ao vivo e podem ser usados por clientes do Experience Platform. |
| `publishDetailsList.destinationType` | String | O tipo de destino. Os valores podem ser `DEV` e `PUBLIC`. `DEV` corresponde ao destino em sua organização de Experience Platform. `PUBLIC` corresponde ao destino enviado para publicação. Pense nessas duas opções em termos do Git, onde a versão `DEV` representa sua ramificação de criação local e a versão `PUBLIC` representa a ramificação principal remota. |
| `publishDetailsList.publishedDate` | String | A data em que o destino foi enviado para publicação, em época. |

{style="table-layout:auto"}

+++

>[!ENDTABS]

## Manipulação de erros de API

Os endpoints da API Destination SDK seguem os princípios gerais de mensagem de erro da API Experience Platform. Consulte [códigos de status da API](../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da Platform.
