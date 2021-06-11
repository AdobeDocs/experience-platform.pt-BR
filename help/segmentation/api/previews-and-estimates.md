---
keywords: Experience Platform; home; tópicos populares; segmentação; Segmentação; Serviço de segmentação; visualizações; estimativas; visualizações e estimativas; estimativas e visualizações; api; API;
solution: Experience Platform
title: Pré-visualizações e Estimativas de pontos de extremidade da API
topic-legacy: developer guide
description: Conforme a definição do segmento é desenvolvida, você pode usar as ferramentas de estimativa e visualização no Adobe Experience Platform para exibir informações de nível de resumo, de modo a ajudar a garantir que você esteja isolando o público-alvo esperado.
exl-id: 2c204f29-825f-4a5e-a7f6-40fc69263614
source-git-commit: a5cc688357e4750dee73baf3fc9af02a9f2e49e3
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 2%

---

# Pré-visualizações e endpoints de estimativas

Conforme você desenvolve uma definição de segmento, pode usar as ferramentas de estimativa e visualização no Adobe Experience Platform para exibir informações de nível de resumo, de modo a ajudar a garantir que você esteja isolando o público-alvo que espera.

* **** As visualizações fornecem listas paginadas de perfis qualificados para uma definição de segmento, permitindo que você compare os resultados com o que espera.

* **** Os cálculos fornecem informações estatísticas sobre uma definição de segmento, como o tamanho projetado do público-alvo, intervalo de confiança e desvio padrão do erro.

>[!NOTE]
>
>Para acessar métricas semelhantes relacionadas aos dados do Perfil do cliente em tempo real, como o número total de fragmentos de perfil e perfis mesclados em namespaces específicos ou o armazenamento de dados do perfil como um todo, consulte o [guia do ponto de extremidade da visualização de perfil (status da amostra de visualização)](../../profile/api/preview-sample-status.md), parte do guia do desenvolvedor da API de perfil.

## Introdução

Os endpoints usados neste guia fazem parte da API [!DNL Adobe Experience Platform Segmentation Service]. Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com êxito, incluindo cabeçalhos necessários e como ler chamadas de API de exemplo.

## Como as estimativas são geradas

Quando a assimilação de registros no armazenamento de perfil aumenta ou diminui a contagem total de perfis em mais de 5%, um trabalho de amostragem é disparado para atualizar a contagem. A forma como a amostragem de dados é acionada depende do método de ingestão:

* **Assimilação em lote:** para assimilação em lote, dentro de 15 minutos da assimilação bem-sucedida de um lote no armazenamento de Perfil, se o limite de aumento ou diminuição de 5% for atingido, uma tarefa será executada para atualizar a contagem.
* **Assimilação de fluxo:** para fluxos de trabalho de dados de fluxo contínuo, uma verificação é feita de hora em hora para determinar se o limite de aumento ou diminuição de 5% foi atingido. Se tiver sido, uma tarefa é acionada automaticamente para atualizar a contagem.

O tamanho da amostra da verificação depende do número geral de entidades no armazenamento de perfis. Esses tamanhos de amostra são representados na tabela a seguir:

| Entidades no armazenamento de perfis | Tamanho da amostra |
| ------------------------- | ----------- |
| Menos de 1 milhão | Conjunto de dados completo |
| 1 a 20 milhões | 1 milhão |
| Mais de 20 milhões | 5% do total |

>[!NOTE]
>
>As estimativas geralmente levam de 10 a 15 segundos para serem executadas, começando com uma estimativa aproximada e refinando à medida que mais registros são lidos.

## Criar uma nova visualização {#create-preview}

Você pode criar uma nova visualização, fazendo uma solicitação de POST ao endpoint `/preview`.

>[!NOTE]
>
>Uma tarefa de estimativa é criada automaticamente quando uma tarefa de visualização é criada. Esses dois trabalhos compartilham a mesma ID.

**Formato da API**

