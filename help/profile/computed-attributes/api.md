---
title: Endpoint da API de atributos computados
description: Saiba como criar, exibir, atualizar e excluir atributos calculados usando a API de perfil do cliente em tempo real.
exl-id: f217891c-574d-4a64-9d04-afc436cf16a9
source-git-commit: 49196473f304585193e87393f8dc5dc37be7e4d9
workflow-type: tm+mt
source-wordcount: '1664'
ht-degree: 2%

---

# Endpoint da API de atributos computados

>[!IMPORTANT]
>
>O acesso à API é restrito. Para saber como obter acesso à API de atributos computados, entre em contato com o Suporte Adobe.

Os atributos computados são funções usadas para agregar dados no nível do evento em atributos no nível do perfil. Essas funções são computadas automaticamente para que possam ser usadas na segmentação, ativação e personalização. Este guia inclui exemplos de chamadas de API para executar operações CRUD básicas usando o ponto de extremidade `/attributes`.

Para saber mais sobre atributos computados, comece lendo a [visão geral sobre atributos computados](overview.md).

## Introdução

O ponto de extremidade de API usado neste guia faz parte da [API de perfil do cliente em tempo real](https://www.adobe.com/go/profile-apis-en).

Antes de continuar, consulte o [Guia de Introdução à API de Perfil](../api/getting-started.md) para obter links para a documentação recomendada, um guia para ler as chamadas de API de exemplo que aparecem neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API de Experience Platform.

Além disso, consulte a documentação do seguinte serviço:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Guia de introdução ao Registro de Esquema](../../xdm/api/getting-started.md#know-your-tenant_id): são fornecidas informações sobre o seu `{TENANT_ID}`, que aparece em respostas neste guia.

## Recuperar uma lista de atributos computados {#list}

Você pode recuperar uma lista de todos os atributos computados para sua organização fazendo uma solicitação GET para o ponto de extremidade `/attributes`.

**Formato da API**

O ponto de extremidade `/attributes` dá suporte a vários parâmetros de consulta para ajudar a filtrar os resultados. Embora esses parâmetros sejam opcionais, seu uso é altamente recomendado para ajudar a reduzir a sobrecarga cara ao listar recursos. Se você fizer uma chamada para esse endpoint sem parâmetros, todos os atributos computados disponíveis para sua organização serão recuperados. Vários parâmetros podem ser incluídos, separados por &quot;E&quot; comercial (`&`).

```http
GET /attributes
GET /attributes?{QUERY_PARAMETERS}
```

Os seguintes parâmetros de consulta podem ser usados ao recuperar uma lista de atributos computados:

| Parâmetro de consulta | Descrição | Exemplo |
| --------------- | ----------- | ------- |
| `limit` | Um parâmetro que especifica o número máximo de itens retornados como parte da resposta. O valor mínimo desse parâmetro é 1 e o valor máximo é 40. Se esse parâmetro não for incluído, por padrão, 20 itens serão retornados. | `limit=20` |
| `offset` | Um parâmetro que especifica o número de itens que devem ser ignorados antes de retornar os itens. | `offset=5` |
| `sortBy` | Um parâmetro que especifica a ordem em que os itens retornados são classificados. As opções disponíveis incluem `name`, `status`, `updateEpoch` e `createEpoch`. Você também pode escolher se deseja classificar em ordem crescente ou decrescente, não incluindo ou incluindo um `-` na frente da opção de classificação. Por padrão, os itens serão classificados por `updateEpoch` em ordem decrescente. | `sortBy=name` |
| `property` | Um parâmetro que permite filtrar em vários campos de atributo computados. As propriedades suportadas incluem `name`, `createEpoch`, `mergeFunction.value`, `updateEpoch` e `status`. As operações compatíveis dependem da propriedade listada. <ul><li>`name`: `EQUAL` (=), `NOT_EQUAL` (!=), `CONTAINS` (=contém()), `NOT_CONTAINS` (=!contém())</li><li>`createEpoch`: `GREATER_THAN_OR_EQUALS` (&lt;=), `LESS_THAN_OR_EQUALS` (>=) </li><li>`mergeFunction.value`: `EQUAL` (=), `NOT_EQUAL` (!=), `CONTAINS` (=contém()), `NOT_CONTAINS` (=!contém())</li><li>`updateEpoch`: `GREATER_THAN_OR_EQUALS` (&lt;=), `LESS_THAN_OR_EQUALS` (>=)</li><li>`status`: `EQUAL` (=), `NOT_EQUAL` (!=), `CONTAINS` (=contém()), `NOT_CONTAINS` (=!contém())</li></ul> | `property=updateEpoch>=1683669114845`<br/>`property=name!=testingrelease`<br/>`property=status=contains(new,processing,disabled)` |

**Solicitação**

A solicitação a seguir recupera os três últimos atributos calculados que foram atualizados em sua organização.

+++ Uma solicitação de amostra para recuperar uma lista de atributos computados.

```shell
curl -X GET https://platform.adobe.io/data/core/ca/attributes?limit=3 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista dos últimos 3 atributos calculados atualizados que pertencem à sua organização e sandbox.

+++ Uma resposta de amostra para recuperar uma lista de atributos computados.

```json
{
    "_links": {
        "last": {
            "href": "/attributes?offset=3&limit=1"
        },
        "next": {
            "href": "/attributes?offset=20&limit=20"
        },
        "prev": {
            "href": "/attributes?offset=0&limit=20"
        },
        "self": {
            "href": "/attributes?offset=0&limit=20"
        }
    },
    "computedAttributes": [
        {
            "id": "2e3bf98c-5840-4eb5-98c9-fcd7bde82188",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses19",
            "displayName": "Multiple Filter Clauses 19",
            "description": "Multiple Filter Clauses 19",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "keepCurrent": false,
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)",
            },
            "mergeFunction": {
                "value": "SUM"
            },
            "status": "DRAFT",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "",
            "createEpoch": 1671223530322,
            "updateEpoch": 1673043640946,
            "createdBy": "{USER_ID}"
        },
        {
            "id": "d9fbbd3d-049a-4561-b826-adc162511950",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses20",
            "displayName": "Multiple Filter Clauses 20",
            "description": "Multiple Filter Clauses 20",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "keepCurrent": true,
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[eventType.equals(\"commerce.backofficeOrderPlaced\", false)].topN(timestamp, 1).map({\"timestamp\": timestamp, \"value\": producedBy}).head()"
            },
            "mergeFunction": {
                "value": "MOST_RECENT"
            },
            "status": "DRAFT",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "",
            "createEpoch": 1671223586455,
            "updateEpoch": 1671223586455,
            "createdBy": "{USER_ID}"
        },
        {
            "id": "afedff07-9d15-4385-b181-49708229d73b",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses18",
            "displayName": "Multiple Filter Clauses 18",
            "description": "Multiple Filter Clauses 18",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)",
            },
            "mergeFunction": {
                "value": "SUM"
            },
            "status": "PROCESSED",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "2023-08-27T00:14:55.028",
            "createEpoch": 1671220358902,
            "updateEpoch": 1671220358902,
            "createdBy": "{USER_ID}"
        }
    ],
    "_page": {
        "offset": 0,
        "limit": 20,
        "count": 3,
        "totalCount": 3
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `_links` | Um objeto que contém as informações de paginação necessárias para acessar a última página de resultados, a próxima página de resultados, a página anterior de resultados ou a página atual de resultados. |
| `computedAttributes` | Uma matriz que contém os atributos calculados com base nos parâmetros de consulta. Mais informações sobre a matriz de atributos computados podem ser encontradas na [seção recuperar um atributo computado específico](#get). |
| `_page` | Um objeto que contém metadados sobre os resultados retornados. Isso inclui informações sobre o deslocamento atual, a contagem de atributos computados retornados, a contagem total de atributos computados, bem como o limite de atributos computados retornados. |

+++

## Criar um atributo calculado {#create}

Para criar um atributo computado, comece fazendo uma solicitação POST para o ponto de extremidade `/attributes` com um corpo de solicitação contendo os detalhes do atributo computado que você deseja criar.

**Formato da API**

```http
POST /attributes
```

**Solicitação**

+++ Um exemplo de solicitação para criar um novo atributo calculado.

```shell
curl -X POST https://platform.adobe.io/data/core/ca/attributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "testing",
        "displayName": "Sample Display Name",
        "description": "Sample Description",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)].sum(commerce.order.priceTotal)"
        },
        "keepCurrent": false,
        "duration": {
            "count": 4,
            "unit": "DAYS"
        },
        "status": "DRAFT"
      }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `name` | O nome do campo de atributo calculado, como uma string. O nome do atributo calculado só pode ser composto por caracteres alfanuméricos sem espaços ou sublinhados. Este valor **deve** ser exclusivo entre todos os atributos computados. Como prática recomendada, esse nome deve ser uma versão camelCase do `displayName`. |
| `description` | Uma descrição do atributo calculado. Isso é especialmente útil depois que vários atributos computados são definidos, pois ajudará outras pessoas em sua organização a determinar o atributo calculado correto a ser usado. |
| `displayName` | O nome de exibição do atributo calculado. Esse é o nome que será exibido ao listar os atributos calculados na interface do usuário do Adobe Experience Platform. |
| `expression` | Um objeto que representa a expressão de consulta do atributo calculado que você está tentando criar. |
| `expression.type` | O tipo da expressão. No momento, somente o PQL é compatível. |
| `expression.format` | O formato da expressão. Atualmente, somente `pql/text` é suportado. |
| `expression.value` | O valor da expressão. |
| `keepCurrent` | Um booleano que determina se o valor do atributo calculado é ou não mantido atualizado usando a atualização rápida. Atualmente, este valor deve ser definido como `false`. |
| `duration` | Um objeto que representa o período de pesquisa do atributo calculado. O período de pesquisa representa até que ponto a pesquisa anterior pode ser realizada para calcular o atributo calculado. |
| `duration.count` | Um número que representa a duração do período de pesquisa. Os valores possíveis dependem do valor do campo `duration.unit`. <ul><li>`HOURS`: 1-24</li><li>`DAYS`: 1-7</li><li>`WEEKS`: 1-4</li><li>`MONTHS`: 1-6</li></ul> |
| `duration.unit` | Uma string que representa a unidade de tempo que será usada para o período de pesquisa. Os valores possíveis incluem: `HOURS`, `DAYS`, `WEEKS` e `MONTHS`. |
| `status` | O status do atributo calculado. Os valores possíveis incluem `DRAFT` e `NEW`. |

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações sobre o atributo calculado recém-criado.

+++ Um exemplo de resposta ao criar um novo atributo calculado.

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680070188696,
    "updateEpoch": 1680070188696,
    "createdBy": "{USER_ID}"
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | A ID gerada pelo sistema do atributo computado recém-criado. |
| `status` | O status do atributo calculado. Pode ser `DRAFT` ou `NEW`. |
| `createEpoch` | A hora em que o atributo calculado foi criado, em segundos. |
| `updateEpoch` | A hora em que o atributo calculado foi atualizado pela última vez, em segundos. |
| `createdBy` | A ID do usuário que criou o atributo calculado. |

+++

## Recuperar um atributo calculado específico {#get}

Você pode recuperar informações detalhadas sobre um atributo calculado específico fazendo uma solicitação GET para o ponto de extremidade `/attributes` e fornecendo a ID do atributo calculado que você deseja recuperar no caminho da solicitação.

**Formato da API**

```http
GET /attributes/{ATTRIBUTE_ID}
```

**Solicitação**

+++ Uma solicitação de amostra para recuperar um atributo calculado específico.

```shell
curl -X GET 'https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre o atributo calculado especificado.

+++ Uma resposta de amostra ao recuperar um atributo calculado específico.

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680070188696,
    "updateEpoch": 1680070188696,
    "createdBy": "{USER_ID}"
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | Uma ID exclusiva, somente leitura, gerada pelo sistema que pode ser usada para fazer referência ao atributo calculado durante outras operações da API. |
| `type` | Uma string que mostra que o objeto retornado é um atributo calculado. |
| `name` | O nome do atributo calculado. |
| `displayName` | O nome de exibição do atributo calculado. Esse é o nome que será exibido ao listar os atributos calculados na interface do usuário do Adobe Experience Platform. |
| `description` | Uma descrição do atributo calculado. Isso é especialmente útil depois que vários atributos computados são definidos, pois ajudará outras pessoas em sua organização a determinar o atributo calculado correto a ser usado. |
| `imsOrgId` | A ID da organização à qual o atributo calculado pertence. |
| `sandbox` | O objeto de sandbox contém detalhes da sandbox na qual o atributo calculado foi configurado. Essas informações são retiradas do cabeçalho da sandbox enviado na solicitação. Para obter mais informações, consulte a [visão geral das sandboxes](../../sandboxes/home.md). |
| `path` | O `path` para o atributo computado. |
| `keepCurrent` | Um booleano que determina se o valor do atributo calculado é ou não mantido atualizado usando a atualização rápida. |
| `expression` | Um objeto que contém a expressão do atributo computado. |
| `mergeFunction` | Um objeto que contém a função de mesclagem para o atributo calculado. Esse valor se baseia no parâmetro de agregação correspondente na expressão do atributo calculado. Os valores possíveis incluem `SUM`, `MIN`, `MAX` e `MOST_RECENT`. |
| `status` | O status do atributo calculado. Pode ser um dos seguintes valores: `DRAFT`, `NEW`, `INITIALIZING`, `PROCESSING`, `PROCESSED`, `FAILED` ou `DISABLED`. |
| `schema` | Um objeto que contém informações sobre o esquema no qual a expressão é avaliada. Atualmente, somente `_xdm.context.profile` é suportado. |
| `lastEvaluationTs` | Um carimbo de data e hora que representa quando o atributo calculado foi avaliado pela última vez. |
| `createEpoch` | A hora em que o atributo calculado foi criado, em segundos. |
| `updateEpoch` | A hora em que o atributo calculado foi atualizado pela última vez, em segundos. |
| `createdBy` | A ID do usuário que criou o atributo calculado. |

+++

## Excluir um atributo calculado específico {#delete}

Você pode excluir um atributo calculado específico fazendo uma solicitação DELETE para o ponto de extremidade `/attributes` e fornecendo a ID do atributo calculado que você deseja excluir no caminho da solicitação.

>[!IMPORTANT]
>
>A solicitação de exclusão só pode ser usada para excluir atributos computados que tenham um status de **rascunho** (`DRAFT`). Este ponto de extremidade **não pode** ser usado para excluir atributos computados em qualquer outro estado.

**Formato da API**

```http
DELETE /attributes/{ATTRIBUTE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{ATTRIBUTE_ID}` | O valor `id` do atributo computado que você deseja excluir. |

**Solicitação**

+++ Um exemplo de solicitação para excluir um atributo calculado.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 com detalhes do atributo calculado excluído.

+++ Um exemplo de resposta ao excluir um atributo calculado.

```json
{
    "id": "03ae581b-5f7b-48da-a9eb-4ef0daf4bc3c",
    "type": "ComputedAttribute",
    "name": "testdemopd2",
    "displayName": "testdemopd2",
    "description": "testdemopd2",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.shipping.shipDate occurs <= 1 days before now) and (timestamp occurs <= 1 days before now)].min(commerce.shipping.shipDate)"
    },
    "mergeFunction": {
        "value": "MIN"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1681365690928,
    "updateEpoch": 1681365690928,
    "createdBy": "{USER_ID}"
}
```

+++

## Atualizar um atributo calculado específico

Você pode atualizar um atributo calculado específico fazendo uma solicitação PATCH para o ponto de extremidade `/attributes` e fornecendo a ID do atributo calculado que você deseja atualizar no caminho da solicitação.

>[!IMPORTANT]
>
>Ao atualizar um atributo calculado, somente os seguintes campos podem ser atualizados:
>
>- Se o status atual for `NEW`, o status só poderá ser alterado para `DISABLED`.
>- Se o status atual for `DRAFT`, você poderá alterar os valores dos seguintes campos: `name`, `description`, `keepCurrent`, `expression` e `duration`. Você também pode alterar a status de `DRAFT` para `NEW`. Qualquer alteração em campos gerados pelo sistema, como `mergeFunction` ou `path`, retornará um erro.
>- Se o status atual for `PROCESSING` ou `PROCESSED`, o status só poderá ser alterado para `DISABLED`.

**Formato da API**

```http
PATCH /attributes/{ATTRIBUTE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{ATTRIBUTE_ID}` | O valor `id` do atributo computado que você deseja atualizar. |

**Solicitação**

A solicitação a seguir atualizará o status do atributo computado de `DRAFT` para `NEW`.

+++ Um exemplo de solicitação para atualizar um atributo calculado.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
    "description": "Sample Description",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "status": "NEW"
 }'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações sobre o atributo calculado recém-atualizado.

+++ Um exemplo de resposta ao atualizar um atributo calculado.

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing123",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "NEW",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680071726825,
    "updateEpoch": 1680074429192,
    "createdBy": "{USER_ID}"
}
```

+++

## Próximas etapas

Agora que você aprendeu as noções básicas sobre atributos computados, você está pronto para começar a defini-los para sua organização. Para saber como usar atributos computados na interface do Experience Platform, leia o [guia da interface do usuário de atributos computados](./ui.md).
