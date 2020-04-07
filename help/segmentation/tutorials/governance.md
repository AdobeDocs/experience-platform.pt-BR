---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Impor conformidade de uso de dados para segmentos de audiência
topic: tutorial
translation-type: tm+mt
source-git-commit: f5bc9beb59e83b0411d98d901d5055122a124d07

---


# Impor conformidade de uso de dados para um segmento de audiência usando APIs

Este tutorial aborda as etapas para impor a conformidade de uso de dados para segmentos de audiência de Perfis de clientes em tempo real usando APIs.

## Introdução

Este tutorial requer uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

- [Perfil](../../profile/home.md)do cliente em tempo real: O Perfil de cliente em tempo real é um repositório de entidade de pesquisa genérico e é usado para gerenciar dados do Modelo de dados de experiência (XDM) na plataforma. O Perfil mescla dados em vários ativos de dados corporativos e fornece acesso a esses dados em uma apresentação unificada.
   - [Mesclar políticas](../../profile/api/merge-policies.md): Regras usadas pelo Perfil do cliente em tempo real para determinar quais dados podem ser mesclados em uma visualização unificada sob determinadas condições. As políticas de mesclagem podem ser configuradas para fins de controle de dados.
- [Segmentação](../home.md): Como o Perfil de cliente em tempo real divide um grande grupo de indivíduos contidos na loja de perfis em grupos menores que compartilham características semelhantes e responderão de forma semelhante às estratégias de marketing.
- [Controle](../../data-governance/home.md)de dados: O Data Governance fornece a infraestrutura para a rotulagem e aplicação de uso de dados (DULE), usando os seguintes componentes:
   - [Rótulos](../../data-governance/labels/user-guide.md)de uso de dados: Rótulos utilizados para descrever conjuntos de dados e campos em termos do nível de sensibilidade com que lidam com os respectivos dados.
   - [Políticas](../../data-governance/api/getting-started.md)de uso de dados: Configurações que indicam quais ações de marketing são permitidas em dados categorizados por rótulos de uso de dados específicos.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas bem-sucedidas para as APIs de plataforma.

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de solução de problemas da plataforma Experience.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para APIs de plataforma, você deve primeiro concluir o tutorial [de](../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas da API da plataforma da experiência, como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos da plataforma Experience são isolados para caixas de proteção virtuais específicas. Todas as solicitações para APIs de plataforma exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Para obter mais informações sobre caixas de proteção na Plataforma, consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Pesquisar uma política de mesclagem para uma definição de segmento

Esse fluxo de trabalho começa acessando um segmento de audiência conhecido. Os segmentos que estão habilitados para uso no Perfil de cliente em tempo real contêm uma ID de política de mesclagem na definição do segmento. Esta política de mesclagem contém informações sobre quais conjuntos de dados devem ser incluídos no segmento, que por sua vez contêm quaisquer rótulos de uso de dados aplicáveis.

Usando a API [de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)segmentação, você pode pesquisar uma definição de segmento por sua ID para encontrar sua política de mesclagem associada.

**Formato da API**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | A ID da definição de segmento que você deseja pesquisar. |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/24379cae-726a-4987-b7b9-79c32cddb5c1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da definição do segmento.

```json
{
    "id": "24379cae-726a-4987-b7b9-79c32cddb5c1",
    "schema": { 
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 90,
    "imsOrgId": "{IMS_ORG}",
    "name": "Cart abandons in CA",
    "description": "",
    "expression": {
        "type": "PQL", 
        "format": "pql/text", 
        "value": "homeAddress.countryISO = 'US'"
    },
    "mergePolicyId": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1556094486000,
    "updateEpoch": 1556094486000,
    "updateTime": 1556094486000
  }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `mergePolicyId` | A ID da política de mesclagem usada para a definição do segmento. Isso será usado na próxima etapa. |

## Localizar os conjuntos de dados de origem da política de mesclagem

As políticas de mesclagem contêm informações sobre seus conjuntos de dados de origem, que por sua vez contêm rótulos DULE. Você pode pesquisar os detalhes de uma política de mesclagem fornecendo a ID da política de mesclagem em uma solicitação GET para a API do Perfil.

**Formato da API**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | A ID da política de mesclagem obtida na etapa [](#lookup-a-merge-policy-for-a-segment-definition)anterior. |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/2b43d78d-0ad4-4c1e-ac2d-574c09b01119 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da política de mesclagem.

```json
{
    "id": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "imsOrgId": "{IMS_ORG}",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type":"dataSetPrecedence", 
        "data": {
            "order" : ["5b95b155419ec801e6eee780", "5b7c86968f7b6501e21ba9df"]
        }
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `schema.name` | O nome do schema associado à política de mesclagem. |
| `attributeMerge.type` | O tipo de configuração de precedência de dados para a política de mesclagem. Se o valor for `dataSetPrecedence`, os conjuntos de dados associados a essa política de mesclagem serão listados em `attributeMerge > data > order`. Se o valor for `timestampOrdered`, todos os conjuntos de dados associados ao schema referenciado `schema.name` serão usados pela política de mesclagem. |
| `attributeMerge.data.order` | Se o `attributeMerge.type` for `dataSetPrecedence`, esse atributo será uma matriz que contém as IDs dos conjuntos de dados usados por essa política de mesclagem. Essas IDs são usadas na próxima etapa. |

## Rótulos de uso de dados de pesquisa para os conjuntos de dados de origem

Depois de coletar as IDs dos conjuntos de dados de origem da política de mesclagem, você pode usar essas IDs para pesquisar os rótulos de uso de dados configurados para os próprios conjuntos de dados e quaisquer campos de dados específicos contidos neles.

A chamada a seguir para a API [do Serviço de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) Catálogo recupera os rótulos de uso de dados associados a um único conjunto de dados fornecendo sua ID no caminho da solicitação:

**Formato da API**

```http
GET /dataSets/{DATASET_ID}/dule
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{DATASET_ID}` | A ID do conjunto de dados cujos rótulos de uso de dados você deseja pesquisar. |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b95b155419ec801e6eee780/dule \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de rótulos de uso de dados associados ao conjunto de dados como um todo, e quaisquer campos de dados específicos associados ao schema de origem.

```json
{
    "connection": {},
    "dataset": {
        "identity": [],
        "contract": [
            "C3"
        ],
        "sensitive": [],
        "contracts": [
            "C3"
        ],
        "identifiability": [],
        "specialTypes": []
    },
    "fields": [],
    "schemaFields": [
        {
            "path": "/properties/personalEmail/properties/address",
            "identity": [
                "I1"
            ],
            "contract": [
                "C2",
                "C9"
            ],
            "sensitive": [],
            "contracts": [
                "C2",
                "C9"
            ],
            "identifiability": [
                "I1"
            ],
            "specialTypes": []
        }
    ]
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `dataset` | Um objeto que contém os rótulos de uso de dados aplicados ao conjunto de dados como um todo. |
| `schemaFields` | Uma matriz de objetos que representa campos de schema específicos que têm rótulos de uso de dados aplicados a eles. |
| `schemaFields.path` | O caminho do campo schema cujos rótulos de uso de dados estão listados no mesmo objeto. |

## Filtrar campos de dados

>[!NOTE] Esta etapa é opcional. Se você não quiser ajustar os dados incluídos em seu segmento com base em suas descobertas na etapa anterior da [pesquisa dos rótulos](#lookup-data-usage-labels-for-the-source-datasets)de uso de dados, vá para a etapa final de [avaliação dos dados para violações](#evaluate-data-for-policy-violations)de política.

Se desejar ajustar os dados incluídos no segmento de audiência, você pode fazer isso usando um dos dois métodos a seguir:

### Atualizar a política de mesclagem da definição do segmento

Atualizar a política de mesclagem de uma definição de segmento ajusta os conjuntos de dados e campos que serão incluídos quando o trabalho de segmento for executado. Consulte a seção sobre como [atualizar uma política](../../profile/api/merge-policies.md) de mesclagem existente no tutorial de política de mesclagem para obter mais informações.

### Restringir campos de dados específicos ao exportar o segmento

Ao exportar um segmento para um conjunto de dados usando a API Perfil do cliente em tempo real, você pode filtrar os dados incluídos na exportação usando o `fields` parâmetro. Quaisquer campos de dados adicionados a esse parâmetro serão incluídos na exportação, enquanto todos os outros campos de dados serão excluídos.

Considere um segmento que tem campos de dados chamados &quot;A&quot;, &quot;B&quot; e &quot;C&quot;. Se você deseja exportar apenas o campo &quot;C&quot;, então o `fields` parâmetro conterá apenas o campo &quot;C&quot;. Ao fazer isso, os campos &quot;A&quot; e &quot;B&quot; seriam excluídos ao exportar o segmento.

Consulte a seção sobre como [exportar um segmento](./evaluate-a-segment.md#export-a-segment) no tutorial de segmentação para obter mais informações.

## Avaliar dados para violações de política

Agora que você coletou os rótulos de uso de dados associados ao segmento de audiência, é possível testar esses rótulos em relação às ações de marketing para avaliar se há violações de política de uso de dados. Para obter etapas detalhadas sobre como executar avaliações de políticas usando a API [do serviço de política](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)DULE, consulte o documento sobre avaliação [de](../../data-governance/enforcement/overview.md)políticas.

## Próximas etapas

Ao seguir este tutorial, você pesquisou os rótulos de uso de dados associados a um segmento de audiência e os testou em busca de violações de política contra ações de marketing específicas. Para obter mais informações sobre o controle de dados na plataforma Experience, consulte a visão geral [do controle de](../../data-governance/home.md)dados.