```http
POST /preview
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
    {
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile",
        "graphType": "none"
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `predicateExpression` | A expressão PQL para consultar os dados. |
| `predicateType` | O tipo de predicado da expressão de consulta em `predicateExpression`. No momento, o único valor aceito para essa propriedade é `pql/text`. |
| `predicateModel` | O nome da classe de esquema [!DNL Experience Data Model] (XDM) na qual os dados do perfil se baseiam. |
| `graphType` | O tipo de gráfico do qual você deseja obter o cluster. Os valores suportados são `none` (não executa identificação de identidade) e `pdg` (executa identificação com base no seu gráfico de identidade privado). |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) com detalhes da visualização recém-criada.

```json
{
    "state": "NEW",
    "previewQueryId": "e890068b-f5ca-4a8f-a6b5-af87ff0caac3",
    "previewQueryStatus": "NEW",
    "previewId": "MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow",
    "previewExecutionId": 0
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `state` | O estado atual do trabalho de visualização. Quando criado pela primeira vez, ele estará no estado &quot;NOVO&quot;. Subsequentemente, ele estará no estado &quot;EXECUTANDO&quot; até que o processamento seja concluído, e nesse ponto se tornará &quot;RESULT_READY&quot; ou &quot;FAILED&quot;. |
| `previewId` | A ID do trabalho de visualização, que será usada para fins de pesquisa ao visualizar uma estimativa ou pré-visualização, conforme descrito na próxima seção. |

## Recupere os resultados de uma visualização específica {#get-preview}

Você pode recuperar informações detalhadas sobre uma visualização específica fazendo uma solicitação do GET para o endpoint `/preview` e fornecendo a ID da visualização no caminho da solicitação.

**Formato da API**

```http
GET /preview/{PREVIEW_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{PREVIEW_ID}` | O valor `previewId` da visualização que você deseja recuperar. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre a visualização especificada.

```json
{
   "results": [{
        "XID_ADOBE-MARKETING-CLOUD-ID-1": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1",
            "endCustomerIds": {
                "XID_COOKIE_ID_1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_1"
                },
                "XID_PROFILE_ID_1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_1"
                }
            }
        }
    },
    {
        "XID_COOKIE-ID-2": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE-ID-2",
            "endCustomerIds": {
                "XID_COOKIE_ID_2-1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_2-1"

                },
                "XID_PROFILE_ID_2": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_2"
                }
            }
        },
        "XID_ADOBE-MARKETING-CLOUD-ID-3": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1000"
        }
    }],
    "state": "RESULT_READY",
    "links": {
        "_self": "https://platform.adobe.io/data/core/ups/preview?expression=<expr-1>&limit=1000",
        "next": "",
        "prev": ""
    },
    "page": {
        "offset": 0,
        "size": 3
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `results` | Uma lista de IDs de entidade, juntamente com suas identidades relacionadas. Os links fornecidos podem ser usados para buscar as entidades especificadas, usando o [endpoint da API de acesso ao perfil](../../profile/api/entities.md). |

## Recuperar os resultados de um trabalho de estimativa específico {#get-estimate}

Depois de criar um trabalho de visualização, você pode usar seu `previewId` no caminho de uma solicitação do GET para o endpoint `/estimate` para exibir informações estatísticas sobre a definição do segmento, incluindo o tamanho projetado do público-alvo, o intervalo de confiança e o desvio padrão do erro.

**Formato da API**

```http
GET /estimate/{PREVIEW_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{PREVIEW_ID}` | Um trabalho de estimativa só é acionado quando um trabalho de visualização é criado e os dois trabalhos compartilham o mesmo valor de ID para fins de pesquisa. Especificamente, esse é o valor `previewId` retornado quando o trabalho de visualização foi criado. |

**Solicitação**

A solicitação a seguir recupera os resultados de um trabalho de estimativa específico.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes do trabalho de estimativa.

```json
{
    "estimatedSize": 4275,
    "numRowsToRead": 4275,
    "estimatedNamespaceDistribution": [
        {
            "namespaceId": "4",
            "profilesMatchedSoFar": 35
        },
        {
            "namespaceId": "6",
            "profilesMatchedSoFar": 4275
        }
    ],
    "state": "RESULT_READY",
    "profilesReadSoFar": 4275,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 4275,
    "totalRows": 4275,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `estimatedNamespaceDistribution` | Uma matriz de objetos que mostra o número de perfis no segmento detalhados por namespace de identidade. O número total de perfis por namespace (somando os valores mostrados para cada namespace) pode ser maior que a métrica de contagem de perfis, pois um perfil pode ser associado a vários namespaces. Por exemplo, se um cliente interagir com sua marca em mais de um canal, vários namespaces serão associados a esse cliente individual. |
| `state` | O estado atual do trabalho de visualização. O estado será &quot;EXECUTANDO&quot; até que o processamento seja concluído, ponto em que se torna &quot;RESULT_READY&quot; ou &quot;FALHA&quot;. |
| `_links.preview` | Quando `state` for &quot;RESULT_READY&quot;, esse campo fornecerá um URL para exibir a estimativa. |

## Próximas etapas

Depois de ler este guia, você deve ter uma melhor compreensão de como trabalhar com visualizações e estimativas usando a API de segmentação. Para saber como acessar métricas relacionadas aos dados do Perfil do cliente em tempo real, como o número total de fragmentos de perfil e perfis mesclados em namespaces específicos ou o armazenamento de dados do perfil como um todo, visite o [guia de ponto de extremidade de visualização de perfil (`/previewsamplestatus`)](../../profile/api/preview-sample-status.md).
