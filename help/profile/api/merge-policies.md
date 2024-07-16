---
keywords: Experience Platform;perfil;perfil de cliente em tempo real;solução de problemas;API
title: Ponto de Extremidade da API de Políticas de Mesclagem
type: Documentation
description: O Adobe Experience Platform permite reunir fragmentos de dados de várias fontes e combiná-los para obter uma visualização completa de cada cliente individual. Ao reunir esses dados, as políticas de mesclagem são as regras que a Platform usa para determinar como os dados serão priorizados e quais dados serão combinados para criar uma visualização unificada.
role: Developer
exl-id: fb49977d-d5ca-4de9-b185-a5ac1d504970
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '2465'
ht-degree: 2%

---

# Ponto de acesso de políticas de mesclagem

O Adobe Experience Platform permite reunir fragmentos de dados de várias fontes e combiná-los para obter uma visualização completa de cada cliente individual. Ao reunir esses dados, as políticas de mesclagem são as regras que [!DNL Platform] usa para determinar como os dados serão priorizados e quais dados serão combinados para criar uma exibição unificada.

Por exemplo, se um cliente interagir com sua marca em vários canais, sua organização terá vários fragmentos de perfil relacionados a esse único cliente que aparecem em vários conjuntos de dados. Quando esses fragmentos são assimilados na Platform, eles são mesclados para criar um único perfil para esse cliente. Quando os dados de várias origens entram em conflito (por exemplo, um fragmento lista o cliente como &quot;único&quot; enquanto o outro lista o cliente como &quot;casado&quot;), a política de mesclagem determina quais informações incluir no perfil do indivíduo.

Usando APIs RESTful ou a interface do usuário, você pode criar novas políticas de mesclagem, gerenciar políticas existentes e definir uma política de mesclagem padrão para sua organização. Este guia fornece etapas para trabalhar com políticas de mesclagem usando a API.

Para trabalhar com políticas de mesclagem usando a interface, consulte o [guia da interface de políticas de mesclagem](../merge-policies/ui-guide.md). Para saber mais sobre as políticas de mesclagem em geral e sua função no Experience Platform, comece lendo a [visão geral das políticas de mesclagem](../merge-policies/overview.md).

## Introdução

