---
title: Endpoint da API de públicos externos
description: Saiba como usar a API de públicos-alvo externos para criar, atualizar, ativar e excluir seus públicos-alvo externos do Adobe Experience Platform.
exl-id: eaa83933-d301-48cb-8a4d-dfeba059bae1
source-git-commit: 0a37ef2f5fc08eb515c7c5056936fd904ea6d360
workflow-type: tm+mt
source-wordcount: '2253'
ht-degree: 5%

---

# Endpoint de públicos externos

Públicos externos permitem carregar dados de perfil de suas fontes externas para o Adobe Experience Platform. Você pode usar o ponto de extremidade `/external-audience` na API do Serviço de segmentação para assimilar um público externo na Experience Platform, exibir detalhes e atualizar públicos externos, bem como excluir públicos externos.

## Introdução

>[!IMPORTANT]
>
>Os pontos de extremidade neste guia recebem o prefixo `/core/ais`, e não `/core/ups`.

Para usar as APIs do Experience Platform, você deve ter concluído o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores de cada um dos cabeçalhos necessários nas chamadas de API do Experience Platform, conforme mostrado abaixo:

- Autorização: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] estão isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Experience Platform] APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre como trabalhar com sandboxes em [!DNL Experience Platform], consulte a [documentação de visão geral das sandboxes](../../sandboxes/home.md).

## Criar público externo {#create-audience}

Você pode criar uma audiência externa fazendo uma solicitação POST para o ponto de extremidade `/external-audience/`.

**Formato da API**

```http
POST /external-audience/
```

**Solicitação**

