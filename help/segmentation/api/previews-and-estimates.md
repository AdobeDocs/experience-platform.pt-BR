---
solution: Experience Platform
title: Visualizações e estimativas de endpoints de API
description: À medida que a definição de segmento é desenvolvida, é possível usar as ferramentas de estimativa e pré-visualização no Adobe Experience Platform para exibir informações em nível de resumo e ajudar a garantir que você esteja isolando o público-alvo esperado.
role: Developer
exl-id: 2c204f29-825f-4a5e-a7f6-40fc69263614
source-git-commit: a374d261e3b34b30869f1a9e8486d52f5bd658cb
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 2%

---

# Visualizações e estimativas de endpoints

À medida que desenvolve uma definição de segmento, você pode usar as ferramentas de estimativa e visualização no Adobe Experience Platform para exibir informações de nível de resumo e ajudar a garantir que esteja isolando o público-alvo que espera.

* As **Visualizações** fornecem listas paginadas de perfis qualificados para uma definição de segmento, permitindo que você compare os resultados com o que espera.

* **Estimativas** fornecem informações estatísticas sobre uma definição de segmento, como o tamanho do público projetado, o intervalo de confiança e o desvio padrão de erro.

>[!NOTE]
>
>Para acessar métricas semelhantes relacionadas aos dados do Perfil do cliente em tempo real, como o número total de fragmentos de perfil e perfis mesclados em namespaces específicos ou o armazenamento de dados do perfil como um todo, consulte o [manual do ponto de extremidade de visualização de perfil (status da amostra de visualização)](../../profile/api/preview-sample-status.md), parte do guia do desenvolvedor da API de perfil.

## Introdução

Os pontos de extremidade usados neste guia fazem parte da API [!DNL Adobe Experience Platform Segmentation Service]. Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo os cabeçalhos necessários e como ler as chamadas de exemplo da API.

## Como as estimativas são geradas

Quando a assimilação de registros no armazenamento de Perfil aumenta ou diminui a contagem total de perfis em mais de 3%, um trabalho de amostragem é acionado para atualizar a contagem. A maneira como a amostragem de dados é acionada depende do método de assimilação:

* **Assimilação em lote:** Para assimilação em lote, em 15 minutos após a assimilação bem-sucedida de um lote no repositório de perfis, se o limite de aumento ou diminuição de 3% for atingido, um trabalho será executado para atualizar a contagem.
* **Assimilação de streaming:** Para fluxos de trabalho de dados de streaming, uma verificação é feita a cada hora para determinar se o limite de aumento ou diminuição de 3% foi atingido. Se tiver sido, uma tarefa será automaticamente acionada para atualizar a contagem.

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

Você pode criar uma nova visualização fazendo uma solicitação POST para o ponto de extremidade `/preview`.

>[!NOTE]
>
>Um trabalho estimado é criado automaticamente quando um trabalho de visualização é criado. Esses dois trabalhos compartilharão a mesma ID.

**Formato da API**

```http
POST /preview
```

**Solicitação**

+++ Um exemplo de solicitação para criar uma visualização.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `predicateExpression` | A expressão PQL pela qual consultar os dados. |
| `predicateType` | O tipo de predicado para a expressão de consulta em `predicateExpression`. Atualmente, o único valor aceito para esta propriedade é `pql/text`. |
| `predicateModel` | O nome da classe de esquema [!DNL Experience Data Model] (XDM) na qual os dados do perfil se baseiam. |
| `graphType` | O tipo de gráfico do qual você deseja obter o cluster. Os valores com suporte são `none` (não executa compilação de identidade) e `pdg` (executa compilação de identidade com base em seu gráfico de identidade privado). |

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) com detalhes da visualização recém-criada.

+++ Uma resposta de exemplo ao criar uma visualização.

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
| `state` | O estado atual do trabalho de visualização. Quando criado inicialmente, ele estará no estado &quot;NEW&quot;. Posteriormente, ele estará no estado &quot;EM EXECUÇÃO&quot; até que o processamento seja concluído, momento em que se torna &quot;RESULT_READY&quot; ou &quot;FAILED&quot;. |
| `previewId` | A ID do trabalho de visualização, a ser usada para fins de pesquisa ao exibir uma estimativa ou visualização, conforme descrito na próxima seção. |

+++

## Recuperar os resultados de uma visualização específica {#get-preview}

Você pode recuperar informações detalhadas sobre uma visualização específica fazendo uma solicitação GET para o ponto de extremidade `/preview` e fornecendo a ID de visualização no caminho da solicitação.

**Formato da API**

```http
GET /preview/{PREVIEW_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{PREVIEW_ID}` | O valor `previewId` da visualização que você deseja recuperar. |

**Solicitação**

+++ Uma solicitação de amostra para recuperar uma visualização.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

+++ Uma resposta de amostra ao recuperar uma visualização.

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
| `results` | Uma lista de IDs de entidade, juntamente com suas identidades relacionadas. Os links fornecidos podem ser usados para pesquisar as entidades especificadas, usando o [ponto de extremidade da API de acesso ao perfil](../../profile/api/entities.md). |

+++

## Recuperar os resultados de um trabalho de estimativa específico {#get-estimate}

Depois de criar um trabalho de visualização, você pode usar seu `previewId` no caminho de uma solicitação GET para o ponto de extremidade `/estimate` para exibir informações estatísticas sobre a definição do segmento, incluindo tamanho do público projetado, intervalo de confiança e desvio padrão de erro.

**Formato da API**

```http
GET /estimate/{PREVIEW_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{PREVIEW_ID}` | Um trabalho estimado só é acionado quando um trabalho de visualização é criado e os dois trabalhos compartilham o mesmo valor de ID para fins de pesquisa. Especificamente, esse é o valor `previewId` retornado quando o trabalho de visualização foi criado. |

**Solicitação**

A solicitação a seguir recupera os resultados de um trabalho de estimativa específico.

+++ Uma solicitação de amostra para recuperar um trabalho estimado.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes do trabalho estimado.

+++ Um exemplo de resposta ao recuperar um trabalho estimado.

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
| `estimatedNamespaceDistribution` | Uma matriz de objetos que mostra o número de perfis na definição de segmento detalhados por namespace de identidade. O número total de perfis por namespace (somando os valores mostrados para cada namespace) pode ser maior que a métrica de contagem de perfis, pois um perfil pode ser associado a vários namespaces. Por exemplo, se um cliente interagir com sua marca em mais de um canal, vários namespaces serão associados a esse cliente individual. |
| `state` | O estado atual do trabalho de visualização. O estado será &quot;RUNNING&quot; até que o processamento seja concluído, momento em que ele se torna &quot;RESULT_READY&quot; ou &quot;FAILED&quot;. |
| `_links.preview` | Quando o `state` é &quot;RESULT_READY&quot;, este campo fornece uma URL para exibir a estimativa. |

+++

## Próximas etapas

Depois de ler este guia, você terá uma melhor compreensão de como trabalhar com visualizações e estimativas usando a API de segmentação. Para saber como acessar métricas relacionadas aos seus dados de Perfil do cliente em tempo real, como o número total de fragmentos de perfil e perfis mesclados em namespaces específicos ou o armazenamento de dados do perfil como um todo, visite o [manual de ponto de extremidade de visualização de perfil (`/previewsamplestatus`)](../../profile/api/preview-sample-status.md).
