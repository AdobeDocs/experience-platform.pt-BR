---
title: Endpoint da API de Pacotes de Ferramentas de Sandbox
description: O ponto de extremidade /packages na API de ferramentas da sandbox permite gerenciar programaticamente pacotes no Adobe Experience Platform.
exl-id: 46efee26-d897-4941-baf4-d5ca0b8311f0
source-git-commit: 1e271a88890f41f66aad93d96dbef23a09d33077
workflow-type: tm+mt
source-wordcount: '2541'
ht-degree: 10%

---

# Endpoint de pacotes

As ferramentas de sandbox permitem selecionar diferentes artefatos (também conhecidos como objetos) e exportá-los em um pacote. Um pacote pode consistir em um único artefato ou em vários artefatos (como conjuntos de dados ou esquemas). Todos os artefatos incluídos em um pacote devem ser da mesma sandbox.

O ponto de extremidade `/packages` na API de ferramentas da sandbox permite gerenciar de forma programática os pacotes em sua organização, incluindo a publicação de um pacote e a importação de um pacote para uma sandbox.

## Criar um pacote {#create}

Você pode criar um pacote de vários artefatos fazendo uma solicitação POST para o ponto de extremidade `/packages` e fornecendo valores para o nome e o tipo do pacote.

**Formato da API**

```http
POST /packages/
```

**Solicitação**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "name": "acme",
      "description": "Acme Business Group",
      "packageType": "PARTIAL",    
      "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
      },
      "expiry": "2023-05-20T20:05:10Z",
      "artifacts": [
        {
          "id": "27115daa-c92b-4f17-a077-d65ffeb0c525",
          "type": "PROFILE_SEGMENT",
          "title": "Acme Profile Segment"
        }      
      ]
  }'
```

| Propriedade | Descrição | Tipo | Obrigatório |
| --- | --- | --- | --- |
| `name` | O nome do seu pacote. | String | Sim |
| `description` | Uma descrição para fornecer mais informações sobre o pacote. | String | Não |
| `packageType` | O tipo de pacote é **PARCIAL** para indicar que você está incluindo artefatos específicos em um pacote. | String | SIM |
| `sourceSandbox` | A sandbox de origem do pacote. | Objeto | Não |
| `expiry` | O carimbo de data e hora que define a data de expiração do pacote. O valor padrão é 90 dias a partir da data de criação. O campo de expiração da resposta será a hora UTC da época. | String (formato de carimbo de data e hora UTC) | Não |
| `artifacts` | Uma lista de artefatos a serem exportados para o pacote. O valor `artifacts` deve ser **nulo** ou **vazio**, quando `packageType` for `FULL`. | Matriz | Não |

**Resposta**

Uma resposta bem-sucedida retorna o pacote recém-criado. A resposta inclui a ID do pacote correspondente, bem como informações sobre status, expiração e lista de artefatos.

```json
{
    "id": "209f886b00444eac9bb5836fe32e7681",
    "version": 0,
    "createdDate": 1684475012105,
    "modifiedDate": 1684475012105,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "requestId": "devxa54a6b56d04f46119d9e3cc006fcc1cb",
    "userId": "platform_exim",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "cjm-mr",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },     
    "packageType": "PARTIAL",
    "expiry": 1684613110000,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

## Atualizar um pacote {#update}

Você pode atualizar um pacote fazendo uma solicitação PUT para o ponto de extremidade `/packages`.

### Adicionar artefatos a um pacote {#add-artifacts}

Para adicionar artefatos a um pacote, você deve fornecer um `id` e incluir **ADD** para o `action`.

**Formato da API**

```http
PUT /packages/
```

**Solicitação**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "ADD",
      "expiry": "2023-05-20T20:05:10Z", 
      "artifacts": [
        {
         "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
         "type": "JOURNEY"
        }      
      ]
  }'
```

| Propriedade | Descrição | Tipo | Obrigatório |
| --- | --- | --- | --- |
| `id` | A ID do pacote a ser atualizado. | String | Sim |
| `action` | Para adicionar artefatos ao pacote, o valor da ação deve ser **ADICIONAR**. Esta ação só tem suporte para tipos de pacote **PARTIAL**. | String | Sim |
| `artifacts` | Uma lista de artefatos a serem adicionados ao pacote. Não haveria alteração no pacote se a lista fosse **nula** ou **vazia**. Os artefatos são deduplicados antes de serem adicionados ao pacote. Consulte a tabela abaixo para obter uma lista completa de artefatos compatíveis. | Matriz | Não |
| `expiry` | O carimbo de data e hora que define a data de expiração do pacote. O valor padrão é 90 dias a partir do momento em que a API de PUT é chamada, se a expiração não for especificada na carga. O campo de expiração da resposta será a hora UTC da época. | String (formato de carimbo de data e hora UTC) | Não |

Os seguintes tipos de artefatos são suportados no momento.

| Artefato | Plataforma | Objeto | Fluxo parcial | Sandbox completa |
| --- | --- | --- | --- | --- |
| `JOURNEY` | Adobe Journey Optimizer | Jornadas | Sim | Não |
| `ID_NAMESPACE` | Plataforma de dados do cliente | Identidades | Sim | Sim |
| `REGISTRY_DATATYPE` | Plataforma de dados do cliente | Tipo de dados | Sim | Sim |
| `REGISTRY_CLASS` | Plataforma de dados do cliente | Classe | Sim | Sim |
| `REGISTRY_MIXIN` | Plataforma de dados do cliente | Grupo de campos | Sim | Sim |
| `REGISTRY_SCHEMA` | Plataforma de dados do cliente | Esquemas | Sim | Sim |
| `CATALOG_DATASET` | Plataforma de dados do cliente | Conjuntos de dados | Sim | Sim |
| `DULE_CONSENT_POLICY` | Plataforma de dados do cliente | Políticas de consentimento e governança | Sim | Sim |
| `PROFILE_SEGMENT` | Plataforma de dados do cliente | Públicos-alvo | Sim | Sim |
| `FLOW` | Plataforma de dados do cliente | Fluxo de dados de origens | Sim | Sim |

**Resposta**

Uma resposta bem-sucedida retorna o pacote atualizado. A resposta inclui a ID do pacote correspondente, bem como informações sobre status, expiração e lista de artefatos.

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 4,
    "createdDate": 1684235842000,
    "modifiedDate": 1684475861366,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },     
    "packageType": "PARTIAL",
    "expiry": 1692251861352,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        },
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

### Excluir artefatos de um pacote {#delete-artifacts}

Para excluir artefatos de um pacote, você deve fornecer um `id` e incluir **DELETE** para o `action`.

**Formato da API**

```http
PUT /packages/
```

**Solicitação**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "DELETE",
      "artifacts": [
        {
          "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
          "type": "JOURNEY"
        }      
      ]
  }'
```

