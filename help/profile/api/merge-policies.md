---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API
title: Ponto de Extremidade da API de Políticas de Mesclagem
topic-legacy: guide
type: Documentation
description: O Adobe Experience Platform permite reunir fragmentos de dados de várias fontes e combiná-los para ver uma visualização completa de cada um dos clientes individuais. Ao reunir esses dados, as políticas de mesclagem são as regras que a Platform usa para determinar como os dados serão priorizados e quais dados serão combinados para criar uma visualização unificada.
exl-id: fb49977d-d5ca-4de9-b185-a5ac1d504970
source-git-commit: 4c544170636040b8ab58780022a4c357cfa447de
workflow-type: tm+mt
source-wordcount: '2258'
ht-degree: 2%

---

# Ponto de extremidade de políticas de mesclagem

O Adobe Experience Platform permite reunir fragmentos de dados de várias fontes e combiná-los para ver uma visualização completa de cada um dos clientes individuais. Ao reunir esses dados, as políticas de mesclagem são as regras que [!DNL Platform] usa para determinar como os dados serão priorizados e quais dados serão combinados para criar uma exibição unificada.

Por exemplo, se um cliente interagir com sua marca em vários canais, sua organização terá vários fragmentos de perfil relacionados a esse único cliente que aparece em vários conjuntos de dados. Quando esses fragmentos são assimilados na Platform, eles são mesclados para criar um único perfil para esse cliente. Quando os dados de várias fontes estão em conflito (por exemplo, um fragmento lista o cliente como &quot;único&quot; enquanto o outro lista o cliente como &quot;casado&quot;), a política de mesclagem determina quais informações devem ser incluídas no perfil do indivíduo.

Usando RESTful APIs ou a interface do usuário, você pode criar novas políticas de mesclagem, gerenciar políticas existentes e definir uma política de mesclagem padrão para sua organização. Este guia fornece etapas para trabalhar com políticas de mesclagem usando a API.

Para trabalhar com políticas de mesclagem usando a interface do usuário, consulte o [guia da interface do usuário de políticas de mesclagem](../merge-policies/ui-guide.md). Para saber mais sobre as políticas de mesclagem em geral e sua função no Experience Platform, comece lendo a [visão geral das políticas de mesclagem](../merge-policies/overview.md).

## Introdução