+++ Um exemplo de solicitação para criar um público-alvo externo.

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "params": {
                "path": "activation/sample-source/example.csv",
                "type": "file",
                "sourceType": "Cloud Storage",
                "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            }
        },
        "ttlInDays": "40",
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }'
```

| Propriedade | Tipo | Descrição |
| -------- | ---- | ----------- |
| `name` | String | O nome do público-alvo externo. |
| `description` | String | Uma descrição opcional para o público-alvo externo. |
| `customAudienceId` | String | Um identificador opcional para seu público-alvo externo. |
| `fields` | Matriz de objetos | A lista de campos e seus tipos de dados. Ao criar a lista de campos, você pode adicionar os seguintes itens: <ul><li>`name`: **Obrigatório** O nome do campo que faz parte da especificação de público-alvo externo.</li><li>`type`: **Obrigatório** O tipo de dados que entra no campo. Os valores com suporte incluem `string`, `number`, `long`, `integer`, `date` (`2025-05-13`), `datetime` (`2025-05-23T20:19:00+00:00`) e `boolean`.</li><li>`identityNs`: **Obrigatório para o campo de identidade** O namespace usado pelo campo de identidade. Os valores suportados incluem todos os namespaces válidos, como `ECID` ou `email`.</li><li>`labels`: *Opcional* Uma matriz de rótulos de controle de acesso para o campo. Mais informações sobre os rótulos de controle de acesso disponíveis podem ser encontradas no [glossário de rótulos de uso de dados](/help/data-governance/labels/reference.md). </li></ul> |
| `sourceSpec` | Objeto | Um objeto que contém as informações onde o público-alvo externo está localizado. Ao usar este objeto, você **deve** incluir as seguintes informações: <ul><li>`path`: **Obrigatório**: o local do público-alvo externo ou a pasta que contém o público-alvo externo na origem. O caminho de arquivo **não pode** conter espaços. Por exemplo, se o caminho for `activation/sample-source/Example CSV File.csv`, defina o caminho como `activation/sample-source/ExampleCSVFile.csv`. Você pode encontrar o caminho para sua origem na coluna de **dados do Source** da seção de fluxos de dados.</li><li>`type`: **Obrigatório** O tipo do objeto que você está recuperando da origem. Este valor pode ser `file` ou `folder`.</li><li>`sourceType`: *Opcional* O tipo de origem da qual você está recuperando. No momento, o único valor com suporte é `Cloud Storage`.</li><li>`cloudType`: **Obrigatório** O tipo de armazenamento em nuvem, com base no tipo de origem. Os valores suportados incluem `S3`, `DLZ`, `GCS`, `Azure` e `SFTP`.</li><li>`baseConnectionId`: a ID da conexão base, e é fornecida pelo seu provedor de origem. Este valor é **necessário** se estiver usando um valor `cloudType` de `S3`, `GCS` ou `SFTP`. Caso contrário, você **não** precisará incluir este parâmetro. Para obter mais informações, leia a [visão geral dos conectores de origem](../../sources/home.md).</li></ul> |
| `ttlInDays` | Número inteiro | A expiração dos dados para o público externo, em dias. Esse valor pode ser definido de 1 a 90. Por padrão, a expiração dos dados está definida como 30 dias. |
| `audienceType` | String | O tipo de público-alvo para o público externo. Atualmente, somente `people` é suportado. |
| `originName` | String | **Obrigatório** A origem do público-alvo. Isso indica de onde o público-alvo vem. Para públicos externos, você deve usar `CUSTOM_UPLOAD`. |
| `namespace` | String | O namespace do público. Por padrão, esse valor está definido como `CustomerAudienceUpload`. |
| `labels` | Matriz de cadeias de caracteres | Os rótulos de controle de acesso que se aplicam ao público-alvo externo. Mais informações sobre os rótulos de controle de acesso disponíveis podem ser encontradas no [glossário de rótulos de uso de dados](/help/data-governance/labels/reference.md). |
| `tags` | Matriz de cadeias de caracteres | As tags que você deseja aplicar ao público-alvo externo. Mais informações sobre tags podem ser encontradas no [guia de gerenciamento de tags](/help/administrative-tags/ui/managing-tags.md). |

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 com detalhes do público-alvo externo recém-criado.

+++ Um exemplo de resposta ao criar um público-alvo externo.

```json
{
    "operationId": "df8cd82f-a214-4b72-b549-d6ee23f1ff1a",
    "operationDetails": {
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "Email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "params": {
                "path": "activation/sample-source/example.csv",
                "type": "file",
                "sourceType": "Cloud Storage",
                "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            }
        },
        "ttlInDays": 40,
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }   
}
```

| Propriedade | Tipo | Descrição |
| -------- | ---- | ----------- |
| `operationId` | String | A ID da operação. Posteriormente, você pode usar essa ID para recuperar o status da criação do público-alvo. |
| `operationDetails` | Objeto | Um objeto que contém os detalhes da solicitação enviada para criar o público-alvo externo. |
| `name` | String | O nome do público-alvo externo. |
| `description` | String | A descrição do público-alvo externo. |
| `fields` | Matriz de objetos | A lista de campos e seus tipos de dados. Essa matriz determina quais campos são necessários no público-alvo externo. |
| `sourceSpec` | Objeto | Um objeto que contém as informações onde o público-alvo externo está localizado. |
| `ttlInDays` | Número inteiro | A expiração dos dados para o público externo, em dias. Esse valor pode ser definido de 1 a 90. Por padrão, a expiração dos dados está definida como 30 dias. |
| `audienceType` | String | O tipo de público-alvo para o público externo. |
| `originName` | String | **Obrigatório** A origem do público-alvo. Isso indica de onde o público-alvo vem. |
| `namespace` | String | O namespace do público. |
| `labels` | Matriz de cadeias de caracteres | Os rótulos de controle de acesso que se aplicam ao público-alvo externo. Mais informações sobre os rótulos de controle de acesso disponíveis podem ser encontradas no [glossário de rótulos de uso de dados](/help/data-governance/labels/reference.md). |


+++

## Recuperar status de criação do público {#retrieve-status}

Você pode recuperar o status do envio de público-alvo externo fazendo uma solicitação GET para o ponto de extremidade `/external-audiences/operations` e fornecendo a ID da operação recebida da resposta de criação de público-alvo externo.

**Formato da API**

```http
GET /external-audiences/operations/{OPERATION_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{OPERATION_ID}` | O valor `id` da operação que você deseja recuperar. |

**Solicitação**

+++ Uma solicitação de amostra para recuperar o status da operação de um público-alvo externo.

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/operations/df8cd82f-a214-4b72-b549-d6ee23f1ff1a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes do status da tarefa do público-alvo externo.

+++ Um exemplo de resposta quando você recupera o status da tarefa de um público-alvo externo.

```json
{
    "operationId": "df8cd82f-a214-4b72-b549-d6ee23f1ff1a",
    "status": "SUCCESS",
    "operationDetails": {
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "Email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "params": {
                "path": "activation/sample-source/example.csv",
                "type": "file",
                "sourceType": "Cloud Storage",
                "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            }
        },
        "ttlInDays": 40,
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    },
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "createdBy": "{USER_ID}",
    "createdAt": 1749324248,
    "updatedBy": "{USER_ID}",
    "updatedAt": 1749624273
}
```

| Propriedade | Tipo | Descrição |
| -------- | ---- | ----------- |
| `operationId` | String | A ID da operação que você está recuperando. |
| `status` | String | O status da operação. Pode ser um dos seguintes valores: `SUCCESS`, `FAILED`, `PROCESSING`. |
| `operationDetails` | Objeto | Um objeto que contém detalhes do público-alvo. |
| `audienceId` | String | A ID do público externo que está sendo enviado pela operação. |
| `createdBy` | String | A ID do usuário que criou o público-alvo externo. |
| `createdAt` | Carimbo de data e hora de época longa | O carimbo de data e hora, em segundos, quando a solicitação para criar o público-alvo externo foi enviada. |
| `updatedBy` | String | A ID do último usuário que atualizou o público. |
| `updatedAt` | Carimbo de data e hora de época longa | O carimbo de data e hora, em segundos, quando o público foi atualizado pela última vez. |

+++

## Atualizar um público externo {#update-audience}

>[!NOTE]
>
>Para usar o ponto de extremidade a seguir, é necessário ter o `audienceId` do público-alvo externo. Você pode obter seu `audienceId` de uma chamada bem-sucedida para o ponto de extremidade `GET /external-audiences/operations/{OPERATION_ID}`.

Você pode atualizar campos do público-alvo externo fazendo uma solicitação PATCH para o ponto de extremidade `/external-audience` e fornecendo a ID do público-alvo no caminho da solicitação.

Ao usar esse endpoint, é possível atualizar os seguintes campos:

- Descrição de público-alvo
- Rótulos do controle de acesso em nível de campo
- Rótulos de controle de acesso no nível do público
- A expiração dos dados do público-alvo

A atualização do campo usando este ponto de extremidade **substitui** o conteúdo do campo solicitado.

**Formato da API**

```http
PATCH /external-audience/{AUDIENCE_ID}
```

**Solicitação**

+++ Um exemplo de solicitação para atualizar a descrição do público-alvo externo.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab\
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "description": "New sample description"
 }'
```

