---
description: Esta página exemplifica a chamada da API usada para recuperar detalhes sobre uma solicitação de publicação de destino por meio do Adobe Experience Platform Destination SDK.
title: Recuperar uma solicitação de publicação de destino
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 4%

---


# Recuperar uma solicitação de publicação de destino

>[!IMPORTANT]
>
>Você só precisará usar esse endpoint da API se estiver enviando um destino (público) produzido para ser usado por outros clientes do Experience Platform. Se estiver criando um destino privado para uso próprio, não será necessário enviar formalmente o destino usando a API de publicação.

>[!IMPORTANT]
>
>**Ponto de acesso da API**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Após configurar e testar seu destino, você pode enviá-lo ao Adobe para análise e publicação. Ler [Enviar para revisão de um destino criado no Destination SDK](../guides/submit-destination.md) para todas as outras etapas, é necessário fazer parte do processo de envio do destino.

Use o endpoint da API de destinos de publicação para enviar uma solicitação de publicação quando:

* Como parceiro de Destination SDK, você deseja disponibilizar o destino produzido em todas as organizações de Experience Platform para que todos os clientes de Experience Platform possam usá-lo;
* Você faz *qualquer atualização* nas suas configurações. As atualizações de configuração são refletidas no destino somente após enviar uma nova solicitação de publicação, que é aprovada pela equipe do Experience Platform.

>[!IMPORTANT]
>
>Todos os nomes de parâmetros e valores suportados pelo Destination SDK são **distinção entre maiúsculas e minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações da API de publicação de destino {#get-started}

Antes de continuar, reveja o [guia de introdução](../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com sucesso, incluindo como obter a permissão de criação de destino necessária e os cabeçalhos necessários.

## Listar solicitações de publicação de destino {#retrieve-list}

Você pode recuperar uma lista de todos os destinos enviados para publicação da sua Organização IMS fazendo uma solicitação de GET para a `/authoring/destinations/publish` endpoint .

**Formato da API**

Use o seguinte formato de API para recuperar todas as solicitações de publicação da sua conta.

```http
GET /authoring/destinations/publish
```

Use o seguinte formato de API para recuperar uma solicitação de publicação específica, definida pela variável `{DESTINATION_ID}` parâmetro.

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

**Solicitação**

As duas solicitações a seguir recuperam todas as solicitações de publicação da Organização IMS ou uma solicitação de publicação específica, dependendo se você passa a variável `DESTINATION_ID` na solicitação.

Selecione cada guia abaixo para visualizar a carga correspondente.

>[!BEGINTABS]

>[!TAB Recuperar todas as solicitações de publicação]

+++Solicitação

A solicitação a seguir recuperará a lista de solicitações de publicação enviadas, com base em [!DNL IMS Org ID] e configuração de sandbox.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Resposta

A resposta a seguir retorna o status HTTP 200 com uma lista de todos os destinos enviados para publicação aos quais você tem acesso, com base na IMS Organization ID e no nome da sandbox usados. One `configId` corresponde à solicitação de publicação para um destino.

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
| `destinationId` | String | A ID de destino da configuração de destino que você enviou para publicação. |
| `publishDetailsList.configId` | String | A ID exclusiva da solicitação de publicação de destino para o destino enviado. |
| `publishDetailsList.allowedOrgs` | String | Retorna as organizações Experience Platform para as quais o destino está disponível. <br> <ul><li> Para `"destinationType": "PUBLIC"`, esse parâmetro retorna `"*"`, o que significa que o destino está disponível para todas as organizações Experience Platform.</li><li> Para `"destinationType": "DEV"`, esse parâmetro retorna a ID da organização usada para criar e testar o destino.</li></ul> |
| `publishDetailsList.status` | String | O status da solicitação de publicação de destino. Os valores possíveis são `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. Destinos com o valor `PUBLISHED` são ativos e podem ser usados por clientes do Experience Platform. |
| `publishDetailsList.destinationType` | String | O tipo de destino. Os valores podem ser `DEV` e `PUBLIC`. `DEV` corresponde ao destino em sua organização Experience Platform. `PUBLIC` corresponde ao destino enviado para publicação. Pense nessas duas opções em termos de Git, onde a variável `DEV` A versão representa a ramificação de criação local e a variável `PUBLIC` representa a ramificação principal remota. |
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

Se você tiver passado um `DESTINATION_ID` na chamada da API, a resposta retorna o status HTTP 200 com informações detalhadas sobre a solicitação de publicação de destino especificada.

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

{style="table-layout:auto"}

+++

>[!ENDTABS]

## Tratamento de erros da API

Os pontos de extremidade da API do Destination SDK seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](../../../landing/troubleshooting.md#api-status-codes) e [erros do cabeçalho da solicitação](../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da plataforma.