O endpoint da API usado neste guia faz parte do [[!DNL Real-time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Antes de continuar, consulte o [guia de introdução](getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API [!DNL Experience Platform].

## Componentes de políticas de mesclagem {#components-of-merge-policies}

As políticas de mesclagem são privadas para a Organização IMS, permitindo que você crie políticas diferentes para mesclar schemas de acordo com as maneiras específicas de que precisa. Qualquer API que acessar dados [!DNL Profile] requer uma política de mesclagem, embora um padrão seja usado se não for explicitamente fornecido. [!DNL Platform] O fornece às organizações uma política de mesclagem padrão, ou você pode criar uma política de mesclagem para uma classe de esquema do Experience Data Model (XDM) específica e marcá-la como padrão para sua organização.

Embora cada organização possa potencialmente ter várias políticas de mesclagem por classe de esquema, cada classe pode ter apenas uma política de mesclagem padrão. Qualquer política de mesclagem definida como padrão será usada nos casos em que o nome da classe de esquema for fornecido e uma política de mesclagem for necessária, mas não fornecida.

>[!NOTE]
>
>Ao definir uma nova política de mesclagem como padrão, qualquer política de mesclagem existente que tenha sido definida anteriormente como padrão será atualizada automaticamente para não ser mais usada como padrão.

### Objeto de política de mesclagem completa

O objeto de política de mesclagem completa representa um conjunto de preferências que controla os aspectos da mesclagem de fragmentos de perfil.

**Objeto de política de mesclagem**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "{SCHEMA_CLASS_NAME}"
        },
        "version": 1,
        "identityGraph": {
            "type": "{IDENTITY_GRAPH_TYPE}"
        },
        "attributeMerge": {
            "type": "{ATTRIBUTE_MERGE_TYPE}"
        },
        "default": "{BOOLEAN}",
        "updateEpoch": "{UPDATE_TIME}"
    }
```

| Propriedade | Descrição |
|---|---|
| `id` | O identificador exclusivo gerado pelo sistema atribuído no momento da criação |
| `name` | Nome amigável pelo qual a política de mesclagem pode ser identificada em exibições de lista. |
| `imsOrgId` | ID da organização à qual esta política de mesclagem pertence |
| `identityGraph` | [Objeto ](#identity-graph) gráfico de identidade que indica o gráfico de identidade do qual as identidades relacionadas serão obtidas. Os fragmentos de perfil encontrados para todas as identidades relacionadas serão mesclados. |
| `attributeMerge` | [Objeto ](#attribute-merge) de mesclagem de atributos que indica a maneira pela qual a política de mesclagem priorizará os atributos de perfil em caso de conflitos de dados. |
| `schema.name` | Parte do objeto [`schema`](#schema), o campo `name` contém a classe de esquema XDM à qual a política de mesclagem está relacionada. Para obter mais informações sobre schemas e classes, leia a [documentação do XDM](../../xdm/home.md). |
| `default` | Valor booleano indicando se essa política de mesclagem é o padrão para o schema especificado. |
| `version` | [!DNL Platform] versão mantida da política de mesclagem. Esse valor somente leitura é incrementado sempre que uma política de mesclagem é atualizada. |
| `updateEpoch` | Data da última atualização da política de mesclagem. |

**Exemplo de política de mesclagem**

```json
    {
        "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
        "name": "profile-default",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "version": 1,
        "identityGraph": {
            "type": "none"
        },
        "attributeMerge": {
            "type": "timestampOrdered"
        },
        "default": true,
        "updateEpoch": 1551660639
    }
```

### Gráfico de identidade {#identity-graph}

[O Adobe Experience Platform Identity ](../../identity-service/home.md) Service emanage os gráficos de identidade usados globalmente e para cada organização no  [!DNL Experience Platform]. O atributo `identityGraph` da política de mesclagem define como determinar as identidades relacionadas para um usuário.

**objeto identityGraph**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

Onde `{IDENTITY_GRAPH_TYPE}` é um dos seguintes:

* **&quot;none&quot;:** Não execute nenhum agrupamento de identidade.
* **&quot;pdg&quot;:** execute a compilação de identidade com base no seu gráfico de identidade privado.

**Exemplo`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### Mesclagem de atributos {#attribute-merge}

Um fragmento de perfil é a informação do perfil para apenas uma identidade da lista de identidades que existem para um usuário específico. Quando o tipo de gráfico de identidade usado resulta em mais de uma identidade, há um potencial para conflitante entre atributos de perfil e a prioridade deve ser especificada. Usando `attributeMerge`, você pode especificar quais atributos de perfil priorizar no caso de um conflito de mesclagem entre conjuntos de dados do tipo Valor-chave (dados de registro).

**objeto attributeMerge**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

Onde `{ATTRIBUTE_MERGE_TYPE}` é um dos seguintes:

* **`timestampOrdered`**: (padrão) Dar prioridade ao perfil que foi atualizado por último. Usando esse tipo de mesclagem, o atributo `data` não é necessário.
* **`dataSetPrecedence`** : Atribua prioridade aos fragmentos de perfil com base no conjunto de dados de onde eles vieram. Isso pode ser usado quando as informações presentes em um conjunto de dados são preferenciais ou confiáveis em relação aos dados em outro conjunto de dados. Ao usar esse tipo de mesclagem, o atributo `order` é necessário, pois lista os conjuntos de dados na ordem de prioridade.
   * **`order`**: Quando &quot;dataSetPrecedence&quot; é usado, uma  `order` matriz deve ser fornecida com uma lista de conjuntos de dados. Nenhum conjunto de dados incluído na lista será mesclado. Em outras palavras, os conjuntos de dados devem ser listados explicitamente para serem mesclados a um perfil. A matriz `order` lista as IDs dos conjuntos de dados em ordem de prioridade.

#### Exemplo de objeto `attributeMerge` usando tipo `dataSetPrecedence`

```json
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order" : [
            "dataSetId_2", 
            "dataSetId_3", 
            "dataSetId_1", 
            "dataSetId_4"
        ]
    }
```

#### Exemplo de objeto `attributeMerge` usando tipo `timestampOrdered`

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### Esquema {#schema}

O objeto schema especifica a classe de esquema do Experience Data Model (XDM) para a qual essa política de mesclagem é criada.

**`schema`objeto**

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

Onde o valor de `name` é o nome da classe XDM na qual o schema associado à política de mesclagem se baseia.

**Exemplo`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

Para saber mais sobre o XDM e trabalhar com esquemas no Experience Platform, comece lendo a [Visão geral do sistema XDM](../../xdm/home.md).

## Acessar políticas de mesclagem {#access-merge-policies}

Usando a API [!DNL Real-time Customer Profile], o endpoint `/config/mergePolicies` permite executar uma solicitação de pesquisa para exibir uma política de mesclagem específica pela ID ou acessar todas as políticas de mesclagem na Organização IMS, filtradas por critérios específicos. Você também pode usar o terminal `/config/mergePolicies/bulk-get` para recuperar várias políticas de mesclagem por suas IDs. As etapas para executar cada uma dessas chamadas são descritas nas seções a seguir.

### Acessar uma única política de mesclagem por ID

Você pode acessar uma única política de mesclagem pela ID fazendo uma solicitação de GET para o endpoint `/config/mergePolicies` e incluindo `mergePolicyId` no caminho da solicitação.

**Formato da API**

```http
GET /config/mergePolicies/{mergePolicyId}
```

| Parâmetro | Descrição |
|---|---|
| `{mergePolicyId}` | O identificador da política de mesclagem que deseja excluir. |

**Solicitação**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/10648288-cda5-11e8-a8d5-f2801f1b9fd1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da política de mesclagem.

```json
{
    "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
    "imsOrgId": "{IMS_ORG}",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "pdg"
    },
    "attributeMerge": {
        "type": "timestampOrdered"
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

Consulte a seção [components of merge policy](#components-of-merge-policies) no início deste documento para obter detalhes sobre cada um dos elementos individuais que compõem uma política de mesclagem.

### Recuperar várias políticas de mesclagem por suas IDs

Você pode recuperar várias políticas de mesclagem fazendo uma solicitação POST para o endpoint `/config/mergePolicies/bulk-get` e incluindo as IDs das políticas de mesclagem que deseja recuperar no corpo da solicitação.

**Formato da API**

```http
POST /config/mergePolicies/bulk-get
```

**Solicitação**

O corpo da solicitação inclui uma matriz &quot;ids&quot; com objetos individuais contendo a &quot;id&quot; para cada política de mesclagem para a qual você deseja recuperar detalhes.

```shell
curl -X POST \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/bulk-get' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "ids": [
          {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b"
          },
          {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130"
          }
        ]
      }'
```

**Resposta**

Uma resposta bem-sucedida retorna o Status HTTP 207 (Multi-Status) e os detalhes das políticas de mesclagem cujas IDs foram fornecidas na solicitação do POST.

```json
{ 
    "results": { 
        "0bf16e61-90e9-4204-b8fa-ad250360957b": {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "none"
            },
            "attributeMerge": {
                "type": "timestampOrdered"
            },
            "default": true,
            "updateEpoch": 1552086578
        },
        "42d4a596-b1c6-46c0-994e-ca5ef1f85130": {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "pdg"
            },
            "attributeMerge": {
                "type": "dataSetPrecedence",
                "order": [
                    "5b76f86b85d0e00000be5c8b",
                    "5b76f8d787a6af01e2ceda18"
                ]
            },
            "default": false,
            "updateEpoch": 1576099719
        }
    }
}
```

Consulte a seção [components of merge policy](#components-of-merge-policies) no início deste documento para obter detalhes sobre cada um dos elementos individuais que compõem uma política de mesclagem.

### Listar várias políticas de mesclagem por critérios

Você pode listar várias políticas de mesclagem na Organização IMS emitindo uma solicitação GET para o endpoint `/config/mergePolicies` e usando parâmetros de consulta opcionais para filtrar, ordenar e paginar a resposta. Vários parâmetros podem ser incluídos, separados por &quot;E&quot; comercial (&amp;). Fazer uma chamada para esse terminal sem parâmetros recuperará todas as políticas de mesclagem disponíveis para sua organização.

**Formato da API**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| Parâmetro | Descrição |
|---|---|
| `default` | Um valor booleano que filtra resultados se as políticas de mesclagem são ou não o padrão para uma classe de esquema. |
| `limit` | Especifica o limite de tamanho de página para controlar o número de resultados incluídos em uma página. Valor padrão: 20º |
| `orderBy` | Especifica o campo pelo qual ordenar os resultados como em `orderBy=name` ou `orderBy=+name` para classificar por nome em ordem crescente ou `orderBy=-name`, para classificar em ordem decrescente. Omitir esse valor resulta na classificação padrão de `name` em ordem crescente. |
| `schema.name` | Nome do schema para o qual recuperar as políticas de mesclagem disponíveis. |
| `identityGraph.type` | Filtros resulta pelo tipo de gráfico de identidade. Os valores possíveis incluem &quot;none&quot; e &quot;pdg&quot; (Gráfico privado). |
| `attributeMerge.type` | Filtra os resultados pelo tipo de mesclagem de atributo usado. Os valores possíveis incluem &quot;timestampOrdered&quot; e &quot;dataSetPrecedence&quot;. |
| `start` | Deslocamento da página - especifique a ID inicial dos dados a serem recuperados. Valor padrão: 0 |
| `version` | Especifique isso se quiser usar uma versão específica da política de mesclagem. Por padrão, a versão mais recente será usada. |

Para obter mais informações sobre `schema.name`, `identityGraph.type` e `attributeMerge.type`, consulte a seção [componentes das políticas de mesclagem](#components-of-merge-policies) fornecida anteriormente neste guia.


**Solicitação**

A solicitação a seguir lista todas as políticas de mesclagem de um determinado schema:

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista paginada de políticas de mesclagem que atendem aos critérios especificados pelos parâmetros de consulta enviados na solicitação.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "none"
            },
            "attributeMerge": {
                "type": "timestampOrdered"
            },
            "default": true,
            "updateEpoch": 1552086578
        },
        {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "pdg"
            },
            "attributeMerge": {
                "type": "dataSetPrecedence",
                "order": [
                    "5b76f86b85d0e00000be5c8b",
                    "5b76f8d787a6af01e2ceda18"
                ]
            },
            "default": false,
            "updateEpoch": 1576099719
        }
    ],
    "_links": {
        "next": {
            "href": "@/mergePolicies?start=K1JJRDpFaWc5QUpZWHY1c2JBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQldBQkVBQVBnaFFQLzM4VUIvL2tKQi8rLysvMUpBLzMrMi8wRkFmLzR4UUwvL0VrRC85em4zRTBEcmNmYi92Kzh4UUwvL05rQVgzRi8rMStqNS80WHQwN2NhUUVzQUFBUUFleGpLQ1JnVXRVcEFCQUFFQVBBRA==&orderBy=&limit=2"
        }
    }
}
```

| Propriedade | Descrição |
|---|---|
| `_links.next.href` | Um endereço de URI para a próxima página de resultados. Use esse URI como parâmetro de solicitação para outra chamada de API para o mesmo terminal para visualizar a página. Se não existir nenhuma próxima página, esse valor será uma string vazia. |

## Criar uma política de mesclagem

Você pode criar uma nova política de mesclagem para sua organização fazendo uma solicitação de POST para o endpoint `/config/mergePolicies`.

**Formato da API**

```http
POST /config/mergePolicies
```

****
SolicitaçãoA solicitação a seguir cria uma nova política de mesclagem, que é configurada pelos valores de atributo fornecidos no payload:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/mergePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Loyalty members ordered by ID",
    "identityGraph" : {
        "type": "none"
    },
    "attributeMerge" : {
        "type":"dataSetPrecedence",
        "order" : [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "schema": {
        "name":"_xdm.context.profile"
    },
    "default": true
}'
```