O ponto de extremidade de API usado neste guia faz parte de [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Antes de continuar, consulte o [guia de introdução](getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do [!DNL Experience Platform].

## Componentes das políticas de mesclagem {#components-of-merge-policies}

As políticas de mesclagem são privadas para sua organização, permitindo criar políticas diferentes para mesclar esquemas das maneiras específicas necessárias. Qualquer API que acesse os dados [!DNL Profile] requer uma política de mesclagem, embora um padrão seja usado se um não for fornecido explicitamente. [!DNL Platform] fornece às organizações uma política de mesclagem padrão, ou você pode criar uma política de mesclagem para uma classe de esquema específica do Experience Data Model (XDM) e marcá-la como o padrão para sua organização.

Embora cada organização possa ter várias políticas de mesclagem por classe de esquema, cada classe pode ter apenas uma política de mesclagem padrão. Qualquer política de mesclagem definida como padrão será usada nos casos em que o nome da classe de esquema for fornecido e uma política de mesclagem for necessária, mas não fornecida.

>[!NOTE]
>
>Ao definir uma nova política de mesclagem como padrão, qualquer política de mesclagem existente definida anteriormente como padrão será atualizada automaticamente para não ser mais usada como padrão.

Para garantir que todos os consumidores de perfil estejam trabalhando com a mesma exibição nas bordas, as políticas de mesclagem podem ser marcadas como ativas na borda. Para que um público-alvo seja ativado na borda (marcado como um público-alvo de borda), ele deve estar vinculado a uma política de mesclagem marcada como ativo na borda. Se um público-alvo estiver **não** vinculado a uma política de mesclagem marcada como ativo na borda, o público-alvo não será marcado como ativo na borda e será marcado como um público de streaming.

Além disso, cada organização só pode ter **uma** política de mesclagem ativa na borda. Se uma política de mesclagem estiver ativa na borda, ela poderá ser usada para outros sistemas na borda, como Perfil do Edge, Segmentação do Edge e Destinos no Edge.

### Concluir objeto de política de mesclagem

O objeto de política de mesclagem completo representa um conjunto de preferências que controlam os aspectos da mesclagem de fragmentos de perfil.

**Objeto de política de mesclagem**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{ORG_ID}",
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
        "isActiveOnEdge": "{BOOLEAN}",
        "default": "{BOOLEAN}",
        "updateEpoch": "{UPDATE_TIME}"
    }
```

| Propriedade | Descrição |
|---|---|
| `id` | O identificador exclusivo gerado pelo sistema atribuído no momento da criação |
| `name` | Nome amigável pelo qual a política de mesclagem pode ser identificada nas exibições de lista. |
| `imsOrgId` | ID da organização à qual essa política de mesclagem pertence |
| `schema.name` | Parte do objeto [`schema`](#schema), o campo `name` contém a classe de esquema XDM à qual a política de mesclagem está relacionada. Para obter mais informações sobre esquemas e classes, leia a [documentação sobre XDM](../../xdm/home.md). |
| `version` | [!DNL Platform] versão mantida da política de mesclagem. Esse valor somente leitura é incrementado sempre que uma política de mesclagem é atualizada. |
| `identityGraph` | Objeto [Gráfico de identidade](#identity-graph) indicando o gráfico de identidade a partir do qual as identidades relacionadas serão obtidas. Os fragmentos de perfil encontrados para todas as identidades relacionadas serão mesclados. |
| `attributeMerge` | Objeto [Mesclagem de atributos](#attribute-merge) indicando a maneira pela qual a política de mesclagem priorizará os atributos de perfil em caso de conflitos de dados. |
| `isActiveOnEdge` | Valor booliano que indica se essa política de mesclagem pode ser usada na borda. Por padrão, este valor é `false`. |
| `default` | Valor booliano que indica se essa política de mesclagem é o padrão do esquema especificado. |
| `updateEpoch` | Data da última atualização da política de mesclagem. |

**Exemplo de política de mesclagem**

```json
    {
        "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
        "name": "profile-default",
        "imsOrgId": "{ORG_ID}",
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
        "isActiveOnEdge": false,
        "default": true,
        "updateEpoch": 1551660639
    }
```

### Gráfico de identidade {#identity-graph}

O [Adobe Experience Platform Identity Service](../../identity-service/home.md) gerencia os gráficos de identidade usados globalmente e para cada organização em [!DNL Experience Platform]. O atributo `identityGraph` da política de mesclagem define como determinar as identidades relacionadas de um usuário.

**objeto identityGraph**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

Onde `{IDENTITY_GRAPH_TYPE}` é um dos seguintes:

* **&quot;nenhum&quot;:** Não executar compilação de identidade.
* **&quot;pdg&quot;:** Execute a compilação de identidade com base em seu gráfico de identidade privado.

**Exemplo`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### Mesclagem de atributo {#attribute-merge}

Um fragmento de perfil são as informações de perfil de apenas uma identidade da lista de identidades existentes para um usuário específico. Quando o tipo de gráfico de identidade usado resulta em mais de uma identidade, há uma possibilidade de atributos de perfil conflitantes e a prioridade deve ser especificada. Usando o `attributeMerge`, você pode especificar quais atributos de perfil priorizar no caso de um conflito de mesclagem entre conjuntos de dados do tipo Valor principal (dados de registro).

**objeto attributeMerge**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

Onde `{ATTRIBUTE_MERGE_TYPE}` é um dos seguintes:

* **`timestampOrdered`**: (padrão) dê prioridade ao perfil que foi atualizado por último. Usando este tipo de mesclagem, o atributo `data` não é necessário.
* **`dataSetPrecedence`**: dê prioridade aos fragmentos de perfil com base no conjunto de dados de onde eles vieram. Isso pode ser usado quando as informações presentes em um conjunto de dados são preferenciais ou confiáveis em relação aos dados em outro conjunto de dados. Ao usar esse tipo de mesclagem, o atributo `order` é necessário, pois lista os conjuntos de dados na ordem de prioridade.
   * **`order`**: Quando &quot;dataSetPrecedence&quot; é usado, uma matriz `order` deve ser fornecida com uma lista de conjuntos de dados. Quaisquer conjuntos de dados não incluídos na lista não serão mesclados. Em outras palavras, os conjuntos de dados devem ser listados explicitamente para serem mesclados em um perfil. A matriz `order` lista as IDs dos conjuntos de dados em ordem de prioridade.

#### Exemplo de objeto `attributeMerge` usando tipo `dataSetPrecedence`

```json
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
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

O objeto de esquema especifica a classe de esquema do Experience Data Model (XDM) para a qual essa política de mesclagem é criada.

**`schema`objeto**

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

Onde o valor de `name` é o nome da classe XDM na qual se baseia o esquema associado à política de mesclagem.

**Exemplo`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

Para saber mais sobre o XDM e trabalhar com esquemas no Experience Platform, comece lendo a [Visão geral do sistema XDM](../../xdm/home.md).

## Acessar políticas de mesclagem {#access-merge-policies}

Usando a API [!DNL Real-Time Customer Profile], o ponto de extremidade `/config/mergePolicies` permite executar uma solicitação de pesquisa para exibir uma política de mesclagem específica por sua ID ou acessar todas as políticas de mesclagem em sua organização, filtradas por critérios específicos. Você também pode usar o ponto de extremidade `/config/mergePolicies/bulk-get` para recuperar várias políticas de mesclagem por meio de suas IDs. As etapas para executar cada uma dessas chamadas são descritas nas seções a seguir.

### Acessar uma única política de mesclagem por ID

Você pode acessar uma única política de mesclagem por sua ID fazendo uma solicitação GET para o ponto de extremidade `/config/mergePolicies` e incluindo `mergePolicyId` no caminho da solicitação.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da política de mesclagem.

```json
{
    "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": "false",
    "default": false,
    "updateEpoch": 1551127597
}
```

Consulte a seção [componentes das políticas de mesclagem](#components-of-merge-policies) no início deste documento para obter detalhes sobre cada um dos elementos individuais que compõem uma política de mesclagem.

### Recuperar várias políticas de mesclagem por suas IDs

Você pode recuperar várias políticas de mesclagem fazendo uma solicitação POST para o ponto de extremidade `/config/mergePolicies/bulk-get` e incluindo as IDs das políticas de mesclagem que deseja recuperar no corpo da solicitação.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Uma resposta bem-sucedida retorna o Status HTTP 207 (Vários status) e os detalhes das políticas de mesclagem cujas IDs foram fornecidas na solicitação POST.

```json
{ 
    "results": { 
        "0bf16e61-90e9-4204-b8fa-ad250360957b": {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": true,
            "default": true,
            "updateEpoch": 1552086578
        },
        "42d4a596-b1c6-46c0-994e-ca5ef1f85130": {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": false,
            "default": false,
            "updateEpoch": 1576099719
        }
    }
}
```

Consulte a seção [componentes das políticas de mesclagem](#components-of-merge-policies) no início deste documento para obter detalhes sobre cada um dos elementos individuais que compõem uma política de mesclagem.

### Listar várias políticas de mesclagem por critérios

Você pode listar várias políticas de mesclagem em sua organização emitindo uma solicitação GET para o ponto de extremidade `/config/mergePolicies` e usando parâmetros de consulta opcionais para filtrar, ordenar e paginar a resposta. Vários parâmetros podem ser incluídos, separados por &quot;E&quot; comercial (&amp;). Fazer uma chamada para esse endpoint sem parâmetros recuperará todas as políticas de mesclagem disponíveis para sua organização.

**Formato da API**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| Parâmetro | Descrição |
|---|---|
| `default` | Um valor booliano que filtra os resultados determinando se as políticas de mesclagem são ou não o padrão de uma classe de esquema. |
| `limit` | Especifica o limite de tamanho de página para controlar o número de resultados incluídos em uma página. Valor padrão: 20 |
| `orderBy` | Especifica o campo pelo qual ordenar resultados como em `orderBy=name` ou `orderBy=+name` para classificar por nome em ordem crescente, ou `orderBy=-name` para classificar em ordem decrescente. A omissão desse valor resulta na classificação padrão de `name` em ordem crescente. |
| `isActiveOnEdge` | Um valor booliano que filtra os resultados determinando se as políticas de mesclagem estão ou não ativas na borda. |
| `schema.name` | Nome do esquema para o qual recuperar as políticas de mesclagem disponíveis. |
| `identityGraph.type` | Filtra os resultados pelo tipo de gráfico de identidade. Os valores possíveis incluem &quot;none&quot; e &quot;pdg&quot; (Gráfico privado). |
| `attributeMerge.type` | Filtra os resultados pelo tipo de mesclagem de atributos usado. Os valores possíveis incluem &quot;timestampOrdered&quot; e &quot;dataSetPrecedence&quot;. |
| `start` | Deslocamento de página - especifique a ID inicial dos dados a serem recuperados. Valor padrão: 0 |
| `version` | Especifique se quiser usar uma versão específica da política de mesclagem. Por padrão, a versão mais recente será usada. |

Para obter mais informações sobre `schema.name`, `identityGraph.type` e `attributeMerge.type`, consulte a seção [componentes das políticas de mesclagem](#components-of-merge-policies) fornecida anteriormente neste guia.


**Solicitação**

A solicitação a seguir lista todas as políticas de mesclagem para um determinado esquema:

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": true,
            "default": true,
            "updateEpoch": 1552086578
        },
        {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": false,
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
| `_links.next.href` | Um endereço URI para a próxima página de resultados. Use esse URI como o parâmetro de solicitação para outra chamada de API para o mesmo endpoint para exibir a página. Se não existir uma próxima página, esse valor será uma cadeia de caracteres vazia. |

## Criar uma política de mesclagem

Você pode criar uma nova política de mesclagem para sua organização fazendo uma solicitação POST para o ponto de extremidade `/config/mergePolicies`.

**Formato da API**

```http
POST /config/mergePolicies
```

**Solicitação**
A solicitação a seguir cria uma nova política de mesclagem, que é configurada pelos valores de atributo fornecidos na carga:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/mergePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Loyalty members ordered by ID",
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type":"dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "schema": {
        "name":"_xdm.context.profile"
    },
    "isActiveOnEdge": true,
    "default": true
}'
```

| Propriedade | Descrição |
|---|---|
| `name` | Um nome amigável pelo qual a política de mesclagem pode ser identificada nas exibições de lista. |
| `identityGraph.type` | O tipo de gráfico de identidade a partir do qual obter identidades relacionadas para mesclagem. Valores possíveis: &quot;none&quot; ou &quot;pdg&quot; (gráfico privado). |
| `attributeMerge` | A maneira pela qual priorizar valores de atributo de perfil em caso de conflitos de dados. |
| `schema` | A classe de esquema XDM associada à política de mesclagem. |
| `isActiveOnEdge` | Especifica se esta política de mesclagem está ativa na borda. |
| `default` | Especifica se essa política de mesclagem é o padrão para o esquema. |

Consulte a seção [componentes das políticas de mesclagem](#components-of-merge-policies) para obter mais informações.

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da política de mesclagem recém-criada.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

Consulte a seção [componentes das políticas de mesclagem](#components-of-merge-policies) no início deste documento para obter detalhes sobre cada um dos elementos individuais que compõem uma política de mesclagem.

## Atualizar uma política de mesclagem {#update}

Você pode modificar uma política de mesclagem existente editando atributos individuais (PATCH) ou substituindo a política de mesclagem inteira por novos atributos (PUT). Exemplos de cada um são mostrados abaixo.

### Editar campos de política de mesclagem individuais

Você pode editar campos individuais para uma política de mesclagem fazendo uma solicitação PATCH para o ponto de extremidade `/config/mergePolicies/{mergePolicyId}`:

**Formato da API**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| Parâmetro | Descrição |
|---|---|
| `{mergePolicyId}` | O identificador da política de mesclagem que você deseja excluir. |

**Solicitação**

A solicitação a seguir atualiza uma política de mesclagem especificada alterando o valor de sua propriedade `default` para `true`:

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | Especifica a operação a ser executada. Exemplos de outras operações PATCH podem ser encontrados na [documentação de patch de JSON](https://datatracker.ietf.org/doc/html/rfc6902) |
| `path` | O caminho do campo a ser atualizado. Os valores aceitos são: &quot;/name&quot;, &quot;/identityGraph.type&quot;, &quot;/attributeMerge.type&quot;, &quot;/schema.name&quot;, &quot;/version&quot;, &quot;/default&quot;, &quot;/isActiveOnEdge&quot; |
| `value` | O valor para o qual definir o campo especificado. |

Consulte a seção [componentes das políticas de mesclagem](#components-of-merge-policies) para obter mais informações.


**Resposta**

Uma resposta bem-sucedida retorna os detalhes da política de mesclagem recém-atualizada.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": true,
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

A solicitação a seguir substitui a política de mesclagem especificada, substituindo seus valores de atributo pelos fornecidos na carga. Como essa solicitação substitui completamente uma política de mesclagem existente, é necessário fornecer todos os mesmos campos que foram necessários ao definir originalmente a política de mesclagem. No entanto, desta vez você está fornecendo valores atualizados para os campos que deseja alterar.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Loyalty members ordered by ID",
        "imsOrgId": "{ORG_ID}",
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
        "isActiveOnEdge": true,
        "default": true,
        "updateEpoch": 1551898378
    }'
```

| Propriedade | Descrição |
|---|---|
| `name` | Um nome amigável pelo qual a política de mesclagem pode ser identificada nas exibições de lista. |
| `identityGraph` | O gráfico de identidade a partir do qual obter identidades relacionadas para mesclagem. |
| `attributeMerge` | A maneira pela qual priorizar valores de atributo de perfil em caso de conflitos de dados. |
| `schema` | A classe de esquema XDM associada à política de mesclagem. |
| `isActiveOnEdge` | Especifica se esta política de mesclagem está ativa na borda. |
| `default` | Especifica se essa política de mesclagem é o padrão para o esquema. |

Consulte a seção [componentes das políticas de mesclagem](#components-of-merge-policies) para obter mais informações.

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da política de mesclagem atualizada.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

## Excluir uma política de mesclagem

Uma política de mesclagem pode ser excluída fazendo uma solicitação DELETE para o ponto de extremidade `/config/mergePolicies` e incluindo a ID da política de mesclagem que você deseja excluir no caminho da solicitação.

>[!NOTE]
>
>Se a política de mesclagem tiver `isActiveOnEdge` definido como true, a política de mesclagem **não poderá** ser excluída. Use os pontos de extremidade [PATCH](#edit-individual-merge-policy-fields) ou [PUT](#overwrite-a-merge-policy) para atualizar a política de mesclagem antes de excluí-la.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma solicitação de exclusão bem-sucedida retorna o Status HTTP 200 (OK) e um corpo de resposta vazio. Para confirmar que a exclusão foi bem-sucedida, você pode executar uma solicitação do GET para visualizar a política de mesclagem pela ID. Se a política de mesclagem tiver sido excluída, você receberá um erro de Status HTTP 404 (Não encontrado).

## Próximas etapas

Agora que você sabe como criar e configurar políticas de mesclagem para sua organização, é possível usá-las para ajustar a exibição de perfis de clientes na Platform e criar públicos a partir dos dados do [!DNL Real-Time Customer Profile].

Consulte a [documentação do Serviço de segmentação do Adobe Experience Platform](../../segmentation/home.md) para começar a definir e trabalhar com públicos.
