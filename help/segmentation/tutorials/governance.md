---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Impor conformidade de uso de dados para segmentos de audiência
topic: tutorial
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '1323'
ht-degree: 1%

---


# Impor conformidade de uso de dados para um segmento de audiência usando APIs

Este tutorial aborda as etapas para impor a conformidade de uso de dados para segmentos de [!DNL Real-time Customer Profile] audiência usando APIs.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do [!DNL Adobe Experience Platform]:

- [!DNL Real-time Customer Profile](../../profile/home.md): [!DNL Real-time Customer Profile] é um repositório de entidade de pesquisa genérico e é usado para gerenciar dados [!DNL Experience Data Model] (XDM) no [!DNL Platform]. O Perfil mescla dados em vários ativos de dados corporativos e fornece acesso a esses dados em uma apresentação unificada.
   - [Mesclar políticas](../../profile/api/merge-policies.md): Regras usadas para [!DNL Real-time Customer Profile] determinar quais dados podem ser mesclados em uma visualização unificada sob determinadas condições. As políticas de mesclagem podem ser configuradas para [!DNL Data Governance] fins.
- [!DNL Segmentation](../home.md): Como [!DNL Real-time Customer Profile] divide um grande grupo de indivíduos contidos na loja de perfis em grupos menores que compartilham características semelhantes e respondem de forma semelhante às estratégias de marketing.
- [!DNL Data Governance](../../data-governance/home.md): [!DNL Data Governance] fornece a infraestrutura para a identificação e aplicação da utilização de dados (DULE), usando os seguintes componentes:
   - [Rótulos](../../data-governance/labels/user-guide.md)de uso de dados: Rótulos utilizados para descrever conjuntos de dados e campos em termos do nível de sensibilidade com que lidam com os respectivos dados.
   - [Políticas](../../data-governance/policies/overview.md)de uso de dados: Configurações que indicam quais ações de marketing são permitidas em dados categorizados por rótulos de uso de dados específicos.
   - [Aplicação](../../data-governance/enforcement/overview.md)de políticas: Permite que você aplique políticas de uso de dados e previna operações de dados que constituem violações de política.