| Propriedade | Descrição |
|---|---|
| `name` | Um nome amigável para o ser humano pelo qual a política de mesclagem pode ser identificada em exibições de lista. |
| `identityGraph.type` | O tipo de gráfico de identidade do qual obter identidades relacionadas para mesclar. Valores possíveis: &quot;none&quot; ou &quot;pdg&quot; (Gráfico privado). |
| `attributeMerge` | A maneira pela qual priorizar valores de atributos de perfil em caso de conflitos de dados. |
| `schema` | A classe de esquema XDM associada à política de mesclagem. |
| `default` | Especifica se essa política de mesclagem é o padrão para o esquema. |

Consulte a seção [componentes das políticas de mesclagem](#components-of-merge-policies) para obter mais informações.

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da política de mesclagem recém-criada.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

Consulte a seção [components of merge policy](#components-of-merge-policies) no início deste documento para obter detalhes sobre cada um dos elementos individuais que compõem uma política de mesclagem.

## Atualizar uma política de mesclagem {#update}

Você pode modificar uma política de mesclagem existente editando atributos individuais (PATCH) ou substituindo toda a política de mesclagem por novos atributos (PUT). Os exemplos de cada um são mostrados abaixo.

### Editar campos de política de mesclagem individuais

Você pode editar campos individuais para uma política de mesclagem fazendo uma solicitação de PATCH para o endpoint `/config/mergePolicies/{mergePolicyId}`:

**Formato da API**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| Parâmetro | Descrição |
|---|---|
| `{mergePolicyId}` | O identificador da política de mesclagem que deseja excluir. |

**Solicitação**

A solicitação a seguir atualiza uma política de mesclagem especificada alterando o valor de sua propriedade `default` para `true`:

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "op": "add",
    "path": "/default",
    "value": "true"
  }'
```

| Propriedade | Descrição |
|---|---|
| `op` | Especifica a operação a ser executada. Exemplos de outras operações do PATCH podem ser encontrados na [documentação do Patch JSON](http://jsonpatch.com) |
| `path` | O caminho do campo a ser atualizado. Os valores aceitos são: &quot;/name&quot;, &quot;/identityGraph.type&quot;, &quot;/attributeMerge.type&quot;, &quot;/schema.name&quot;, &quot;/version&quot;, &quot;/default&quot; |
| `value` | O valor para definir o campo especificado como. |

Consulte a seção [componentes das políticas de mesclagem](#components-of-merge-policies) para obter mais informações.


**Resposta**

Uma resposta bem-sucedida retorna os detalhes da política de mesclagem recém-atualizada.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

### Substituir uma política de mesclagem

Outra maneira de modificar uma política de mesclagem é usar uma solicitação PUT, que substitui toda a política de mesclagem.

**Formato da API**

```http
PUT /config/mergePolicies/{mergePolicyId}
```

| Parâmetro | Descrição |
|---|---|
| `{mergePolicyId}` | O identificador da política de mesclagem que você deseja substituir. |

**Solicitação**

A solicitação a seguir substitui a política de mesclagem especificada, substituindo seus valores de atributo por aqueles fornecidos na carga útil. Como essa solicitação substitui completamente uma política de mesclagem existente, é necessário fornecer todos os mesmos campos necessários ao definir originalmente a política de mesclagem. No entanto, desta vez você fornece valores atualizados para os campos que deseja alterar.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Loyalty members ordered by ID",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "version": 1,
        "identityGraph": {
            "type": "none"
        },
        "attributeMerge": {
            "type": "dataSetPrecedence",
            "order": [
                "5b76f86b85d0e00000be5c8b",
                "5b76f8d787a6af01e2ceda18"
            ]
        },
        "default": true,
        "updateEpoch": 1551898378
    }'
```

| Propriedade | Descrição |
|---|---|
| `name` | Um nome amigável para o ser humano pelo qual a política de mesclagem pode ser identificada em exibições de lista. |
| `identityGraph` | O gráfico de identidade do qual obter identidades relacionadas para mesclar. |
| `attributeMerge` | A maneira pela qual priorizar valores de atributos de perfil em caso de conflitos de dados. |
| `schema` | A classe de esquema XDM associada à política de mesclagem. |
| `default` | Especifica se essa política de mesclagem é o padrão para o esquema. |

Consulte a seção [componentes das políticas de mesclagem](#components-of-merge-policies) para obter mais informações.


**Resposta**

Uma resposta bem-sucedida retorna os detalhes da política de mesclagem atualizada.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

## Excluir uma política de mesclagem

Uma política de mesclagem pode ser excluída fazendo uma solicitação DELETE ao endpoint `/config/mergePolicies` e incluindo a ID da política de mesclagem que você deseja excluir no caminho da solicitação.

**Formato da API**

```http
DELETE /config/mergePolicies/{mergePolicyId}
```

| Parâmetro | Descrição |
|---|---|
| `{mergePolicyId}` | O identificador da política de mesclagem que deseja excluir. |

**Solicitação**

A solicitação a seguir exclui uma política de mesclagem.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma solicitação de exclusão bem-sucedida retorna o Status HTTP 200 (OK) e um corpo de resposta vazio. Para confirmar que a exclusão foi bem-sucedida, é possível executar uma solicitação do GET para exibir a política de mesclagem por sua ID. Se a política de mesclagem foi excluída, você receberá um erro HTTP Status 404 (Not Found).

## Próximas etapas

Agora que você sabe como criar e configurar políticas de mesclagem para sua organização, pode usá-las para ajustar a visualização dos perfis do cliente no Platform e criar segmentos de público-alvo a partir dos dados [!DNL Real-time Customer Profile].

Consulte a [documentação do Serviço de segmentação do Adobe Experience Platform](../../segmentation/home.md) para começar a definir e trabalhar com segmentos.
