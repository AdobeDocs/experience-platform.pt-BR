---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Mesclar políticas - API de Perfil do cliente em tempo real
topic: guide
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '2397'
ht-degree: 1%

---


# Mesclar ponto final de políticas

A Adobe Experience Platform permite que você reúna dados de várias fontes e os combine para ver uma visualização completa de cada um de seus clientes individuais. Ao reunir esses dados, as políticas de mesclagem são as regras que [!DNL Platform] usam para determinar como os dados serão priorizados e quais dados serão combinados para criar essa visualização unificada. Usando RESTful APIs ou a interface do usuário, você pode criar novas políticas de mesclagem, gerenciar políticas existentes e definir uma política de mesclagem padrão para sua organização. Este guia mostra as etapas para trabalhar com políticas de mesclagem usando a API. Para trabalhar com políticas de mesclagem usando a interface do usuário, consulte o guia [do usuário das políticas de](../ui/merge-policies.md)mesclagem.

## Introdução

O terminal da API usado neste guia faz parte da [[!DNL Real-time Customer Perfil API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). Antes de continuar, reveja o guia [de](getting-started.md) introdução para obter links para a documentação relacionada, um guia para ler as chamadas de API de amostra neste documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer [!DNL Experience Platform] API.

## Componentes das políticas de mesclagem {#components-of-merge-policies}

As políticas de mesclagem são privadas para sua Organização IMS, permitindo que você crie políticas diferentes para unir schemas da maneira específica que você precisa. Qualquer API que acesse [!DNL Profile] dados requer uma política de mesclagem, embora um padrão seja usado se não for fornecido explicitamente. [!DNL Platform] fornece uma política de mesclagem padrão ou você pode criar uma política de mesclagem para um schema específico e marcá-la como padrão para sua organização. Cada organização pode potencialmente ter várias políticas de mesclagem por schema, no entanto, cada schema pode ter apenas uma política de mesclagem padrão. Qualquer política de mesclagem definida como padrão será usada nos casos em que o nome do schema for fornecido e uma política de mesclagem for necessária, mas não fornecida. Quando você define uma política de mesclagem como padrão, qualquer política de mesclagem existente definida anteriormente como padrão será automaticamente atualizada para não ser mais usada como padrão.

### Objeto de política de mesclagem completa

O objeto de política de mesclagem completa representa um conjunto de preferências que controla os aspectos da união de fragmentos de perfis.

**Objeto de política de mesclagem**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "{SCHEMA_NAME}"
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
| `name` | Nome amigável pelo qual a política de mesclagem pode ser identificada nas visualizações de lista. |
| `imsOrgId` | ID da organização à qual esta política de mesclagem pertence |
| `identityGraph` | [Objeto de gráfico](#identity-graph) de identidade que indica o gráfico de identidade a partir do qual as identidades relacionadas serão obtidas. Os fragmentos de perfil encontrados para todas as identidades relacionadas serão mesclados. |
| `attributeMerge` | [Objeto de mesclagem](#attribute-merge) de atributo que indica a maneira pela qual a política de mesclagem priorizará os atributos do perfil em caso de conflitos de dados. |
| `schema` | O objeto [schema](#schema) no qual a política de mesclagem pode ser usada. |
| `default` | Valor booliano que indica se essa política de mesclagem é o padrão para o schema especificado. |
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

[O Adobe Experience Platform Identity Service](../../identity-service/home.md) gerencia os gráficos de identidade usados globalmente e para cada organização em [!DNL Experience Platform]. O `identityGraph` atributo da política de mesclagem define como determinar as identidades relacionadas para um usuário.

**objeto identityGraph**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

Quando `{IDENTITY_GRAPH_TYPE}` for uma das seguintes opções:

* **&quot;nenhum&quot;:** Não execute nenhum ajuste de identidade.
* **&quot;pdg&quot;:** Realize a identificação com base no seu gráfico de identidade particular.

**Exemplo`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### Mesclagem de atributo {#attribute-merge}

Um fragmento de perfil são as informações do perfil para apenas uma identidade da lista de identidades que existem para um usuário específico. Quando o tipo de gráfico de identidade usado resulta em mais de uma identidade, há um potencial para atributos de perfil conflitantes e a prioridade deve ser especificada. Usando `attributeMerge`, você pode especificar quais atributos de perfil priorizar no evento de um conflito de mesclagem entre conjuntos de dados do tipo Valor-chave (dados de registro).

**objeto attributeMerge**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

Quando `{ATTRIBUTE_MERGE_TYPE}` for uma das seguintes opções:

* **`timestampOrdered`**: (padrão) Atribua prioridade ao perfil que foi atualizado por último em caso de conflito. Usando esse tipo de mesclagem, o `data` atributo não é obrigatório. `timestampOrdered` também suporta carimbos de data e hora personalizados que terão prioridade ao mesclar fragmentos de perfil dentro ou entre conjuntos de dados. Para saber mais, consulte a seção Apêndice sobre como [usar carimbos de data e hora](#custom-timestamps)personalizados.
* **`dataSetPrecedence`** : Atribua prioridade aos fragmentos do perfil com base no conjunto de dados de onde eles vieram. Isso pode ser usado quando as informações presentes em um conjunto de dados são preferenciais ou confiáveis em vez de dados em outro conjunto de dados. Ao usar esse tipo de mesclagem, o `order` atributo é obrigatório, pois lista os conjuntos de dados na ordem de prioridade.
   * **`order`**: Quando &quot;dataSetPrecedence&quot; é usado, uma `order` matriz deve ser fornecida com uma lista de conjuntos de dados. Nenhum conjunto de dados incluído na lista será unido. Em outras palavras, os conjuntos de dados devem ser listados explicitamente para serem mesclados em um perfil. A `order` matriz lista as IDs dos conjuntos de dados em ordem de prioridade.

**Exemplo de objeto attributeMerge usando`dataSetPrecedence`tipo**

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

**Exemplo de objeto attributeMerge usando`timestampOrdered`tipo**

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### Esquema {#schema}

O objeto schema especifica o schema do Modelo de Dados de Experiência (XDM) para o qual essa política de mesclagem é criada.

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

Para saber mais sobre o XDM e trabalhar com schemas no Experience Platform, comece lendo a visão geral [do sistema](../../xdm/home.md)XDM.

## Acessar políticas de mesclagem {#access-merge-policies}

Usando a [!DNL Real-time Customer Profile] API, o `/config/mergePolicies` terminal permite executar uma solicitação de pesquisa para visualização de uma política de mesclagem específica por sua ID ou acessar todas as políticas de mesclagem na organização IMS, filtradas por critérios específicos. Você também pode usar o `/config/mergePolicies/bulk-get` endpoint para recuperar várias políticas de mesclagem por suas IDs. As etapas para executar cada uma dessas chamadas são descritas nas seções a seguir.

### Acessar uma única política de mesclagem por ID

Você pode acessar uma única política de mesclagem por meio de sua ID, fazendo uma solicitação de GET para o `/config/mergePolicies` ponto final e incluindo o `mergePolicyId` no caminho da solicitação.

**Formato da API**

```http
GET /config/mergePolicies/{mergePolicyId}
```

| Parâmetro | Descrição |
|---|---|
| `{mergePolicyId}` | O identificador da política de mesclagem que você deseja excluir. |

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

Consulte a seção [componentes das políticas](#components-of-merge-policies) de mesclagem no início deste documento para obter detalhes sobre cada um dos elementos individuais que compõem uma política de mesclagem.

### Recuperar várias políticas de mesclagem por suas IDs

Você pode recuperar várias políticas de mesclagem, fazendo uma solicitação POST para o `/config/mergePolicies/bulk-get` ponto final e incluindo as IDs das políticas de mesclagem que deseja recuperar no corpo da solicitação.

**Formato da API**

```http
POST /config/mergePolicies/bulk-get
```

**Solicitação**

O corpo da solicitação inclui uma matriz &quot;ids&quot; com objetos individuais que contêm a &quot;id&quot; para cada política de mesclagem para a qual você deseja recuperar detalhes.

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

Uma resposta bem-sucedida retorna o Status HTTP 207 (Multi-Status) e os detalhes das políticas de mesclagem cujas IDs foram fornecidas na solicitação de POST.

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

Consulte a seção [componentes das políticas](#components-of-merge-policies) de mesclagem no início deste documento para obter detalhes sobre cada um dos elementos individuais que compõem uma política de mesclagem.

### Lista de várias políticas de mesclagem por critérios

É possível lista de várias políticas de mesclagem na Organização IMS emitindo uma solicitação de GET para o `/config/mergePolicies` ponto de extremidade e usando parâmetros de query opcionais para filtrar, solicitar e paginar a resposta. Vários parâmetros podem ser incluídos, separados por E comercial (&amp;). Efetuar uma chamada para este terminal sem parâmetros recuperará todas as políticas de mesclagem disponíveis para a sua organização.

**Formato da API**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| Parâmetro | Descrição |
|---|---|
| `default` | Um valor booliano que filtros resulta se as políticas de mesclagem são ou não o padrão para uma classe de schema. |
| `limit` | Especifica o limite de tamanho de página para controlar o número de resultados que são incluídos em uma página. Valor padrão: 20 |
| `orderBy` | Especifica o campo pelo qual ordenar os resultados como em `orderBy=name` ou `orderBy=+name` para classificar por nome em ordem crescente, ou `orderBy=-name`, para classificar em ordem decrescente. A omissão desse valor resulta na classificação padrão de `name` em ordem crescente. |
| `schema.name` | Nome do schema para o qual recuperar as políticas de mesclagem disponíveis. |
| `identityGraph.type` | Filtros resulta pelo tipo de gráfico de identidade. Os valores possíveis incluem &quot;none&quot; e &quot;pdg&quot; (Gráfico privado). |
| `attributeMerge.type` | Resultados de filtros pelo tipo de mesclagem de atributo usado. Os valores possíveis incluem &quot;timestampOrdered&quot; e &quot;dataSetPrecedence&quot;. |
| `start` | Deslocamento da página - especifique a ID inicial dos dados a serem recuperados. Valor padrão: 0 |
| `version` | Especifique essa opção se você estiver procurando usar uma versão específica da política de mesclagem. Por padrão, a versão mais recente será usada. |

Para obter mais informações sobre `schema.name`, `identityGraph.type`e `attributeMerge.type`, consulte a seção [componentes das políticas](#components-of-merge-policies) de mesclagem fornecida anteriormente neste guia.


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

Uma resposta bem-sucedida retorna uma lista paginada de políticas de mesclagem que atendem aos critérios especificados pelos parâmetros de query enviados na solicitação.

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
| `_links.next.href` | Um endereço de URI para a próxima página de resultados. Use esse URI como parâmetro de solicitação para outra chamada de API para o mesmo terminal para visualização da página. Se não houver nenhuma próxima página, esse valor será uma string vazia. |

## Criar uma política de mesclagem

Você pode criar uma nova política de mesclagem para a sua organização, fazendo uma solicitação POST para o `/config/mergePolicies` endpoint.

**Formato da API**

```http
POST /config/mergePolicies
```

**Solicitação** A solicitação a seguir cria uma nova política de mesclagem, que é configurada pelos valores de atributo fornecidos na carga:

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
| `name` | Um nome amigável para os humanos pelo qual a política de mesclagem pode ser identificada em visualizações listas. |
| `identityGraph.type` | O tipo de gráfico de identidade a partir do qual obter identidades relacionadas para mesclar. Valores possíveis: &quot;none&quot; ou &quot;pdg&quot; (Gráfico privado). |
| `attributeMerge` | A maneira pela qual priorizar os valores do atributo do perfil em caso de conflito de dados. |
| `schema` | A classe de schema XDM associada à política de mesclagem. |
| `default` | Especifica se essa política de mesclagem é o padrão para o schema. |

Consulte os [componentes da seção de políticas](#components-of-merge-policies) de mesclagem para obter mais informações.

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

Consulte a seção [componentes das políticas](#components-of-merge-policies) de mesclagem no início deste documento para obter detalhes sobre cada um dos elementos individuais que compõem uma política de mesclagem.

## Atualizar uma política de mesclagem {#update}

É possível modificar uma política de mesclagem existente editando atributos individuais (PATCH) ou substituindo toda a política de mesclagem por novos atributos (PUT). Os exemplos de cada um são mostrados abaixo.

### Editar campos de política de mesclagem individuais

É possível editar campos individuais para uma política de mesclagem, fazendo uma solicitação de PATCH para o `/config/mergePolicies/{mergePolicyId}` endpoint:

**Formato da API**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| Parâmetro | Descrição |
|---|---|
| `{mergePolicyId}` | O identificador da política de mesclagem que você deseja excluir. |

**Solicitação**

A solicitação a seguir atualiza uma política de mesclagem especificada alterando o valor de sua `default` propriedade para `true`:

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
| `op` | Especifica a operação a ser realizada. Exemplos de outras operações de PATCH podem ser encontrados na documentação do Patch [JSON](http://jsonpatch.com) |
| `path` | O caminho do campo a ser atualizado. Os valores aceitos são: &quot;/name&quot;, &quot;/identityGraph.type&quot;, &quot;/attributeMerge.type&quot;, &quot;/schema.name&quot;, &quot;/version&quot;, &quot;/default&quot; |
| `value` | O valor para definir o campo especificado como. |

Consulte os [componentes da seção de políticas](#components-of-merge-policies) de mesclagem para obter mais informações.


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

A solicitação a seguir substitui a política de mesclagem especificada, substituindo seus valores de atributo pelos fornecidos na carga. Como essa solicitação substitui completamente uma política de mesclagem existente, é necessário fornecer todos os mesmos campos que foram necessários ao definir originalmente a política de mesclagem. No entanto, desta vez você fornece valores atualizados para os campos que deseja alterar.

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
| `name` | Um nome amigável para os humanos pelo qual a política de mesclagem pode ser identificada em visualizações listas. |
| `identityGraph` | O gráfico de identidade do qual obter identidades relacionadas para mesclar. |
| `attributeMerge` | A maneira pela qual priorizar os valores do atributo do perfil em caso de conflito de dados. |
| `schema` | A classe de schema XDM associada à política de mesclagem. |
| `default` | Especifica se essa política de mesclagem é o padrão para o schema. |

Consulte os [componentes da seção de políticas](#components-of-merge-policies) de mesclagem para obter mais informações.


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

Uma política de mesclagem pode ser excluída fazendo uma solicitação de DELETE para o `/config/mergePolicies` ponto final e incluindo a ID da política de mesclagem que você deseja excluir no caminho da solicitação.

**Formato da API**

```http
DELETE /config/mergePolicies/{mergePolicyId}
```

| Parâmetro | Descrição |
|---|---|
| `{mergePolicyId}` | O identificador da política de mesclagem que você deseja excluir. |

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

Uma solicitação de exclusão bem-sucedida retorna o Status HTTP 200 (OK) e um corpo de resposta vazio. Para confirmar se a exclusão foi bem-sucedida, é possível executar uma solicitação de GET para visualização da política de mesclagem por sua ID. Se a política de mesclagem tiver sido excluída, você receberá um erro HTTP Status 404 (Não encontrado).

## Próximas etapas

Agora que você sabe como criar e configurar políticas de mesclagem para sua Organização IMS, pode usá-las para criar segmentos de audiência a partir de seus [!DNL Real-time Customer Profile] dados. Consulte a documentação [do Serviço de segmentação da](../../segmentation/home.md) Adobe Experience Platform para começar a definir e trabalhar com segmentos.

## Apêndice

Esta seção fornece informações complementares relacionadas ao trabalho com políticas de mesclagem.

### Uso de carimbos de data e hora personalizados {#custom-timestamps}

Como os registros de Perfis são ingeridos no Experience Platform, um carimbo de data e hora do sistema é obtido no momento da ingestão e adicionado ao registro. Quando `timestampOrdered` for selecionado como o tipo `attributeMerge` de uma política de mesclagem, os perfis serão mesclados com base no carimbo de data e hora do sistema. Em outras palavras, a mesclagem é feita com base no carimbo de data e hora para quando o registro foi ingerido na Plataforma.

Ocasionalmente, pode haver casos de uso, como preenchimento retroativo de dados ou garantia da ordem correta dos eventos, se os registros forem ingeridos fora de ordem, quando for necessário fornecer um carimbo de data e hora personalizado e a política de mesclagem respeitar o carimbo de data e hora personalizado em vez do carimbo de data e hora do sistema.

Para usar um carimbo de data e hora personalizado, a Mixin [de Detalhes de Auditoria do Sistema de Origem](#mixin-details) Externa deve ser adicionada ao schema do Perfil. Depois de adicionado, o carimbo de data e hora personalizado pode ser preenchido usando o `xdm:lastUpdatedDate` campo. Quando um registro é ingerido com o `xdm:lastUpdatedDate` campo preenchido, o Experience Platform usará esse campo para unir registros ou fragmentos de perfil dentro e entre conjuntos de dados. Se não `xdm:lastUpdatedDate` estiver presente ou não estiver preenchida, a Plataforma continuará a usar o carimbo de data e hora do sistema.

>[!NOTE]
>
>É necessário garantir que o `xdm:lastUpdatedDate` carimbo de data e hora seja preenchido ao enviar um PATCH no mesmo registro.

Para obter instruções passo a passo sobre como trabalhar com schemas usando a API do Registro do schema, incluindo como adicionar mixins a schemas, visite o [tutorial para criar um schema usando a API](../../xdm/tutorials/create-schema-api.md).

Para trabalhar com carimbos de data e hora personalizados usando a interface do usuário, consulte a seção sobre como [usar carimbos de data e hora](../ui/merge-policies.md#custom-timestamps) personalizados no guia [do usuário das políticas de](../ui/merge-policies.md)mesclagem.

#### Detalhes da auditoria do sistema de origem externa Detalhes da combinação {#mixin-details}

O exemplo a seguir mostra os campos preenchidos corretamente na Mixin de Detalhes de Auditoria do Sistema de Origem Externa. A combinação completa do JSON também pode ser visualizada na reunião [pública do Modelo de Dados de Experiência (XDM) no GitHub](https://github.com/adobe/xdm/blob/master/schemas/common/external-source-system-audit-details.schema.json) .

```json
{
  "xdm:createdBy": "{CREATED_BY}",
  "xdm:createdDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastUpdatedBy": "{LAST_UPDATED_BY}",
  "xdm:lastUpdatedDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastActivityDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastReferencedDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastViewedDate": "2018-01-02T15:52:25+00:00"
 }
```