| Propriedade | Tipo | Descrição |
| -------- | ---- | ----------- |
| `description` | String | A descrição atualizada do público-alvo externo. |

Além disso, você pode atualizar os seguintes parâmetros:

| Propriedade | Tipo | Descrição |
| -------- | ---- | ----------- |
| `labels` | Matriz | Uma matriz que contém a lista atualizada de rótulos de acesso para o público-alvo. Mais informações sobre os rótulos de controle de acesso disponíveis podem ser encontradas no [glossário de rótulos de uso de dados](/help/data-governance/labels/reference.md). |
| `fields` | Matriz de objetos | Uma matriz que contém os campos e seus rótulos associados para o público-alvo externo. Somente os campos listados na solicitação do PATCH serão atualizados. Mais informações sobre os rótulos de controle de acesso disponíveis podem ser encontradas no [glossário de rótulos de uso de dados](/help/data-governance/labels/reference.md). |
| `ttlInDays` | Número inteiro | A expiração dos dados para o público externo, em dias. Esse valor pode ser definido de 1 a 90. |

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes do público-alvo externo atualizado.

+++ Um exemplo de resposta ao atualizar a descrição do público-alvo externo.

```json
{
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceName": "Sample external audience",
    "description": "New sample description",
    "fields": [
        {
            "name": "ppid",
            "type": "string",
            "identityNs": "Email"
        },
        {
            "name": "list_id",
            "type": "string",
            "labels": ["core/C2", "custom/deep"]
        },
        {
            "name": "delete",
            "type": "number"
        },
        {
            "name": "process_consent",
            "type": "string"
        }
    ],
    "sourceSpec": {
        "path": "activation/sample-source/example.csv",
        "type": "file",
        "sourceType": "Cloud Storage",
        "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
        },
    "ttlInDays": 40,
    "labels": ["core/C1"],
    "audienceType": "people",
    "originName": "CUSTOM_UPLOAD",
    "createdBy": "{USER_ID}",
    "createdAt": 1749324248,
    "updatedBy": "{USER_ID}",
    "updatedAt": 1749624273
}
```