| Propriedade | Descrição | Tipo | Obrigatório |
| --- | --- | --- | --- |
| `id` | A ID do pacote a ser atualizado. | String | Sim |
| `action` | Para excluir artefatos de um pacote, o valor da ação deve ser **DELETE**. Esta ação só tem suporte para tipos de pacote **PARTIAL**. | String | Sim |
| `artifacts` | Uma lista de artefatos a serem excluídos do pacote. Não haveria alteração no pacote se a lista fosse **nula** ou **vazia**. | Matriz | Não |

**Resposta**

Uma resposta bem-sucedida retorna o pacote atualizado. A resposta inclui a ID do pacote correspondente, bem como informações sobre status, expiração e lista de artefatos.

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 5,
    "createdDate": 1684235842000,
    "modifiedDate": 1684478830416,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },      
    "packageType": "PARTIAL",
    "expiry": 1692254830403,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

### Atualizar campos de metadados em um pacote {#update-metadata}

>[!NOTE]
>
>A ação **UPDATE** é usada para atualizar os campos de metadados do pacote e **não pode** ser usada para adicionar/excluir artefatos a um pacote.

Para atualizar os campos de metadados em um pacote, você deve fornecer um `id` e incluir **UPDATE** para o `action`.

**Formato da API**

```http
PUT /packages/
```

**Solicitação**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "UPDATE",
      "name": "acme",
      "description": "Acme Business Group",  
      "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
      }
  }'
