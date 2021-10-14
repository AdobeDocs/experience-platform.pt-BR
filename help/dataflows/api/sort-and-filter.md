---
title: Classificação e filtragem de respostas na API do serviço de fluxo
description: Este tutorial aborda a sintaxe para classificação e filtragem usando parâmetros de consulta na API do Serviço de fluxo, incluindo alguns casos de uso avançados.
source-git-commit: ccca81357bd7d7083abd3f395aa547c85ebf65fd
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 6%

---

# Classificação e filtragem de respostas na API do Serviço de fluxo

Ao executar solicitações de listagem (GET) na [API do Serviço de Fluxo](https://www.adobe.io/experience-platform-apis/references/flow-service/), você pode usar parâmetros de consulta para classificar e filtrar respostas. Este guia fornece uma referência sobre como usar esses parâmetros para casos de uso diferentes.

## Classificação

Você pode classificar respostas usando um parâmetro de consulta `orderby`. Os seguintes recursos podem ser classificados na API:

* [Conexões](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Connections)
* [Conexões de origem](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Source-connections)
* [Conexões do Target](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Target-connections)
* [Fluxos](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Flows)
* [Execuções](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Runs)

Para usar o parâmetro , você deve definir seu valor para a propriedade específica pela qual deseja classificar (por exemplo, `?orderby=name`). Você pode anexar o valor com um sinal de mais (`+`) para ordem crescente ou sinal de menos (`-`) para ordem decrescente. Se nenhum prefixo de pedido for fornecido, a lista será classificada em ordem crescente por padrão.

```http
GET /flows?orderby=name
GET /flows?orderby=-name
```

Você também pode combinar um parâmetro de classificação com um parâmetro de filtragem usando um símbolo &quot;e&quot; (`&`).

```http
GET /flows?property=state==enabled&orderby=createdAt
```

## Filtragem

Você pode filtrar respostas usando um parâmetro `property` com uma expressão de valor-chave. Por exemplo, `?property=id==12345` retorna apenas recursos cuja propriedade `id` é igual exatamente a `12345`.

A filtragem pode ser aplicada genericamente em qualquer propriedade em uma entidade, desde que o caminho válido para essa propriedade seja conhecido.

>[!NOTE]
>
>Se uma propriedade estiver aninhada dentro de um item de matriz, você deverá anexar colchetes (`[]`) à matriz no caminho. Consulte a seção sobre [filtragem nas propriedades da matriz](#arrays) para obter exemplos.

**Retorna todas as conexões de origem onde o nome da tabela de origem é  `lead`:**

```http
GET /sourceConnections?property=params.tableName==lead
```

**Retorna todos os fluxos para uma ID de segmento específica:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

### Combinação de filtros

Vários filtros `property` podem ser incluídos em uma query, desde que sejam separados por caracteres &quot;e&quot; (`&`). Uma relação AND é assumida ao combinar filtros, o que significa que uma entidade deve atender a todos os filtros para que seja incluída na resposta.

**Retorna todos os fluxos ativados para uma ID de segmento:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a&property=state==enabled
```

### Filtragem nas propriedades da matriz {#arrays}

Você pode filtrar com base nas propriedades dos itens em matrizes ao anexar `[]` ao nome da propriedade da matriz.

**Fluxos de retorno associados a conexões de origem específicas:**

```http
GET /flows?property=sourceConnectionIds[]==9874984,6980696
```

**Fluxos de retorno com uma transformação contendo uma ID de valor do seletor específico:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

**Retornar conexões de origem com uma coluna com um  `name` valor específico:**

```http
GET /sourceConnections?property=params.columns[].name==firstName
```

**Procure a ID de execução de fluxo para um destino filtrando a ID do segmento:**

```http
GET /runs?property=metrics.recordSummary.targetSummaries[].entitySummaries[].id==segment:068d6e2c-b546-4c73-bfb7-9a9d33375659
```

### `count`

Qualquer consulta de filtragem pode ser anexada com `count` parâmetro de consulta com um valor `true` para retornar a contagem dos resultados. A resposta da API contém uma propriedade `count` cujo valor representa a contagem do total de itens filtrados. Os itens filtrados reais não são retornados nesta chamada.

**Retorna a contagem de fluxos ativados no sistema:**

```http
GET /flows?property=state==enabled&count=true
```

A resposta à query acima seria semelhante ao seguinte:

```json
{
  "count": 95
}
```

### Propriedades filtráveis por recurso

Dependendo da entidade do Serviço de Fluxo que você está recuperando, diferentes propriedades podem ser usadas para filtragem. As tabelas abaixo detalham os campos de nível raiz de cada recurso que são comumente empregados na filtragem de casos de uso.

**`connectionSpec`**

| Propriedade | Exemplo |
| --- | --- |
| `id` | `/connectionSpecs?property=id==736873,9485095` |
| `name` | `/connectionSpecs?property=name==TestConn` |
| `providerId` | `/connectionSpecs?property=providerId==3897933` |
| `attributes.{ATTRIBUTE_NAME}` | `/connectionSpecs?property=attributes.sampleAttribute="abc"` |

{style=&quot;table-layout:auto&quot;}

**`flowSpec`**

| Propriedade | Exemplo |
| --- | --- |
| `id` | `/flowSpecs?property=id==736873,9485095` |
| `name` | `/flowSpecs?property=name==TestConn` |
| `providerId` | `/flowSpecs?property=providerId==3897933` |

{style=&quot;table-layout:auto&quot;}

**`connection`**

| Propriedade | Exemplo |
| --- | --- |
| `id` | `/connections?property=id==736873,9485095` |
| `name` | `/connections?property=name==TestConn` |
| `description` | `/connections?property=description==Test%20description` |
| `connectionSpec.id` | `/connections?property=connectionSpec.id==938903,849048` |
| `state` | `/connections?property=state==enabled` |

{style=&quot;table-layout:auto&quot;}

**`sourceConnection`**

| Propriedade | Exemplo |
| --- | --- |
| `id` | `/sourceConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/sourceConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/sourceConnections?property=baseConnectionId==983908,4908095` |

{style=&quot;table-layout:auto&quot;}

**`targetConnection`**

| Propriedade | Exemplo |
| --- | --- |
| `id` | `/targetConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/targetConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/targetConnections?property=baseConnectionId==983908,4908095` |

{style=&quot;table-layout:auto&quot;}

**`flow`**

| Propriedade | Exemplo |
| --- | --- |
| `id` | `/flows?property=id==736873,9485095` |
| `name` | `/flows?property=name==TestFlow` |
| `description` | `/flows?property=description==Test%20description` |
| `flowSpec.id` | `/flows?property=flowSpec.id==938903,849048` |
| `state` | `/flows?property=state==enabled` |
| `sourceConnectionIds` | `/flows?property=sourceConnectionIds[]==9874984,6980696` |
| `targetConnectionIds` | `/flows?property=targetConnectionIds[]==598590,690666` |

{style=&quot;table-layout:auto&quot;}

**`run`**

| Propriedade | Exemplo |
| --- | --- |
| `id` | `/runs?property=id==736873,9485095` |
| `flowId` | `/runs?property=flowId==8749844` |
| `state` | `/runs?property=state==inProgress` |

{style=&quot;table-layout:auto&quot;}

## Próximas etapas

Este guia cobriu como usar os parâmetros de consulta `orderby` e `property` para classificar e filtrar respostas na API do Serviço de Fluxo. Para obter guias passo a passo sobre como usar a API para fluxos de trabalho comuns na Platform, consulte os tutoriais da API contidos na documentação [sources](../../sources/home.md) e [destination](../../destinations/home.md).
