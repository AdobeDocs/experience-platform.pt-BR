---
solution: Experience Platform
title: Impor a conformidade do uso de dados para um segmento de público-alvo usando APIs
type: Tutorial
description: Este tutorial aborda as etapas para aplicar definições de segmento de conformidade de uso de dados usando APIs.
exl-id: 2299328c-d41a-4fdc-b7ed-72891569eaf2
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1348'
ht-degree: 6%

---

# Impor a conformidade de uso de dados para uma definição de segmento usando APIs

Este tutorial aborda as etapas para impor a conformidade do uso de dados para definições de segmento usando APIs.

## Introdução

Este tutorial requer entendimento prático dos seguintes componentes do [!DNL Adobe Experience Platform]:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): [!DNL Real-Time Customer Profile] é um repositório de entidade de pesquisa genérico e é usado para gerenciar dados de [!DNL Experience Data Model (XDM)] em [!DNL Platform]. O perfil mescla dados em vários ativos de dados corporativos e fornece acesso a esses dados em uma apresentação unificada.
   - [Políticas de mesclagem](../../profile/api/merge-policies.md): regras usadas por [!DNL Real-Time Customer Profile] para determinar quais dados podem ser mesclados em uma exibição unificada em determinadas condições. As políticas de mesclagem podem ser configuradas para fins de governança de dados.
- [[!DNL Segmentation]](../home.md): Como o [!DNL Real-Time Customer Profile] divide um grande grupo de indivíduos contidos no armazenamento de Perfil em grupos menores que compartilham características semelhantes e responderão de forma semelhante às estratégias de marketing.
- [Governança de Dados](../../data-governance/home.md): a Governança de Dados fornece a infraestrutura para rotulagem e aplicação de uso de dados, usando os seguintes componentes:
   - [Rótulos de uso de dados](../../data-governance/labels/user-guide.md): rótulos usados para descrever conjuntos de dados e campos em termos do nível de sensibilidade com que tratar seus respectivos dados.
   - [Políticas de uso de dados](../../data-governance/policies/overview.md): configurações que indicam quais ações de marketing são permitidas em dados categorizados por rótulos de uso de dados específicos.
   - [Imposição de política](../../data-governance/enforcement/overview.md): permite que você imponha políticas de uso de dados e impeça operações de dados que constituam violações de política.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para as APIs do [!DNL Platform].