```

| Propriedade | Descrição | Tipo | Obrigatório |
| --- | --- | --- | --- |
| `id` | A ID do pacote a ser atualizado. | String | Sim |
| `action` | Para atualizar os campos de metadados em um pacote, o valor da ação deve ser **UPDATE**. Esta ação só tem suporte para tipos de pacote **PARTIAL**. | String | Sim |
| `name` | O nome atualizado do pacote. Não são permitidos nomes de pacote duplicados. | Matriz | Sim |
| `sourceSandbox` | A sandbox da Source deve pertencer à mesma organização especificada no cabeçalho da solicitação. | Objeto | Sim |

**Resposta**

Uma resposta bem-sucedida retorna o pacote atualizado. A resposta inclui a ID do pacote correspondente, bem como informações sobre sua descrição, status, expiração e lista de artefatos.

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 6,
    "createdDate": 1684235842000,
    "modifiedDate": 1684479094129,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",    
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "packageType": "PARTIAL",
    "expiry": 1692255094127,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

## Excluir um pacote {#delete}

Para excluir um pacote, faça uma solicitação DELETE para o ponto de extremidade `/packages` e especifique a ID do pacote que deseja excluir.

**Formato da API**

```http
DELETE /packages/{PACKAGE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{PACKAGE_ID}` | A ID do pacote que você deseja excluir. |

**Solicitação**

A solicitação a seguir exclui o pacote com a ID {PACKAGE_ID}.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Resposta**

Uma resposta bem-sucedida retorna um motivo que mostra a ID do pacote excluída.

```json
{
    "reason": "Package d30e0424a37b46ada6a5cf37f47a86ff deleted"
}
```

## Publish um pacote {#publish}

Para habilitar a importação de um pacote em uma sandbox, você deve publicá-lo. Faça uma solicitação GET para o ponto de extremidade `/packages` ao especificar a ID do pacote que você deseja publicar.

**Formato da API**

```http
GET /packages/{PACKAGE_ID}/export
```

| Parâmetro | Descrição |
| --- | --- |
| `{PACKAGE_ID}` | A ID do pacote que você deseja publicar. |

**Solicitação**

A solicitação a seguir publica o pacote com a ID {PACKAGE_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}\export \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

| Propriedade | Descrição | Tipo | Obrigatório |
| --- | --- | --- | --- |
| `expiryPeriod` | Esse período especificado pelo usuário define a data de expiração do pacote (em dias) a partir da hora em que o pacote foi publicado. Esse valor não deve ser negativo.<br> Se nenhum valor for especificado, o padrão será calculado como 90 (dias) a partir da data de publicação. | Número inteiro | Não |

**Resposta**

Uma resposta bem-sucedida retorna o pacote publicado.

```json
{
    "name": "acme",
    "description": "Acme Business Group",
    "visibility": "TENANT",
    "sourceSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "type": "PARTIAL",
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285"
}
```

## Pesquisar um pacote {#look-up-package}

Você pode pesquisar um pacote individual fazendo uma solicitação GET para o ponto de extremidade `/packages` que inclui a ID correspondente do pacote no caminho da solicitação.

**Formato da API**

```http
GET /packages/{PACKAGE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{PACKAGE_ID}` | A ID do pacote que você deseja pesquisar. |

**Solicitação**

A solicitação a seguir recupera informações de {PACKAGE_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Resposta**

Uma resposta bem-sucedida retorna detalhes da ID de pacote consultada. A resposta inclui o nome, a descrição, a data de publicação e a data de expiração, a sandbox de origem do pacote, bem como uma lista de artefatos.

```json
{
    "id": "8f585fad94d042cd82dbcba594108a41",
    "version": 2,
    "createdDate": 1685597784000,
    "modifiedDate": 1685597810000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
    "packageType": "PARTIAL",
    "expiry": 1693373810000,
    "publishDate": 1685597810000,
    "status": "PUBLISHED",
    "artifactsList": [
        {
            "id": "f4f57771-2bd2-469a-9c13-8d803eeb6515",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        },
        {
            "id": "7f4caca7-a477-400d-a41e-c4735f8e780d",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ],
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    }
}
```

## Listar pacotes {#list-packages}

Você pode listar todos os pacotes em sua organização fazendo uma solicitação GET para o ponto de extremidade `/packages`.

**Formato da API**

```http
GET /packages/?{QUERY_PARAMS}
```

| Parâmetro | Descrição |
| --- | --- |
| `{QUERY_PARAMS}` | Parâmetros de consulta opcionais para filtrar os resultados. Consulte a seção sobre [parâmetros de consulta](./appendix.md) para obter mais informações. |

**Solicitação**

A solicitação a seguir recupera informações dos pacotes com base em {QUERY_PARAMS}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/?property=status==DRAFT,PUBLISHED&property=createdDate>=2023-05-11T18:29:59.999Z&property=createdDate<=2023-05-16T18:29:59.999Z&start=0&orderby=-createdDate&limit=20 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de pacotes pertencentes à sua organização, incluindo detalhes como nome, status, expiração e lista de artefatos.

```json
{
    "totalElements": 109,
    "currentPage": 0,
    "totalPages": 6,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "8f585fad94d042cd82dbcba594108a41",
            "version": 2,
            "createdDate": 1685597784000,
            "modifiedDate": 1685597810000,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "tenantId": "c875b077162b40409c1327b16da99c1b",
            "name": "acme",
            "description": "Acme Business Group",
            "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
            "packageType": "PARTIAL",
            "expiry": 1693373810000,
            "publishDate": 1685597810000,
            "status": "PUBLISHED",
            "artifactsList": [
                {
                    "id": "f4f57771-2bd2-469a-9c13-8d803eeb6515",
                    "type": "JOURNEY",
                    "found": false,
                    "count": 0
                },
                {
                    "id": "7f4caca7-a477-400d-a41e-c4735f8e780d",
                    "type": "JOURNEY",
                    "found": false,
                    "count": 0
                }
            ],
            "sourceSandbox": {
                "name": "acme-sandbox",
                "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
            }
        },
        {
            "id": "0d7e427ce4cb4dc1b78e30ef61b125c1",
            "version": 2,
            "createdDate": 1685555213000,
            "modifiedDate": 1685555275000,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "tenantId": "7d7d8bbe3c7c4a8ea701cc5e42c57aeb",
            "name": "acme",
            "description": "Acme Business Group",
            "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
            "packageType": "PARTIAL",
            "expiry": 1693331275000,
            "publishDate": 1685555275000,
            "status": "PUBLISHED",
            "artifactsList": [
                {
                    "id": "626a9669a9f5b818db270e95",
                    "type": "CATALOG_DATASET",
                    "found": false,
                    "count": 0
                }
            ],
            "sourceSandbox": {
                "name": "acme-sandbox",
                "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
            }
        }
    ]
}
```

## Importar um pacote {#import}

Esse ponto de extremidade é usado para buscar os objetos conflitantes na sandbox de destino especificada. Objetos conflitantes representam objetos semelhantes que já estão presentes na sandbox de destino.

**Formato da API**

```http
GET /packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName
```

| Parâmetro | Descrição |
| --- | --- |
| `{PACKAGE_ID}` | A ID do pacote que você deseja pesquisar. |

**Solicitação**

A solicitação a seguir importa o {PACKAGE_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Os conflitos são retornados na resposta. A resposta mostra o pacote original mais o fragmento `alternatives` como uma matriz ordenada por classificação.

+++Exibir resposta

```json
[
    {
        "artifact": {
            "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
            "type": "REGISTRY_SCHEMA",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/176f33f6a8ff6542de1256f8dc01cce4be1b3a68fd5f5bc5",
                "type": "REGISTRY_SCHEMA",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870_1686403052050"
            },
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/1b37c3403e4e12c7aa46ea9dfe380a9f2b72d4da9db62b46",
                "type": "REGISTRY_SCHEMA",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870_1686218766627"
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::REGISTRY_SCHEMA::https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c"
    },
    {
        "artifact": {
            "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
            "type": "REGISTRY_CLASS",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "https://ns.adobe.com/cjmstage/classes/1dd81d61cdaa89a89382d0a424db77494475bd1db3105feb",
                "type": "REGISTRY_CLASS",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870_1686564843736"
            },
            {
                "id": "https://ns.adobe.com/cjmstage/classes/2511fb5396a630b2cd3d5d9e9b69d42ce66a4289db8ac917",
                "type": "REGISTRY_CLASS",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870_1686408152916"
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::REGISTRY_CLASS::https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26"
    },
    {
        "artifact": {
            "id": "4d4c874ec3344d64bf8b3160e60ac78b",
            "type": "MAPPING_SET",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: 4d4c874ec3344d64bf8b3160e60ac78b"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "6b49c959d77c48e9904f7616fe2e7848",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            },
            {
                "id": "7b363da9e6704afb9716f57193d5246f",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            },
            {
                "id": "93ca0b4f437c4eaf9f1986408679e965",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::MAPPING_SET::4d4c874ec3344d64bf8b3160e60ac78b"
    }
]
```

+++

## Enviar uma importação {#submit-import}

>[!NOTE]
>
>É inerente à resolução de conflitos que o artefato alternativo já exista na sandbox de destino.

Você pode enviar uma importação para um pacote depois de ter revisado conflitos e fornecido substituições fazendo uma solicitação POST para o ponto de extremidade `/packages`. O resultado é fornecido como uma carga, o que inicia o trabalho de importação para a sandbox de destino, conforme especificado na carga.

A carga também aceita o nome e a descrição do trabalho especificado pelo usuário para o trabalho de importação. Se o nome e a descrição especificados pelo usuário não estiverem disponíveis, o nome e a descrição do pacote serão usados para o nome e a descrição do trabalho.

**Formato da API**

```http
POST /packages/import
```

**Solicitação**

A solicitação a seguir recupera pacotes a serem importados. A carga é um mapa de substituições em que, se existir uma entrada, a chave é o `artifactId` fornecido pelo pacote, e a alternativa é o valor. Se o mapa ou conteúdo estiver **vazio**, nenhuma substituição será executada.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages/import/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
       "id": "09484a599f5f4a5faa43986643964615",
       "name": "acme",
       "description": "Acme Business Group",
       "destinationSandbox": {
         "name": "cjm-mr",
         "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
     },
     "alternatives": {
       "https://ns.adobe.com/cjmstage/schemas/ac33bbd22eb4ad6656e1c7e12e9f520261fb39fd28a902a9": {
         "id": "https://ns.adobe.com/cjmstage/schemas/a3b935344685afad4e52c753161cf673ec23d4fb1b3e9ce",
         "type": "REGISTRY_SCHEMA"
       }
     }
  }'
```

| Propriedade | Descrição | Tipo | Obrigatório |
| --- | --- | --- | --- |
| `alternatives` | `alternatives` representa o mapeamento dos artefatos da sandbox de origem para os artefatos da sandbox de destino existentes. Como já estão lá, o trabalho de importação evita a criação desses artefatos na sandbox de destino. | String | Não |

**Resposta**

```json
{
    "name": "acme",
    "description": "Acme Business Group",
    "visibility": "TENANT",
    "sourceSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "destinationSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "type": "PARTIAL",
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285"
}
```

## Listar todos os objetos dependentes {#dependent-objects}

Liste todos os objetos dependentes dos objetos exportados em um pacote fazendo uma solicitação POST para o ponto de extremidade `/packages` ao especificar a ID do pacote.

**Formato da API**

```http
POST /packages/{PACKAGE_ID}/children
```

| Parâmetro | Descrição |
| --- | --- |
| `{PACKAGE_ID}` | A ID do pacote. |

**Solicitação**

A solicitação a seguir lista todos os objetos dependentes de {PACKAGE_ID}.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d'[
      {
        "id": "4d4c874ec3344d64bf8b3160e60ac78b",
        "type": "MAPPING_SET"
      },
      {
        "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
        "type": "REGISTRY_SCHEMA"
      },
      {
        "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
        "type": "REGISTRY_CLASS"
      }
  ]'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de filhos dos objetos.

```json
[
    {
        "id": "4d4c874ec3344d64bf8b3160e60ac78b",
        "title": "4d4c874ec3344d64bf8b3160e60ac78b",
        "type": "MAPPING_SET",
        "children": [
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870",
                "type": "REGISTRY_SCHEMA"
            }
        ]
    },
    {
        "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
        "title": "Dean Dataset 1 - adhoc schema - 1618950408870",
        "type": "REGISTRY_SCHEMA",
        "children": [
            {
                "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870",
                "type": "REGISTRY_CLASS"
            }
        ]
    },
    {
        "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
        "title": "Dean Dataset 1 - Adhoc class - 1618950408870",
        "type": "REGISTRY_CLASS",
        "children": []
    }
]
```

## Verificar permissões com base em função para importar todos os artefatos do pacote {#role-based-permissions}

Você pode verificar se tem permissões para importar artefatos de pacote fazendo uma solicitação GET para o ponto de extremidade `/packages` ao especificar a ID do pacote e o nome da sandbox de destino.

**Formato da API**

```http
GET /packages/preflight/{packageId}?targetSandbox=<sandbox_name
```

| Parâmetro | Descrição |
| --- | --- |
| `{PACKAGE_ID}` | A ID do pacote que você deseja importar. |

**Solicitação**

A solicitação a seguir verifica suas permissões para o {PACKAGE_ID} e a sandbox.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/preflight/{PACKAGE_ID}?targetSandbox=<sandbox_name> \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma resposta bem-sucedida retorna as permissões de recurso para a sandbox de destino, incluindo uma lista de permissões necessárias, permissões ausentes, tipo de artefato e uma decisão sobre se a criação é permitida.

+++Exibir resposta

```json
{
  "packageID": "b7bda68eb1214c86824f1d7204616e51",
  "targetSandboxName": "acme-sandbox",
  "permissionResponse": [
    {
      "artifactID": "4aca57b6-8b83-450b-a460-e8a07ca79a44",
      "requiredPermissions": {
        "resources": [
          {
            "palmResourceType": "Sandbox",
            "resourcePermissions": [
              "view"
            ]
          },
          {
            "palmResourceType": "Schema",
            "resourcePermissions": [
              "read"
            ]
          },
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "read"
            ]
          },
          {
            "palmResourceType": "Segment",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Composition",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Query",
            "resourcePermissions": [
              "write"
            ]
          },
          {
            "palmResourceType": "SegmentDashboard",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "missingPermissions": {
        "resources": []
      },
      "artifactType": "PROFILE_SEGMENT",
      "creationAllowed": true
    },
    {
      "artifactID": "36bb82bc-a00d-4d6b-a598-227d43e027c1",
      "requiredPermissions": {
        "resources": [
          {
            "palmResourceType": "Sandbox",
            "resourcePermissions": [
              "view"
            ]
          },
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Dataset",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "missingPermissions": {
        "resources": [
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Dataset",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "artifactType": "PROFILE_MERGE",
      "creationAllowed": false
    }
  ]
}
```

+++

## Listar trabalhos de exportação/importação {#list-jobs}

Você pode listar trabalhos atuais de exportação/importação fazendo uma solicitação GET para o ponto de extremidade `/packages`.

**Formato da API**

```http
GET /packages/jobs?{QUERY_PARAMS}
```

| Parâmetro | Descrição |
| --- | --- |
| `{QUERY_PARAMS}` | Parâmetros de consulta opcionais para filtrar os resultados. Consulte a seção sobre [parâmetros de consulta](./appendix.md) para obter mais informações. |

**Solicitação**

A solicitação a seguir lista todos os trabalhos de importação bem-sucedidos.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/jobs?property=requestType==IMPORT&property=jobStatus==SUCCESS&orderby=createdDate&start=0&limit=5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Resposta**

Uma resposta bem-sucedida retorna todos os trabalhos de importação bem-sucedidos.

```json
{
    "totalElements": 42,
    "currentPage": 0,
    "totalPages": 9,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "3c1b92cf47a246d7bfbe6fd507c5d543",
            "name": "acme",
            "updated": 1685973675401,
            "created": 1685973675401,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "ead59d21405f4184a94dd786a1bf040d",
            "name": "acme1",
            "updated": 1685986367198,
            "created": 1685986367198,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "85ddaa3c2f6c475088167cde7a9d4326",
            "name": "acme2",
            "updated": 1686147692568,
            "created": 1686147692568,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "c49a4fcb31954cbd828ece1da096c8f5",
            "name": "acme3",
            "updated": 1686148007586,
            "created": 1686148007586,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "a3669315baed4cf2af49bf9ce90b8158",
            "name": "acme4",
            "updated": 1686148651910,
            "created": 1686148651910,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        }
    ]
}
```

## Compartilhar pacotes entre organizações {#org-linking}

O ponto de extremidade `/handshake` na API de ferramentas da sandbox permite que você faça parceria com outras organizações para compartilhar pacotes.

### Envio de uma solicitação de compartilhamento {#send-request}

Envie uma solicitação a uma organização parceira de destino para compartilhar aprovação fazendo uma solicitação POST para o ponto de extremidade `/handshake/bulkCreate`. Isso é necessário antes de compartilhar pacotes privados.

**Formato da API**

```http
POST /handshake/bulkCreate
```

**Solicitação**

A solicitação a seguir inicia o compartilhamento de aprovação entre uma organização parceira de destino e a organização de origem.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/handshake/bulkCreate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "targetIMSOrgIds":["acme@AdobeOrg"],
      "sourceIMSDetails":{
        "id":"acme@AdobeOrg",
        "name":"acme_org"
      } 
  }' 
```

| Propriedade | Descrição | Tipo | Obrigatório |
| --- | --- | --- | --- |
| `targetIMSOrgIds` | Uma lista de organizações de destino para enviar solicitação de compartilhamento. | Matriz | Sim |
| `sourceIMSDetails` | Detalhes sobre a organização de origem. | Objeto | Sim |

**Resposta**

Uma resposta bem-sucedida retorna detalhes sobre sua solicitação de compartilhamento.

```json
{
    "successfulRequests": {
        "acme@AdobeOrg": {
            "id": "{ID}",
            "version": 0,
            "createdDate": 1724938816798,
            "modifiedDate": 1724938816798,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "sourceIMSOrgId": "{ORG_ID}",
            "targetIMSOrgId": "{TARGET_ID}",
            "sourceRegion": "va6",
            "sourceIMSOrgName": "{SOURCE_NAME}",
            "status": "APPROVAL_PENDING",
            "createdByName": "{CREATED_BY}",
            "modifiedByName": "{MODIFIED_BY}",
            "modifiedByIMSOrgId": "{ORG_ID}",
            "statusHistory": "[{\"actionTakenBy\":\"acme@98ff67fa661fdf6549420b.e\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"INITIATED\",\"actionTimeStamp\":1724938816885}]",
            "linkingId": "{LINKIND_ID}"
        }
    },
    "failedRequests": {}
}
```

### Aprovação de solicitações de compartilhamento recebidas {#approve-requests}

Aprove as solicitações de compartilhamento das organizações parceiras de destino fazendo uma solicitação POST para o ponto de extremidade `/handshake/action`. Após a aprovação, as organizações de parceiros de origem podem compartilhar pacotes privados.

**Formato da API**

```http
POST /handshake/action
```

**Solicitações**

A solicitação a seguir aprova uma solicitação de compartilhamento de uma organização parceira de destino.

```shell
curl -X POST  \
  https://platform.adobe.io/data/foundation/exim/handshake/action \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "linkingID":"{LINKING_ID}",
      "status":"APPROVED",
      "reason":"Done",
      "targetIMSOrgDetails":{
          "id":"acme@AdobeOrg",
          "name":"acme",
          "region":"va7"
      }
  }'