- [Caixas de proteção](../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas bem-sucedidas para as [!DNL Platform] APIs.

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de [!DNL Experience Platform] solução de problemas.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o tutorial [de](../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de [!DNL Experience Platform] API, como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Pesquisar uma política de mesclagem para uma definição de segmento {#merge-policy}

Esse fluxo de trabalho começa acessando um segmento de audiência conhecido. Os segmentos que estão habilitados para uso em [!DNL Real-time Customer Profile] contêm uma ID de política de mesclagem dentro de sua definição de segmento. Esta política de mesclagem contém informações sobre quais conjuntos de dados devem ser incluídos no segmento, que por sua vez contêm quaisquer rótulos de uso de dados aplicáveis.

Usando a [!DNL Segmentation] API, você pode pesquisar uma definição de segmento por sua ID para encontrar sua política de mesclagem associada.

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

## Localizar os conjuntos de dados de origem da política de mesclagem {#datasets}

As políticas de mesclagem contêm informações sobre seus conjuntos de dados de origem, que por sua vez contêm rótulos de uso de dados. Você pode pesquisar os detalhes de uma política de mesclagem fornecendo a ID da política de mesclagem em uma solicitação de GET para a [!DNL Profile] API. Para obter mais informações sobre as políticas de mesclagem, consulte o guia [de ponto de extremidade de políticas de](../../profile/api/merge-policies.md)mesclagem.

**Formato da API**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | A ID da política de mesclagem obtida na etapa [](#merge-policy)anterior. |

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

## Avaliar conjuntos de dados para violações de política

>[!NOTE]
>
> Esta etapa supõe que você tenha pelo menos uma política de uso de dados ativa que impeça a execução de ações de marketing específicas em dados que contenham determinados rótulos. Se você não tiver políticas de uso aplicáveis para os conjuntos de dados que estão sendo avaliados, siga o tutorial [de criação de](../../data-governance/policies/create.md) política para criar um antes de continuar com esta etapa.

Depois de obter as IDs dos conjuntos de dados de origem da política de mesclagem, você pode usar a API [do serviço de política](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) DULE para avaliar esses conjuntos de dados em relação a ações de marketing específicas a fim de verificar violações da política de uso de dados.

Para avaliar os conjuntos de dados, forneça o nome da ação de marketing no caminho de uma solicitação de POST, fornecendo as IDs do conjunto de dados no corpo da solicitação, como mostrado no exemplo abaixo.

**Formato da API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parâmetro | Descrição |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | O nome da ação de marketing associada à política de uso de dados pela qual você está avaliando os conjuntos de dados. Dependendo de a política ter sido definida pelo Adobe ou pela sua organização, você deve usar `/marketingActions/core` ou `/marketingActions/custom`, respectivamente. |

**Solicitação**

A solicitação a seguir testa a ação de `exportToThirdParty` marketing em relação aos conjuntos de dados obtidos na etapa [](#datasets)anterior. A carga da solicitação é uma matriz que contém as IDs de cada conjunto de dados.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `entityType` | Cada item na matriz de carga deve indicar o tipo de entidade que está sendo definida. Nesse caso de uso, o valor sempre será &quot;dataSet&quot;. |
| `entityID` | Cada item na matriz de carga deve fornecer a ID exclusiva para um conjunto de dados. |

**Resposta**

Uma resposta bem-sucedida retorna o URI para a ação de marketing, os rótulos de uso de dados que foram coletados dos conjuntos de dados fornecidos e uma lista de quaisquer políticas de uso de dados que foram violadas como resultado do teste da ação contra esses rótulos. Neste exemplo, a política &quot;Exportar dados para terceiros&quot; é mostrada no `violatedPolicies` storage, indicando que a ação de marketing acionou uma violação de política.

```json
{
  "timestamp": 1556324277895,
  "clientId": "{CLIENT_ID}",
  "userId": "{USER_ID}",
  "imsOrg": "{IMS_ORG}",
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
      "imsOrg": "{IMS_ORG}",
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
| `discoveredLabels` | Uma lista dos conjuntos de dados que foram fornecidos na carga da solicitação, exibindo os rótulos no nível do conjunto de dados e no nível do campo que foram encontrados em cada um. |
| `violatedPolicies` | Um storage que lista quaisquer políticas de uso de dados que foram violadas ao testar a ação de marketing (especificada em `marketingActionRef`) em relação ao fornecido `duleLabels`. |

Usando os dados retornados na resposta da API, você pode configurar protocolos em seu aplicativo de experiência para aplicar adequadamente as violações de política quando elas ocorrem.

## Filtrar campos de dados

Se o segmento de audiência não passar na avaliação, você poderá ajustar os dados incluídos no segmento por meio de um dos dois métodos descritos abaixo.

### Atualizar a política de mesclagem da definição do segmento

Atualizar a política de mesclagem de uma definição de segmento ajusta os conjuntos de dados e campos que serão incluídos quando o trabalho de segmento for executado. Consulte a seção sobre como [atualizar uma política](../../profile/api/merge-policies.md#update) de mesclagem existente no tutorial de política de mesclagem de API para obter mais informações.

### Restringir campos de dados específicos ao exportar o segmento

Ao exportar um segmento para um conjunto de dados usando a [!DNL Segmentation] API, você pode filtrar os dados incluídos na exportação usando o `fields` parâmetro. Quaisquer campos de dados adicionados a esse parâmetro serão incluídos na exportação, enquanto todos os outros campos de dados serão excluídos.

Considere um segmento que tem campos de dados chamados &quot;A&quot;, &quot;B&quot; e &quot;C&quot;. Se você deseja exportar apenas o campo &quot;C&quot;, então o `fields` parâmetro conterá apenas o campo &quot;C&quot;. Ao fazer isso, os campos &quot;A&quot; e &quot;B&quot; seriam excluídos ao exportar o segmento.

Consulte a seção sobre como [exportar um segmento](./evaluate-a-segment.md#export) no tutorial de segmentação para obter mais informações.

## Próximas etapas

Ao seguir este tutorial, você pesquisou os rótulos de uso de dados associados a um segmento de audiência e os testou em busca de violações de política contra ações de marketing específicas. Para obter mais informações sobre [!DNL Data Governance] em [!DNL Experience Platform], leia a visão geral para [!DNL Data Governance](../../data-governance/home.md).