### Leitura de chamadas de API de amostra

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para APIs do [!DNL Platform], primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] estão isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm um conteúdo (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Pesquisar uma política de mesclagem para uma definição de segmento {#merge-policy}

Esse fluxo de trabalho começa acessando uma definição de segmento conhecida. As definições de segmento habilitadas para uso em [!DNL Real-Time Customer Profile] contêm uma ID de política de mesclagem na definição de segmento. Essa política de mesclagem contém informações sobre quais conjuntos de dados devem ser incluídos na definição do segmento, que por sua vez contém quaisquer rótulos de uso de dados aplicáveis.

Usando a API [!DNL Segmentation], você pode pesquisar uma definição de segmento por sua ID para encontrar a política de mesclagem associada.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da definição de segmento.

```json
{
    "id": "24379cae-726a-4987-b7b9-79c32cddb5c1",
    "schema": { 
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 90,
    "imsOrgId": "{ORG_ID}",
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

## Localizar os conjuntos de dados de origem na política de mesclagem {#datasets}

As políticas de mesclagem contêm informações sobre os conjuntos de dados de origem, que por sua vez contêm rótulos de uso de dados. Você pode pesquisar os detalhes de uma política de mesclagem fornecendo a ID da política de mesclagem em uma solicitação GET para a API [!DNL Profile]. Mais informações sobre políticas de mesclagem podem ser encontradas no [manual do ponto de extremidade de políticas de mesclagem](../../profile/api/merge-policies.md).

**Formato da API**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | A ID da política de mesclagem obtida na [etapa anterior](#merge-policy). |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/2b43d78d-0ad4-4c1e-ac2d-574c09b01119 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da política de mesclagem.

```json
{
    "id": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "imsOrgId": "{ORG_ID}",
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
            "order": ["5b95b155419ec801e6eee780", "5b7c86968f7b6501e21ba9df"]
        }
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `schema.name` | O nome do esquema associado à política de mesclagem. |
| `attributeMerge.type` | O tipo de configuração de precedência de dados para a política de mesclagem. Se o valor for `dataSetPrecedence`, os conjuntos de dados associados a essa política de mesclagem serão listados em `attributeMerge > data > order`. Se o valor for `timestampOrdered`, todos os conjuntos de dados associados ao esquema referenciado em `schema.name` serão usados pela política de mesclagem. |
| `attributeMerge.data.order` | Se o `attributeMerge.type` for `dataSetPrecedence`, esse atributo será uma matriz que contém as IDs dos conjuntos de dados usados por essa política de mesclagem. Essas IDs são usadas na próxima etapa. |

## Avaliar conjuntos de dados para violações de política

>[!NOTE]
>
> Essa etapa pressupõe que você tenha pelo menos uma política de uso de dados ativa que impeça que ações de marketing específicas sejam executadas em dados que contenham determinados rótulos. Se você não tiver nenhuma política de uso aplicável para os conjuntos de dados que estão sendo avaliados, siga o [tutorial de criação de política](../../data-governance/policies/create.md) para criar uma antes de continuar com esta etapa.

Depois de obter as IDs dos conjuntos de dados de origem da política de mesclagem, você poderá usar a [API do Serviço de política](https://www.adobe.io/experience-platform-apis/references/policy-service/) para avaliar esses conjuntos de dados em relação a ações de marketing específicas para verificar violações da política de uso de dados.

Para avaliar os conjuntos de dados, você deve fornecer o nome da ação de marketing no caminho de uma solicitação POST, além de fornecer as IDs do conjunto de dados no corpo da solicitação, como mostrado no exemplo abaixo.

**Formato da API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parâmetro | Descrição |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | O nome da ação de marketing associada à política de uso de dados pela qual você está avaliando os conjuntos de dados. Dependendo se a política foi definida pelo Adobe ou por sua organização, você deve usar `/marketingActions/core` ou `/marketingActions/custom`, respectivamente. |

**Solicitação**

A solicitação a seguir testa a ação de marketing `exportToThirdParty` em relação aos conjuntos de dados obtidos na [etapa anterior](#datasets). A carga da solicitação é uma matriz que contém as IDs de cada conjunto de dados.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    {
      "entityType": "dataSet",
      "entityId": "5b95b155419ec801e6eee780"
    },
    {
      "entityType": "dataSet",
      "entityId": "5b7c86968f7b6501e21ba9df"
    }
  ]'
```

| Propriedade | Descrição |
| --- | --- |
| `entityType` | Cada item na matriz de carga útil deve indicar o tipo de entidade que está sendo definido. Nesse caso de uso, o valor sempre será &quot;dataSet&quot;. |
| `entityID` | Cada item na matriz de carga deve fornecer a ID exclusiva para um conjunto de dados. |

**Resposta**

Uma resposta bem-sucedida retorna o URI da ação de marketing, os rótulos de uso de dados coletados dos conjuntos de dados fornecidos e uma lista de quaisquer políticas de uso de dados que foram violadas como resultado do teste da ação com esses rótulos. Neste exemplo, a política &quot;Exportar dados para terceiros&quot; é mostrada na matriz `violatedPolicies`, indicando que a ação de marketing acionou uma violação de política.

```json
{
  "timestamp": 1556324277895,
  "clientId": "{CLIENT_ID}",
  "userId": "{USER_ID}",
  "imsOrg": "{ORG_ID}",
  "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
  "duleLabels": [
    "C1",
    "C2",
    "C4",
    "C5"
  ],
  "discoveredLabels": [
    {
      "entityType": "dataSet",
      "entityId": "5b95b155419ec801e6eee780",
      "dataSetLabels": {
        "connection": {
          "labels": []
        },
        "dataSet": {
          "labels": [
            "C5"
          ]
        },
        "fields": [
          {
            "labels": [
              "C2",
            ],
            "path": "/properties/_customer"
          },
          {
            "labels": [
              "C5"
            ],
            "path": "/properties/geoUnit"
          },
          {
            "labels": [
              "C1"
            ],
            "path": "/properties/identityMap"
          }
        ]
      }
    },
    {
      "entityType": "dataSet",
      "entityId": "5b7c86968f7b6501e21ba9df",
      "dataSetLabels": {
        "connection": {
          "labels": []
        },
        "dataSet": {
          "labels": [
            "C5"
          ]
        },
        "fields": [
          {
            "labels": [
              "C5"
            ],
            "path": "/properties/createdByBatchID"
          },
          {
            "labels": [
              "C5"
            ],
            "path": "/properties/faxPhone"
          }
        ]
      }
    }
  ],
  "violatedPolicies": [
    {
      "name": "Export Data to Third Party",
      "status": "ENABLED",
      "marketingActionRefs": [
        "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
      ],
      "description": "Conditions under which data cannot be exported to a third party",
      "deny": {
        "operator": "OR",
        "operands": [
          {
            "label": "C1"
          },
          {
            "operator": "AND",
            "operands": [
              {
                "label": "C3"
              },
              {
                "label": "C7"
              }
            ]
          }
        ]
      },
      "imsOrg": "{ORG_ID}",
      "created": 1565651746693,
      "createdClient": "{CREATED_CLIENT}",
      "createdUser": "{CREATED_USER",
      "updated": 1565723012139,
      "updatedClient": "{UPDATED_CLIENT}",
      "updatedUser": "{UPDATED_USER}",
      "_links": {
        "self": {
          "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
        }
      },
      "id": "5d51f322e553c814e67af1a3"
    }
  ]
}
```

| Propriedade | Descrição |
| --- | --- |
| `duleLabels` | Uma lista de rótulos de uso de dados que foram extraídos dos conjuntos de dados fornecidos. |
| `discoveredLabels` | Uma lista dos conjuntos de dados fornecidos na carga da solicitação, exibindo os rótulos de nível de conjunto de dados e de nível de campo encontrados em cada um. |
| `violatedPolicies` | Uma matriz que lista quaisquer políticas de uso de dados que foram violadas ao testar a ação de marketing (especificada em `marketingActionRef`) em relação ao `duleLabels` fornecido. |

Usando os dados retornados na resposta da API, você pode configurar protocolos no aplicativo de experiência para aplicar adequadamente as violações de política quando elas ocorrerem.

## Filtrar campos de dados

Se a definição de segmento não passar na avaliação, você poderá ajustar os dados incluídos na definição de segmento por meio de um dos dois métodos descritos abaixo.

### Atualizar a política de mesclagem da definição do segmento

Atualizar a política de mesclagem de uma definição de segmento ajustará os conjuntos de dados e campos que serão incluídos quando o trabalho do segmento for executado. Consulte a seção sobre [atualização de uma política de mesclagem existente](../../profile/api/merge-policies.md#update) no tutorial de política de mesclagem de APIs para obter mais informações.

### Restringir campos de dados específicos ao exportar a definição de segmento

Ao exportar uma definição de segmento para um conjunto de dados usando a API [!DNL Segmentation], você pode filtrar os dados incluídos na exportação usando o parâmetro `fields`. Quaisquer campos de dados adicionados a esse parâmetro serão incluídos na exportação, enquanto todos os outros campos de dados serão excluídos.

Considere uma definição de segmento que tenha campos de dados chamados &quot;A&quot;, &quot;B&quot; e &quot;C&quot;. Se você deseja exportar apenas o campo &quot;C&quot;, o parâmetro `fields` conterá apenas o campo &quot;C&quot;. Ao fazer isso, os campos &quot;A&quot; e &quot;B&quot; seriam excluídos ao exportar a definição do segmento.

Consulte a seção sobre [exportação de uma definição de segmento](./evaluate-a-segment.md#export) no tutorial de segmentação para obter mais informações.

## Próximas etapas

Ao seguir este tutorial, você pesquisou os rótulos de uso de dados associados a uma definição de segmento e os testou quanto a violações de política em relação a ações de marketing específicas. Para obter mais informações sobre a Governança de dados no [!DNL Experience Platform], leia a visão geral da [Governança de dados](../../data-governance/home.md).