+++

## Iniciar assimilação de público {#start-audience-ingestion}

>[!IMPORTANT]
>
>Você **não** poderá iniciar uma nova assimilação para o público externo se uma assimilação de público anterior já estiver em andamento.

>[!NOTE]
>
>Para usar o ponto de extremidade a seguir, é necessário ter o `audienceId` do público-alvo externo. Você pode obter seu `audienceId` de uma chamada bem-sucedida para o ponto de extremidade `GET /external-audiences/operations/{OPERATION_ID}`.

Você pode iniciar uma assimilação de público-alvo fazendo uma solicitação POST para o endpoint a seguir ao fornecer a ID do público-alvo.

**Formato da API**

```http
POST /external-audience/{AUDIENCE_ID}/runs
```

**Solicitação**

A solicitação a seguir aciona uma execução de assimilação para o público-alvo externo.

+++ Um exemplo de solicitação para iniciar uma assimilação de público-alvo.

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "dataFilterStartTime": 764245635
 }' 
```

| Propriedade | Tipo | Descrição |
| -------- | ---- | ----------- |
| `dataFilterStartTime` | Carimbo de data e hora da época | **Obrigatório** O intervalo que especifica a hora inicial para determinar quais arquivos serão processados. Isso significa que os arquivos selecionados serão arquivos **após** no horário especificado. |
| `dataFilterEndTime` | Carimbo de data e hora da época | O intervalo que especifica a hora final em que o fluxo será executado para selecionar quais arquivos serão processados. Isto significa que os arquivos selecionados serão arquivos **antes** do horário especificado. |

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes sobre a execução da assimilação.

+++ Um exemplo de resposta ao iniciar a assimilação do público-alvo.

```json
{
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
    "differentialIngestion": true,
    "dataFilterStartTime": 764245635,
    "dataFilterEndTime": 4565657575,
    "createdAt": 4565657575,
    "createdBy:" "{USER_ID}"
}
```

| Propriedade | Tipo | Descrição |
| -------- | ---- | ----------- |
| `audienceName` | String | O nome do público para o qual você está iniciando uma assimilação. |
| `audienceId` | String | A ID da audiência. |
| `runId` | String | A ID da execução de assimilação que você iniciou. |
| `differentialIngestion` | Booleano | Um campo que determina se a assimilação é uma assimilação parcial baseada na diferença desde a última assimilação ou uma assimilação completa de público. |
| `dataFilterStartTime` | Carimbo de data e hora da época | O intervalo que especifica a hora inicial em que o fluxo é executado para selecionar quais arquivos foram processados. |
| `dataFilterEndTime` | Carimbo de data e hora da época | O intervalo que especifica a hora final em que o fluxo é executado para selecionar quais arquivos foram processados. |
| `createdAt` | Carimbo de data e hora de época longa | O carimbo de data e hora, em segundos, quando a solicitação para criar o público-alvo externo foi enviada. |
| `createdBy` | String | A ID do usuário que criou o público-alvo externo. |

+++

## Recuperar status de assimilação de público específico {#retrieve-ingestion-status}

>[!NOTE]
>
>Para usar o endpoint a seguir, é necessário ter o `audienceId` do público-alvo externo e o `runId` da ID de execução da assimilação. Você pode obter `audienceId` de uma chamada bem-sucedida para o ponto de extremidade `GET /external-audiences/operations/{OPERATION_ID}` e `runId` de uma chamada bem-sucedida anterior do ponto de extremidade `POST /external-audience/{AUDIENCE_ID}/runs`.

Você pode recuperar o status de uma assimilação de público-alvo fazendo uma solicitação GET para o endpoint a seguir enquanto fornece o público-alvo e as IDs de execução.

**Formato da API**

```http
GET /external-audience/{AUDIENCE_ID}/runs/{RUN_ID}
```

**Solicitação**

A solicitação a seguir recupera o status de assimilação para o público-alvo externo.

+++ Uma solicitação de amostra para recuperar o status de assimilação do público-alvo externo.

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs/fb342311-725d-4b48-ab7d-c6105fbc2b8b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da assimilação do público-alvo externo.

+++ Um exemplo de resposta ao recuperar a assimilação do público-alvo externo.

```json
{
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
    "status": "SUCCESS",
    "differentialIngestion": true,
    "dataFilterStartTime": 764245635,
    "dataFilterEndTime": 3456788568,
    "createdAt": 1749324248,
    "createdBy": "{USER_ID}",
    "details": [
        {
            "stage": "DATASET_INGEST",
            "status": "SUCCESS",
            "flowRunId": "{FLOW_RUN_ID}"
        },
        {
            "stage": "PROFILE_STORE_INGEST",
            "status": "SUCCESS",
            "flowRunId": "{FLOW_RUN_ID}"
        }
    ]
}
```

| Propriedade | Tipo | Descrição |
| -------- | ---- | ----------- |
| `audienceName` | String | O nome do público. |
| `audienceId` | String | A ID da audiência. |
| `runId` | String | A ID da execução de assimilação. |
| `status` | String | O status da execução da assimilação. Os status possíveis incluem `SUCCESS` e `FAILED`. |
| `differentialIngestion` | Booleano | Um campo que determina se a assimilação é uma assimilação parcial baseada na diferença desde a última assimilação ou uma assimilação completa de público. |
| `dataFilterStartTime` | Carimbo de data e hora da época | O intervalo que especifica a hora inicial em que o fluxo é executado para selecionar quais arquivos foram processados. |
| `dataFilterEndTime` | Carimbo de data e hora da época | O intervalo que especifica a hora final em que o fluxo é executado para selecionar quais arquivos foram processados. |
| `createdAt` | Carimbo de data e hora de época longa | O carimbo de data e hora, em segundos, quando a solicitação para criar o público-alvo externo foi enviada. |
| `createdBy` | String | A ID do usuário que criou o público-alvo externo. |
| `details` | Matriz de objetos | Um objeto que contém os detalhes da execução de assimilação. <ul><li>`stage`: O estágio da execução de assimilação. Pode ser `DATASET_INGEST` ou `PROFILE_STORE_INGEST`, que representam a assimilação do data lake e a assimilação do perfil.</li><li>`status`: o status da assimilação no estágio. Os status possíveis incluem `SUCCESS` e `FAILED`.</li><li>`flowRunId`: A ID da execução do fluxo de assimilação do estágio.</li></ul> |

+++

## Listar execuções de assimilação de público {#list-ingestion-runs}

>[!NOTE]
>
>Para usar o ponto de extremidade a seguir, é necessário ter o `audienceId` do público-alvo externo. Você pode obter seu `audienceId` de uma chamada bem-sucedida para o ponto de extremidade `GET /external-audiences/operations/{OPERATION_ID}`.

Você pode recuperar todas as execuções de assimilação para o público externo selecionado fazendo uma solicitação GET para o endpoint a seguir ao fornecer a ID de público. Vários parâmetros podem ser incluídos, separados por &quot;E&quot; comercial (`&`).

**Formato da API**

<!-- The following endpoint supports several query parameters to help filter your results. While these parameters are optional, their use is strongly recommended to help focus your results. -->

```http
GET /external-audience/{AUDIENCE_ID}/runs
```

<!-- **Query parameters**

+++ A list of available query parameters. 

| Parameter | Description | Example |
| --------- | ----------- | ------- |
| `limit` | The maximum number of items returned in the response. This value can range from 1 to 40. By default, the limit is set to 20. | `limit=30` |
| `sortBy` | The order in which the returned items are sorted. You can sort by either `name` or by `createdAt`. Additionally, you can add a `-` sign to sort by **descending** order instead of **ascending** order. By default, the items are sorted by `createdAt` in descending order. | `sortBy=name` |
| `property` | A filter to determine which audience ingestion runs are displayed. You can filter on the following properties: <ul><li>`name`: Lets you filter by the audience name. If using this property, you can compare by using `=`, `!=`, `=contains`, or `!=contains`. </li><li>`createdAt`: Lets you filter by the ingestion time. If using this property, you can compare by using `>=` or `<=`.</li><li>`status`: Lets you filter by the ingestion run's status. If using this property, you can compare by using `=`, `!=`, `=contains`, or `!=contains`. </li></ul>  | `property=createdAt<1683669114845`<br/>`property=name=demo_audience`<br/>`property=status=SUCCESS` |

+++ -->

**Solicitação**

A solicitação a seguir recupera todas as execuções de assimilação para o público-alvo externo.

+++ Uma solicitação de amostra para obter uma lista de execuções de assimilação de público-alvo.

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de execuções de assimilação para o público externo especificado.

+++ Uma resposta de amostra quando você recupera uma lista de execuções de assimilação de público-alvo.

```json
{
    "runs": [
        {
            "audienceName": "Sample external audience",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
            "status": "SUCCESS",
            "differentialIngestion": true,
            "dataFilterStartTime": 764245635,
            "dataFilterEndTime": 3456788568,
            "createdAt": 1785678909,
            "createdBy": "{USER_NAME}"
        },
        {
            "audienceName": "Sample external audience 2",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "runId": "406e38e4-fbd5-43e1-8d0c-01ccb3f9ad10",
            "status": "SUCCESS",
            "differentialIngestion": true,
            "dataFilterStartTime": 764245635,
            "dataFilterEndTime": 3456788568,
            "createdAt": 1749324248,
            "createdBy": "{USER_ID}"
        }
    ]
}
```

<!-- ,
    "_page": {
        "limit": 20,
        "count": 2,
        "totalCount": 2
    }
    
| `_page` | Object | An object that contains the pagination information about the list of results. |
     -->

| Propriedade | Tipo | Descrição |
| -------- | ---- | ----------- |
| `runs` | Objeto | Um objeto que contém a lista de execuções de assimilação que pertence ao público-alvo. Mais informações sobre este objeto podem ser encontradas na [seção recuperar status de assimilação](#retrieve-ingestion-status). |

+++

## Excluir um público-alvo externo {#delete-audience}

>[!NOTE]
>
>Para usar o ponto de extremidade a seguir, é necessário ter o `audienceId` do público-alvo externo. Você pode obter seu `audienceId` de uma chamada bem-sucedida para o ponto de extremidade `GET /external-audiences/operations/{OPERATION_ID}`.

É possível excluir um público-alvo externo fazendo uma solicitação DELETE para o seguinte endpoint ao fornecer a ID do público-alvo.

**Formato da API**

```http
DELETE /external-audience/{AUDIENCE_ID}
```

**Solicitação**

A solicitação a seguir exclui o público-alvo externo especificado.

+++ Um exemplo de solicitação para excluir o público-alvo externo.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 com um corpo de resposta vazio.

## Próximas etapas {#next-steps}

Depois de ler este guia, você compreenderá melhor como criar, gerenciar e excluir públicos-alvo externos usando as APIs do Experience Platform. Para saber como usar públicos externos com a interface do Experience Platform, leia a [documentação do Portal de público-alvo](../ui/audience-portal.md).

## Apêndice {#appendix}

A seção a seguir lista os códigos de erro disponíveis ao usar a API de públicos-alvo externos.

| Código de erro da plataforma | Código de status | Mensagem | Descrição |
| ------------------- | ----------- | ------- | ----------- |
| 100910-400 | 400 | `BAD_REQUEST` | Ocorreu uma solicitação inválida devido a uma falha ao validar as solicitações. |
| 100911-400 | 400 | `BAD_REQUEST` | Um token inválido é fornecido. |
| 100920-401 | 401 | `UNAUTHORIZED` | Um cabeçalho está ausente. |
| 100921-401 | 401 | `UNAUTHORIZED` | Um `imsOrgId` inválido foi fornecido. |
| 100922-401 | 401 | `UNAUTHORIZED` | Você não está autorizado a usar as APIs de públicos-alvo externos. |
| 100940-404 | 404 | `NOT_FOUND` | O público-alvo solicitado não foi encontrado. |
| 100950-409 | 409 | `DUPLICATE_RESOURCE` | O público já existe. |
| 100960-422 | 422 | `UNPROCESSABLE_ENTITY` | A estrutura de solicitação é válida, mas não pode ser processada devido a erros lógicos ou semânticos. |
| 100970-500 | 500 | `INTERNAL_SERVER_ERROR` | Houve um problema ao processar a solicitação no sistema. |
| 100970-502 | 502 | `BAD_GATEWAY` | Há problemas de dependência downstream. |