```

| Propriedade | Descrição | Tipo | Obrigatório |
| --- | --- | --- | --- |
| `linkingID` | A ID da solicitação de compartilhamento à qual você está respondendo. | String | Sim |
| `status` | A ação que está sendo tomada na solicitação de compartilhamento. | String | Sim |
| `reason` | O motivo pelo qual a ação está sendo executada. | String | Sim |
| `targetIMSOrgDetails` | Detalhes sobre a organização de destino onde o valor da ID deve ser a **ID** da organização de destino, o valor do nome deve ser o **NAME** da organização de destino e o valor da região deve ser a **REGION** da organização de destino. | Objeto | Sim |

**Resposta**

Uma resposta bem-sucedida retorna detalhes sobre a solicitação de compartilhamento aprovada.

```json
{
    "id": "{ID}",
    "version": 1,
    "createdDate": 1726737474000,
    "modifiedDate": 1726737541731,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sourceIMSOrgId": "{ORG_ID}",
    "targetIMSOrgId": "{TARGET_ID}",
    "sourceRegion": "va7",
    "targetRegion": "va7",
    "sourceOrgName": "{SOURCE_ORG}",
    "targetOrgName": "{TARGET_ORG}",
    "status": "APPROVED",
    "createdByName": "{CREATED_BY}",
    "modifiedByIMSOrgId": "{MODIFIED_BY}",
    "statusHistory": "[{\"actionTakenBy\":\"{ACTION_BY}\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"acme@AdobeOrg\",\"action\":\"INITIATED\",\"actionTimeStamp\":1726737474450,\"reason\":null},{\"actionTakenBy\":null,\"actionTakenByName\":null,\"actionTakenByImsOrgID\":\"745F37C35E4B776E0A49421B@AdobeOrg\",\"action\":\"APPROVED\",\"actionTimeStamp\":1726737541818,\"reason\":\"Done\"}]",
    "linkingId": "{LINKING_ID}"
}
```

### Listar solicitações de compartilhamento de saída/entrada {#outgoing-and-incoming-requests}

Liste as solicitações de compartilhamento de entrada e saída fazendo uma solicitação GET para o ponto de extremidade `handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING`.

**Formato da API**

```http
POST handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING
```

| Parâmetro | Valores aceitos/padrão |
| --- | --- |
| `property` | Especifica a propriedade pela qual filtrar, como status. Os valores aceitáveis para o status são: `APPROVED`, `REJECTED` e `IN_PROGRESS`. |
| `start` | O valor padrão de início é `0`. |
| `limit` | O valor padrão do limite é `20`. |
| `orderBy` | Classifica registros em ordem crescente ou decrescente. |
| `requestType` | Aceita `INCOMING` ou `OUTGOING`. |

**Solicitação**

A solicitação a seguir retorna uma lista de todas as solicitações de compartilhamento de entrada e saída.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id:{ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de solicitações de compartilhamento de entrada e saída e seus detalhes.

```json
{
    "totalElements": 1,
    "currentPage": 0,
    "totalPages": 1,
    "hasPreviousPage": false,
    "hasNextPage": false,
    "data": [
        {
            "id": "{ID}",
            "version": 1,
            "createdDate": 1724929446000,
            "modifiedDate": 1724929617000,
            "modifiedBy": "{MODIFIED_BY}",
            "sourceIMSOrgId": "{ORG_ID}",
            "targetIMSOrgId": "{TARGET_ID}",
            "sourceRegion": "va7",
            "targetRegion": "va6",
             "sourceOrgName": "{SOURCE_ORG}",
            "targetOrgName": "{TARGET_ORG}",
            "status": "APPROVED",
            "createdByName": "{CREATED_BY}",
            "modifiedByName": "{MODIFIED_BY}",
            "modifiedByIMSOrgId": "{MODIFIED_BY}",
            "statusHistory": "[{\"actionTakenBy\":\"{ACTION_BY}\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"INITIATED\",\"actionTimeStamp\":1724929442467,\"reason\":null},{\"actionTakenBy\":null,\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"APPROVED\",\"actionTimeStamp\":1724929617531,\"reason\":\"Done\"}]",
            "linkingId": "{LINKING_ID}"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

## Transferir pacotes

Use o ponto de extremidade `/transfer` na API de ferramentas da sandbox para buscar e criar novas solicitações de compartilhamento de pacotes.

### Nova solicitação de compartilhamento {#share-request}

Busque um pacote de uma organização de origem publicada e compartilhe-o com uma organização de destino fazendo uma solicitação POST para o ponto de extremidade `/transfer` e, ao mesmo tempo, fornecendo a ID do pacote e a ID da organização de destino.

**Formato da API**

```http
POST /transfer
```

**Solicitação**

A solicitação a seguir busca um pacote de organizações de origem e o compartilha com uma organização de destino.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/transfer/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "packageId": "{PACKAGE_ID}",
      "targets": [
          {
              "imsOrgId": "{TARGET_IMS_ORG}"
          }
      ]
  }'
```

| Propriedade | Descrição | Tipo | Obrigatório |
| --- | --- | --- | --- |
| `packageId` | A ID do pacote que você deseja compartilhar. | String | Sim |
| `targets` | Uma lista de organizações com as quais compartilhar pacotes. | Matriz | Sim |

**Resposta**

Uma resposta bem-sucedida retorna detalhes do pacote solicitado e seu status de compartilhamento.

```json
[
    {
        "id": "{ID}",
        "version": 0,
        "createdDate": 1726480559313,
        "modifiedDate": 1726480559313,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceIMSOrgId": "{ORG_ID}",
        "targetIMSOrgId": "{TARGET_ID}",
        "packageId": "{PACKAGE_ID}",
        "status": "PENDING",
        "initiatedBy": "acme@3ec9197a65a86f34494221.e",
        "transferDetails": {
            "messages": [
                "Fetched Package",
                "Fetched Manifest"
            ],
            "additionalMetadata": null
        },
        "requestType": "PRIVATE"
    }
]
```

### Buscar uma solicitação de compartilhamento por ID {#fetch-transfer-by-id}

Busque os detalhes de uma solicitação de compartilhamento fazendo uma solicitação GET para o ponto de extremidade `/transfer/{TRANSFER_ID}` ao fornecer a ID de transferência.

**Formato da API**

```http
GET /transfer/{TRANSFER_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{TRANSFER_ID}` | A ID da transferência que você deseja buscar. |

**Solicitação**

A solicitação a seguir busca uma transferência com a ID {TRANSFER_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/0c843180a64c445ca1beece339abc04b \
  -H 'x-api-key: {API__KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Resposta**

Uma resposta bem-sucedida retorna detalhes de uma solicitação de compartilhamento.

```json
{
    "id": "{ID}",
    "sourceIMSOrgId": "{ORG_ID}",
    "sourceOrgName": "{SOURCE_ORG}",
    "targetIMSOrgId": "{TARGET_ID}",
    "targetOrgName": "{TARGET_ORG}",
    "packageId": "{PACKAGE_ID}",
    "packageName": "{PACKAGE_NAME}",
    "status": "COMPLETED",
    "initiatedBy": "{INITIATED_BY}",
    "createdDate": 1724442856000,
    "transferDetails": {
        "messages": [
            "Fetched Package",
            "Fetched Manifest",
            "Tenant Identified",
            "Fetched Sandbox Id",
            "Fetched Blob Files",
            "Message Published to Kafka",
            "Completed Transfer"
        ],
        "additionalMetadata": null
    },
    "requestType": "PRIVATE"
}
```

### Obter lista de compartilhamento {#transfers-list}

Busque uma lista de solicitações de transferência fazendo uma solicitação GET para o ponto de extremidade `/transfer/list?{QUERY_PARAMETERS}`, alterando os parâmetros de consulta conforme necessário.

**Formato da API**

```http
GET `/transfer/list?{QUERY_PARAMETERS}`
```

| Parâmetro | Valores aceitos/padrão |
| --- | --- |
| `property` | Especifica a propriedade pela qual filtrar, como status. Os valores aceitáveis para o status são: `COMPLETED`, `PENDING`, `IN_PROGRESS`, `FAILED`. |
| `start` | O valor padrão de início é `0`. |
| `limit` | O valor padrão do limite é `20`. |
| `orderBy` | A ordenação só aceita o campo `createdDate`. |

**Solicitação**

A solicitação a seguir busca uma lista de solicitações de transferência dos parâmetros de pesquisa fornecidos.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/list?property=status==COMPLETED&start=0&limit=2&orderBy=-createdDate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de todas as solicitações de transferência dos parâmetros de pesquisa fornecidos.

```json
{
    "totalElements": 43,
    "currentPage": 0,
    "totalPages": 22,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_ORG}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "{PACKAGE_NAME}",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1726129077000,
            "createdDate": 1726129062000,
            "transferDetails": {
                "messages": [
                    "Fetched Package",
                    "Fetched Manifest",
                    "Tenant Identified",
                    "Fetched Sandbox Id",
                    "Fetched Blob Files",
                    "Message Published to Kafka",
                    "Completed Transfer",
                    "Finished with status: COMPLETED"
                ],
                "additionalMetadata": null
            },
            "requestType": "PRIVATE"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_ORG}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "{PACKAGE_NAME}",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1726066046000,
            "createdDate": 1726065936000,
            "transferDetails": {
                "messages": [
                    "Fetched Package",
                    "Fetched Manifest",
                    "Tenant Identified",
                    "Fetched Sandbox Id",
                    "Fetched Blob Files",
                    "Message Published to Kafka",
                    "Completed Transfer",
                    "Finished with status: COMPLETED"
                ],
                "additionalMetadata": null
            },
            "requestType": "PRIVATE"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

### Atualizar disponibilidade do pacote de privado para público {#update-availability}

Altere um pacote de privado para público fazendo uma solicitação GET para o ponto de extremidade `/transfer/list?property=status%3D%3DCOMPLETED%2CFAILED&requestType=PUBLIC`. Por padrão, um pacote é criado com disponibilidade privada.

**Solicitação**

A solicitação a seguir altera a disponibilidade de pacotes de privada para pública.

```shell
curl -X GET \
  http://platform.adobe.io/data/foundation/transfer/list?property=status%3D%3DCOMPLETED%2CFAILED&requestType=PUBLIC \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
      "id":"{ID}",
      "action":"UPDATE",
      "packageVisibility":"PUBLIC"
  }'
```

| Propriedade | Descrição | Tipo | Obrigatório |
| --- | --- | --- | --- |
| `id` | A ID do pacote a ser atualizado. | String | Sim |
| `action` | Para atualizar a visibilidade para pública, o valor da ação deve ser **UPDATE**. | String | Sim |
| `packageVisbility` | Para atualizar a visibilidade, o valor de packageVisibility deve ser **PUBLIC**. | String | Sim |

**Resposta**

Uma resposta bem-sucedida retorna detalhes sobre um pacote e sua visibilidade.

```json
{
    "id": "{ID}",
    "version": 7,
    "createdDate": 1729624618000,
    "modifiedDate": 1729658596340,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "name": "acme",
    "imsOrgId": "{ORG_ID}",
    "packageType": "PARTIAL",
    "expiry": 1737434596325,
    "status": "PUBLISH_FAILED",
    "packageVisibility": "PUBLIC",
    "artifactsList": [
        {
            "id": "{ID}",
            "type": "PROFILE_SEGMENT",
            "found": false,
            "count": 0,
            "title": "Acme Profile Segment"
        }
    ],
    "schemaMapping": {},
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    }
}
```

### Solicitação para importar um pacote público {#pull-public-package}

Importe um pacote de uma organização de origem com disponibilidade pública fazendo uma solicitação POST para o ponto de extremidade `/transfer/pullRequest`.

**Formato da API**

```http
POST /transfer/pullRequest
```

**Solicitação**

A solicitação a seguir importará um pacote e definirá sua disponibilidade para public.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/transfer/pullRequest \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "imsOrgId": "{ORG_ID}",
      "packageId": "{PACKAGE_ID}"
  }'
```

| Propriedade | Descrição | Tipo | Obrigatório |
| --- | --- | --- | --- |
| `imsOrgId` | A ID da organização de origem do pacote. | String | Sim |
| `packageId` | A ID do pacote a ser importado. | String | Sim |

**Resposta**

Uma resposta bem-sucedida retorna detalhes sobre o pacote público importado.

```json
{
    "id": "{ID}",
    "version": 0,
    "createdDate": 1729658890425,
    "modifiedDate": 1729658890425,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sourceIMSOrgId": "{ORG_ID}",
    "targetIMSOrgId": "{TARGET_ID}",
    "packageId": "{PACKAGE_ID}",
    "status": "PENDING",
    "initiatedBy": "{INITIATED_BY}",
    "pipelineMessageId": "{MESSAGE_ID}",
    "requestType": "PUBLIC"
}
```

### Listar pacotes públicos {#list-public-packages}

Busque uma lista de pacotes com visibilidade pública fazendo uma solicitação GET para o ponto de extremidade `/transfer/list?{QUERY_PARAMS}`.

**Formato da API**

```http
GET /transfer/list?{QUERY_PARAMS}
```

| Parâmetro | Valores aceitos/padrão |
| --- | --- |
| `property` | Especifica a propriedade pela qual filtrar, como status. Os valores aceitáveis para o status são: `COMPLETED` e `FAILED`. |
| `start` | O valor padrão de início é `0`. |
| `limit` | O valor padrão do limite é `20`. |
| `orderBy` | A ordenação só aceita o campo `createdDate`. |
| `requestType` | Aceita `PUBLIC` ou `PRIVATE`. |

**Solicitação**

A solicitação a seguir busca uma lista de pacotes com disponibilidade pública.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/list?property=status%3D%3DCOMPLETED%2CFAILED&requestType=PUBLIC&orderby=-createdDate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de pacotes públicos e seus detalhes.

+++Exibir resposta

```json
{
    "totalElements": 14,
    "currentPage": 0,
    "totalPages": 1,
    "hasPreviousPage": false,
    "hasNextPage": false,
    "data": [
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public package demo",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729359318000,
            "createdDate": 1729359316000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public package demo",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729359284000,
            "createdDate": 1729359283000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Test Private Flow Final",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284462000,
            "createdDate": 1729275962000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOUCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Fest",
            "status": "FAILED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284104000,
            "createdDate": 1729253854000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284667000,
            "createdDate": 1729253421000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284957000,
            "createdDate": 1729253143000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284562000,
            "createdDate": 1729252975000,
            "requestType": "PUBLIC"
        },
        {
               "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Private Package Test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284262000,
            "createdDate": 1729229755000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Demo Package 1016",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284784000,
            "createdDate": 1729208888000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284934000,
            "createdDate": 1729153097000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284912000,
            "createdDate": 1729153043000,
            "requestType": "PUBLIC"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

+++

## Copiar carga do pacote (#package-payload)

Você pode copiar a carga de um pacote público fazendo uma solicitação GET para o ponto de extremidade `/packages/payload` que inclui a ID correspondente do pacote no caminho da solicitação.

**Formato da API**

```http
GET /packages/payload/{PACKAGE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{PACKAGE_ID}` | A ID do pacote que você deseja copiar. |

**Solicitação**

A solicitação a seguir busca a carga de um pacote com a ID {PACKAGE_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/payload/{PACKAGE_ID} \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "imsOrgId": "{ORG_ID}",
      "packageId": "{PACKAGE_ID}"
  }'
```

| Propriedade | Descrição | Tipo | Obrigatório |
| --- | --- | --- | --- |
| `imsOrdId` | A ID da organização à qual o pacote pertence. | String | Sim |
| `packageId` | A ID do pacote cuja carga você está solicitando. | String | Sim |

**Resposta**

Uma resposta bem-sucedida retorna a carga do pacote.

```json
{
    "imsOrgId": "{ORG_ID}",
    "packageId": "{PACKAGE_ID}"
}
```
