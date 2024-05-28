---
title: Endpoint da API de conteúdo
description: Saiba como recuperar seus dados de acesso usando a API do Privacy Service.
role: Developer
badgePrivateBeta: label="Beta privado" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: c527771e051d39032642afae33945a45e5183a5f
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 1%

---

# Endpoint de conteúdo

>[!IMPORTANT]
>
>A variável `/content` o endpoint está atualmente na versão beta e sua organização pode ainda não ter acesso a ele. A funcionalidade e a documentação estão sujeitas a alterações.

<!-- Q) Should this be called 'access information' or 'customer content'? -->

Aproveite a segurança aprimorada ao recuperar &quot;informações de acesso&quot; (as informações que um titular de privacidade pode solicitar legitimamente para acessar). O URL de download fornecido na resposta a uma `/jobs/{JOB_ID}` A solicitação do GET agora aponta para um ponto de acesso de serviço da Adobe. Em seguida, você pode fazer uma solicitação GET para `/jobs/:JOB_ID/content` para retornar os dados do cliente no formato JSON. Esse método de acesso implementa várias camadas de autenticação e controle de acesso para melhorar a segurança.

Antes de usar este guia, consulte o [guia de introdução](./getting-started.md) para obter informações sobre os cabeçalhos de autenticação necessários, apresentados na chamada de API de exemplo abaixo.

>[!TIP]
>
>Se, atualmente, você não souber a ID do trabalho para as informações de acesso necessárias, faça uma chamada para o `/jobs`e use parâmetros de consulta adicionais para filtrar os resultados. Uma lista completa dos parâmetros de consulta disponíveis pode ser encontrada no [manual de endpoint de processos de privacidade](./privacy-jobs.md).

## Recuperar informações do trabalho de privacidade

Para recuperar informações sobre uma ordem de produção específica, como seu status de processamento atual, inclua o `jobId` no caminho de uma solicitação GET para o `/jobs` terminal.

**Formato da API**

```http
GET /jobs/{JOB_ID}
```

**Solicitação**

A solicitação a seguir recupera os detalhes do job cujo `jobId` é fornecido no caminho da solicitação.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do trabalho especificado.

>[!NOTE]
>
>Os processos de privacidade devem ter o `complete` status para conter a variável `downloadUrl`.

```json
{
    "jobId":"dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5",
    "requestId":"17129380910360540RX-753",
    "userKey":"1234",
    "action":"access",
    "status":"complete",
    "submittedBy":"jsnow@adobe.com",
    "createdDate":"04/12/2024 04:08 PM GMT",
    "lastModifiedDate":"04/12/2024 04:08 PM GMT",
    "userIds":[{
        "namespace":"ECID",
        "value":"1234",
        "type":"standard",
        "namespaceId":4,
        "isDeletedClientSide":false
        }],
    "productResponses":[{
        "product":"Identity",
        "retryCount":0,
        "processedDate":"04/12/2024 04:08 PM GMT",
        "productStatusResponse":{"status":"submitted"
        }}],
    "downloadUrl":"https://platform-stage.adobe.io/data/core/privacy/jobs/dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5/content",
    "regulation":"gdpr"
}
```

| Propriedade | Descrição |
|----------------------|---------------------------------------------------------------------------------------------------------------|
| `jobId` | Um identificador exclusivo para o trabalho de privacidade. |
| `requestId` | Um identificador exclusivo para a solicitação específica feita ao Privacy Service. |
| `userKey` | `userKey` é o `key` que você forneceu quando enviou a solicitação de acesso a dados pessoais. A variável `key` value é a sua oportunidade de fornecer um identificador para o titular dos dados que faz sentido para você. Normalmente, é um identificador exclusivo que seu sistema criou para rastrear esse titular de dados. DICA: Você pode listar todos os processos de privacidade ativos e comparar suas `key` para cada tarefa. |
| `action` | O tipo de ação solicitada. Os valores aceitos são `access` e `delete`. |
| `status` | O status atual do trabalho de privacidade. |
| `submittedBy` | O endereço de email da pessoa que enviou o trabalho de privacidade. |
| `createdDate` | A data e hora em que o trabalho de privacidade foi criado. |
| `lastModifiedDate` | A data e a hora em que o trabalho de privacidade foi modificado pela última vez. |
| `userIds` | Uma matriz que contém identificadores de usuário e informações relacionadas. |
| `userIds.namespace` | O namespace usado para o identificador do usuário. |
| `userIds.value` | O valor real do identificador do usuário. |
| `userIds.type` | O tipo de identificador (por exemplo `standard` ou `custom`). |
| `userIds.namespaceId` | Um identificador para o namespace usado para categorizar e gerenciar identidades de usuário. |
| `userIds.isDeletedClientSide` | Um booliano que indica se o identificador foi excluído no lado do cliente. |
| `productResponses` | Uma matriz que contém respostas de diferentes produtos ou serviços relacionados ao trabalho de privacidade. |
| `productResponses.product` | O nome do produto ou serviço usado para adquirir informações sobre o titular dos dados. |
| `productResponses.retryCount` | O número de vezes que a solicitação foi repetida. |
| `productResponses.processedDate` | A data e a hora em que a resposta do produto foi processada. |
| `productResponses.productStatusResponse` | Um objeto que contém o status da resposta do produto. |
| `productResponses.productStatusResponse.status` | O status da resposta do produto. |
| `downloadURL` | Esse atributo fornece um endpoint, que está disponível para chamada por 60 dias após a conclusão da tarefa. O status do trabalho deve ser `complete` e a variável `action` deve ser `access`. Caso contrário, esse campo estará ausente. |
| `regulation` | O quadro regulamentar em que a solicitação de privacidade está sendo processada, como `gdpr`, `ccpa`, `lgpd_bra`, `pdpa_tha`e assim por diante. |

{style="table-layout:auto"}

## Recuperar informações de acesso do cliente {#retrieve-access-data}

Para obter as &quot;informações de acesso&quot; produzidas em resposta à consulta do titular dos dados, faça uma solicitação GET ao `/jobs/{JOB_ID}/content` terminal. A resposta é um arquivo zip (*.zip) que contém uma pasta com subpastas para cada produto que contém dados sobre o titular dos dados.

>[!TIP]
>
>Você precisa de uma ID de tarefa específica para fazer esta solicitação. Se precisar recuperar a ID de trabalho específica, primeiro faça uma solicitação GET à `/jobs` e use parâmetros de consulta adicionais para filtrar os resultados. Informações detalhadas, incluindo os parâmetros de consulta permitidos, podem ser encontradas na [manual de endpoint de processos de privacidade](./privacy-jobs.md).

**Formato da API**

```http
GET /jobs/{JOB_ID}/content
```

**Solicitação**

A solicitação a seguir retorna &quot;informações de acesso&quot; para a ID do trabalho fornecida na solicitação.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/32d429b1-f7f4-11ee-a365-574bcf5a525d/content \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'Accept: application/json`
```

**Resposta**

A resposta é um arquivo zip (*.zip). Normalmente, as informações são retornadas no formato JSON, embora isso não possa ser garantido. Os dados extraídos podem ser retornados em qualquer formato.

<!-- ## Constraints {#constraints}

During this private beta, the following constraints apply when using the `/content` endpoint:

- The new `/content` download URL is only available in STAGE environments. It is not yet available in PROD environments
- The `downloadUrl` should not be present in the JSON response unless the job has a `complete` status. Within the beta, the `downloadUrl` appears before a privacy job is complete.
- The `downloadUrl` is also currently provided for `delete` jobs (which should never have a download URL). -->
