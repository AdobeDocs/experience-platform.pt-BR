---
title: Classificação e filtragem de respostas na API do serviço de fluxo
description: Este tutorial aborda a sintaxe para classificação e filtragem usando parâmetros de consulta na API de serviço de fluxo, incluindo alguns casos de uso avançados.
exl-id: 029c3199-946e-4f89-ba7a-dac50cc40c09
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 2%

---

# Classificação e filtragem de respostas na API do Serviço de fluxo

Ao executar solicitações de listagem (GET) na [API de Serviço de Fluxo](https://www.adobe.io/experience-platform-apis/references/flow-service/), você pode usar parâmetros de consulta para classificar e filtrar respostas. Este guia fornece uma referência sobre como usar esses parâmetros para casos de uso diferentes.

## Classificação

Você pode classificar respostas usando um parâmetro de consulta `orderby`. Os seguintes recursos podem ser classificados na API:

* [Conexões](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Connections)
* [Conexões do Source](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Source-connections)
* [Conexões de destino](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Target-connections)
* [Fluxos](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Flows)
* [Execuções](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Runs)

Para usar o parâmetro, você deve definir seu valor para a propriedade específica pela qual deseja classificar (por exemplo, `?orderby=name`). Você pode anexar o valor com um sinal de mais (`+`) em ordem crescente ou com um sinal de menos (`-`) em ordem decrescente. Se nenhum prefixo de ordenação for fornecido, a lista será classificada em ordem crescente por padrão.

```http
GET /flows?orderby=name
GET /flows?orderby=-name
```

Você também pode combinar um parâmetro de classificação com um parâmetro de filtragem usando um símbolo &quot;and&quot; (`&`).

```http
GET /flows?property=state==enabled&orderby=createdAt
```

## Filtragem

Você pode filtrar respostas usando um parâmetro `property` com uma expressão de valor-chave. Por exemplo, `?property=id==12345` retorna apenas recursos cuja propriedade `id` seja exatamente igual a `12345`.

A filtragem pode ser aplicada genericamente em qualquer propriedade em uma entidade, desde que o caminho válido para essa propriedade seja conhecido.

>[!NOTE]
>
>Se uma propriedade estiver aninhada dentro de um item de matriz, você deve anexar colchetes (`[]`) à matriz no caminho. Consulte a seção sobre [filtragem em propriedades de matriz](#arrays) para obter exemplos.

**Retorna todas as conexões de origem em que o nome da tabela de origem é `lead`:**

```http
GET /sourceConnections?property=params.tableName==lead
```

**Retornar todos os fluxos para uma ID de segmento específica:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

### Combinação de filtros

Vários filtros `property` podem ser incluídos em uma consulta, desde que sejam separados por caracteres &quot;e&quot; (`&`). Uma relação AND é presumida ao combinar filtros, o que significa que uma entidade deve satisfazer todos os filtros para ser incluída na resposta.

**Retornar todos os fluxos habilitados para uma ID de segmento:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a&property=state==enabled
```

### Filtragem nas propriedades da matriz {#arrays}

Você pode filtrar com base nas propriedades dos itens dentro das matrizes, anexando `[]` ao nome da propriedade de matriz.

**Retornar fluxos associados a conexões de origem específicas:**

```http
GET /flows?property=sourceConnectionIds[]==9874984,6980696
```

**Fluxos de retorno que têm uma transformação contendo uma ID de valor de seletor específica:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

**Retorne conexões de origem que tenham uma coluna com um valor `name` específico:**

```http
GET /sourceConnections?property=params.columns[].name==firstName
```

**Procure a ID de execução do fluxo para um destino filtrando a ID do segmento:**

```http
GET /runs?property=metrics.recordSummary.targetSummaries[].entitySummaries[].id==segment:068d6e2c-b546-4c73-bfb7-9a9d33375659
```

### `count`

Qualquer consulta de filtragem pode ser anexada ao parâmetro de consulta `count` com um valor de `true` para retornar a contagem dos resultados. A resposta da API contém uma propriedade `count` cujo valor representa a contagem do total de itens filtrados. Os itens reais filtrados não são retornados nesta chamada.

**Retorna a contagem de fluxos habilitados no sistema:**

```http
GET /flows?property=state==enabled&count=true
```

A resposta à consulta acima seria semelhante ao seguinte:

```json
{
  "count": 95
}
```

### Propriedades filtráveis por recurso

Dependendo da entidade do Serviço de Fluxo que você está recuperando, propriedades diferentes podem ser usadas para filtragem. As tabelas abaixo detalham os campos de nível raiz de cada recurso normalmente empregado na filtragem de casos de uso.

**`connectionSpec`**

| Propriedade | Exemplo |
| --- | --- |
| `id` | `/connectionSpecs?property=id==736873,9485095` |
| `name` | `/connectionSpecs?property=name==TestConn` |
| `providerId` | `/connectionSpecs?property=providerId==3897933` |
| `attributes.{ATTRIBUTE_NAME}` | `/connectionSpecs?property=attributes.sampleAttribute="abc"` |

{style="table-layout:auto"}

**`flowSpec`**

| Propriedade | Exemplo |
| --- | --- |
| `id` | `/flowSpecs?property=id==736873,9485095` |
| `name` | `/flowSpecs?property=name==TestConn` |
| `providerId` | `/flowSpecs?property=providerId==3897933` |

{style="table-layout:auto"}

**`connection`**

| Propriedade | Exemplo |
| --- | --- |
| `id` | `/connections?property=id==736873,9485095` |
| `name` | `/connections?property=name==TestConn` |
| `description` | `/connections?property=description==Test%20description` |
| `connectionSpec.id` | `/connections?property=connectionSpec.id==938903,849048` |
| `state` | `/connections?property=state==enabled` |

{style="table-layout:auto"}

**`sourceConnection`**

| Propriedade | Exemplo |
| --- | --- |
| `id` | `/sourceConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/sourceConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/sourceConnections?property=baseConnectionId==983908,4908095` |

{style="table-layout:auto"}

**`targetConnection`**

| Propriedade | Exemplo |
| --- | --- |
| `id` | `/targetConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/targetConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/targetConnections?property=baseConnectionId==983908,4908095` |

{style="table-layout:auto"}

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

{style="table-layout:auto"}

**`run`**

| Propriedade | Exemplo |
| --- | --- |
| `id` | `/runs?property=id==736873,9485095` |
| `flowId` | `/runs?property=flowId==8749844` |
| `state` | `/runs?property=state==inProgress` |

{style="table-layout:auto"}

## Casos de uso {#use-cases}

Leia esta seção para obter alguns exemplos específicos de como você pode usar a filtragem e a classificação para retornar informações sobre determinados conectores ou para ajudá-lo a resolver problemas de depuração. Se houver algum caso de uso adicional que você queira que o Adobe adicione, use as **[!UICONTROL Opções detalhadas de feedback]** na página para enviar uma solicitação.

**Filtrar para retornar conexões somente a um determinado destino**

Você pode usar filtros para retornar conexões somente a determinados destinos. Primeiro, consulte o ponto de extremidade `connectionSpecs` como abaixo:

```http
GET /connectionSpecs
```

Em seguida, pesquise o `connectionSpec` desejado, inspecionando o parâmetro `name`. Por exemplo, pesquise por Amazon Ads, Pega, SFTP etc. no parâmetro `name`. O `id` correspondente é o `connectionSpec` pelo qual você pode pesquisar na próxima chamada de API.

Por exemplo, filtre seus destinos para retornar apenas conexões existentes com conexões do Amazon S3:

```http
GET /connections?property=connectionSpec.id==4890fc95-5a1f-4983-94bb-e060c08e3f81
```

**Filtrar para retornar fluxos de dados somente a destinos**

Ao consultar o ponto de extremidade `/flows`, em vez de retornar todos os fluxos de dados de origens e destinos, você pode usar um filtro para retornar fluxos de dados somente a destinos. Para fazer isso, use `isDestinationFlow` como parâmetro de consulta, desta forma:

```http
GET /flows?property=inheritedAttributes.properties.isDestinationFlow==true
```

**Filtrar para retornar fluxos de dados somente a uma determinada origem ou destino**

Você pode filtrar fluxos de dados para retornar fluxos de dados a um determinado destino ou somente a partir de uma determinada origem. Por exemplo, filtre seus destinos para retornar apenas conexões existentes com conexões do Amazon S3:

```http
GET /flows?property=inheritedAttributes.targetConnections[].connectionSpec.id==4890fc95-5a1f-4983-94bb-e060c08e3f81
```

**Filtrar para obter todas as execuções de um fluxo de dados por um período específico**

É possível filtrar as execuções de fluxo de dados de um fluxo de dados para observar apenas as execuções em um determinado intervalo de tempo, como abaixo:

```
GET /runs?property=flowId==<flow-id>&property=metrics.durationSummary.startedAtUTC>1593134665781&property=metrics.durationSummary.startedAtUTC<1653134665781
```

**Filtro para retornar somente fluxos de dados com falha**

Para fins de depuração, você pode filtrar e ver todas as execuções de fluxo de dados com falha para um determinado fluxo de dados de origem ou destino, como abaixo:

```http
GET /runs?property=flowId==<flow-id>&property=metrics.statusSummary.status==Failed
```

## Próximas etapas

Este guia abordou como usar os parâmetros de consulta `orderby` e `property` para classificar e filtrar respostas na API do Serviço de Fluxo. Para obter guias passo a passo sobre como usar a API para fluxos de trabalho comuns no Experience Platform, consulte os tutoriais da API contidos na documentação de [fontes](../../sources/home.md) e [destinos](../../destinations/home.md).
